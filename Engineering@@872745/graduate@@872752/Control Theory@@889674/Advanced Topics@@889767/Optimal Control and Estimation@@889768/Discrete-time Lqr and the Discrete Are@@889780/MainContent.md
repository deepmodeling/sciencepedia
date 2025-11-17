## Introduction
The discrete-time Linear Quadratic Regulator (LQR) is a cornerstone of modern optimal control theory, providing a powerful and systematic framework for designing feedback controllers. Its significance lies in its ability to balance performance objectives against control effort, yielding an [optimal policy](@entry_id:138495) for linear systems that operate in [discrete time](@entry_id:637509) steps, a common scenario in [digital control](@entry_id:275588). However, deriving this [optimal policy](@entry_id:138495) requires solving a fundamental nonlinear [matrix equation](@entry_id:204751). This article addresses the problem of how to find this [optimal control](@entry_id:138479) law, from its theoretical derivation to its practical computation and application.

The journey begins in the **Principles and Mechanisms** chapter, where we will rigorously derive the optimal LQR control law using [dynamic programming](@entry_id:141107) and introduce its heart: the Discrete Algebraic Riccati Equation (DARE). We will explore the critical conditions of [stabilizability and detectability](@entry_id:176335) that guarantee a unique, stable solution and discuss robust numerical methods for finding it. Next, the **Applications and Interdisciplinary Connections** chapter broadens our perspective, revealing how LQR theory forms the bedrock for advanced paradigms like stochastic (LQG) and constrained (MPC) control, and finds surprising utility in fields like [macroeconomics](@entry_id:146995). Finally, the **Hands-On Practices** chapter provides a set of targeted problems, allowing you to solidify your understanding by applying these concepts to concrete examples, from scalar systems to diagnosing stability conditions.

## Principles and Mechanisms

This chapter delves into the foundational principles and mechanisms of the discrete-time Linear Quadratic Regulator (LQR). We will rigorously formulate the optimal control problem, derive its solution through the principle of dynamic programming, and establish the central role of the Discrete Algebraic Riccati Equation (DARE). Furthermore, we will investigate the conditions for the [existence and uniqueness](@entry_id:263101) of a stabilizing solution and explore numerically robust methods for its computation.

### The Infinite-Horizon LQR Problem

The discrete-time LQR problem seeks to design an optimal control sequence for a linear time-invariant (LTI) system. Consider the system described by the [state-space](@entry_id:177074) equation:

$x_{k+1} = A x_k + B u_k$

where $x_k \in \mathbb{R}^n$ is the state vector at time step $k$, $u_k \in \mathbb{R}^m$ is the control input, and the matrices $A \in \mathbb{R}^{n \times n}$ and $B \in \mathbb{R}^{n \times m}$ are constant.

The objective is to find a control sequence $\{u_k\}_{k=0}^{\infty}$ that minimizes a quadratic performance index, or cost function, over an infinite horizon. A general and powerful form of this [cost function](@entry_id:138681) includes a cross-weighting term between the state and control input:

$J(x_0, \{u_k\}) = \sum_{k=0}^{\infty} \left( x_k^{\top} Q x_k + 2 x_k^{\top} N u_k + u_k^{\top} R u_k \right)$

Here, $Q \in \mathbb{R}^{n \times n}$, $N \in \mathbb{R}^{n \times m}$, and $R \in \mathbb{R}^{m \times m}$ are weighting matrices that penalize the magnitude of the state, the coupling between state and input, and the control effort, respectively.

For this optimization problem to be well-posed, the [cost functional](@entry_id:268062) $J$ must be bounded below and, for a unique solution to exist, it must be strictly convex with respect to the control sequence $\{u_k\}$. The stage cost, $l(x_k, u_k) = x_k^{\top} Q x_k + 2 x_k^{\top} N u_k + u_k^{\top} R u_k$, can be written as a quadratic form:

$l(x_k, u_k) = \begin{pmatrix} x_k \\ u_k \end{pmatrix}^{\top} \begin{pmatrix} Q & N \\ N^{\top} & R \end{pmatrix} \begin{pmatrix} x_k \\ u_k \end{pmatrix}$

To ensure this cost is always non-negative, it is standard to require the [block matrix](@entry_id:148435) to be positive semidefinite. However, for [strict convexity](@entry_id:193965) with respect to the input sequence, a slightly stronger set of conditions is necessary. Consider a variation in the input sequence, $\{\delta u_k\}$, which is not identically zero. This causes a variation in the state trajectory, $\{\delta x_k\}$. The second variation of the cost, $\delta^2 J$, is the sum of stage costs evaluated at these variations. For [strict convexity](@entry_id:193965), we require $\delta^2 J > 0$. If we choose a variation where only the first term $\delta u_0$ is non-zero, then $\delta x_0 = 0$, and the first term in the sum for $\delta^2 J$ becomes $\delta u_0^{\top} R \delta u_0$. To guarantee this term is strictly positive for any non-zero $\delta u_0$, the matrix $R$ must be positive definite. This, combined with the overall non-negativity of the stage cost, leads to the minimal assumptions for a [well-posed problem](@entry_id:268832) [@problem_id:2700972].

The standard assumptions on the weighting matrices are therefore:
1.  $Q$ and $R$ are symmetric, i.e., $Q = Q^{\top}$ and $R = R^{\top}$.
2.  The input weighting matrix $R$ is **positive definite** ($R \succ 0$). This ensures that any control action has a cost, preventing unbounded control signals.
3.  The [block matrix](@entry_id:148435) $\begin{pmatrix} Q & N \\ N^{\top} & R \end{pmatrix}$ is **positive semidefinite** ($\succeq 0$). This guarantees that the stage cost is always non-negative.

Given that $R \succ 0$, the third condition is equivalent to the **Schur complement condition** $Q - N R^{-1} N^{\top} \succeq 0$. These conditions collectively ensure that the total cost $J$ is a strictly convex function of the input sequence $\{u_k\}$, which is a critical property for establishing the existence and uniqueness of an optimal control law.

### Solution via Dynamic Programming

The solution to the LQR problem is elegantly found using **dynamic programming**. The core idea is encapsulated in Bellman's **Principle of Optimality**: an [optimal policy](@entry_id:138495) has the property that whatever the initial state and initial decision are, the remaining decisions must constitute an [optimal policy](@entry_id:138495) with regard to the state resulting from the first decision.

For the infinite-horizon, time-invariant problem, we postulate a time-invariant, quadratic **[value function](@entry_id:144750)** $V(x)$, representing the optimal cost-to-go from state $x$:

$V(x) = x^{\top} P x$

where $P$ is a symmetric, [positive semidefinite matrix](@entry_id:155134) to be determined. The Bellman equation for this problem is a [fixed-point equation](@entry_id:203270) for the value function:

$V(x_k) = \min_{u_k} \left\{ x_k^{\top} Q x_k + 2 x_k^{\top} N u_k + u_k^{\top} R u_k + V(x_{k+1}) \right\}$

Substituting $V(x) = x^{\top} P x$ and the [system dynamics](@entry_id:136288) $x_{k+1} = A x_k + B u_k$, we get:

$x_k^{\top} P x_k = \min_{u_k} \left\{ x_k^{\top} Q x_k + 2 x_k^{\top} N u_k + u_k^{\top} R u_k + (A x_k + B u_k)^{\top} P (A x_k + B u_k) \right\}$

The expression to be minimized is a quadratic function of $u_k$. To find the minimum, we compute its gradient with respect to $u_k$ and set it to zero:

$\nabla_{u_k} (\dots) = 2 R u_k + 2 N^{\top} x_k + 2 B^{\top} P A x_k + 2 B^{\top} P B u_k = 0$

Solving for $u_k$ gives the optimal control law:

$u_k^* = - (R + B^{\top} P B)^{-1} (B^{\top} P A + N^{\top}) x_k$

This is a **static state-feedback law** of the form $u_k = -K x_k$. The optimal feedback **gain matrix** $K$ is therefore:

$K = (R + B^{\top} P B)^{-1} (B^{\top} P A + N^{\top})$ [@problem_id:2700990]

Note the term $B^{\top} P B$ in the inverse. This term arises because the control input $u_k$ quadratically affects the cost of the next state, $V(x_{k+1})$. This is a fundamental structural difference from the continuous-time LQR problem, where the corresponding gain is $K_c = R^{-1}(B^{\top}P + N^{\top})$ [@problem_id:2701023].

By substituting the optimal control $u_k^*$ back into the Bellman equation, we enforce the fixed-point property. After algebraic manipulation, we find that this must hold for all $x_k$, which implies an algebraic equation for the matrix $P$ itself. This equation is the celebrated **Discrete Algebraic Riccati Equation (DARE)**:

$P = A^{\top}PA + Q - (A^{\top}PB+N)(R+B^{\top}PB)^{-1}(B^{\top}PA+N^{\top})$ [@problem_id:2701002]

This single, nonlinear [matrix equation](@entry_id:204751) is the cornerstone of the discrete-time LQR solution. Its solution, $P$, simultaneously defines the optimal cost ($J^* = x_0^{\top} P x_0$) and the optimal control gain $K$.

It is insightful to view the DARE as a [fixed-point equation](@entry_id:203270). The finite-horizon LQR problem is solved by a [backward recursion](@entry_id:637281) known as the Riccati [difference equation](@entry_id:269892), $P_k = \mathcal{R}(P_{k+1})$, where $\mathcal{R}$ is the **Riccati operator**. The DARE, $P = \mathcal{R}(P)$, is precisely the condition for $P$ to be a fixed point of this operator. This signifies that the infinite-horizon solution is the steady-state limit of the finite-horizon solution as the time horizon tends to infinity [@problem_id:2700973].

### The Role of the Cross-Weighting Term

The presence of the cross-weighting matrix $N$ introduces a correlation between the state and the optimal control action in the cost function. There are two equivalent ways to understand and solve this problem [@problem_id:2700971].

The first is the direct approach, as derived above, where the terms involving $N$ appear explicitly in both the DARE and the gain formula for $K$.

The second approach is a change of variables, often called **completing the square**. We define a new control variable $\tilde{u}_k$ that absorbs the cross-term:

$\tilde{u}_k = u_k + R^{-1} N^{\top} x_k$

Substituting $u_k = \tilde{u}_k - R^{-1} N^{\top} x_k$ into the [system dynamics](@entry_id:136288) and stage cost yields a new, equivalent LQR problem. The modified dynamics become:

$x_{k+1} = (A - B R^{-1} N^{\top}) x_k + B \tilde{u}_k = \tilde{A} x_k + B \tilde{u}_k$

And the stage cost becomes:

$l(x_k, \tilde{u}_k) = x_k^{\top} (Q - N R^{-1} N^{\top}) x_k + \tilde{u}_k^{\top} R \tilde{u}_k = x_k^{\top} \tilde{Q} x_k + \tilde{u}_k^{\top} R \tilde{u}_k$

This transformed problem is a standard LQR problem with zero cross-weighting, defined by the new system matrix $\tilde{A}$ and state-weighting matrix $\tilde{Q}$. Its solution yields an optimal feedback law for the new control, $\tilde{u}_k^* = -\tilde{K} x_k$. We can then recover the [optimal control](@entry_id:138479) for the original system as:

$u_k^* = \tilde{u}_k^* - R^{-1} N^{\top} x_k = -(\tilde{K} + R^{-1} N^{\top}) x_k$

This demonstrates that the [optimal policy](@entry_id:138495) remains a static state-feedback law. This transformation is not only computationally useful but also provides insight: the cross-term effectively modifies the open-loop dynamics and the state penalty.

### Existence, Uniqueness, and Stability of the Solution

Having derived the DARE, we must ask: when does it have a meaningful solution? We are interested in a specific type of solution: one that leads to a stable closed-loop system. A symmetric, positive semidefinite solution $P$ to the DARE is called a **stabilizing solution** if the resulting closed-loop system matrix, $A_{cl} = A - BK$, is **Schur stable**, meaning all its eigenvalues lie strictly inside the unit disk of the complex plane ($\rho(A_{cl})  1$) [@problem_id:2701002].

A fundamental theorem in control theory states that, given the [cost function](@entry_id:138681) is well-posed ($R \succ 0$ and $\begin{pmatrix} Q  N \\ N^{\top}  R \end{pmatrix} \succeq 0$), a unique positive semidefinite stabilizing solution $P$ to the DARE exists if and only if two system-theoretic conditions are met [@problem_id:2701017].

1.  **The pair $(A, B)$ is stabilizable.** A system is stabilizable if all of its [unstable modes](@entry_id:263056) (eigenvalues of $A$ with magnitude $|\lambda| \ge 1$) are controllable. This condition is necessary because if an unstable mode cannot be influenced by the control input, no feedback law can stabilize the system, and the infinite-horizon cost will diverge for any initial condition that excites this mode.

2.  **The pair $(Q^{1/2}, A)$ is detectable.** (Here $Q^{1/2}$ is any matrix such that $(Q^{1/2})^{\top}Q^{1/2}=Q$). A system is detectable if all of its [unobservable modes](@entry_id:168628) are stable. In this context, it means any unstable mode of $A$ must be "visible" to the cost function. To understand why, consider a pathological case where an unstable eigenvector $v$ (with $Av = \lambda v$, $|\lambda| \ge 1$) is also in the nullspace of $Q$ ($Qv=0$). If we initialize the system at $x_0=v$ and apply zero control ($u_k \equiv 0$), the state trajectory is $x_k = \lambda^k v$. The cost incurred is $\sum x_k^{\top}Qx_k = \sum |\lambda|^{2k} v^{\top}Qv = 0$. The optimizer sees a cost of zero for allowing an unstable mode to grow unbounded. It therefore has no incentive to apply control effort (which is always costly as $R \succ 0$) to stabilize this mode. Consequently, the "optimal" closed-loop system would not be stable. The detectability condition rules out this [pathology](@entry_id:193640), ensuring that any unstable state trajectory will eventually incur a non-zero cost, forcing the optimizer to stabilize it [@problem_id:2700949].

These two conditions—[stabilizability and detectability](@entry_id:176335)—are the weakest possible requirements for guaranteeing a unique and meaningful solution to the infinite-horizon LQR problem. They are less restrictive than full [controllability and observability](@entry_id:174003), which are not necessary [@problem_id:2701017].

### Numerical Solution via the Symplectic Pencil

While the DARE can sometimes be solved by iterating the corresponding difference equation, this approach can be slow or numerically sensitive. A more robust and computationally reliable method involves recasting the problem in a geometric framework by analyzing the properties of an associated **[symplectic matrix](@entry_id:142706) pencil** [@problem_id:2700976].

The [optimality conditions](@entry_id:634091) of the LQR problem give rise to a set of linear [difference equations](@entry_id:262177) for the state $x_k$ and a [costate](@entry_id:276264) vector $p_k$. These can be arranged into a $2n$-dimensional generalized [state-space](@entry_id:177074) system of the form $\mathcal{M} z_{k+1} = \mathcal{N} z_k$, where $z_k = \begin{pmatrix} x_k \\ p_k \end{pmatrix}$. The matrices defining the pencil $\mathcal{N} - z \mathcal{M}$ are given by:

$\mathcal{N} = \begin{bmatrix} A  0 \\ -Q  I \end{bmatrix}, \qquad \mathcal{M} = \begin{bmatrix} I  B R^{-1} B^{\top} \\ 0  A^{\top} \end{bmatrix}$

(For problems with a cross-term $N$, these matrices have a slightly more complex form). The stabilizing solution $P$ to the DARE induces a relationship between the state and [costate](@entry_id:276264), $p_k = P x_k$. This implies that the optimal trajectories evolve on an $n$-dimensional subspace within the $2n$-dimensional generalized state space, spanned by vectors of the form $\begin{pmatrix} I \\ P \end{pmatrix}x_k$.

The central result is that this subspace is precisely the [invariant subspace](@entry_id:137024) of the pencil $\mathcal{N} - z \mathcal{M}$ that corresponds to its $n$ generalized eigenvalues lying strictly inside the unit circle. The problem of solving the DARE is thus transformed into the problem of finding a specific invariant subspace of a [matrix pencil](@entry_id:751760).

This geometric characterization leads directly to a numerically superior algorithm based on the **generalized Schur decomposition (or QZ algorithm)** [@problem_id:2700997]. The procedure is as follows:
1.  **Construct the pencil:** Form the $2n \times 2n$ matrices $\mathcal{N}$ and $\mathcal{M}$ as defined above.
2.  **Decompose:** Compute the generalized Schur decomposition of the pair $(\mathcal{N}, \mathcal{M})$, which finds [orthogonal matrices](@entry_id:153086) $U$ and $V$ such that $U^{\top}\mathcal{N}V = S$ and $U^{\top}\mathcal{M}V = T$ are upper quasi-triangular.
3.  **Reorder:** Apply orthogonal transformations to reorder the decomposition so that the generalized eigenvalues $\lambda_i = s_{ii}/t_{ii}$ satisfying $|\lambda_i|  1$ correspond to the first $n$ diagonal elements.
4.  **Extract Subspace:** After reordering, the first $n$ columns of the matrix $V$ form an [orthonormal basis](@entry_id:147779) for the desired [stable invariant subspace](@entry_id:755318). Partition this [basis matrix](@entry_id:637164) as $\begin{pmatrix} V_{11} \\ V_{21} \end{pmatrix}$, where $V_{11}, V_{21} \in \mathbb{R}^{n \times n}$.
5.  **Recover Solution:** The [stabilizability and detectability](@entry_id:176335) assumptions guarantee that the block $V_{11}$ is nonsingular. The unique stabilizing solution to the DARE is then recovered by solving a linear system:

    $P = V_{21} V_{11}^{-1}$

This method avoids the potentially ill-conditioned nature of iterating the DARE directly and is the standard approach used in high-quality numerical software for [control systems design](@entry_id:273663).