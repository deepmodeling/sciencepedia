## Introduction
In the vast landscape of numerical optimization, quasi-Newton methods stand out as a powerful class of algorithms that efficiently navigate complex functions by approximating [second-order derivative](@entry_id:754598) information. While popular methods like BFGS excel by maintaining a positive-definite Hessian approximation, this very feature becomes a limitation when dealing with non-convex problems rife with [saddle points](@entry_id:262327). This article introduces the Symmetric Rank-One (SR1) update, a distinct and elegant quasi-Newton method that addresses this gap. By not enforcing positive definiteness, the SR1 update can faithfully model the true local curvature, making it an indispensable tool for modern [nonconvex optimization](@entry_id:634396).

Across the following chapters, you will gain a comprehensive understanding of this method. The "Principles and Mechanisms" chapter will derive the SR1 formula from first principles and explore its unique properties, including its ability to handle negative curvature. The "Applications and Interdisciplinary Connections" chapter will showcase its utility in diverse fields from [computational chemistry](@entry_id:143039) to machine learning, where nonconvexity is the norm. Finally, "Hands-On Practices" will offer concrete exercises to solidify your knowledge and build practical skills for implementing and analyzing the SR1 update.

## Principles and Mechanisms

In the preceding chapter, we established the motivation for quasi-Newton methods: to construct approximations of the Hessian matrix that are computationally cheaper than computing the exact second derivatives, yet still provide sufficient curvature information to guide the optimization process efficiently. The core of any quasi-Newton method is its update rule, the algebraic procedure that refines the Hessian approximation from one iteration to the next. This chapter delves into the principles and mechanisms of one of the most elegant and distinctive of these rules: the **Symmetric Rank-One (SR1) update**.

### The Secant Condition: A Local Curvature Constraint

At the heart of all quasi-Newton methods lies the **[secant condition](@entry_id:164914)**. To understand it, recall that the Hessian matrix $\nabla^2 f(x)$ relates a small change in position, a vector $s$, to the corresponding change in the gradient, a vector $y$. For a quadratic function, this relationship is exact: $y = H s$. For a general nonlinear function, the Mean Value Theorem tells us that $y_k = \nabla f(x_{k+1}) - \nabla f(x_k) = \bar{H}_k s_k$, where $s_k = x_{k+1} - x_k$ and $\bar{H}_k$ is the average Hessian along the line segment between $x_k$ and $x_{k+1}$.

Quasi-Newton methods leverage this relationship as a constraint on the next Hessian approximation, $B_{k+1}$. We demand that the new approximation correctly mimics the action of the true Hessian at least for the most recent step taken. This gives rise to the [secant condition](@entry_id:164914):

$B_{k+1} s_k = y_k$

This equation, however, presents a challenge. It represents $n$ [linear equations](@entry_id:151487) for the $n(n+1)/2$ unknown elements of the [symmetric matrix](@entry_id:143130) $B_{k+1}$. This is an [underdetermined system](@entry_id:148553), meaning there are infinitely many matrices $B_{k+1}$ that satisfy the condition. The various quasi-Newton methods (BFGS, DFP, SR1) are distinguished by the additional constraints they impose to select a unique solution from this infinite set.

### Derivation of the Symmetric Rank-One (SR1) Update

The SR1 update is derived from what is arguably the simplest possible additional constraint: the change from $B_k$ to $B_{k+1}$ should be a **symmetric [rank-one matrix](@entry_id:199014)**. A [rank-one matrix](@entry_id:199014) represents the minimal non-trivial change one can make to a matrix.

Let's derive this update from first principles  . We propose an update of the form:

$B_{k+1} = B_k + \Delta B_k$

where $\Delta B_k$ is a symmetric [rank-one matrix](@entry_id:199014). Such a matrix can be written as $\gamma z z^\top$ for some non-zero scalar $\gamma$ and vector $z$. The update is thus:

$B_{k+1} = B_k + \gamma z z^\top$

Now, we enforce the [secant condition](@entry_id:164914), $B_{k+1} s_k = y_k$:

$(B_k + \gamma z z^\top) s_k = y_k$

$B_k s_k + \gamma z (z^\top s_k) = y_k$

Rearranging this equation to isolate the correction term gives:

$\gamma (z^\top s_k) z = y_k - B_k s_k$

This equation reveals a critical insight: the vector $z$ must be parallel to the vector $y_k - B_k s_k$. This vector, which we can call the **secant residual**, represents the discrepancy between the gradient change predicted by our current approximation ($B_k s_k$) and the one actually observed ($y_k$). Let us choose $z = y_k - B_k s_k$. Substituting this back into the equation, we get:

$\gamma ((y_k - B_k s_k)^\top s_k) (y_k - B_k s_k) = y_k - B_k s_k$

Assuming $y_k - B_k s_k$ is not the zero vector (in which case $B_k$ already satisfies the [secant condition](@entry_id:164914) and no update is needed), we can find $\gamma$:

$\gamma = \frac{1}{(y_k - B_k s_k)^\top s_k}$

This is valid only if the denominator is non-zero. Substituting our expressions for $\gamma$ and $z$ into the update form yields the definitive SR1 update formula:

$B_{k+1} = B_k + \frac{(y_k - B_k s_k)(y_k - B_k s_k)^\top}{(y_k - B_k s_k)^\top s_k}$

By its very construction, this update guarantees that $B_{k+1}s_k = y_k$, provided the denominator is non-zero. This means the angle between the vectors $y_k$ and $B_{k+1}s_k$ is zero .

### Core Properties of the SR1 Update

The algebraic form of the SR1 update endows it with several important properties that define its character and utility.

#### Symmetry Preservation

The SR1 update preserves the symmetry of the Hessian approximation. If $B_k$ is symmetric, then $B_{k+1}$ will also be symmetric. This is because the correction term is an [outer product](@entry_id:201262) of a vector with itself, $v v^\top$ (where $v = y_k - B_k s_k$), scaled by a scalar. Any such [outer product](@entry_id:201262) is inherently symmetric, since $(v v^\top)^\top = (v^\top)^\top v^\top = v v^\top$. The sum of two symmetric matrices ($B_k$ and the correction) is always symmetric  .

#### The "Memoryless" Property

A crucial aspect of the SR1 update is that it focuses exclusively on satisfying the most recent [secant condition](@entry_id:164914), $B_{k+1}s_k = y_k$. In general, it makes no attempt to preserve past secant conditions. That is, even if $B_k s_{k-1} = y_{k-1}$ held true, it is not guaranteed that $B_{k+1} s_{k-1} = y_{k-1}$ will hold after the update. The update "forgets" old curvature information in its pursuit of satisfying the new information . There are, however, special circumstances where this property does not hold. For quadratic functions, if the search directions $\{s_0, s_1, \dots, s_{k-1}\}$ are mutually orthogonal with respect to the matrix $B_k$, then the SR1 update possesses a "[hereditary property](@entry_id:151340)," preserving all past secant conditions. This leads to the remarkable result that, given $n$ [linearly independent](@entry_id:148207) search directions, the SR1 method can generate the exact Hessian of a quadratic function in at most $n$ iterations .

#### Finite Termination Example

Consider minimizing a quadratic function $f(x) = \frac{1}{2}x^\top Q x$ in $\mathbb{R}^3$, where $Q$ is a diagonal matrix. If we start with an initial approximation $B_0$ that already matches some columns of $Q$, and we take steps along the canonical basis directions ($s_0=e_1, s_1=e_2, s_2=e_3$), we can observe this property in action. For steps $s_0=e_1$ and $s_1=e_2$, if $B_0$ already satisfies the [secant condition](@entry_id:164914) (i.e., the first two columns of $B_0$ match $Q$), the term $y_k - B_k s_k$ will be zero, and the update is skipped. On the third step, $s_2=e_3$, the update will correct the final column of the matrix, resulting in $B_3 = Q$ . This illustrates how SR1 builds the Hessian approximation piece by piece.

### The Double-Edged Sword: Indefinite Hessians and Negative Curvature

The most defining—and controversial—feature of the SR1 update is its relationship with **positive definiteness**. Most other popular quasi-Newton methods, like BFGS, are explicitly designed to generate a sequence of [symmetric positive definite](@entry_id:139466) (SPD) Hessian approximations. An SPD matrix $B_k$ guarantees that the search direction $p_k = -B_k^{-1} g_k$ is a descent direction, a highly desirable property for ensuring [stable convergence](@entry_id:199422) in [line search methods](@entry_id:172705).

The SR1 update offers no such guarantee. Starting with an SPD matrix $B_k$, the updated matrix $B_{k+1}$ may be indefinite or even [negative definite](@entry_id:154306). This property, which can be seen as either a bug or a feature, stems directly from the denominator of the update formula, $d_k = (y_k - B_k s_k)^\top s_k$. The correction added to $B_k$ is a [rank-one matrix](@entry_id:199014) of the form $\frac{v v^\top}{d_k}$. Since $v v^\top$ is always positive semidefinite, the sign of the correction is determined entirely by the sign of $d_k$. If $d_k  0$, we are subtracting a [positive semidefinite matrix](@entry_id:155134) from $B_k$, an operation that can easily destroy positive definiteness .

Let's illustrate with a simple example. Consider a 2D problem where we have:
$B_k = \begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix}, \quad s_k = \begin{pmatrix} 1 \\ 0 \end{pmatrix}, \quad y_k = \begin{pmatrix} -2 \\ 0 \end{pmatrix}$

Here, $B_k$ is the identity matrix, which is positive definite. We compute the denominator:
$y_k - B_k s_k = \begin{pmatrix} -2 \\ 0 \end{pmatrix} - \begin{pmatrix} 1 \\ 0 \end{pmatrix} = \begin{pmatrix} -3 \\ 0 \end{pmatrix}$
$(y_k - B_k s_k)^\top s_k = \begin{pmatrix} -3  0 \end{pmatrix} \begin{pmatrix} 1 \\ 0 \end{pmatrix} = -3$

Since the denominator is negative, we anticipate a potential loss of [positive definiteness](@entry_id:178536). The update is:
$B_{k+1} = B_k + \frac{\begin{pmatrix} -3 \\ 0 \end{pmatrix} \begin{pmatrix} -3  0 \end{pmatrix}}{-3} = \begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix} - \frac{1}{3} \begin{pmatrix} 9  0 \\ 0  0 \end{pmatrix} = \begin{pmatrix} -2  0 \\ 0  1 \end{pmatrix}$

The new matrix $B_{k+1}$ has eigenvalues $-2$ and $1$. It is indefinite. The SR1 update has taken a [positive definite matrix](@entry_id:150869) and, by incorporating the new curvature information, produced an indefinite one .

While the potential loss of a guaranteed descent direction seems like a major drawback, it is also SR1's greatest strength. By allowing for indefinite Hessian approximations, the SR1 method can accurately model the true [curvature of a function](@entry_id:173664), even in non-convex regions like those near a saddle point. This ability is invaluable in many contexts, particularly when using [trust-region methods](@entry_id:138393) that can effectively utilize information about [negative curvature](@entry_id:159335).

Consider the saddle function $f(x,y) = x^2 - y^2$, whose true Hessian is the constant [indefinite matrix](@entry_id:634961) $H = \mathrm{diag}(2, -2)$. If we take a step that probes the [negative curvature](@entry_id:159335) and apply the SR1 update, the resulting matrix $B_{k+1}$ can become indefinite, capturing the essential geometry of the problem. In contrast, the BFGS update, which is designed to preserve [positive definiteness](@entry_id:178536), would fail to do so. Under the same conditions, BFGS would produce a positive definite approximation, effectively modeling the saddle as a convex bowl. This highlights the fundamental trade-off: BFGS prioritizes stability and descent directions at the cost of geometric fidelity, while SR1 prioritizes geometric fidelity at the cost of guaranteed descent directions  . If an algorithm takes steps that persistently explore a direction of negative curvature, the SR1 update can even generate a sequence of matrices $\{B_k\}$ whose negative eigenvalue converges to the true [negative curvature](@entry_id:159335) of the function .

### Practical Implementation: The Challenge of Breakdown

The SR1 update's primary practical challenge is the possibility of its denominator, $(y_k - B_k s_k)^\top s_k$, being zero or very close to zero. A zero denominator leads to a division by zero, and a near-zero denominator can cause a massive, numerically unstable update that pollutes the accumulated curvature information in $B_k$. This breakdown can occur in two distinct situations :

1.  **Secant Condition Already Met:** If $y_k = B_k s_k$, the numerator and denominator are both zero. This is a benign case where no update is needed, as $B_k$ already holds the correct curvature information for the direction $s_k$.

2.  **Orthogonality:** It is also possible that $y_k - B_k s_k \neq 0$ but this vector is orthogonal to the step $s_k$. This is a more problematic breakdown of the formula.

To ensure robustness, any practical implementation of the SR1 method must include a **safeguard** or **skip condition**. The update is only performed if the denominator is sufficiently large relative to the magnitudes of the vectors involved. A standard condition is to skip the update if:

$|(y_k - B_k s_k)^\top s_k| \le \eta \|y_k - B_k s_k\| \|s_k\|$

for a small positive tolerance $\eta$ (e.g., $10^{-8}$)  . This condition essentially checks if the angle between the secant residual vector and the step vector is close to $90$ degrees. If the condition is met, the update is skipped, and we set $B_{k+1} = B_k$. While this prevents numerical catastrophe, frequent skipping can slow convergence as new curvature information is discarded.

The risk of generating non-descent directions and the need for a skipping mechanism mean that SR1 updates must be embedded within a robust globalization framework. A simple [line search](@entry_id:141607) may fail. Instead, a [trust-region method](@entry_id:173630), which is naturally equipped to handle indefinite models, or a [line search method](@entry_id:175906) with safeguards for non-descent directions, is essential for a reliable SR1-based optimizer .