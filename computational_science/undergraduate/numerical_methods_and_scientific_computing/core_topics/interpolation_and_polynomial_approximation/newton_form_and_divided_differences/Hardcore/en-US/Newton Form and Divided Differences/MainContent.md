## Introduction
Polynomial interpolation is a fundamental technique in [numerical analysis](@entry_id:142637), providing a way to approximate complex functions or discrete data with simpler, analytically tractable polynomials. While various methods exist for constructing an [interpolating polynomial](@entry_id:750764), such as the Lagrange and Vandermonde forms, they often suffer from computational inefficiency and a lack of flexibility. For instance, adding a single new data point requires a complete recalculation of the entire polynomial. This article addresses these limitations by focusing on the Newton form of the [interpolating polynomial](@entry_id:750764), a powerful representation built upon the elegant theory of [divided differences](@entry_id:138238).

This exploration is structured to build a comprehensive understanding from theory to practice. The journey begins in the **Principles and Mechanisms** chapter, where we will derive the Newton form, introduce the [recursive definition](@entry_id:265514) of [divided differences](@entry_id:138238), and master their systematic computation using a [divided difference table](@entry_id:177983). Following this, the **Applications and Interdisciplinary Connections** chapter will showcase the remarkable versatility of Newton interpolation, demonstrating its use in solving real-world problems in fields from engineering and finance to signal processing and machine learning. Finally, the **Hands-On Practices** section will offer a curated set of problems to solidify your skills and deepen your intuition. We begin by examining the core structure of the Newton form and the mechanisms that make it so efficient and adaptable.

## Principles and Mechanisms

While the [existence and uniqueness](@entry_id:263101) of an interpolating polynomial are guaranteed, its representation is not unique. Different bases for the space of polynomials of degree at most $n$ give rise to different forms of the [interpolating polynomial](@entry_id:750764), such as the Lagrange and Vandermonde (monomial basis) forms. In this chapter, we explore the Newton form of the interpolating polynomial. This representation is not only computationally efficient but also remarkably flexible, providing deep theoretical insights and a natural pathway to more advanced interpolation schemes.

### The Newton Basis: A More Flexible Approach to Interpolation

Given a set of $n+1$ distinct nodes $\{x_0, x_1, \dots, x_n\}$ and corresponding data values $\{y_0, y_1, \dots, y_n\}$, the Newton form of the [interpolating polynomial](@entry_id:750764) $P_n(x)$ is expressed as:

$$P_n(x) = c_0 + c_1(x-x_0) + c_2(x-x_0)(x-x_1) + \dots + c_n \prod_{i=0}^{n-1} (x-x_i)$$

This can be written more compactly as:

$$P_n(x) = \sum_{k=0}^{n} c_k \prod_{j=0}^{k-1} (x-x_j)$$

where the empty product for $k=0$ is defined as 1. The set of polynomials $\{1, (x-x_0), (x-x_0)(x-x_1), \dots, \prod_{j=0}^{n-1} (x-x_j)\}$ is known as the **Newton basis**. A key advantage of this basis is its nested structure. Notice that $P_k(x)$ is formed by simply adding a new term to $P_{k-1}(x)$:

$$P_k(x) = P_{k-1}(x) + c_k \prod_{j=0}^{k-1} (x-x_j)$$

This property is immensely practical. If we have already constructed an [interpolating polynomial](@entry_id:750764) for a set of points and wish to add a new data point $(x_{n+1}, y_{n+1})$, we do not need to recompute the entire polynomial, as is necessary with the Lagrange or Vandermonde forms. We simply need to find the new coefficient $c_{n+1}$ and append the corresponding term to our existing polynomial. This extensibility is a hallmark of the Newton form. The central challenge, then, lies in determining the coefficients $c_k$.

### Divided Differences: The Building Blocks of the Newton Form

The coefficients $c_k$ of the Newton polynomial are known as **[divided differences](@entry_id:138238)**. Let us derive them directly from the interpolation condition, $P_n(x_i) = y_i$.

For the first coefficient, $c_0$, we evaluate the polynomial at the first node, $x_0$:

$$P_n(x_0) = c_0 + c_1(x_0-x_0) + c_2(x_0-x_0)(x_0-x_1) + \dots$$

Every term after the first contains the factor $(x-x_0)$, which becomes zero. The expression collapses beautifully:

$$P_n(x_0) = c_0$$

Since the polynomial must interpolate the first data point, $P_n(x_0) = y_0$. Therefore, $c_0 = y_0$. Geometrically, this means the first coefficient of the Newton polynomial is simply the y-coordinate of the first data point, which is the intersection of the polynomial curve with the vertical line $x=x_0$ . We denote this zeroth-order divided difference as $f[x_0] = f(x_0) = y_0$.

To find $c_1$, we evaluate at the next node, $x_1$:

$$P_n(x_1) = c_0 + c_1(x_1-x_0) = f[x_0] + c_1(x_1-x_0)$$

We know $P_n(x_1) = y_1 = f(x_1)$, so we can solve for $c_1$:

$$c_1 = \frac{f(x_1) - f[x_0]}{x_1 - x_0}$$

This expression is the **first-order divided difference**, denoted $f[x_0, x_1]$. It represents the slope of the [secant line](@entry_id:178768) connecting the first two data points.

Proceeding to $x_2$ to find $c_2$:

$$P_n(x_2) = f[x_0] + f[x_0, x_1](x_2-x_0) + c_2(x_2-x_0)(x_2-x_1) = y_2$$

Solving for $c_2$ yields a more complex expression. However, a remarkable pattern emerges. The coefficient $c_k$ can be expressed by a [recursive formula](@entry_id:160630). We define the **k-th order divided difference** as:

$$f[x_i, x_{i+1}, \dots, x_{i+k}] = \frac{f[x_{i+1}, \dots, x_{i+k}] - f[x_i, \dots, x_{i+k-1}]}{x_{i+k} - x_i}$$

With this definition, it can be shown that the coefficients of the Newton polynomial are precisely the [divided differences](@entry_id:138238) that begin with $x_0$:

$$c_k = f[x_0, x_1, \dots, x_k]$$

Thus, the Newton form of the [interpolating polynomial](@entry_id:750764) is explicitly:

$$P_n(x) = f[x_0] + f[x_0, x_1](x-x_0) + f[x_0, x_1, x_2](x-x_0)(x-x_1) + \dots + f[x_0, \dots, x_n]\prod_{i=0}^{n-1}(x-x_i)$$

It is important to note that the value of a divided difference $f[x_0, \dots, x_k]$ is independent of the order of the nodes $x_0, \dots, x_k$. It is a symmetric function of its arguments. However, the structure of the Newton polynomial itself depends on the chosen ordering of the nodes.

### Systematic Computation: The Divided Difference Table

The [recursive definition](@entry_id:265514) of [divided differences](@entry_id:138238) lends itself to a systematic and elegant computational scheme known as the **[divided difference table](@entry_id:177983)**. For $n+1$ points, we construct a triangular table where each column corresponds to a different order of divided difference.

| $x_i$ | $f[x_i]$ (0th order) | $f[x_i, x_{i+1}]$ (1st order) | $f[x_i, x_{i+1}, x_{i+2}]$ (2nd order) | $\dots$ |
| :---: | :---: | :---: | :---: | :---: |
| $x_0$ | $f[x_0]$ | | | |
| | | $f[x_0, x_1]$ | | |
| $x_1$ | $f[x_1]$ | | $f[x_0, x_1, x_2]$ | |
| | | $f[x_1, x_2]$ | | $\ddots$ |
| $x_2$ | $f[x_2]$ | | $f[x_1, x_2, x_3]$ | |
| | | $f[x_2, x_3]$ | | |
| $x_3$ | $f[x_3]$ | | | |
| $\vdots$| $\vdots$| $\vdots$| | |

Each entry in the table is computed from the two entries to its immediate left in the previous column. The coefficients $c_k = f[x_0, \dots, x_k]$ for the Newton polynomial are then simply read from the top diagonal of the completed table.

Let's illustrate with an example. Suppose we are given the data points $(0, 5), (1, 2), (3, 20), (4, 41)$ and want to find the interpolating polynomial . We have $x_0=0, x_1=1, x_2=3, x_3=4$.

First, we populate the zeroth-order column with the y-values:
$f[x_0]=5, f[x_1]=2, f[x_2]=20, f[x_3]=41$.

Next, we compute the first-order differences:
$f[x_0, x_1] = \frac{2-5}{1-0} = -3$
$f[x_1, x_2] = \frac{20-2}{3-1} = \frac{18}{2} = 9$
$f[x_2, x_3] = \frac{41-20}{4-3} = \frac{21}{1} = 21$

Then, the second-order differences:
$f[x_0, x_1, x_2] = \frac{9 - (-3)}{3-0} = \frac{12}{3} = 4$
$f[x_1, x_2, x_3] = \frac{21 - 9}{4-1} = \frac{12}{3} = 4$

Finally, the third-order difference:
$f[x_0, x_1, x_2, x_3] = \frac{4 - 4}{4-0} = 0$

The coefficients are the top diagonal: $c_0=5, c_1=-3, c_2=4, c_3=0$. The Newton polynomial is:
$P_3(x) = 5 - 3(x-0) + 4(x-0)(x-1) + 0(x-0)(x-1)(x-3)$
$P_3(x) = 5 - 3x + 4x(x-1) = 5 - 3x + 4x^2 - 4x = 4x^2 - 7x + 5$.
The fact that $c_3=0$ reveals that the four data points lie on a parabola, not a general cubic curve.

### Theoretical Foundations and Geometric Interpretations

Divided differences are not merely algebraic conveniences; they have deep connections to calculus and geometry.

The first-order divided difference $f[x_0, x_1]$ is the slope of the [secant line](@entry_id:178768) through $(x_0, f(x_0))$ and $(x_1, f(x_1))$. The Mean Value Theorem states that if $f$ is differentiable, there exists a point $\xi \in (x_0, x_1)$ such that $f'(\xi) = f[x_0, x_1]$.

This relationship generalizes. For a function $f$ that is $k$ times continuously differentiable, the **Generalized Mean Value Theorem** states that for any distinct nodes $x_0, \dots, x_k$, there exists a point $\xi$ in the smallest interval containing these nodes such that:
$$f[x_0, x_1, \dots, x_k] = \frac{f^{(k)}(\xi)}{k!}$$
This remarkable result connects the $k$-th order divided difference to the $k$-th derivative of the function, establishing [divided differences](@entry_id:138238) as discrete analogs of derivatives. For instance, for the function $f(x)=x^n$, the first-order divided difference $f[a,b]$ for $a \neq b$ is $\frac{b^n - a^n}{b-a} = \sum_{k=0}^{n-1} a^k b^{n-1-k}$ . As $b \to a$, this sum approaches $n a^{n-1}$, which is $f'(a)$, consistent with the theorem.

This connection provides a powerful geometric interpretation for the second-order divided difference, $f[x_0, x_1, x_2]$. Let $p_2(x)$ be the unique parabola interpolating the three points $(x_0, f(x_0)), (x_1, f(x_1)), (x_2, f(x_2))$. The Newton form is $p_2(x) = f[x_0] + f[x_0,x_1](x-x_0) + f[x_0,x_1,x_2](x-x_0)(x-x_1)$. Taking the second derivative gives:
$$p_2''(x) = 2 f[x_0, x_1, x_2]$$
The second derivative of the interpolating parabola is a constant, equal to twice the second divided difference. Since curvature involves the second derivative, $f[x_0, x_1, x_2]$ is directly related to how much the interpolating parabola bends. Specifically, the curvature at the vertex of the parabola is exactly $2|f[x_0, x_1, x_2]|$ .

### Computational Efficiency: Evaluation and Complexity

From a practical standpoint, the Newton form offers significant computational advantages.

First, let's consider the complexity of finding the polynomial's coefficients. Constructing the [divided difference table](@entry_id:177983) for $N$ points requires calculating approximately $N^2/2$ [divided differences](@entry_id:138238), each taking a constant number of [floating-point operations](@entry_id:749454) (FLOPs). Therefore, the overall cost to determine the Newton coefficients is $O(N^2)$ . This compares favorably to the most direct alternative: solving the $V \mathbf{a} = \mathbf{y}$ system for the monomial coefficients, where $V$ is the Vandermonde matrix. Using standard Gaussian elimination, this is an $O(N^3)$ operation. While specialized algorithms for Vandermonde systems can achieve $O(N^2)$ complexity, the divided difference approach is conceptually straightforward and often more numerically stable.

Second, once the coefficients $c_k = f[x_0, \dots, x_k]$ are found, evaluating the polynomial $P_n(x)$ at a new point is highly efficient. The nested structure of the Newton form,
$$P_n(x) = c_0 + (x-x_0)(c_1 + (x-x_1)(c_2 + \dots + (x-x_{n-1})c_n)\dots)$$
is perfectly suited for **nested evaluation**, also known as **Horner's method**. We can evaluate this from the inside out:
1.  Initialize result with the last coefficient: `val = c_n`.
2.  Iterate backwards from $k = n-1$ down to $0$: `val = val * (x - x_k) + c_k`.
3.  The final `val` is $P_n(x)$.

This algorithm requires only $n$ multiplications and $n$ additions, an optimal $O(n)$ process. For instance, to estimate the thermal conductivity of an alloy at $T=300$ K using a cubic polynomial fit to data at $100, 200, 400, 600$ K, one would first compute the coefficients $c_0, c_1, c_2, c_3$ via a [divided difference table](@entry_id:177983). Then, the value $P_3(300)$ can be found with just three multiplications and three additions using this nested scheme .

Finally, it is crucial to remember the Uniqueness Theorem. Although the Lagrange, Vandermonde, and Newton forms appear algebraically distinct, they all represent the same unique polynomial. Any correct implementation of these forms must yield identical values for any input $x$. Verifying this equivalence algorithmically, for instance by comparing the output of a Newton evaluator with that of a stable Lagrange evaluator (like the barycentric formula), provides a powerful confirmation of the underlying theory .

### Advanced Applications: Error Estimation and Hermite Interpolation

The true power of the divided difference framework is revealed in its application to more advanced problems, including [error analysis](@entry_id:142477) and interpolation with derivative constraints.

#### Error of Interpolation

The error of the [interpolating polynomial](@entry_id:750764), $E_n(x) = f(x) - P_n(x)$, can be expressed exactly using a divided difference. The error formula is:

$$f(x) - P_n(x) = f[x_0, x_1, \dots, x_n, x] \prod_{i=0}^{n} (x-x_i)$$

This formula, while elegant, is not immediately practical for computing the error at a point $x$, because the term $f[x_0, \dots, x_n, x]$ itself depends on the value $f(x)$ that we are trying to approximate. However, it provides the foundation for a powerful estimation technique. If we have access to one additional data point, $(x_{n+1}, f(x_{n+1}))$, we can make the reasonable approximation:

$$f[x_0, \dots, x_n, x] \approx f[x_0, \dots, x_n, x_{n+1}]$$

This is valid if $x$ is close to the other nodes. The term on the right is a constant that can be computed from the data. This leads to the error estimate:

$$f(x) - P_n(x) \approx f[x_0, \dots, x_{n+1}] \prod_{i=0}^{n} (x-x_i)$$

Notice that the right-hand side is precisely the term we would add to $P_n(x)$ to get the next-degree interpolating polynomial, $P_{n+1}(x)$. Thus, the difference between successive interpolating polynomials, $P_{n+1}(x) - P_n(x)$, serves as a computable estimate for the error in $P_n(x)$ .

#### Hermite Interpolation with Confluent Nodes

A more sophisticated problem is **Hermite interpolation**, where we seek a polynomial that matches not only function values but also derivative values at the nodes. For example, find a polynomial $p(x)$ such that $p(x_i) = f(x_i)$ and $p'(x_i) = f'(x_i)$ at a set of nodes.

The divided difference framework extends to this problem with remarkable elegance through the concept of **confluent nodes**. What is the meaning of a divided difference with repeated arguments, like $f[x_0, x_0]$? We can define it by taking a limit:

$$f[x_0, x_0] \equiv \lim_{x_1 \to x_0} f[x_0, x_1] = \lim_{x_1 \to x_0} \frac{f(x_1) - f(x_0)}{x_1 - x_0}$$

By the definition of the derivative, this limit is simply $f'(x_0)$ . This gives us a powerful new tool: a first-order divided difference with two confluent (identical) nodes is defined to be the first derivative at that node.

This principle allows us to incorporate derivative information directly into the [divided difference table](@entry_id:177983). To enforce the conditions $p(x_0) = f(x_0)$ and $p'(x_0) = f'(x_0)$, we simply list the node $x_0$ twice in our node sequence. For instance, to satisfy the four conditions $f(0)=2, f'(0)=-1, f(3)=10, f'(3)=4$, we use the node sequence $z_0=0, z_1=0, z_2=3, z_3=3$. The [divided difference table](@entry_id:177983) is constructed as usual, with the special rules for confluent nodes:
-   $f[z_0, z_1] = f[0, 0] = f'(0) = -1$
-   $f[z_2, z_3] = f[3, 3] = f'(3) = 4$
-   Other entries are computed with the standard [recursive formula](@entry_id:160630), such as $f[z_1, z_2] = f[0, 3] = \frac{f(3)-f(0)}{3-0}$.

By completing the table for this confluent node sequence, we can find the coefficients of the unique cubic Hermite interpolant in Newton form, demonstrating the profound generality and utility of the divided difference concept .