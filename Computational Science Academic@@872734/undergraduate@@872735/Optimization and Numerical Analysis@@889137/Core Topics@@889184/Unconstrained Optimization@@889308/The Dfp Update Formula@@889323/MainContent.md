## Introduction
The quest for efficient and reliable algorithms to solve [optimization problems](@entry_id:142739) is a central theme in numerical analysis and [applied mathematics](@entry_id:170283). Among the most powerful techniques for [unconstrained optimization](@entry_id:137083) are quasi-Newton methods, which seek to emulate the rapid convergence of Newton's method without its prohibitive computational cost. The Davidon-Fletcher-Powell (DFP) formula represents a pioneering breakthrough in this class of algorithms, offering an ingenious way to approximate the inverse of the Hessian matrix iteratively. This article addresses the fundamental challenge of modeling a function's curvature efficiently, a gap that the DFP method elegantly fills.

Across the following chapters, you will gain a deep understanding of this landmark algorithm. The first chapter, "Principles and Mechanisms," will deconstruct the DFP formula, explaining its derivation from the [secant condition](@entry_id:164914) and detailing its crucial mathematical properties, such as symmetry and positive definiteness. The second chapter, "Applications and Interdisciplinary Connections," will situate DFP within the broader optimization landscape, compare it with the now-dominant BFGS method, and explore its adaptations for large-scale and constrained problems in science and engineering. Finally, the "Hands-On Practices" section will provide concrete exercises to solidify your grasp of the update's mechanics. We begin by exploring the core principles that make the DFP update a cornerstone of modern optimization theory.

## Principles and Mechanisms

The Davidon-Fletcher-Powell (DFP) formula stands as a landmark achievement in the development of quasi-Newton methods for [unconstrained optimization](@entry_id:137083). It provides an iterative procedure for approximating the inverse Hessian matrix of an objective function without the need to compute second derivatives. This chapter elucidates the fundamental principles governing the DFP update, its essential mathematical properties, and the mechanisms that ensure its stability and effectiveness.

### The DFP Update Formula

In a quasi-Newton [optimization algorithm](@entry_id:142787), we seek to minimize a function $f(\mathbf{x})$ by generating a sequence of iterates $\mathbf{x}_k$. At each iteration $k$, we move from the current point $\mathbf{x}_k$ to a new point $\mathbf{x}_{k+1}$ along a search direction $\mathbf{p}_k$. The update is given by $\mathbf{x}_{k+1} = \mathbf{x}_k + \alpha_k \mathbf{p}_k$, where $\alpha_k$ is a step length determined by a [line search](@entry_id:141607). The search direction is computed using an approximation to the inverse Hessian, denoted by a [symmetric positive-definite matrix](@entry_id:136714) $H_k$:
$$
\mathbf{p}_k = -H_k \mathbf{g}_k
$$
where $\mathbf{g}_k = \nabla f(\mathbf{x}_k)$ is the gradient at $\mathbf{x}_k$.

After taking the step, we gain new information about the curvature of the function from the change in position, $\mathbf{s}_k = \mathbf{x}_{k+1} - \mathbf{x}_k$, and the corresponding change in the gradient, $\mathbf{y}_k = \mathbf{g}_{k+1} - \mathbf{g}_k$. The DFP method uses this information to update the inverse Hessian approximation from $H_k$ to $H_{k+1}$. The celebrated **DFP update formula** is a rank-two correction to the previous approximation:

$$
H_{k+1} = H_k + \frac{\mathbf{s}_k \mathbf{s}_k^T}{\mathbf{s}_k^T \mathbf{y}_k} - \frac{H_k \mathbf{y}_k \mathbf{y}_k^T H_k}{\mathbf{y}_k^T H_k \mathbf{y}_k}
$$

Here, terms like $\mathbf{u}\mathbf{v}^T$ represent the outer product of vectors $\mathbf{u}$ and $\mathbf{v}$, resulting in a matrix. The denominators $\mathbf{s}_k^T \mathbf{y}_k$ and $\mathbf{y}_k^T H_k \mathbf{y}_k$ are scalars. This update elegantly incorporates the new curvature information contained in the pair $(\mathbf{s}_k, \mathbf{y}_k)$ to refine the model of the function's geometry.

### The Secant Condition: The Core Rationale

The central idea behind all quasi-Newton methods is to build a Hessian approximation that mimics the behavior of the true Hessian. The foundation for this is the first-order Taylor series expansion of the gradient $\nabla f(\mathbf{x})$ around $\mathbf{x}_{k+1}$:
$$
\nabla f(\mathbf{x}) \approx \nabla f(\mathbf{x}_{k+1}) + \nabla^2 f(\mathbf{x}_{k+1}) (\mathbf{x} - \mathbf{x}_{k+1})
$$
Evaluating this approximation at $\mathbf{x} = \mathbf{x}_k$ gives:
$$
\mathbf{g}_k \approx \mathbf{g}_{k+1} + \nabla^2 f(\mathbf{x}_{k+1}) (\mathbf{x}_k - \mathbf{x}_{k+1})
$$
Rearranging the terms and using our definitions $\mathbf{s}_k = \mathbf{x}_{k+1} - \mathbf{x}_k$ and $\mathbf{y}_k = \mathbf{g}_{k+1} - \mathbf{g}_k$, we arrive at an approximate relationship involving the true Hessian at the new point, $B_{k+1} = \nabla^2 f(\mathbf{x}_{k+1})$:
$$
\mathbf{y}_k \approx B_{k+1} \mathbf{s}_k
$$
Quasi-Newton methods elevate this approximation to a condition. They require the *new* Hessian approximation, let's also call it $B_{k+1}$, to satisfy this equation exactly for the most recent step:
$$
B_{k+1} \mathbf{s}_k = \mathbf{y}_k
$$
This is known as the **[secant equation](@entry_id:164522)**. It ensures that the updated model of the Hessian correctly relates the change in gradient to the change in position along the most recent step direction.

The DFP method works with the inverse Hessian approximation, $H_k$. To find the equivalent condition for $H_{k+1}$, we can assume $B_{k+1}$ is invertible and left-multiply the [secant equation](@entry_id:164522) by its inverse, $H_{k+1} = B_{k+1}^{-1}$:
$$
H_{k+1} (B_{k+1} \mathbf{s}_k) = H_{k+1} \mathbf{y}_k
$$
$$
(H_{k+1} B_{k+1}) \mathbf{s}_k = H_{k+1} \mathbf{y}_k
$$
$$
I \mathbf{s}_k = H_{k+1} \mathbf{y}_k
$$
This leads to the primary condition that the DFP update is designed to satisfy, known as the **inverse [secant equation](@entry_id:164522)** [@problem_id:2212542]:
$$
H_{k+1} \mathbf{y}_k = \mathbf{s}_k
$$
This equation is the fundamental requirement that the DFP formula is constructed to fulfill. It is the mathematical embodiment of incorporating the latest curvature information into the inverse Hessian model.

### Verification of the Secant Condition

It is instructive to directly verify that the DFP formula indeed satisfies the inverse [secant equation](@entry_id:164522). We can do this through straightforward algebraic manipulation [@problem_id:2212506]. Let us right-multiply the DFP formula by the vector $\mathbf{y}_k$:
$$
H_{k+1} \mathbf{y}_k = H_k \mathbf{y}_k + \left( \frac{\mathbf{s}_k \mathbf{s}_k^T}{\mathbf{s}_k^T \mathbf{y}_k} \right) \mathbf{y}_k - \left( \frac{H_k \mathbf{y}_k \mathbf{y}_k^T H_k}{\mathbf{y}_k^T H_k \mathbf{y}_k} \right) \mathbf{y}_k
$$
We analyze the second and third terms on the right-hand side. For the second term, we recognize that $\mathbf{s}_k^T \mathbf{y}_k$ is a scalar. Thus, we can regroup the terms:
$$
\frac{(\mathbf{s}_k \mathbf{s}_k^T) \mathbf{y}_k}{\mathbf{s}_k^T \mathbf{y}_k} = \frac{\mathbf{s}_k (\mathbf{s}_k^T \mathbf{y}_k)}{\mathbf{s}_k^T \mathbf{y}_k} = \mathbf{s}_k
$$
Similarly, for the third term, the denominator $\mathbf{y}_k^T H_k \mathbf{y}_k$ is also a scalar. We can regroup the numerator as $(H_k \mathbf{y}_k) (\mathbf{y}_k^T H_k \mathbf{y}_k)$, leading to:
$$
\frac{(H_k \mathbf{y}_k \mathbf{y}_k^T H_k) \mathbf{y}_k}{\mathbf{y}_k^T H_k \mathbf{y}_k} = \frac{(H_k \mathbf{y}_k) (\mathbf{y}_k^T H_k \mathbf{y}_k)}{\mathbf{y}_k^T H_k \mathbf{y}_k} = H_k \mathbf{y}_k
$$
Substituting these simplifications back into the main expression, we find that the terms involving $H_k \mathbf{y}_k$ cancel out:
$$
H_{k+1} \mathbf{y}_k = H_k \mathbf{y}_k + \mathbf{s}_k - H_k \mathbf{y}_k = \mathbf{s}_k
$$
This confirms that the DFP formula is precisely constructed to satisfy the inverse [secant condition](@entry_id:164914), regardless of the specific values of $\mathbf{s}_k$ and $\mathbf{y}_k$ (provided the denominators are non-zero).

### Key Properties of the DFP Update

For a quasi-Newton method to be robust and effective, the sequence of matrices ${H_k}$ it generates should possess certain desirable properties. The DFP update ensures two of these are maintained under specific conditions: symmetry and positive definiteness.

#### Symmetry Preservation

The true Hessian matrix of a twice continuously differentiable function is symmetric. It is therefore natural to require that its approximation, and by extension its inverse approximation $H_k$, also be symmetric. The DFP formula is designed to preserve this property. If we start with a symmetric matrix $H_0$ (the identity matrix is a common choice), then every subsequent $H_k$ will also be symmetric [@problem_id:2212534].

To see this, we can examine the transpose of the update formula:
$$
H_{k+1}^T = H_k^T + \left( \frac{\mathbf{s}_k \mathbf{s}_k^T}{\mathbf{s}_k^T \mathbf{y}_k} \right)^T - \left( \frac{H_k \mathbf{y}_k \mathbf{y}_k^T H_k}{\mathbf{y}_k^T H_k \mathbf{y}_k} \right)^T
$$
Assuming $H_k$ is symmetric (i.e., $H_k^T = H_k$), the first term is symmetric. The second term involves the [outer product](@entry_id:201262) $\mathbf{s}_k \mathbf{s}_k^T$, which is inherently symmetric. Its transpose is itself. For the third term, we use the property $(ABC)^T = C^T B^T A^T$:
$$
(H_k \mathbf{y}_k \mathbf{y}_k^T H_k)^T = H_k^T (\mathbf{y}_k^T)^T \mathbf{y}_k^T H_k^T = H_k \mathbf{y}_k \mathbf{y}_k^T H_k
$$
Since each component of the update is symmetric, their sum is also symmetric. Therefore, $H_{k+1}^T = H_{k+1}$, and by induction, symmetry is preserved throughout the iterative process.

#### Positive Definiteness and the Curvature Condition

The most critical property of the inverse Hessian approximation $H_k$ is that it must be **[positive definite](@entry_id:149459)**. A [symmetric matrix](@entry_id:143130) $H$ is positive definite if the quadratic form $\mathbf{z}^T H \mathbf{z} > 0$ for all non-zero vectors $\mathbf{z}$. This property is essential because it guarantees that the search direction $\mathbf{p}_k = -H_k \mathbf{g}_k$ is a **descent direction**, meaning it makes an angle greater than 90 degrees with the gradient vector. This ensures that a small step along $\mathbf{p}_k$ will decrease the function value:
$$
\mathbf{g}_k^T \mathbf{p}_k = \mathbf{g}_k^T (-H_k \mathbf{g}_k) = -\mathbf{g}_k^T H_k \mathbf{g}_k  0
$$
The inequality holds because $H_k$ is positive definite and $\mathbf{g}_k$ is non-zero (otherwise the minimum is found).

The DFP update preserves positive definiteness if and only if a single condition on the step and gradient-change vectors is met. This is the **curvature condition** [@problem_id:2212498]:
$$
\mathbf{s}_k^T \mathbf{y}_k > 0
$$
This condition has a clear geometric interpretation. The term $\mathbf{s}_k^T \mathbf{y}_k = (\mathbf{x}_{k+1} - \mathbf{x}_k)^T(\nabla f(\mathbf{x}_{k+1}) - \nabla f(\mathbf{x}_k))$ approximates the second-order directional derivative. A positive value implies that the function's gradient is increasing along the step direction $\mathbf{s}_k$, indicating [positive curvature](@entry_id:269220), which is consistent with moving towards a minimum.

Failure to satisfy the curvature condition can have catastrophic consequences for the algorithm. If $\mathbf{s}_k^T \mathbf{y}_k \le 0$, the DFP update is not guaranteed to produce a [positive definite](@entry_id:149459) $H_{k+1}$. As an example, consider a step where $H_k = I$, $\mathbf{s}_k = \begin{pmatrix} 2 \\ 0 \end{pmatrix}$, and $\mathbf{y}_k = \begin{pmatrix} -1 \\ 1 \end{pmatrix}$. Here, the curvature condition is violated: $\mathbf{s}_k^T \mathbf{y}_k = -2  0$. Applying the DFP formula yields the updated matrix [@problem_id:2212483]:
$$
H_{k+1} = \begin{pmatrix} -1.5  0.5 \\ 0.5  0.5 \end{pmatrix}
$$
The eigenvalues of this matrix are approximately $0.618$ and $-1.618$. The presence of a negative eigenvalue means the matrix is indefinite, not positive definite. Using this $H_{k+1}$ in the next iteration may produce a search direction that increases the function value, causing the optimization to fail.

To prevent this, practical implementations do not rely on chance. The step length $\alpha_k$ is chosen by a line search procedure that explicitly enforces conditions to guarantee $\mathbf{s}_k^T \mathbf{y}_k > 0$. The most common are the **strong Wolfe conditions**, which require $\alpha_k$ to satisfy:
1. $f(\mathbf{x}_k + \alpha_k \mathbf{p}_k) \le f(\mathbf{x}_k) + c_1 \alpha_k \mathbf{g}_k^T \mathbf{p}_k$ (Sufficient Decrease)
2. $|\mathbf{g}(\mathbf{x}_k + \alpha_k \mathbf{p}_k)^T \mathbf{p}_k| \le c_2 |\mathbf{g}_k^T \mathbf{p}_k|$ (Curvature Condition)
where $0  c_1  c_2  1$.

The second Wolfe condition directly ensures the curvature requirement for the DFP update. By rearranging the inequality, we can show that $\mathbf{g}_{k+1}^T \mathbf{p}_k \ge -c_2(-\mathbf{g}_k^T \mathbf{p}_k) = c_2 \mathbf{g}_k^T \mathbf{p}_k$. Using this, we can establish a lower bound on the curvature term [@problem_id:2212526]:
$$
\mathbf{s}_k^T \mathbf{y}_k = \alpha_k (\mathbf{g}_{k+1}^T - \mathbf{g}_k^T) \mathbf{p}_k \ge \alpha_k (c_2 - 1) \mathbf{g}_k^T \mathbf{p}_k = (1-c_2)(-\alpha_k \mathbf{g}_k^T \mathbf{p}_k)
$$
Since $c_2  1$ and $-\alpha_k \mathbf{g}_k^T \mathbf{p}_k > 0$, this guarantees that $\mathbf{s}_k^T \mathbf{y}_k$ is strictly positive, thus securing the [positive definiteness](@entry_id:178536) of $H_{k+1}$.

### An Illustrative Example of a DFP Iteration

To consolidate these principles, let us perform one full iteration of the DFP algorithm [@problem_id:2212537]. Consider the task of minimizing the simple quadratic function $f(x_1, x_2) = x_1^2 + 2x_2^2$. We start at the initial point $\mathbf{x}_0 = \begin{pmatrix} 2 \\ 1 \end{pmatrix}$ with the initial inverse Hessian approximation $H_0 = I = \begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix}$.

1.  **Compute Gradient and Search Direction**:
    The gradient is $\nabla f(\mathbf{x}) = \begin{pmatrix} 2x_1 \\ 4x_2 \end{pmatrix}$. At $\mathbf{x}_0$, the gradient is $\mathbf{g}_0 = \begin{pmatrix} 4 \\ 4 \end{pmatrix}$.
    The search direction is $\mathbf{p}_0 = -H_0 \mathbf{g}_0 = -\begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix} \begin{pmatrix} 4 \\ 4 \end{pmatrix} = \begin{pmatrix} -4 \\ -4 \end{pmatrix}$.

2.  **Perform Exact Line Search**:
    We need to find $\alpha > 0$ that minimizes $\phi(\alpha) = f(\mathbf{x}_0 + \alpha \mathbf{p}_0) = f(2-4\alpha, 1-4\alpha)$.
    $\phi(\alpha) = (2-4\alpha)^2 + 2(1-4\alpha)^2 = (4 - 16\alpha + 16\alpha^2) + 2(1 - 8\alpha + 16\alpha^2) = 6 - 32\alpha + 48\alpha^2$.
    Setting the derivative to zero, $\phi'(\alpha) = -32 + 96\alpha = 0$, gives the optimal step length $\alpha_0 = \frac{32}{96} = \frac{1}{3}$.

3.  **Update Position and Compute Step Vectors**:
    The new position is $\mathbf{x}_1 = \mathbf{x}_0 + \alpha_0 \mathbf{p}_0 = \begin{pmatrix} 2 \\ 1 \end{pmatrix} + \frac{1}{3} \begin{pmatrix} -4 \\ -4 \end{pmatrix} = \begin{pmatrix} 2/3 \\ -1/3 \end{pmatrix}$.
    The step vector is $\mathbf{s}_0 = \mathbf{x}_1 - \mathbf{x}_0 = \begin{pmatrix} -4/3 \\ -4/3 \end{pmatrix}$.
    The new gradient is $\mathbf{g}_1 = \nabla f(\mathbf{x}_1) = \begin{pmatrix} 2(2/3) \\ 4(-1/3) \end{pmatrix} = \begin{pmatrix} 4/3 \\ -4/3 \end{pmatrix}$.
    The gradient difference is $\mathbf{y}_0 = \mathbf{g}_1 - \mathbf{g}_0 = \begin{pmatrix} 4/3 \\ -4/3 \end{pmatrix} - \begin{pmatrix} 4 \\ 4 \end{pmatrix} = \begin{pmatrix} -8/3 \\ -16/3 \end{pmatrix}$.

4.  **Apply DFP Update Formula**:
    We first compute the necessary scalar products and matrices:
    - $\mathbf{s}_0^T \mathbf{y}_0 = (-\frac{4}{3})(-\frac{8}{3}) + (-\frac{4}{3})(-\frac{16}{3}) = \frac{32}{9} + \frac{64}{9} = \frac{96}{9} = \frac{32}{3}$. Note that the curvature condition is satisfied.
    - $H_0 \mathbf{y}_0 = I \mathbf{y}_0 = \mathbf{y}_0$.
    - $\mathbf{y}_0^T H_0 \mathbf{y}_0 = \mathbf{y}_0^T \mathbf{y}_0 = (-\frac{8}{3})^2 + (-\frac{16}{3})^2 = \frac{64}{9} + \frac{256}{9} = \frac{320}{9}$.
    The two correction terms are:
    - $\frac{\mathbf{s}_0 \mathbf{s}_0^T}{\mathbf{s}_0^T \mathbf{y}_0} = \frac{1}{32/3} \begin{pmatrix} 16/9  16/9 \\ 16/9  16/9 \end{pmatrix} = \frac{3}{32} \frac{16}{9} \begin{pmatrix} 1  1 \\ 1  1 \end{pmatrix} = \frac{1}{6} \begin{pmatrix} 1  1 \\ 1  1 \end{pmatrix}$.
    - $\frac{H_0 \mathbf{y}_0 \mathbf{y}_0^T H_0}{\mathbf{y}_0^T H_0 \mathbf{y}_0} = \frac{\mathbf{y}_0 \mathbf{y}_0^T}{\mathbf{y}_0^T \mathbf{y}_0} = \frac{1}{320/9} \begin{pmatrix} 64/9  128/9 \\ 128/9  256/9 \end{pmatrix} = \frac{1}{320} \begin{pmatrix} 64  128 \\ 128  256 \end{pmatrix} = \frac{1}{5} \begin{pmatrix} 1  2 \\ 2  4 \end{pmatrix}$.
    Finally, we compute $H_1$:
    $$
    H_1 = H_0 + \frac{\mathbf{s}_0 \mathbf{s}_0^T}{\mathbf{s}_0^T \mathbf{y}_0} - \frac{H_0 \mathbf{y}_0 \mathbf{y}_0^T H_0}{\mathbf{y}_0^T H_0 \mathbf{y}_0} = \begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix} + \begin{pmatrix} 1/6  1/6 \\ 1/6  1/6 \end{pmatrix} - \begin{pmatrix} 1/5  2/5 \\ 2/5  4/5 \end{pmatrix} = \begin{pmatrix} \frac{29}{30}  -\frac{7}{30} \\ -\frac{7}{30}  \frac{11}{30} \end{pmatrix}
    $$
    This new matrix, $H_1$, is symmetric and positive definite. It represents a more accurate approximation of the true inverse Hessian at $\mathbf{x}_1$ and will be used to compute the search direction for the next iteration. A similar procedure can be used to compute other properties of the updated matrix, such as its trace [@problem_id:2212543].

### Theoretical Guarantees and Duality

Beyond its practical utility, the DFP method exhibits remarkable theoretical properties, particularly when applied to a special class of functions.

#### Finite Termination on Quadratics

One of the most powerful theoretical results for the DFP method concerns its performance on strictly convex quadratic functions of the form $f(\mathbf{x}) = \frac{1}{2}\mathbf{x}^T Q \mathbf{x} - \mathbf{b}^T \mathbf{x}$, where $Q$ is a [symmetric positive-definite matrix](@entry_id:136714). When the DFP algorithm is applied to such a function in an $n$-dimensional space, using exact line searches at each step, it possesses the **finite termination property**: it is guaranteed to find the exact minimum in at most $n$ iterations. Furthermore, after exactly $n$ steps, the inverse Hessian approximation becomes the true inverse Hessian of the function [@problem_id:2212512]:
$$
H_n = Q^{-1}
$$
This result is independent of the starting point $\mathbf{x}_0$ and the initial approximation $H_0$. The underlying reason for this behavior is that the DFP method generates a sequence of search directions $\{\mathbf{p}_0, \mathbf{p}_1, \dots, \mathbf{p}_{n-1}\}$ that are **Q-conjugate**, meaning $\mathbf{p}_i^T Q \mathbf{p}_j = 0$ for all $i \neq j$. This property, which DFP shares with the [conjugate gradient method](@entry_id:143436), ensures that the minimization along each new direction does not spoil the minimization achieved in previous directions.

#### Duality with the BFGS Method

The DFP formula belongs to a family of quasi-Newton updates known as the Broyden family. Its closest relative is the Broyden-Fletcher-Goldfarb-Shanno (BFGS) method, which is now the most widely used quasi-Newton algorithm. The DFP and BFGS methods are considered **duals** of each other.

The DFP formula provides an update for the inverse Hessian approximation, $H_k$. The BFGS formula, conversely, provides an update for the direct Hessian approximation, $B_k = H_k^{-1}$. The striking relationship between them is revealed by a simple interchange of variables [@problem_id:2212507].

The DFP update for $H_{k+1}$ is:
$$
H_{k+1}^{\text{DFP}} = H_k + \frac{\mathbf{s}_k \mathbf{s}_k^T}{\mathbf{s}_k^T \mathbf{y}_k} - \frac{H_k \mathbf{y}_k \mathbf{y}_k^T H_k}{\mathbf{y}_k^T H_k \mathbf{y}_k}
$$
The BFGS update for $B_{k+1}$ is:
$$
B_{k+1}^{\text{BFGS}} = B_k + \frac{\mathbf{y}_k \mathbf{y}_k^T}{\mathbf{y}_k^T \mathbf{s}_k} - \frac{B_k \mathbf{s}_k \mathbf{s}_k^T B_k}{\mathbf{s}_k^T B_k \mathbf{s}_k}
$$
A direct comparison shows that the BFGS formula for $B_{k+1}$ can be obtained from the DFP formula for $H_{k+1}$ simply by swapping the roles of $\mathbf{s}_k$ and $\mathbf{y}_k$ everywhere, and replacing $H_k$ with $B_k$. This elegant duality links the two most important rank-two updates in optimization. While theoretically beautiful, the DFP method was found to be more susceptible to [numerical instability](@entry_id:137058) and less robust with inexact line searches compared to BFGS, which has led to the latter's dominance in modern optimization software. Nonetheless, the principles and mechanisms pioneered by the DFP algorithm laid the essential groundwork for the entire field of quasi-Newton optimization.