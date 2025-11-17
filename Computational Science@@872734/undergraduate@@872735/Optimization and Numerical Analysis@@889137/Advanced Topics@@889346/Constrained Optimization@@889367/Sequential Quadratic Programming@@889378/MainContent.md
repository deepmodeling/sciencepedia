## Introduction
Sequential Quadratic Programming (SQP) stands as one of the most powerful and versatile algorithms for solving [constrained nonlinear optimization](@entry_id:634866) problems, which are ubiquitous in science, engineering, and finance. These problems are often intractable to solve directly due to the complex, nonlinear nature of their objectives and constraints. This article provides a comprehensive guide to understanding and applying the SQP method, bridging the gap between theoretical concepts and practical problem-solving.

The journey begins in the **Principles and Mechanisms** chapter, where we will dissect the core iterative strategy of SQP, exploring how it constructs and solves a sequence of simpler Quadratic Program (QP) subproblems. Next, in **Applications and Interdisciplinary Connections**, we will showcase the method's real-world power, demonstrating its use in diverse fields from optimal control in robotics to [portfolio optimization](@entry_id:144292) in finance. Finally, the **Hands-On Practices** section will solidify your understanding by guiding you through practical exercises, allowing you to apply the principles you've learned to concrete optimization tasks. This structured approach will equip you with a robust understanding of both the 'how' and the 'why' behind this essential optimization technique.

## Principles and Mechanisms

Sequential Quadratic Programming (SQP) stands as one of the most effective and widely utilized methods for solving general [nonlinear optimization](@entry_id:143978) problems. Its power lies in an elegant iterative strategy: at each step, it approximates the complex, nonlinear problem with a simpler, more structured one that can be solved efficiently. This chapter elucidates the fundamental principles and core mechanisms that underpin the SQP algorithm, from the formulation of its subproblem to the theoretical connections that guarantee its performance and the practical considerations that ensure its robustness.

### The Core Idea: A Sequence of Quadratic Approximations

A general [nonlinear programming](@entry_id:636219) (NLP) problem can be expressed in the form:
$$
\begin{align*}
\underset{x \in \mathbb{R}^n}{\text{minimize}}  \quad f(x) \\
\text{subject to}  \quad h(x) = 0 \\
 \quad g(x) \le 0
\end{align*}
$$
where $f: \mathbb{R}^n \to \mathbb{R}$ is the objective function, $h: \mathbb{R}^n \to \mathbb{R}^m$ represents a set of $m$ equality constraints, and $g: \mathbb{R}^n \to \mathbb{R}^p$ represents a set of $p$ [inequality constraints](@entry_id:176084). The functions $f$, $h$, and $g$ are assumed to be smooth.

The direct solution of this problem is often intractable due to the nonlinearities in both the objective and the constraints. The central strategy of SQP is to replace this difficult problem with a sequence of more manageable ones. At a given iterate $x_k$, the algorithm computes a search direction, or step, $p$, by solving an approximation of the original NLP. This approximation is constructed by modeling the essential features of the original problem in a neighborhood of $x_k$.

The critical simplification is twofold. First, the nonlinear constraints are replaced by their first-order Taylor approximations around the current iterate $x_k$. For a step $p = x - x_k$, the constraints $h(x)=0$ and $g(x) \le 0$ are approximated by:
$$
\begin{align*}
h(x_k) + \nabla h(x_k)^T p = 0 \\
g(x_k) + \nabla g(x_k)^T p \le 0
\end{align*}
$$
where $\nabla h(x_k)$ and $\nabla g(x_k)$ are the Jacobian matrices of the respective constraint functions evaluated at $x_k$. This [linearization](@entry_id:267670) is the cornerstone of the method. Its primary computational motivation is that it transforms the complex, curved [feasible region](@entry_id:136622) of the NLP into a polytope defined by linear equations and inequalities.

Second, the objective function is modeled by a quadratic function. This provides a better approximation of the function's local behavior than a simple linear model, as it captures curvature information. The combination of a quadratic objective and [linear constraints](@entry_id:636966) defines a **Quadratic Program (QP)**. The ability to formulate this subproblem as a QP is the principal reason for the linearization of constraints, as highly efficient and mature solvers exist for this class of problems [@problem_id:2202046]. This iterative process of forming and solving a QP at each step gives the method its name: **Sequential Quadratic Programming**.

### The Role of the Lagrangian in the Quadratic Model

To construct an appropriate quadratic model for the objective, we must account for the influence of the constraints. The **Lagrangian function**, $L(x, \lambda, \mu)$, provides a systematic way to do this by combining the objective and constraint functions into a single entity:
$$
L(x, \lambda, \mu) = f(x) + \lambda^T h(x) + \mu^T g(x)
$$
Here, $\lambda \in \mathbb{R}^m$ and $\mu \in \mathbb{R}^p$ are vectors of **Lagrange multipliers** associated with the equality and [inequality constraints](@entry_id:176084), respectively [@problem_id:2202030]. The Lagrangian is central to [constrained optimization theory](@entry_id:635923) because the [optimality conditions](@entry_id:634091) for the original NLP, known as the Karush-Kuhn-Tucker (KKT) conditions, are expressed in terms of its gradient and Hessian.

The SQP subproblem at an iterate $(x_k, \lambda_k, \mu_k)$ is constructed to find a step $p$ that makes progress toward satisfying these KKT conditions. The objective of the QP subproblem is therefore a quadratic model of the Lagrangian function, not just the [objective function](@entry_id:267263) $f(x)$. The full QP subproblem is formulated as:
$$
\begin{align*}
\underset{p \in \mathbb{R}^n}{\text{minimize}}  \quad \frac{1}{2} p^T B_k p + \nabla f(x_k)^T p \\
\text{subject to}  \quad h(x_k) + \nabla h(x_k)^T p = 0 \\
 \quad g(x_k) + \nabla g(x_k)^T p \le 0
\end{align*}
$$
The matrix $B_k$ is a symmetric matrix that approximates the **Hessian of the Lagrangian function**, $\nabla_{xx}^2 L(x_k, \lambda_k, \mu_k)$. The linear term, $\nabla f(x_k)^T p$, represents the first-order change in the [objective function](@entry_id:267263). The term involving the gradient of the Lagrangian, $\nabla_x L(x_k, \lambda_k, \mu_k)$, is implicitly represented, as its components are split between the QP objective and the QP constraints' Lagrange multipliers.

### Solving the Subproblem and Interpreting the Result

At each major iteration of the SQP algorithm, a specialized **QP solver** is invoked to solve the subproblem defined above. The primary role of this solver is to compute the optimal step vector $p_k$, which serves as a **search direction** for updating the current variable estimate $x_k$ [@problem_id:2201997]. The new iterate is then typically found via a [line search](@entry_id:141607), $x_{k+1} = x_k + \alpha_k p_k$, where $\alpha_k$ is a step length chosen to ensure progress towards a solution.

Let's illustrate the mechanics of solving the subproblem with an example. Consider minimizing $f(x_1, x_2) = x_1^2 + \exp(x_2)$ subject to the equality constraint $c(x_1, x_2) = x_1^2 + x_2^2 - 1 = 0$. Starting from $x_0 = (1, 1)^T$ and approximating the Hessian of the Lagrangian with the identity matrix, $B_0 = I$, the QP subproblem becomes:
$$
\min_{p} \frac{1}{2}p^T p + \nabla f(x_0)^T p \quad \text{subject to} \quad c(x_0) + \nabla c(x_0)^T p = 0
$$
We evaluate the necessary quantities at $x_0 = (1, 1)^T$:
$$
\nabla f(x_0) = \begin{pmatrix} 2 \\ \exp(1) \end{pmatrix}, \quad c(x_0) = 1^2 + 1^2 - 1 = 1, \quad \nabla c(x_0) = \begin{pmatrix} 2 \\ 2 \end{pmatrix}
$$
The KKT conditions for this QP subproblem form a system of linear equations for the step $p_0$ and the QP's Lagrange multiplier $\nu_0$. Solving this system yields the search direction $p_0$ [@problem_id:2202032].

A profound insight arises when the solution to the QP subproblem is the zero vector, $p_k = 0$. If this occurs, the KKT conditions for the QP simplify to reveal that the current point $x_k$ is, in fact, a KKT point for the original nonlinear problem. Specifically, the QP feasibility condition $c(x_k) + \nabla c(x_k)^T p_k = 0$ implies $c(x_k) = 0$ (primal feasibility). The QP [stationarity condition](@entry_id:191085) implies that there exists a multiplier $\nu_k$ (the multiplier from the QP) such that $\nabla f(x_k) + \nabla c(x_k) \nu_k = 0$ (stationarity). Thus, $x_k$ satisfies the NLP's KKT conditions with multiplier $\nu_k$, and the algorithm can terminate [@problem_id:2201970].

### The Connection to Newton's Method

The structure of the SQP subproblem is not arbitrary; it can be rigorously derived by applying **Newton's method** to find a root of the KKT conditions of the original NLP. For an equality-constrained problem, the KKT conditions form a system of nonlinear equations in terms of the variables $x$ and the multipliers $\lambda$:
$$
\begin{cases}
\nabla_x L(x, \lambda)  = \nabla f(x) + \nabla h(x) \lambda = 0 \\
h(x)  = 0
\end{cases}
$$
Applying one step of Newton's method at an iterate $(x_k, \lambda_k)$ to solve this system for a step $(p, \Delta\lambda)$ leads to the linear system:
$$
\begin{pmatrix}
\nabla_{xx}^2 L(x_k, \lambda_k) & \nabla h(x_k) \\
\nabla h(x_k)^T & 0
\end{pmatrix}
\begin{pmatrix}
p \\
\Delta\lambda
\end{pmatrix}
=
\begin{pmatrix}
-\nabla_x L(x_k, \lambda_k) \\
-h(x_k)
\end{pmatrix}
$$
This linear system is precisely the KKT system for the QP subproblem, provided we set the QP Hessian $B_k = \nabla_{xx}^2 L(x_k, \lambda_k)$ and identify the new multiplier estimate as $\lambda_{k+1} = \lambda_k + \Delta\lambda$. This connection reveals that SQP is a Newton-like method applied in the combined space of primal variables and dual multipliers [@problem_id:2202015].

This perspective also clarifies the role of the QP multipliers. The multipliers obtained from solving the QP subproblem at step $k$ provide a high-quality estimate for the multipliers of the original problem at the solution. They are used to form the next multiplier estimate, $\lambda_{k+1}$ [@problem_id:2201973], which is then used in constructing the Hessian approximation for the subsequent iteration.

### Practical Mechanisms: Hessian Updates and Globalization

#### Quasi-Newton Hessian Approximations
In practice, computing the exact second derivatives required for the Hessian of the Lagrangian, $\nabla_{xx}^2 L$, can be prohibitively expensive or analytically intractable. **Quasi-Newton SQP** methods circumvent this by building an approximation $B_k$ using only first-order information (gradients).

After computing a step $p_k$ and finding the next iterate $x_{k+1} = x_k + p_k$ (assuming a full step for simplicity), we can compute the change in the gradient of the Lagrangian. The update vectors are defined as:
$$
s_k = x_{k+1} - x_k = p_k
$$
$$
y_k = \nabla_x L(x_{k+1}, \lambda_{k+1}) - \nabla_x L(x_k, \lambda_{k+1})
$$
Note that the same multiplier estimate, $\lambda_{k+1}$, is used for both gradient evaluations to properly isolate the effect of the change in $x$. The matrix $B_{k+1}$ should ideally satisfy the **[secant condition](@entry_id:164914)**, $B_{k+1} s_k = y_k$. The **Broyden-Fletcher-Goldfarb-Shanno (BFGS)** update formula is a popular and effective way to update $B_k$ to a new matrix $B_{k+1}$ that satisfies this condition while remaining symmetric and [positive definite](@entry_id:149459) (under certain conditions):
$$
B_{k+1} = B_k - \frac{B_k s_k s_k^T B_k}{s_k^T B_k s_k} + \frac{y_k y_k^T}{y_k^T s_k}
$$
This update allows the algorithm to accumulate curvature information over iterations without ever explicitly forming the true Hessian matrix [@problem_id:2202033].

#### Globalization with Merit Functions
The search direction $p_k$ generated by the QP subproblem is based on a local model at $x_k$. Taking a full step $x_k + p_k$ may not be productive if $x_k$ is far from the solution; it could lead to an increase in the objective value or [constraint violation](@entry_id:747776). To ensure reliable convergence from any starting point (a property known as **globalization**), the algorithm must carefully control the step length $\alpha_k$.

This is achieved using a **[merit function](@entry_id:173036)**, $\phi(x; \mu)$. A [merit function](@entry_id:173036) is a composite scalar function designed to balance the two competing goals of optimization: reducing the [objective function](@entry_id:267263) $f(x)$ and satisfying the constraints (i.e., reducing their violation). A common example is the $\ell_1$ [penalty function](@entry_id:638029):
$$
\phi(x; \mu) = f(x) + \mu \sum_{i=1}^m |h_i(x)| + \mu \sum_{j=1}^p \max(0, g_j(x))
$$
where $\mu > 0$ is a [penalty parameter](@entry_id:753318). The search direction $p_k$ can be shown to be a descent direction for this [merit function](@entry_id:173036) under suitable assumptions. The algorithm then performs a **line search** along $p_k$ to find a step length $\alpha_k \in (0, 1]$ that yields a [sufficient decrease](@entry_id:174293) in the value of the [merit function](@entry_id:173036). This procedure ensures that each step makes measurable progress towards the solution, even from highly infeasible points, thereby guiding the iterates toward a KKT point [@problem_id:2202029].

### Robustness: Handling Infeasible Subproblems

A practical challenge in SQP is that the linearized constraints of the QP subproblem may be mutually inconsistent, rendering the QP infeasible. This can happen even if the original NLP is feasible. A robust SQP solver must be able to handle this situation without terminating prematurely.

When a QP subproblem is found to be infeasible, the algorithm enters a **feasibility restoration phase**. The objective temporarily shifts from making progress on the Lagrangian model to simply finding a new point with reduced [constraint violation](@entry_id:747776). This is accomplished by solving an auxiliary optimization problem, often a linear program, whose goal is to minimize a measure of infeasibility, such as the $\ell_1$ norm of the constraint residuals. For instance, the algorithm might seek a step that minimizes $\|h(x_k+p)\|_1 + \|[g(x_k+p)]_+\|_1$ with respect to the linearized constraints. Once a step is taken that improves feasibility, the algorithm can return to the standard SQP mode of minimizing the quadratic model of the Lagrangian [@problem_id:2202017]. This two-phase strategy makes the SQP method a powerful and reliable tool for a wide range of real-world optimization problems.