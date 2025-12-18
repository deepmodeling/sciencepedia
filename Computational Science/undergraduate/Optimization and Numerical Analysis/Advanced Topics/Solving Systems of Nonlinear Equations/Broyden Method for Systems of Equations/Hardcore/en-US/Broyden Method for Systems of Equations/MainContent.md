## Introduction
Solving [systems of nonlinear equations](@entry_id:178110) of the form $\mathbf{F}(\mathbf{x}) = \mathbf{0}$ is a fundamental task that arises in nearly every branch of science and engineering. While Newton's method provides a powerful and rapidly converging framework for this problem, its practical application is often hampered by a significant drawback: the need to compute and invert a potentially large and complex Jacobian matrix at every single iteration. This computational burden can render the method impractical for the [large-scale systems](@entry_id:166848) encountered in real-world modeling.

This article introduces the Broyden method, a pioneering quasi-Newton algorithm designed specifically to overcome this limitation. It belongs to a class of methods that replace the true Jacobian with an approximation that is intelligently and cheaply updated from one iteration to the next. By doing so, it dramatically reduces computational cost while maintaining a fast, superlinear rate of convergence. Across the following chapters, you will gain a comprehensive understanding of this elegant and efficient numerical tool. The "Principles and Mechanisms" chapter will deconstruct the theory behind the method, from the foundational [secant condition](@entry_id:164914) to the [rank-one update](@entry_id:137543) formula. The "Applications and Interdisciplinary Connections" chapter will showcase its broad utility in fields ranging from [computational fluid dynamics](@entry_id:142614) to economics. Finally, the "Hands-On Practices" will provide concrete exercises to solidify your grasp of the core concepts.

## Principles and Mechanisms

Building upon the foundation of Newton's method for solving [systems of nonlinear equations](@entry_id:178110), $\mathbf{F}(\mathbf{x}) = \mathbf{0}$, we now turn to a class of methods designed to overcome its primary practical limitation: the high computational cost associated with the Jacobian matrix. While Newton's method, with its iterative step $\mathbf{x}_{k+1} = \mathbf{x}_k - J(\mathbf{x}_k)^{-1}\mathbf{F}(\mathbf{x}_k)$, offers rapid quadratic convergence, the requirement to compute the $n \times n$ Jacobian matrix $J(\mathbf{x}_k)$ and solve a linear system at every single iteration can be prohibitively expensive, especially for large systems. This chapter explores the principles and mechanisms of **quasi-Newton methods**, with a focus on the pioneering and widely used **Broyden's method**, which artfully circumvents these costs.

### The Quasi-Newton Approach: From Exact to Approximate Jacobians

The central idea behind quasi-Newton methods is to replace the true, and costly, Jacobian matrix $J(\mathbf{x}_k)$ with an approximation that is easier to compute and update. The iterative step of a generic quasi-Newton method is thus formulated as:
$$ \mathbf{x}_{k+1} = \mathbf{x}_k - B_k^{-1} \mathbf{F}(\mathbf{x}_k) $$
or, more practically, by solving the linear system:
$$ B_k \mathbf{s}_k = -\mathbf{F}(\mathbf{x}_k) \quad \text{where} \quad \mathbf{s}_k = \mathbf{x}_{k+1} - \mathbf{x}_k $$
Here, $B_k$ is the approximation to the Jacobian at the $k$-th iteration. The defining characteristic that makes a method "quasi-Newton" is that instead of recomputing this matrix from scratch at each step, it is updated from the previous approximation, $B_{k-1}$, using information gathered during the most recent step . This update procedure is designed to be computationally cheap, thereby avoiding the expensive partial derivative calculations and, as we will see, potentially the costly linear solve as well.

The critical question, then, is how to construct a meaningful update. A random or arbitrary approximation would likely lead to poor convergence. The ingenuity of quasi-Newton methods lies in the condition imposed upon the updated matrix.

### The Secant Condition: A Foundational Constraint

Quasi-Newton methods build their Jacobian approximations upon a simple yet powerful principle known as the **[secant condition](@entry_id:164914)**. This condition ensures that the new Jacobian approximation, $B_{k+1}$, is consistent with the most recently observed behavior of the function $\mathbf{F}$.

Let us define the step taken in iteration $k$ as the vector $\mathbf{s}_k = \mathbf{x}_{k+1} - \mathbf{x}_k$, and the corresponding change in the function value as the vector $\mathbf{y}_k = \mathbf{F}(\mathbf{x}_{k+1}) - \mathbf{F}(\mathbf{x}_k)$. A [fundamental theorem of calculus](@entry_id:147280) states that $\mathbf{F}(\mathbf{x}_{k+1}) - \mathbf{F}(\mathbf{x}_k) = \int_0^1 J(\mathbf{x}_k + t\mathbf{s}_k) \mathbf{s}_k \, dt$. This suggests the relationship $\mathbf{y}_k \approx J(\mathbf{x}_{k+1}) \mathbf{s}_k$. The [secant condition](@entry_id:164914) elevates this approximation to a requirement for our new model. It enforces that the updated Jacobian approximation, $B_{k+1}$, must satisfy the following equation exactly :
$$ B_{k+1} \mathbf{s}_k = \mathbf{y}_k $$
This equation is central to all quasi-Newton methods. It demands that the new linear model of the function, when acting on the previous step direction $\mathbf{s}_k$, yields the exact change in function value $\mathbf{y}_k$ that was observed.

A powerful geometric interpretation accompanies this algebraic condition. Consider the affine model of the function $\mathbf{F}$ at the new point $\mathbf{x}_{k+1}$, built using our approximation $B_{k+1}$:
$$ \mathbf{m}_{k+1}(\mathbf{x}) = \mathbf{F}(\mathbf{x}_{k+1}) + B_{k+1} (\mathbf{x} - \mathbf{x}_{k+1}) $$
If we evaluate this model at the *previous* iterate, $\mathbf{x} = \mathbf{x}_k$, we get:
$$ \mathbf{m}_{k+1}(\mathbf{x}_k) = \mathbf{F}(\mathbf{x}_{k+1}) + B_{k+1} (\mathbf{x}_k - \mathbf{x}_{k+1}) = \mathbf{F}(\mathbf{x}_{k+1}) - B_{k+1} \mathbf{s}_k $$
The [secant condition](@entry_id:164914), $B_{k+1} \mathbf{s}_k = \mathbf{y}_k = \mathbf{F}(\mathbf{x}_{k+1}) - \mathbf{F}(\mathbf{x}_k)$, implies that $\mathbf{m}_{k+1}(\mathbf{x}_k) = \mathbf{F}(\mathbf{x}_{k+1}) - (\mathbf{F}(\mathbf{x}_{k+1}) - \mathbf{F}(\mathbf{x}_k)) = \mathbf{F}(\mathbf{x}_k)$. This means the linear model constructed at the new point $\mathbf{x}_{k+1}$ is constrained to pass exactly through the previous point $(\mathbf{x}_k, \mathbf{F}(\mathbf{x}_k))$ . It is, in essence, a multi-dimensional generalization of the [secant line](@entry_id:178768) used in the one-dimensional [secant method](@entry_id:147486).

### Broyden's Method: The Least-Change Update

For a system in $\mathbb{R}^n$, the [secant equation](@entry_id:164522) $B_{k+1} \mathbf{s}_k = \mathbf{y}_k$ provides $n$ [linear equations](@entry_id:151487) to determine the $n^2$ elements of the matrix $B_{k+1}$. When $n > 1$, this system is underdetermined, meaning there are infinitely many matrices $B_{k+1}$ that satisfy the condition. Broyden's genius was to propose choosing the unique matrix that satisfies the [secant condition](@entry_id:164914) while being "closest" to the previous approximation, $B_k$. This is known as a **least-change update**.

Specifically, Broyden's first method (or "good" Broyden method) is derived by solving the following optimization problem :
$$ \min_{B \in \mathbb{R}^{n \times n}} \| B - B_k \|_F \quad \text{subject to} \quad B \mathbf{s}_k = \mathbf{y}_k $$
Here, $\| \cdot \|_F$ is the **Frobenius norm**, defined as $\|A\|_F = \sqrt{\sum_{i=1}^n \sum_{j=1}^n a_{ij}^2}$. Minimizing this norm corresponds to minimizing the sum of squared changes in all elements of the matrix.

The solution to this constrained optimization problem, which can be found using Lagrange multipliers, is the celebrated **Broyden update formula**:
$$ B_{k+1} = B_k + \frac{(\mathbf{y}_k - B_k \mathbf{s}_k) \mathbf{s}_k^T}{\mathbf{s}_k^T \mathbf{s}_k} $$
The update term is the outer product of the vector $(\mathbf{y}_k - B_k \mathbf{s}_k)$ and the vector $\mathbf{s}_k$, scaled by the scalar $1/(\mathbf{s}_k^T \mathbf{s}_k)$. A matrix formed by the [outer product](@entry_id:201262) of two vectors is a **[rank-one matrix](@entry_id:199014)**. Therefore, Broyden's method updates the Jacobian approximation with a simple and computationally inexpensive **[rank-one update](@entry_id:137543)** .

#### Illustrative Example: Jacobian Update

Let's solidify this with a numerical example. Consider solving $F(x_1, x_2) = \mathbf{0}$ for $F(x_1, x_2) = \begin{pmatrix} x_1^2 - 2x_2 - 1 \\ x_1 + x_2^2 - 3 \end{pmatrix}$. Suppose we start with an initial guess $\mathbf{x}_0 = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$ and an initial Jacobian approximation $B_0 = I = \begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix}$. After one step, we arrive at the new iterate $\mathbf{x}_1 = \begin{pmatrix} 3 \\ 2 \end{pmatrix}$. We wish to compute the updated approximation $B_1$ .

First, we compute the step vector $\mathbf{s}_0$ and the change in function value vector $\mathbf{y}_0$:
$$ \mathbf{s}_0 = \mathbf{x}_1 - \mathbf{x}_0 = \begin{pmatrix} 3 \\ 2 \end{pmatrix} - \begin{pmatrix} 1 \\ 1 \end{pmatrix} = \begin{pmatrix} 2 \\ 1 \end{pmatrix} $$
$$ \mathbf{F}(\mathbf{x}_0) = \begin{pmatrix} 1^2 - 2(1) - 1 \\ 1 + 1^2 - 3 \end{pmatrix} = \begin{pmatrix} -2 \\ -1 \end{pmatrix} $$
$$ \mathbf{F}(\mathbf{x}_1) = \begin{pmatrix} 3^2 - 2(2) - 1 \\ 3 + 2^2 - 3 \end{pmatrix} = \begin{pmatrix} 4 \\ 4 \end{pmatrix} $$
$$ \mathbf{y}_0 = \mathbf{F}(\mathbf{x}_1) - \mathbf{F}(\mathbf{x}_0) = \begin{pmatrix} 4 - (-2) \\ 4 - (-1) \end{pmatrix} = \begin{pmatrix} 6 \\ 5 \end{pmatrix} $$
Now, we compute the terms for the update formula:
$$ \mathbf{s}_0^T \mathbf{s}_0 = 2^2 + 1^2 = 5 $$
$$ B_0 \mathbf{s}_0 = \begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix} \begin{pmatrix} 2 \\ 1 \end{pmatrix} = \begin{pmatrix} 2 \\ 1 \end{pmatrix} $$
$$ \mathbf{y}_0 - B_0 \mathbf{s}_0 = \begin{pmatrix} 6 \\ 5 \end{pmatrix} - \begin{pmatrix} 2 \\ 1 \end{pmatrix} = \begin{pmatrix} 4 \\ 4 \end{pmatrix} $$
Finally, we assemble the update for $B_1$:
$$ B_1 = B_0 + \frac{(\mathbf{y}_0 - B_0 \mathbf{s}_0) \mathbf{s}_0^T}{\mathbf{s}_0^T \mathbf{s}_0} = \begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix} + \frac{1}{5} \begin{pmatrix} 4 \\ 4 \end{pmatrix} \begin{pmatrix} 2  1 \end{pmatrix} $$
$$ B_1 = \begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix} + \frac{1}{5} \begin{pmatrix} 8  4 \\ 8  4 \end{pmatrix} = \begin{pmatrix} 1+\frac{8}{5}  \frac{4}{5} \\ \frac{8}{5}  1+\frac{4}{5} \end{pmatrix} = \begin{pmatrix} \frac{13}{5}  \frac{4}{5} \\ \frac{8}{5}  \frac{9}{5} \end{pmatrix} $$
This new matrix $B_1$ now carries information from the first step and will be used to compute the next step, $\mathbf{s}_1$.

### Practical Efficiency: The Sherman-Morrison Formula

While the [rank-one update](@entry_id:137543) for $B_k$ is cheap (an $O(n^2)$ operation), the iteration still requires solving the linear system $B_k \mathbf{s}_k = -\mathbf{F}(\mathbf{x}_k)$, which generally costs $O(n^3)$ [floating-point operations](@entry_id:749454) (FLOPs). A remarkable enhancement in efficiency is achieved by reformulating the method to update the *inverse* of the Jacobian approximation, which we denote as $H_k = B_k^{-1}$, directly.

A [rank-one update](@entry_id:137543) to a matrix induces a corresponding [rank-one update](@entry_id:137543) to its inverse. This relationship is given by the **Sherman-Morrison formula**. Applying this formula to the Broyden update for $B_{k+1}$ gives the following update for its inverse, $H_{k+1} = B_{k+1}^{-1}$:
$$ H_{k+1} = H_k + \frac{(\mathbf{s}_k - H_k \mathbf{y}_k) \mathbf{s}_k^T H_k}{\mathbf{s}_k^T H_k \mathbf{y}_k} $$
With this formula, we can maintain and update the inverse approximation $H_k$ at each step. The primary computation of the iteration, finding the step $\mathbf{s}_k$, now becomes a simple [matrix-vector multiplication](@entry_id:140544), which costs only $O(n^2)$ FLOPs:
$$ \mathbf{s}_k = -H_k \mathbf{F}(\mathbf{x}_k) $$
The entire iteration, including the update of $H_k$, can thus be performed in $O(n^2)$ operations, a significant improvement over Newton's method's $O(n^3)$ cost.

#### Illustrative Example: Inverse Update

Let's apply this inverse update formula. Suppose for a certain problem, we are at an iterate $\mathbf{x}_k = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$ with an inverse Jacobian approximation $H_k = B_k^{-1} = \begin{pmatrix} \frac{1}{2}  \frac{1}{4} \\ \frac{1}{2}  \frac{1}{2} \end{pmatrix}$. The next iterate is found to be $\mathbf{x}_{k+1} = \begin{pmatrix} \frac{1}{2} \\ \frac{1}{2} \end{pmatrix}$, and the function values give us the vectors $\mathbf{s}_k = \begin{pmatrix} -1/2 \\ -1/2 \end{pmatrix}$ and $\mathbf{y}_k = \begin{pmatrix} -15/4 \\ -1/4 \end{pmatrix}$ .

We compute the necessary components for the inverse update:
$$ H_k \mathbf{y}_k = \begin{pmatrix} \frac{1}{2}  \frac{1}{4} \\ \frac{1}{2}  \frac{1}{2} \end{pmatrix} \begin{pmatrix} -15/4 \\ -1/4 \end{pmatrix} = \begin{pmatrix} -31/16 \\ -2 \end{pmatrix} $$
$$ \mathbf{s}_k - H_k \mathbf{y}_k = \begin{pmatrix} -1/2 \\ -1/2 \end{pmatrix} - \begin{pmatrix} -31/16 \\ -2 \end{pmatrix} = \begin{pmatrix} 23/16 \\ 3/2 \end{pmatrix} $$
$$ \mathbf{s}_k^T H_k = \begin{pmatrix} -1/2  -1/2 \end{pmatrix} \begin{pmatrix} 1/2  1/4 \\ 1/2  1/2 \end{pmatrix} = \begin{pmatrix} -1/2  -3/8 \end{pmatrix} $$
$$ \text{denominator} = \mathbf{s}_k^T (H_k \mathbf{y}_k) = \begin{pmatrix} -1/2  -1/2 \end{pmatrix} \begin{pmatrix} -31/16 \\ -2 \end{pmatrix} = \frac{31}{32} + 1 = \frac{63}{32} $$
The update term is:
$$ \frac{(\mathbf{s}_k - H_k \mathbf{y}_k) \mathbf{s}_k^T H_k}{\mathbf{s}_k^T H_k \mathbf{y}_k} = \frac{1}{63/32} \begin{pmatrix} 23/16 \\ 3/2 \end{pmatrix} \begin{pmatrix} -1/2  -3/8 \end{pmatrix} = \frac{32}{63} \begin{pmatrix} -23/32  -69/128 \\ -3/4  -9/16 \end{pmatrix} = \begin{pmatrix} -23/63  -23/84 \\ -8/21  -2/7 \end{pmatrix} $$
Finally, the updated inverse is:
$$ H_{k+1} = H_k + \text{update term} = \begin{pmatrix} 1/2  1/4 \\ 1/2  1/2 \end{pmatrix} + \begin{pmatrix} -23/63  -23/84 \\ -8/21  -2/7 \end{pmatrix} = \begin{pmatrix} \frac{17}{126}  -\frac{1}{42} \\ \frac{5}{42}  \frac{3}{14} \end{pmatrix} $$
This new matrix $H_{k+1}$ can now be used to find the next step with a simple [matrix-vector product](@entry_id:151002).

### Performance Analysis: Cost and Convergence

The motivation for Broyden's method is its computational efficiency. To quantify this, let's analyze the operational cost. Consider a system of size $n=30$ where the Jacobian is dense and complex. Typical costs in FLOPs might be: evaluating $\mathbf{F}(\mathbf{x})$ costs $C_F = 15n^2$, evaluating the true Jacobian $J(\mathbf{x})$ costs $C_J = 20n^3$, and solving an $n \times n$ linear system costs $C_{solve} = \frac{2}{3}n^3$. A Broyden [rank-one update](@entry_id:137543) is much cheaper, say $C_{update} = 3n^2$ .

The cost of two iterations of **Newton's method** involves two function evaluations, two Jacobian evaluations, and two linear solves:
$$ C_{\text{Newton}} = 2(C_F + C_J + C_{solve}) $$
For **Broyden's method**, if we start with an exact Jacobian $B_0 = J(\mathbf{x}_0)$, the first iteration is identical to Newton's. The second iteration, however, re-uses the old function value $\mathbf{F}(\mathbf{x}_1)$, performs a cheap update to get $B_1$, and then solves a linear system. The cost for two iterations is:
$$ C_{\text{Broyden}} = (C_F + C_J + C_{solve}) + (C_F + C_{update} + C_{solve}) = 2C_F + C_J + 2C_{solve} + C_{update} $$
The cost reduction is therefore:
$$ \Delta C = C_{\text{Newton}} - C_{\text{Broyden}} = C_J - C_{update} $$
With $n=30$, this reduction is $20(30^3) - 3(30^2) = 540000 - 2700 = 537,300$ FLOPs. This demonstrates the substantial savings achieved in every iteration after the first, by replacing the expensive Jacobian evaluation with a cheap [rank-one update](@entry_id:137543).

This computational saving comes at the cost of a reduced convergence rate. While Newton's method exhibits [quadratic convergence](@entry_id:142552) (the number of correct digits roughly doubles each iteration), Broyden's method has a slower **superlinear** convergence rate. For the one-dimensional case, Broyden's method reduces to the secant method, whose [order of convergence](@entry_id:146394) is the [golden ratio](@entry_id:139097), $p = \frac{1+\sqrt{5}}{2} \approx 1.618$ . In multiple dimensions, the convergence is still superlinear (i.e., faster than linear, $||\mathbf{e}_{k+1}|| \le C ||\mathbf{e}_k||^p$ with $p>1$) but generally not as fast as Newton's method. This trade-off—slower convergence per iteration for a much lower cost per iteration—is often highly favorable, making Broyden's method a workhorse algorithm in [scientific computing](@entry_id:143987).

Finally, it is important to recognize a potential vulnerability. The method relies on solving the system $B_k \mathbf{s}_k = -\mathbf{F}(\mathbf{x}_k)$ or equivalently, on the existence of $B_k^{-1}$. If the approximation $B_k$ becomes singular or nearly singular during the iterative process, the algorithm can fail. If $B_k$ is singular, the linear system for the step $\mathbf{s}_k$ is no longer guaranteed to have a unique solution; it may have no solutions or infinitely many, preventing the algorithm from computing a well-defined next step . Robust software implementations of Broyden's method include safeguards, such as monitoring the conditioning of $B_k$ and periodically resetting the approximation to the true Jacobian if it degrades.