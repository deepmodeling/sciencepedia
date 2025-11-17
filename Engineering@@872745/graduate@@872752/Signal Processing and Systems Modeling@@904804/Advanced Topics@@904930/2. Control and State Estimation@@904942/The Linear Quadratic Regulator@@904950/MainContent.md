## Introduction
The Linear Quadratic Regulator (LQR) stands as a cornerstone of modern control theory, offering a powerful and systematic method for designing optimal feedback controllers. Its significance lies in its ability to translate high-level performance goals—such as minimizing tracking errors while conserving energy—into a mathematically tractable optimization problem. The central challenge in control design is often managing this trade-off between aggressive performance and practical constraints, a problem that LQR elegantly solves for a broad class of [linear systems](@entry_id:147850).

This article provides a comprehensive exploration of the LQR framework. In the first chapter, **Principles and Mechanisms**, we will delve into the theoretical heart of LQR, deriving the optimal control law via [dynamic programming](@entry_id:141107) and establishing the crucial role of the Algebraic Riccati Equation. We will also define the necessary conditions of [stabilizability and detectability](@entry_id:176335) that guarantee a stable and meaningful solution.

Building on this foundation, the second chapter, **Applications and Interdisciplinary Connections**, will demonstrate the remarkable versatility of LQR. We will extend the basic regulator to solve tracking and [disturbance rejection](@entry_id:262021) problems, connect it to [state estimation](@entry_id:169668) through the celebrated Linear-Quadratic-Gaussian (LQG) framework, and explore its role as the theoretical bedrock for advanced methods like Model Predictive Control (MPC).

Finally, the third chapter, **Hands-On Practices**, will bridge theory and application through a series of guided problems designed to reinforce the key computational and conceptual aspects of LQR [controller design](@entry_id:274982).

## Principles and Mechanisms

This chapter delves into the theoretical foundations and mechanical workings of the Linear Quadratic Regulator (LQR). We will formally define the LQR problem in both continuous and [discrete time](@entry_id:637509), derive the optimal control law from first principles, establish the [necessary and sufficient conditions](@entry_id:635428) for the existence of a stable solution, and explore key computational and practical aspects of its implementation.

### The Linear Quadratic Regulator Problem Formulation

At its core, the LQR problem is an [optimal control](@entry_id:138479) problem for a linear system with a quadratic performance index. This structure is not only mathematically tractable but also represents a wide range of practical objectives, such as minimizing tracking errors and control energy.

#### The Continuous-Time Infinite-Horizon Problem

Consider a continuous-time linear time-invariant (LTI) system described by the [state-space](@entry_id:177074) equation:
$$
\dot{x}(t) = A x(t) + B u(t)
$$
where $x(t) \in \mathbb{R}^{n}$ is the [state vector](@entry_id:154607), $u(t) \in \mathbb{R}^{m}$ is the control input vector, and $A$ and $B$ are constant matrices of appropriate dimensions. The objective is to find a control input function $u(\cdot)$ that minimizes an infinite-horizon quadratic [cost functional](@entry_id:268062), $J$:
$$
J(u) = \int_{0}^{\infty} \left( x(t)^{\top} Q x(t) + u(t)^{\top} R u(t) \right) \, dt
$$
This [cost functional](@entry_id:268062) represents the accumulated penalty over all future time. The term $x(t)^{\top} Q x(t)$ penalizes deviations of the state from the origin, while $u(t)^{\top} R u(t)$ penalizes the use of control energy. The matrices $Q$ and $R$ are weighting matrices that allow the designer to specify the relative importance of state regulation versus control effort.

#### The Discrete-Time Infinite-Horizon Problem

The discrete-time counterpart addresses systems that evolve in [discrete time](@entry_id:637509) steps, governed by the state-update equation:
$$
x_{k+1} = A x_{k} + B u_{k}
$$
The corresponding infinite-horizon quadratic cost is a summation:
$$
J(\{u_k\}) = \sum_{k=0}^{\infty} \left( x_{k}^{\top} Q x_{k} + u_{k}^{\top} R u_{k} \right)
$$
As in the continuous-time case, the goal is to find a sequence of control inputs $\{u_k\}_{k=0}^{\infty}$ that minimizes this total cost.

#### Assumptions on Weighting Matrices

For the LQR problem to be mathematically well-posed and physically meaningful, specific assumptions must be placed on the weighting matrices $Q$ and $R$ [@problem_id:2913505].

First, without loss of generality, we assume that **$Q$ and $R$ are symmetric matrices** ($Q=Q^{\top}$, $R=R^{\top}$). Any quadratic form $v^{\top}Mv$ depends only on the symmetric part of the matrix $M$, since $v^{\top}Mv = v^{\top}\left(\frac{M+M^{\top}}{2}\right)v$. Thus, any non-symmetric component can be discarded without changing the cost value.

Second, to ensure the [cost functional](@entry_id:268062) $J$ is bounded below (typically by zero), the integrand or summand must be non-negative for all possible states and controls. This requires that $x^{\top}Qx \ge 0$ for all $x$ and $u^{\top}Ru \ge 0$ for all $u$. These are the definitions of [positive semidefiniteness](@entry_id:147720). Therefore, we require **$Q \succeq 0$ and $R \succeq 0$**.

Third, for the optimization problem to have a unique, well-behaved solution, the cost must be strictly convex with respect to the control input $u$. The portion of the stage cost that depends on $u$ is $u^{\top}Ru$. For this term to be strictly convex, the matrix $R$ must be **[positive definite](@entry_id:149459), $R \succ 0$**. This condition ensures that any non-zero control action incurs a strictly positive cost, preventing [singular control](@entry_id:166459) problems where infinite control authority could be applied with zero penalty.

In summary, the standard assumptions for the LQR problem are:
1.  $Q$ is symmetric and positive semidefinite ($Q=Q^{\top} \succeq 0$).
2.  $R$ is symmetric and positive definite ($R=R^{\top} \succ 0$).

#### Extension to Cross-Product Costs

The standard LQR formulation can be extended to include a [cross-product term](@entry_id:148190) between the state and control input [@problem_id:2719910]:
$$
J=\int_{0}^{\infty}\Big(x^{\top}Qx+2x^{\top}Su+u^{\top}Ru\Big)\,dt
$$
This form is useful in various applications, including system transformations that eliminate the [cross-product term](@entry_id:148190) through a change of variables in the control input. For the integrand to be jointly convex in the combined vector $\begin{pmatrix} x^{\top}  u^{\top} \end{pmatrix}^{\top}$, it is necessary and sufficient that the [block matrix](@entry_id:148435) representing the quadratic form be positive semidefinite:
$$
\begin{pmatrix}
Q  S \\
S^{\top}  R
\end{pmatrix} \succeq 0
$$
This single condition encapsulates the [convexity](@entry_id:138568) requirement for the entire stage cost. A necessary consequence of this condition (by examining the principal submatrices) is that both $Q \succeq 0$ and $R \succeq 0$ must hold. The subsequent derivations in this chapter will focus on the standard case ($S=0$) for clarity, but the principles can be extended to the cross-term formulation.

### Derivation of the Optimal Feedback Law

The solution to the LQR problem is a linear state-feedback law. We can derive this elegant result using the [principle of optimality](@entry_id:147533) from [dynamic programming](@entry_id:141107).

#### The Principle of Optimality and the Hamilton-Jacobi-Bellman Equation

The **[principle of optimality](@entry_id:147533)**, formulated by Richard Bellman, states that an [optimal policy](@entry_id:138495) has the property that whatever the initial state and initial decision are, the remaining decisions must constitute an [optimal policy](@entry_id:138495) with regard to the state resulting from the first decision. For [continuous-time systems](@entry_id:276553), this principle is mathematically expressed through the **Hamilton-Jacobi-Bellman (HJB) equation**.

Let $V(x,t)$ be the optimal cost-to-go from state $x$ at time $t$. For the infinite-horizon, time-invariant problem, the [value function](@entry_id:144750) $V$ depends only on the state $x$. The HJB equation for this stationary problem is:
$$
0 = \min_{u} \left\{ x^{\top} Q x + u^{\top} R u + \left(\nabla_{x}V(x)\right)^{\top} (A x + B u) \right\}
$$
This equation states that at any point along an optimal trajectory, the rate of change of the optimal cost, combined with the instantaneous cost, must be zero, where the control $u$ is chosen to achieve this minimum.

#### The Quadratic Value Function and the Algebraic Riccati Equation

A key insight into the LQR problem is that for a linear system with a quadratic cost, the value function is itself a [quadratic form](@entry_id:153497) of the state [@problem_id:2719933]. We posit a solution of the form:
$$
V(x) = x^{\top} P x
$$
where $P$ is a symmetric, [positive semidefinite matrix](@entry_id:155134). The gradient of this [value function](@entry_id:144750) is $\nabla_{x}V(x) = 2Px$. Substituting this into the HJB equation gives:
$$
0 = \min_{u} \left\{ x^{\top} Q x + u^{\top} R u + (2Px)^{\top} (A x + B u) \right\}
$$
The expression inside the minimum is a quadratic function of $u$. Since we assumed $R \succ 0$, this function is strictly convex in $u$ and has a unique minimum. To find the minimum, we set the gradient with respect to $u$ to zero:
$$
\frac{\partial}{\partial u} \left( \dots \right) = 2Ru + 2B^{\top}Px = 0
$$
Solving for $u$ gives the optimal control law as a linear function of the state:
$$
u^{\star}(t) = -R^{-1} B^{\top} P x(t)
$$
This is the celebrated **linear state-feedback** law, where the gain matrix is $K = R^{-1} B^{\top} P$.

Substituting this [optimal control](@entry_id:138479) $u^{\star}$ back into the HJB equation yields:
$$
0 = x^{\top} Q x + (u^{\star})^{\top} R u^{\star} + 2x^{\top} P (A x + B u^{\star})
$$
After algebraic manipulation and recognizing that the resulting equation must hold for all $x$, we arrive at a [matrix equation](@entry_id:204751) for the unknown matrix $P$:
$$
A^{\top} P + P A - P B R^{-1} B^{\top} P + Q = 0
$$
This fundamental equation is the **continuous-time Algebraic Riccati Equation (ARE)**. The solution to the LQR problem hinges on finding the appropriate solution $P$ to this equation.

A parallel derivation exists for the discrete-time case [@problem_id:2913502]. Starting with the Bellman equation $V(x_k) = \min_{u_k} \{ x_k^{\top}Qx_k + u_k^{\top}Ru_k + V(x_{k+1}) \}$ and the quadratic value function ansatz $V(x_k) = x_k^{\top}Px_k$, a similar minimization and substitution procedure yields the optimal discrete-time control law:
$$
u_{k}^{\star} = -(R + B^{\top} P B)^{-1} B^{\top} P A x_{k}
$$
and the **discrete-time Algebraic Riccati Equation (DARE)**:
$$
P = A^{\top} P A - A^{\top} P B (R + B^{\top} P B)^{-1} B^{\top} P A + Q
$$

An alternative and equally powerful derivation involves a "[completing the square](@entry_id:265480)" argument [@problem_id:2719933]. By adding and subtracting the term $\frac{d}{dt}(x^{\top}Px)$ to the cost integrand, one can rearrange the expression into a perfect square involving the control input, plus residual terms that vanish precisely when $P$ satisfies the ARE. This method elegantly reveals the optimal control law as the term that zeroes out the perfect square.

#### Guarantee of Global Optimality

A crucial feature of the LQR framework is that the derived solution is **globally optimal**, not merely a [local minimum](@entry_id:143537) [@problem_id:2913491]. This strong guarantee stems directly from the [dynamic programming principle](@entry_id:188984). The HJB equation constructs the value function by performing a global minimization over all [admissible controls](@entry_id:634095) at each state-time point. The [verification theorem](@entry_id:185180) of optimal control formalizes this: any solution that satisfies the HJB equation is the globally optimal one.

The convexity of the LQR problem plays a vital role. The stage cost is convex in $(x,u)$, and the dynamics are linear. This makes the Hamiltonian (the expression minimized in the HJB equation) strictly convex in the control input $u$. Consequently, the minimization step has a unique global minimizer at each point, which prevents the existence of spurious local optima and ensures the resulting feedback law is uniquely and globally optimal.

### Conditions for Existence and Stability

The derivation of the Riccati equation provides the mechanics for finding the matrix $P$, but it does not guarantee that a "good" solution exists. For the infinite-[horizon problem](@entry_id:161031), we require a solution $P$ that is not only positive semidefinite but also **stabilizing**, meaning the resulting closed-loop system $\dot{x} = (A-BK)x$ (or $x_{k+1}=(A-BK)x_k$) is asymptotically stable. The existence of such a solution depends on fundamental structural properties of the system matrices, namely **[stabilizability](@entry_id:178956)** and **detectability**.

#### The Necessity of Stabilizability

The pair $(A,B)$ is **stabilizable** if all [unstable modes](@entry_id:263056) of the system can be influenced by the control input. More formally, every eigenvalue of $A$ with $\text{Re}(\lambda) \ge 0$ (for continuous time) or $|\lambda| \ge 1$ (for [discrete time](@entry_id:637509)) must be controllable.

Stabilizability is a necessary condition for the existence of a stabilizing LQR solution [@problem_id:2913459] [@problem_id:2913490]. To see why, suppose the system has an unstable mode that is uncontrollable. By definition, no control input $u(t)$ can alter the dynamics of this mode. If the system is initialized with a component in this unstable mode, that component of the state will grow without bound. This would cause the integral (or sum) in the [cost functional](@entry_id:268062) $J$ to diverge to infinity. Since no control can prevent this, a finite optimal cost cannot be guaranteed for all initial states, and more importantly, no feedback law can stabilize the system. Therefore, the ability to stabilize the system in the first place—[stabilizability](@entry_id:178956)—is a prerequisite.

#### The Necessity of Detectability

The pair $(C,A)$ is **detectable** if all [unstable modes](@entry_id:263056) of the system are observable through the output matrix $C$. In the LQR context, we consider detectability with respect to the state weighting, where the "output" is $C_Qx$ with $C_Q$ being any matrix such that $Q = C_Q^{\top}C_Q$ (e.g., $C_Q = Q^{1/2}$).

Detectability of $(Q^{1/2},A)$ is also a necessary condition for a stabilizing LQR solution [@problem_id:2913459] [@problem_id:2913490]. Suppose this condition fails. This implies there is an unstable mode (eigenvector $v$ with eigenvalue $\lambda$ where $\text{Re}(\lambda) \ge 0$ or $|\lambda| \ge 1$) that is "invisible" to the [cost function](@entry_id:138681), meaning $Qv=0$. Consider initializing the system in this mode, $x_0 = v$. If we apply zero control, $u(t) \equiv 0$, the state evolves as $x(t) = e^{\lambda t} v$. The cost integrand for this trajectory is $x(t)^{\top}Qx(t) = |e^{\lambda t}|^2 v^{\top}Qv = 0$. The total cost is zero. Since the cost can never be negative, this zero-cost trajectory must be optimal. However, the corresponding control law, $u(t) \equiv 0$, is not stabilizing because the state $x(t)$ grows unboundedly. The LQR solution would thus fail to be stabilizing. To avoid this pathological case, every unstable mode must be "detected" by the [cost function](@entry_id:138681), forcing the optimal controller to stabilize it.

#### The Main Existence Theorem

These two conditions are not only necessary but also sufficient. This leads to the fundamental theorem of infinite-horizon LQR:

*A unique, symmetric, positive semidefinite, stabilizing solution $P$ to the Algebraic Riccati Equation (ARE or DARE) exists if and only if the pair $(A,B)$ is stabilizable and the pair $(Q^{1/2}, A)$ is detectable.*

### Computational Methods and Practical Considerations

#### The Hamiltonian Matrix Approach

The Algebraic Riccati Equation is a nonlinear matrix equation, and solving it directly can be challenging. A powerful alternative method connects the ARE to the spectral properties of a **Hamiltonian matrix** [@problem_id:2913508]. For the continuous-time case, the Hamiltonian matrix is defined as:
$$
H = \begin{pmatrix} A  -BR^{-1}B^{\top} \\ -Q  -A^{\top} \end{pmatrix}
$$
This $2n \times 2n$ matrix arises from the linearized state-[costate](@entry_id:276264) dynamics derived from Pontryagin's Minimum Principle. Under the standard [stabilizability and detectability](@entry_id:176335) assumptions, the matrix $H$ has no eigenvalues on the imaginary axis. Its eigenvalues are symmetric with respect to the imaginary axis, meaning there are exactly $n$ stable eigenvalues (with $\text{Re}(\lambda)0$) and $n$ unstable eigenvalues (with $\text{Re}(\lambda)>0$).

The stabilizing solution $P$ of the ARE can be constructed from the $n$-dimensional [stable invariant subspace](@entry_id:755318) of $H$. If the columns of $\begin{pmatrix} X \\ Y \end{pmatrix}$ form a basis for this subspace, where $X, Y \in \mathbb{R}^{n \times n}$, then the stabilizing solution is given by:
$$
P = Y X^{-1}
$$
This method transforms the problem of solving a nonlinear [matrix equation](@entry_id:204751) into a more tractable eigenproblem, which is the basis for many robust [numerical solvers](@entry_id:634411) for the ARE.

#### The Finite-Horizon Problem and the Differential Riccati Equation

The LQR framework readily extends to finite-horizon problems, where the cost is minimized over an interval $[0, T]$ [@problem_id:2913474]. A finite-[horizon problem](@entry_id:161031) may also include a **terminal cost**, $x(T)^{\top}P_f x(T)$, which penalizes the final state at time $T$. The performance index is:
$$
J(u) = \int_{0}^{T} \big( x^{\top} Q x + u^{\top} R u \big)\, dt + x(T)^{\top} P_{f} x(T)
$$
In this case, the [value function](@entry_id:144750) $V(x,t) = x^{\top}P(t)x$ becomes time-varying. The matrix $P(t)$ is the solution to the **Differential Riccati Equation (DRE)**:
$$
-\dot{P}(t) = A^{\top} P(t) + P(t) A - P(t) B R^{-1} B^{\top} P(t) + Q
$$
This equation is solved *backward* in time from the terminal condition $P(T) = P_f$. The terminal [cost matrix](@entry_id:634848) $P_f$ thus serves as the boundary condition for the DRE. A larger $P_f$ (in the sense of the Loewner order) results in a larger $P(t)$ for all $t$, leading to more aggressive control action, especially near the final time $T$. In the limit as the weight on the terminal cost goes to infinity (e.g., $P_f = \alpha I$ with $\alpha \to \infty$), the LQR controller attempts to enforce a hard constraint $x(T)=0$.

The infinite-horizon solution $P$ of the ARE can be viewed as the steady-state limit of the finite-horizon solution $P(t)$ as the horizon $T$ approaches infinity (and $t$ is held fixed far from the terminal time) [@problem_id:2913502].

#### Tuning the Regulator: The Q-R Trade-off

The choice of the weighting matrices $Q$ and $R$ is the primary mechanism for a designer to tune the performance of the LQR controller [@problem_id:2913479]. These matrices encode the fundamental trade-off between **state regulation performance** and **control effort**.

-   **Increasing $Q$**: For a fixed $R$, increasing the penalty on the state (e.g., replacing $Q$ with $\gamma Q$ for $\gamma  1$) forces the controller to be more aggressive in driving the state to zero. This typically results in a faster response and smaller state deviations, but at the expense of larger control signals and higher energy consumption. The corresponding Riccati solution $P$ increases in the Loewner order.

-   **Increasing $R$**: For a fixed $Q$, increasing the penalty on the control input (e.g., replacing $R$ with $\rho R$ for $\rho  1$) makes control action more "expensive". The optimal controller becomes more conservative, using smaller control signals. This leads to a slower system response. In the limit as $\rho \to \infty$, the control cost becomes prohibitive, the optimal gain $K$ tends to zero, and the closed-loop [system dynamics](@entry_id:136288) approach those of the open-loop (uncontrolled) system.

-   **Scaling Invariance**: The LQR gain depends on the *ratio* of penalties, not their absolute values. If both $Q$ and $R$ are multiplied by the same positive scalar $c$, the [cost functional](@entry_id:268062) is simply scaled by $c$, but the underlying trade-off remains identical. This is reflected in the fact that the optimal gain matrix $K$ is unchanged, while the Riccati solution matrix scales to $P' = cP$. This insight simplifies tuning, as one can often fix one matrix (e.g., $R=I$) and adjust the other to achieve the desired performance.

In conclusion, the Linear Quadratic Regulator provides a powerful and systematic framework for designing optimal feedback controllers. Its elegant solution, rooted in the [principle of optimality](@entry_id:147533) and the Riccati equation, comes with strong guarantees of stability and global optimality, making it a cornerstone of modern control theory and practice.