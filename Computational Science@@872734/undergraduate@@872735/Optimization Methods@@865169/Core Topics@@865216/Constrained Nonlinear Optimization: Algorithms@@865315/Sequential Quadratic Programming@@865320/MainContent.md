## Introduction
Sequential Quadratic Programming (SQP) is one of the most powerful and reliable methods for solving [nonlinear optimization](@entry_id:143978) problems, which are ubiquitous in science, engineering, and finance. These problems, characterized by nonlinear objective functions and constraints, often lack direct analytical solutions due to their complexity. SQP addresses this challenge by ingeniously breaking down a difficult nonlinear problem into a sequence of more manageable Quadratic Programming (QP) subproblems, which are then solved iteratively to find a solution.

This article provides a comprehensive guide to understanding and applying the SQP method. The first chapter, **Principles and Mechanisms**, will demystify the core of the algorithm, explaining how the QP subproblems are constructed from local information and how the process converges to a solution. Next, **Applications and Interdisciplinary Connections** will showcase the versatility of SQP by exploring its use in diverse fields such as [optimal control](@entry_id:138479), power systems engineering, and [biomechanics](@entry_id:153973), highlighting how the method is adapted to solve real-world challenges. Finally, the **Hands-On Practices** chapter offers practical exercises to solidify your understanding, from setting up your first QP subproblem to exploring advanced concepts like [sensitivity analysis](@entry_id:147555). By the end, you will have a solid grasp of both the theory behind SQP and its practical implementation.

## Principles and Mechanisms

Sequential Quadratic Programming (SQP) stands as one of the most effective and widely used methods for solving general Nonlinear Programming (NLP) problems. As its name suggests, the core strategy of SQP is to address a complex NLP by solving a sequence of simpler, more structured Quadratic Programming (QP) subproblems. This chapter elucidates the principles that underpin the construction of these subproblems and the mechanisms that ensure the iterative process converges robustly to a solution.

### The Core Iterative Strategy

A general NLP seeks to find a vector $x \in \mathbb{R}^n$ that minimizes a nonlinear [objective function](@entry_id:267263) $f(x)$ subject to a set of nonlinear equality and [inequality constraints](@entry_id:176084), typically written as $h(x) = 0$ and $g(x) \le 0$. The landscape defined by the objective function and the [feasible region](@entry_id:136622) defined by the constraints can be arbitrarily complex, making a direct solution intractable.

The SQP method approaches this challenge iteratively. Starting from an initial guess $x_0$, the algorithm generates a sequence of iterates $\{x_k\}$ that aims to converge to a local minimizer $x^*$. The transition from one iterate, $x_k$, to the next, $x_{k+1}$, is determined by solving an approximation of the original NLP that is centered at $x_k$. This approximation is specifically designed to be a Quadratic Program (QP), which involves minimizing a quadratic [objective function](@entry_id:267263) subject to [linear constraints](@entry_id:636966).

The solution to this QP subproblem at iteration $k$ is a step vector, denoted $p_k$. This vector represents the optimal direction and length of movement from $x_k$ *within the simplified model*. It is not the final solution to the NLP, but rather a **search direction** that points towards a better estimate of the solution. A specialized "QP solver" is employed as a subroutine to efficiently compute this search direction. The next iterate is then found by moving from $x_k$ along this direction:

$$
x_{k+1} = x_k + \alpha_k p_k
$$

Here, $\alpha_k \in (0, 1]$ is a step length determined by a globalization procedure, such as a line search, to ensure that each step makes meaningful progress. Therefore, the fundamental role of the QP subproblem within each major SQP iteration is to compute the optimal search direction based on local information at the current iterate [@problem_id:2201997].

### Constructing the QP Subproblem: A Local Model

The power of SQP lies in how it constructs the QP subproblem. The goal is to create a model that is both a faithful local representation of the original NLP and is computationally easy to solve. This is achieved by combining a quadratic model of the objective with a linear model of the constraints.

#### Linearizing the Constraints

Nonlinear constraints are the primary source of difficulty in many optimization problems. The SQP method simplifies them by replacing the nonlinear constraint functions $h(x)$ and $g(x)$ with their first-order Taylor series approximations around the current iterate $x_k$. For a proposed step $p = x - x_k$, the constraints become:

$$
h(x_k) + \nabla h(x_k)^T p = 0
$$
$$
g(x_k) + \nabla g(x_k)^T p \le 0
$$

Here, $\nabla h(x_k)$ and $\nabla g(x_k)$ are the Jacobian matrices of the respective constraint functions evaluated at $x_k$. This linearization transforms the complex, curved boundaries of the original feasible region into a simple polyhedron (in the space of the step vector $p$). The primary computational motivation for this step is that linear constraints are the defining feature of a QP subproblem, for which highly efficient and mature solvers exist [@problem_id:2202046].

#### Quadratic Modeling via the Lagrangian

With the constraints linearized, we must define a suitable objective for the QP subproblem. Simply using a [quadratic approximation](@entry_id:270629) of the original objective function $f(x)$ is insufficient, as it would ignore the crucial influence of the constraints on the location of the optimum. A constrained optimum is a point where the gradient of the objective is balanced by the gradients of the [active constraints](@entry_id:636830). This trade-off is mathematically captured by the **Lagrangian function**.

For a general NLP with objective $f(x)$, equality constraints $h(x) = 0$, and [inequality constraints](@entry_id:176084) $g(x) \le 0$, the Lagrangian function $\mathcal{L}(x, \lambda, \mu)$ is defined as:

$$
\mathcal{L}(x, \lambda, \mu) = f(x) + \lambda^T h(x) + \mu^T g(x)
$$

Here, $\lambda$ and $\mu$ are vectors of **Lagrange multipliers**, which can be interpreted as prices or sensitivities associated with violating the constraints. For example, if we consider the problem of minimizing $f(x_1, x_2) = \exp(x_1) + x_1 x_2^2 + 3x_2$ subject to $h(x_1, x_2) = x_1^2 + \sin(x_2) - 5 = 0$ and $g(x_1, x_2) = x_1 + x_2 - 2 \le 0$, the associated Lagrangian function is:

$$
\mathcal{L}(x_1, x_2, \lambda, \mu) = (\exp(x_1) + x_1 x_2^2 + 3x_2) + \lambda (x_1^2 + \sin(x_2) - 5) + \mu (x_1 + x_2 - 2)
$$
[@problem_id:2202030]

The objective of the QP subproblem is a second-order (quadratic) approximation of the Lagrangian function. At iteration $k$, with iterate $x_k$ and multiplier estimates $\lambda_k, \mu_k$, the QP objective is formulated as:

$$
\min_{p} \quad \nabla f(x_k)^T p + \frac{1}{2} p^T B_k p
$$

The matrix $B_k$ is a symmetric matrix that approximates the Hessian of the Lagrangian function with respect to $x$, i.e., $B_k \approx \nabla_{xx}^2 \mathcal{L}(x_k, \lambda_k, \mu_k)$. The gradient term involves only $\nabla f(x_k)$ because terms involving the multipliers are incorporated into the KKT conditions of the QP, as we will see next.

### The Complete QP Subproblem and its Solution

Combining the linearized constraints and the quadratic model of the Lagrangian, we arrive at the full QP subproblem at iteration $k$:

$$
\begin{align*}
\underset{p \in \mathbb{R}^n}{\text{minimize}}  \quad \nabla f(x_k)^T p + \frac{1}{2} p^T B_k p \\
\text{subject to}  \quad h(x_k) + \nabla h(x_k)^T p = 0 \\
 \quad g(x_k) + \nabla g(x_k)^T p \le 0
\end{align*}
$$

Solving this QP yields the search direction $p_k$ and a set of Lagrange multipliers associated with the QP's linear constraints. These QP multipliers provide excellent estimates for the Lagrange multipliers of the original NLP, which we can denote as $\lambda_{k+1}$ and $\mu_{k+1}$.

Let's illustrate with an example. Consider minimizing $f(x_1, x_2) = x_1^2 + \exp(x_2)$ subject to $c(x_1, x_2) = x_1^2 + x_2^2 - 1 = 0$. We wish to find the first SQP step $p_0$ from the initial guess $x_0 = (1, 1)^T$. For simplicity, we approximate the Hessian of the Lagrangian with the identity matrix, $B_0 = I$. First, we evaluate the necessary functions at $x_0$:

- Objective gradient: $\nabla f(x_0) = \begin{pmatrix} 2x_1 \\ \exp(x_2) \end{pmatrix} \Big|_{(1,1)} = \begin{pmatrix} 2 \\ \exp(1) \end{pmatrix}$
- Constraint value: $c(x_0) = 1^2 + 1^2 - 1 = 1$
- Constraint Jacobian: $\nabla c(x_0)^T = \begin{pmatrix} 2x_1  2x_2 \end{pmatrix} \Big|_{(1,1)} = \begin{pmatrix} 2  2 \end{pmatrix}$

The QP subproblem is to minimize $\frac{1}{2}p^T p + \begin{pmatrix} 2  \exp(1) \end{pmatrix} p$ subject to $1 + \begin{pmatrix} 2  2 \end{pmatrix} p = 0$. The solution to this QP is the search direction $p_0$. By solving the associated KKT system, we find $p_0 = \left(\frac{2 \exp(1) - 5}{4}, \frac{3 - 2 \exp(1)}{4}\right)^T$ [@problem_id:2202032]. This vector provides the direction for our first step towards the solution.

This process has a deep connection to Newton's method. The first-order [optimality conditions](@entry_id:634091) for a constrained problem, known as the Karush-Kuhn-Tucker (KKT) conditions, form a system of nonlinear equations. Applying Newton's method to solve this system results in a linear system of equations to be solved at each step. It can be shown that this Newton system is identical to the KKT system of the SQP subproblem when the exact Hessian of the Lagrangian, $B_k = \nabla_{xx}^2 \mathcal{L}(x_k, \lambda_k)$, is used [@problem_id:2202015]. This insight reveals that SQP is essentially a Newton-like method for constrained optimization, which helps explain its rapid local convergence.

Furthermore, the Lagrange multipliers obtained from solving the QP subproblem are used to update our estimates for the true multipliers of the NLP. For instance, if $\lambda_k$ is the current estimate and the QP solver yields a QP multiplier $\nu$, the new estimate is often taken as $\lambda_{k+1} = \nu$. In other formulations, especially those related to the Newton interpretation, the QP multiplier represents the *step* for the multipliers, so $\lambda_{k+1} = \lambda_k + \nu$ [@problem_id:2201973]. This [iterative refinement](@entry_id:167032) of the multipliers is critical, as they are needed to form an accurate Hessian of the Lagrangian.

### Practical Implementation: The Hessian and Globalization

Two key practical issues must be addressed to turn the theoretical SQP framework into a robust and efficient algorithm: how to handle the Hessian matrix $B_k$ and how to ensure the algorithm makes steady progress towards a solution from any starting point.

#### Quasi-Newton Hessian Approximations

Computing the exact Hessian of the Lagrangian, $\nabla_{xx}^2 \mathcal{L}$, can be prohibitively expensive or analytically intractable. A highly successful practical alternative is to use **quasi-Newton methods** to build an approximation $B_k$ using only first-order (gradient) information. The most popular of these is the **Broyden–Fletcher–Goldfarb–Shanno (BFGS)** update.

After taking a step $s_k = x_{k+1} - x_k = \alpha_k p_k$, we compute the change in the gradient of the Lagrangian:

$$
y_k = \nabla_x \mathcal{L}(x_{k+1}, \lambda_{k+1}) - \nabla_x \mathcal{L}(x_k, \lambda_{k+1})
$$

The vector $y_k$ captures the curvature information revealed by the step $s_k$. The BFGS formula then updates the previous Hessian approximation $B_k$ to a new matrix $B_{k+1}$ that satisfies the [secant condition](@entry_id:164914) $B_{k+1}s_k = y_k$:

$$
B_{k+1} = B_k - \frac{B_k s_k s_k^T B_k}{s_k^T B_k s_k} + \frac{y_k y_k^T}{y_k^T s_k}
$$

This update adds rank-two corrections to $B_k$ to progressively incorporate information about the problem's true curvature, without ever needing to compute second derivatives [@problem_id:2202033]. This has profound implications for convergence speed. While an SQP method using the exact Hessian converges locally at a **quadratic** rate, a quasi-Newton SQP method typically achieves a **superlinear** [rate of convergence](@entry_id:146534)—slower than quadratic, but still remarkably fast and achieved at a much lower computational cost per iteration [@problem_id:2201981].

#### Globalization via Merit Functions

The search direction $p_k$ is derived from a local model. A full step, $x_k + p_k$, may not be an improvement over $x_k$ in the context of the original NLP, especially when far from the solution. The iterate might move to a region with a much higher objective value or a much larger [constraint violation](@entry_id:747776). To ensure reliable progress from any starting point (i.e., to **globalize** the method), a [line search](@entry_id:141607) is performed along the direction $p_k$ to find a suitable step length $\alpha_k$.

The line search needs a criterion to judge whether a [potential step](@entry_id:148892) is "good". This is the role of a **[merit function](@entry_id:173036)**. A [merit function](@entry_id:173036) is a single, scalar-valued function that balances the dual goals of reducing the objective function $f(x)$ and satisfying the constraints. By seeking a step length $\alpha_k$ that reduces the [merit function](@entry_id:173036), we ensure that every step makes consistent progress toward a constrained optimum.

A common choice is the **$l_1$ [exact penalty function](@entry_id:176881)**:

$$
\phi_1(x; \rho) = f(x) + \rho \sum_i |h_i(x)| + \rho \sum_j \max(0, g_j(x))
$$

The **penalty parameter** $\rho > 0$ controls the weight given to constraint violations relative to the objective function value [@problem_id:2202029]. A key requirement for the [line search](@entry_id:141607) to succeed is that the search direction $p_k$ must be a descent direction for the [merit function](@entry_id:173036). For the $l_1$ [merit function](@entry_id:173036), this can be guaranteed if the [penalty parameter](@entry_id:753318) $\rho$ is chosen to be sufficiently large. Specifically, it can be shown that $p_k$ is a descent direction if $\rho$ is greater than the magnitude of the largest estimated Lagrange multiplier (in the [infinity norm](@entry_id:268861)). For a problem with multiplier estimates $\lambda_{k+1}$, the condition is:

$$
\rho > \|\lambda_{k+1}\|_{\infty} = \max_i |\lambda_{k+1, i}|
$$

This provides a practical rule for updating the [penalty parameter](@entry_id:753318) during the optimization process: at each iteration, ensure $\rho$ is larger than the maximum absolute value of the newly computed QP multipliers [@problem_id:2201986]. If the parameter is too small, the algorithm might prioritize reducing $f(x)$ at the expense of moving too far from the [feasible region](@entry_id:136622). If it is too large, the algorithm becomes overly focused on feasibility, potentially ignoring promising reductions in the objective.

By combining the local power of the QP model with the global reliability of a [merit function](@entry_id:173036) line search, quasi-Newton SQP methods provide a powerful and versatile tool for tackling a vast range of [nonlinear optimization](@entry_id:143978) problems in science and engineering.