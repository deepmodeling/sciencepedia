## Introduction
In the realm of [numerical analysis](@entry_id:142637), the challenge of fitting a continuous function to a discrete set of data points is fundamental. While various solutions exist, the Newton form of the interpolating polynomial stands out as a particularly elegant and computationally powerful method. It addresses the common problem of needing an approach that is not only accurate but also efficient, especially when data is acquired sequentially. This article provides a deep dive into this essential tool.

The following sections will guide you through a complete understanding of the Newton polynomial. In **Principles and Mechanisms**, we will dissect its architecture, learn the method of [divided differences](@entry_id:138238) for calculating its coefficients, and uncover the theoretical connection between these coefficients and derivatives. Next, in **Applications and Interdisciplinary Connections**, we will explore its vast utility, from modeling rocket trajectories and financial curves to its foundational role in deriving other critical [numerical algorithms](@entry_id:752770). Finally, the **Hands-On Practices** section offers practical exercises to solidify your command of the core concepts. We begin by examining the principles that make the Newton form a cornerstone of approximation theory.

## Principles and Mechanisms

Following our introduction to the fundamental problem of [polynomial interpolation](@entry_id:145762), we now delve into one of the most elegant and practical solutions: the Newton form of the interpolating polynomial. While the Lagrange form provides a direct and conceptually straightforward construction, the Newton form offers significant computational advantages and deeper theoretical insights. Its structure is inherently recursive, which makes it particularly well-suited for situations where data points are added sequentially. This section will dissect the principles and mechanisms of the Newton form, from its constituent basis polynomials to the calculation and interpretation of its coefficients.

### The Architecture of the Newton Polynomial

Given a set of $n+1$ distinct data points $(x_0, y_0), (x_1, y_1), \dots, (x_n, y_n)$, the Newton form of the unique [interpolating polynomial](@entry_id:750764) of degree at most $n$ is expressed as a [linear combination](@entry_id:155091) of a special set of basis polynomials:

$P_n(x) = a_0 \pi_0(x) + a_1 \pi_1(x) + \dots + a_n \pi_n(x) = \sum_{j=0}^{n} a_j \pi_j(x)$

The key to this form lies in the definition of the **Newton basis polynomials**, $\pi_j(x)$. They are defined by a nested product structure:

$\pi_0(x) = 1$

$\pi_j(x) = \prod_{i=0}^{j-1} (x - x_i) \quad \text{for } j = 1, 2, \dots, n$

This definition gives rise to a sequence of polynomials of increasing degree. For example, for a set of three nodes $\{x_0, x_1, x_2\}$, the first three basis polynomials are explicitly [@problem_id:2189908]:

- $\pi_0(x) = 1$ (a constant, degree 0)
- $\pi_1(x) = x - x_0$ (a linear polynomial, degree 1)
- $\pi_2(x) = (x - x_0)(x - x_1)$ (a quadratic polynomial, degree 2)

Notice the elegant telescoping property: $\pi_j(x) = \pi_{j-1}(x) \cdot (x - x_{j-1})$ for $j \ge 2$. This nested structure is the source of many of the Newton form's computational advantages. The coefficients $a_j$ in this basis are known as **[divided differences](@entry_id:138238)**, which are the central quantities we must determine.

### Determining the Coefficients: The Method of Divided Differences

To find the coefficients $a_j$, we enforce the interpolation conditions, $P_n(x_k) = y_k$, for $k=0, 1, \dots, n$. This process reveals a remarkably simple structure. Let's evaluate $P_n(x)$ at the nodes in order:

- At $x = x_0$:
$P_n(x_0) = a_0 \pi_0(x_0) + a_1 \pi_1(x_0) + a_2 \pi_2(x_0) + \dots = y_0$
Since $\pi_j(x_0) = 0$ for all $j \ge 1$, this equation simplifies to $a_0 \cdot 1 = y_0$. Thus, the first coefficient is simply the first data value:
$a_0 = y_0$

- At $x = x_1$:
$P_n(x_1) = a_0 \pi_0(x_1) + a_1 \pi_1(x_1) + a_2 \pi_2(x_1) + \dots = y_1$
Here, $\pi_0(x_1)=1$, $\pi_1(x_1) = (x_1 - x_0)$, and $\pi_j(x_1) = 0$ for all $j \ge 2$. The equation becomes $a_0 + a_1(x_1 - x_0) = y_1$. Solving for $a_1$:
$a_1 = \frac{y_1 - a_0}{x_1 - x_0} = \frac{y_1 - y_0}{x_1 - x_0}$

- At $x = x_2$:
$P_n(x_2) = a_0 + a_1(x_2-x_0) + a_2(x_2-x_0)(x_2-x_1) = y_2$.
This equation can be solved for $a_2$ since $a_0$ and $a_1$ are already known.

This process demonstrates that the system of linear equations for the coefficients $\{a_j\}$ is **lower-triangular** [@problem_id:2189951]. A lower-triangular system can be solved efficiently using **[forward substitution](@entry_id:139277)**, and it guarantees the [existence and uniqueness](@entry_id:263101) of the coefficients $a_j$, provided the nodes $x_i$ are distinct (which ensures that the diagonal entries, such as $x_1-x_0$, are non-zero).

This sequential determination gives rise to the formal definition of **[divided differences](@entry_id:138238)**. The coefficient $a_k$ is the $k$-th order divided difference of the function values with respect to the nodes $x_0, \dots, x_k$, denoted $f[x_0, \dots, x_k]$.

- Zeroth-order: $a_0 = f[x_0] = y_0$
- First-order: $a_1 = f[x_0, x_1] = \frac{f[x_1] - f[x_0]}{x_1 - x_0}$
- Second-order: $a_2 = f[x_0, x_1, x_2] = \frac{f[x_1, x_2] - f[x_0, x_1]}{x_2 - x_0}$

The general [recursive definition](@entry_id:265514) for the $k$-th order divided difference is:
$f[x_i, \dots, x_{i+k}] = \frac{f[x_{i+1}, \dots, x_{i+k}] - f[x_i, \dots, x_{i+k-1}]}{x_{i+k} - x_i}$

This [recursive definition](@entry_id:265514) allows for the systematic computation of all necessary coefficients using a **[divided difference table](@entry_id:177983)**. For example, to find the coefficient $a_3 = f[x_0, x_1, x_2, x_3]$ for the data points $(0, 1), (1, 3), (2, 2), (4, 5)$ [@problem_id:2189951], we construct the table:

| $x_i$ | $f[x_i]$ | $f[x_{i}, x_{i+1}]$ | $f[x_i, \dots, x_{i+2}]$ | $f[x_i, \dots, x_{i+3}]$ |
|---|---|---|---|---|
| 0 | 1 | | | |
| | | $f[x_0, x_1] = \frac{3-1}{1-0} = 2$ | | |
| 1 | 3 | | $f[x_0, x_1, x_2] = \frac{-1-2}{2-0} = -\frac{3}{2}$ | |
| | | $f[x_1, x_2] = \frac{2-3}{2-1} = -1$ | | $a_3 = \frac{5/6 - (-3/2)}{4-0} = \frac{7}{12}$ |
| 2 | 2 | | $f[x_1, x_2, x_3] = \frac{3/2 - (-1)}{4-1} = \frac{5}{6}$ | |
| | | $f[x_2, x_3] = \frac{5-2}{4-2} = \frac{3}{2}$ | | |
| 4 | 5 | | | |

The coefficients of the Newton polynomial $P_3(x)$ are the top entries in each column: $a_0 = 1$, $a_1 = 2$, $a_2 = -3/2$, and $a_3 = 7/12$.

### The Meaning of Divided Differences

Divided differences are not merely computational artifacts; they possess profound geometric and analytic meaning.

#### Geometric and Physical Interpretation

The first divided difference, $f[x_0, x_1] = \frac{f(x_1) - f(x_0)}{x_1 - x_0}$, is precisely the slope of the secant line connecting the points $(x_0, f(x_0))$ and $(x_1, f(x_1))$ [@problem_id:2189913]. This provides a direct physical interpretation. In a study of [thermal expansion](@entry_id:137427), where length $L$ is a function of temperature $T$, the coefficient $a_1 = \frac{L_1 - L_0}{T_1 - T_0}$ represents the average rate of expansion over the temperature interval $[T_0, T_1]$ [@problem_id:2189967]. For a vehicle whose position is $x(t)$, the divided difference $x[t_0, t_1]$ is its [average velocity](@entry_id:267649) [@problem_id:2189934].

This interpretation extends to higher orders. The second divided difference, $f[x_0, x_1, x_2]$, can be interpreted as a measure of curvature. More precisely, it is the leading coefficient (the coefficient of the $x^2$ term) of the unique quadratic polynomial that interpolates the three points $(x_0, y_0)$, $(x_1, y_1)$, and $(x_2, y_2)$ [@problem_id:2189913]. In general, the coefficient $a_k = f[x_0, \dots, x_k]$ is the leading coefficient of the unique polynomial of degree $k$ that interpolates the first $k+1$ data points.

#### Connection to Derivatives

Divided differences are fundamentally linked to derivatives. The Mean Value Theorem for derivatives states that for a differentiable function $f$ on $[x_0, x_1]$, there exists some point $c \in (x_0, x_1)$ such that $f'(c) = \frac{f(x_1) - f(x_0)}{x_1 - x_0} = f[x_0, x_1]$. Thus, the first divided difference is equal to the value of the first derivative at some intermediate point. For instance, for the vehicle with position $x(t) = 2t^3 - 5t^2$, the [average velocity](@entry_id:267649) over $[1, 3]$ is $6.0 \text{ m/s}$. The Mean Value Theorem guarantees there is a time $c \in (1, 3)$ where the instantaneous velocity $x'(c)$ is exactly $6.0 \text{ m/s}$; a calculation shows this occurs at $c \approx 2.14$ s [@problem_id:2189934].

This relationship generalizes. For a function $f$ that is $n$ times continuously differentiable, there exists a point $\xi$ in the interval containing the nodes $\{x_0, \dots, x_n\}$ such that:

$f[x_0, x_1, \dots, x_n] = \frac{f^{(n)}(\xi)}{n!}$

This important theorem establishes the divided difference as a discrete approximation to the scaled $n$-th derivative. It provides a theoretical bridge between the discrete data points we have and the underlying continuous function from which they may be sampled.

### Assembling and Utilizing the Newton Polynomial

Once the [divided differences](@entry_id:138238) are computed, they are plugged into the Newton form. For instance, using coefficients $a_0 = 2$, $a_1 = -1$, and $a_2 = 0.5$ for basis polynomials constructed from nodes $x_0=0$ and $x_1=1$, the polynomial is [@problem_id:2189942]:

$P_2(x) = a_0 + a_1(x-x_0) + a_2(x-x_0)(x-x_1)$
$P_2(x) = 2 + (-1)(x-0) + 0.5(x-0)(x-1)$
$P_2(x) = 2 - x + 0.5x(x-1) = 2 - x + 0.5x^2 - 0.5x$
$P_2(x) = 0.5x^2 - 1.5x + 2$

While this expanded form is useful, the unexpanded Newton form possesses several key advantages.

#### Uniqueness and Equivalence

Although the Newton and Lagrange forms appear algebraically distinct, they must represent the same polynomial. The **Uniqueness Theorem for Polynomial Interpolation** states that for any set of $n+1$ data points with distinct abscissas, there exists one and only one polynomial of degree at most $n$ that passes through all of them. Since both the Newton and Lagrange methods produce a polynomial of degree at most $n$ satisfying the interpolation conditions, they must be mathematically identical [@problem_id:2189947]. To see why, consider the difference polynomial $Q(x) = P_N(x) - P_L(x)$. $Q(x)$ has a degree of at most $n$, yet it evaluates to zero at all $n+1$ nodes $x_0, \dots, x_n$. A non-zero polynomial of degree $n$ can have at most $n$ roots. Therefore, $Q(x)$ must be the zero polynomial, proving $P_N(x) \equiv P_L(x)$.

#### The Additive Property: A Key Advantage

The most significant practical advantage of the Newton form is its recursive or additive nature. The polynomial $P_n(x)$ is built directly from $P_{n-1}(x)$:

$P_n(x) = P_{n-1}(x) + a_n \prod_{i=0}^{n-1} (x - x_i)$

This means that if a new data point $(x_n, y_n)$ is acquired, we do not need to recompute the entire polynomial from scratch, which would be necessary with the Lagrange form. We simply compute the new required [divided differences](@entry_id:138238) and add one more term to our existing polynomial.

For example, if we have the second-degree polynomial $P_2(x) = 1 + 2(x-1) + 2(x-1)(x-2)$ interpolating $(1,1), (2,3), (4,19)$, and we add a new point $(5,45)$, we only need to calculate the new highest-order coefficient, $a_3 = f[1, 2, 4, 5]$. A quick calculation yields $a_3=1$. The new third-degree polynomial is simply [@problem_id:2189928]:

$P_3(x) = P_2(x) + a_3(x-x_0)(x-x_1)(x-x_2)$
$P_3(x) = [1 + 2(x-1) + 2(x-1)(x-2)] + 1 \cdot (x-1)(x-2)(x-4)$

This efficiency is crucial in adaptive algorithms and real-time data processing, where models must be updated as new information becomes available.

### The Interpolation Error Formula and Its Consequences

A central question in [approximation theory](@entry_id:138536) is: how well does $P_n(x)$ approximate the true function $f(x)$? The additive nature of the Newton form provides a direct path to an expression for the **[interpolation error](@entry_id:139425)**, $E_n(x) = f(x) - P_n(x)$.

If we consider $x$ itself as a new node, we can write:
$f(x) = P_n(x) + f[x_0, \dots, x_n, x] \prod_{i=0}^{n} (x-x_i)$

This identity arises naturally from the definition of the $(n+1)$-th degree polynomial interpolating at $x_0, \dots, x_n$ and $x$. Rearranging gives the exact error formula:

$E_n(x) = f(x) - P_n(x) = f[x_0, \dots, x_n, x] \prod_{i=0}^{n} (x-x_i)$

This elegant formula reveals several truths. First, the error is guaranteed to be zero at the interpolation nodes $x_0, \dots, x_n$, as the product term becomes zero. Second, the error at any other point $x$ depends on two factors: the $(n+1)$-th order divided difference (which relates to the function's $(n+1)$-th derivative) and the product of the distances from $x$ to each node.

This error formula can also be used to find [divided differences](@entry_id:138238). For example, if we are given $f(x) = \cos(\frac{\pi x}{4})$ and its quadratic interpolant $P_2(x)$ at nodes $\{-1, 0, 1\}$, we can find the third-order divided difference $f[-1, 0, 1, 2]$ by evaluating the error at $x=2$ [@problem_id:2189939]:

$f[-1, 0, 1, 2] = \frac{f(2) - P_2(2)}{(2 - (-1))(2-0)(2-1)} \approx 0.02860$

While it may seem that increasing the degree $n$ of the [interpolating polynomial](@entry_id:750764) should always improve accuracy, this is not the case. The error formula shows that the behavior of the $(n+1)$-th derivative (or divided difference) is critical. For some functions, particularly when using equally spaced nodes, the magnitude of [higher-order derivatives](@entry_id:140882) can grow extremely rapidly. This can cause the [interpolating polynomial](@entry_id:750764) to develop large oscillations between nodes, especially near the ends of the interpolation interval, leading to a very poor approximation. This troubling behavior is known as the **Runge phenomenon**. For the classic Runge function $f(x) = \frac{1}{1 + 25x^2}$, a calculation with four equally spaced nodes on $[0, 1]$ already yields a large third-order divided difference, $f[0, 1/3, 2/3, 1] = -45000/24089 \approx -1.868$ [@problem_id:2189974], hinting at the rapid growth that causes this divergence. This phenomenon serves as a crucial reminder of the limitations of [high-degree polynomial interpolation](@entry_id:168346) and motivates the use of alternative strategies, such as piecewise interpolation (splines) or non-uniform node spacing (e.g., Chebyshev nodes), which are beyond the scope of this article.