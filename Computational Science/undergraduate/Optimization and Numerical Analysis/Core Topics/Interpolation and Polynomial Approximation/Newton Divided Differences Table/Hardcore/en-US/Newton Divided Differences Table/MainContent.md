## Introduction
Approximating continuous functions from a set of discrete data points is a fundamental task across science, engineering, and finance. Polynomial interpolation stands as one of the most powerful and foundational techniques for achieving this, allowing us to create a smooth model that passes exactly through our known data. However, the way we represent this polynomial has significant implications for its computational efficiency and practical utility. While the standard [power series](@entry_id:146836) form is familiar, it can be cumbersome to work with when data changes or when we need deeper insight into the model's structure.

This article addresses this challenge by focusing on the Newton form of the interpolating polynomial, a representation built upon the elegant concept of **[divided differences](@entry_id:138238)**. This approach offers superior computational properties, particularly for updating models with new data and for understanding the relationship between the data and the polynomial's characteristics. By mastering the Newton [divided differences](@entry_id:138238) table, you will gain a versatile tool for transforming raw numbers into actionable mathematical models.

Across the following chapters, we will embark on a comprehensive exploration of this method. In **Principles and Mechanisms**, you will learn the core [recursive definition](@entry_id:265514) of [divided differences](@entry_id:138238), master the step-by-step construction of the [divided difference table](@entry_id:177983), and explore the fundamental properties that make this method so powerful. Next, in **Applications and Interdisciplinary Connections**, we will see the method in action, applying it to problems in physics, engineering design, trajectory modeling, and financial analysis. Finally, **Hands-On Practices** will provide you with the opportunity to solidify your knowledge by tackling a series of targeted problems. Let's begin by delving into the principles that govern this indispensable numerical tool.

## Principles and Mechanisms

In the preceding chapter, we introduced polynomial interpolation as a fundamental tool for approximating functions from a set of discrete data points. While various forms of the [interpolating polynomial](@entry_id:750764) exist, the Newton form offers significant computational advantages, particularly when adding new data points. The coefficients of the Newton polynomial are not arbitrary; they are specific quantities known as **[divided differences](@entry_id:138238)**. This chapter delves into the principles governing these [divided differences](@entry_id:138238), their systematic calculation via the [divided differences](@entry_id:138238) table, their fundamental properties, and their profound connection to [differential calculus](@entry_id:175024).

### The Divided Difference as a Polynomial Coefficient

The Newton form of an [interpolating polynomial](@entry_id:750764) of degree $n$ passing through the points $(x_0, f(x_0)), \dots, (x_n, f(x_n))$ is expressed as:

$P_n(x) = c_0 + c_1(x-x_0) + c_2(x-x_0)(x-x_1) + \dots + c_n(x-x_0)(x-x_1)\cdots(x-x_{n-1})$

The power of this form lies in the structure of its coefficients, $c_k$. Each coefficient can be determined sequentially.

Let's determine the first few coefficients by enforcing the interpolation conditions, $P_n(x_i) = f(x_i)$.

For $x=x_0$:
$P_n(x_0) = c_0 = f(x_0)$
The first coefficient, $c_0$, is simply the function value at the starting node, $x_0$. We define this as the **zeroth-order divided difference**:
$c_0 = f[x_0] \equiv f(x_0)$

For $x=x_1$:
$P_n(x_1) = c_0 + c_1(x_1-x_0) = f(x_1)$
Substituting $c_0 = f[x_0]$ and solving for $c_1$:
$f(x_0) + c_1(x_1-x_0) = f(x_1) \implies c_1 = \frac{f(x_1) - f(x_0)}{x_1 - x_0}$
This is the familiar formula for the slope of the [secant line](@entry_id:178768) connecting the first two points. We define this as the **first-order divided difference**:
$c_1 = f[x_0, x_1] \equiv \frac{f[x_1] - f[x_0]}{x_1 - x_0}$

Continuing this process for $x=x_2$ allows us to solve for $c_2$, and so on. The general coefficient $c_k$ is defined as the **$k$-th order divided difference** involving the points $x_0, x_1, \dots, x_k$, denoted $f[x_0, x_1, \dots, x_k]$.

This establishes a crucial identity: the coefficients in the Newton form of the interpolating polynomial are precisely the [divided differences](@entry_id:138238) along the top diagonal of the [divided difference table](@entry_id:177983). For instance, if a quadratic polynomial is written in Newton form as $P(x) = 7 + 2(x - 0) - 0.5(x - 0)(x - 3)$ based on nodes $x_0 = 0$, $x_1 = 3$, and $x_2 = 5$, we can immediately identify the [divided differences](@entry_id:138238) by inspection :
$f[x_0] = 7$
$f[x_0, x_1] = 2$
$f[x_0, x_1, x_2] = -0.5$

### The Recursive Calculation and the Divided Difference Table

While one could derive each coefficient by successively evaluating the polynomial, a far more systematic and elegant method exists. The [divided differences](@entry_id:138238) can be computed recursively. The **$k$-th order divided difference** is defined in terms of two $(k-1)$-th order differences:

$f[x_i, x_{i+1}, \dots, x_{i+k}] = \frac{f[x_{i+1}, \dots, x_{i+k}] - f[x_i, \dots, x_{i+k-1}]}{x_{i+k} - x_i}$

This [recursive definition](@entry_id:265514) is the engine for constructing a **Newton [divided difference table](@entry_id:177983)**. The table provides a structured method for computing all necessary [divided differences](@entry_id:138238), column by column, from lower order to higher order.

Let's construct a complete table for a set of four data points: $(1, 5), (2, 2), (4, 8), (5, 1)$ . Here, $x_0=1, x_1=2, x_2=4, x_3=5$.

**Column 0: Zeroth-order differences, $f[x_i]$**
These are simply the function values, $y_i$.

**Column 1: First-order differences, $f[x_i, x_{i+1}]$**
These are computed from Column 0.
$f[x_0, x_1] = \frac{f[x_1] - f[x_0]}{x_1 - x_0} = \frac{2 - 5}{2 - 1} = -3$
$f[x_1, x_2] = \frac{f[x_2] - f[x_1]}{x_2 - x_1} = \frac{8 - 2}{4 - 2} = 3$
$f[x_2, x_3] = \frac{f[x_3] - f[x_2]}{x_3 - x_2} = \frac{1 - 8}{5 - 4} = -7$

**Column 2: Second-order differences, $f[x_i, x_{i+1}, x_{i+2}]$**
These are computed from Column 1. The denominator now involves the "outer" $x$ values.
$f[x_0, x_1, x_2] = \frac{f[x_1, x_2] - f[x_0, x_1]}{x_2 - x_0} = \frac{3 - (-3)}{4 - 1} = \frac{6}{3} = 2$.
A similar calculation for three points, such as $(0,1), (1,2), (3,-4)$, would yield $f[0,1,3] = \frac{f[1,3]-f[0,1]}{3-0} = \frac{-3-1}{3} = -\frac{4}{3}$ .

$f[x_1, x_2, x_3] = \frac{f[x_2, x_3] - f[x_1, x_2]}{x_3 - x_1} = \frac{-7 - 3}{5 - 2} = -\frac{10}{3}$

**Column 3: Third-order differences, $f[x_0, x_1, x_2, x_3]$**
Finally, this is computed from Column 2.
$f[x_0, x_1, x_2, x_3] = \frac{f[x_1, x_2, x_3] - f[x_0, x_1, x_2]}{x_3 - x_0} = \frac{-\frac{10}{3} - 2}{5 - 1} = \frac{-\frac{16}{3}}{4} = -\frac{4}{3}$

The complete table is as follows:

| $i$ | $x_i$ | $f[x_i]$ | $f[x_i, \dots]$ | $f[x_i, \dots]$ | $f[x_i, \dots]$ |
|---|---|---|---|---|---|
| 0 | 1 | 5 | | | |
| | | | -3 | | |
| 1 | 2 | 2 | | 2 | |
| | | | 3 | | $-\frac{4}{3}$ |
| 2 | 4 | 8 | | $-\frac{10}{3}$ | |
| | | | -7 | | |
| 3 | 5 | 1 | | | |

### Constructing the Newton Interpolating Polynomial

Once the [divided difference table](@entry_id:177983) is computed, writing the Newton polynomial is straightforward. The required coefficients, $c_k = f[x_0, \dots, x_k]$, are found along the top diagonal of the table.

For the table above, the coefficients for the cubic polynomial interpolating the four points are $c_0=5$, $c_1=-3$, $c_2=2$, and $c_3=-\frac{4}{3}$. The polynomial is:
$P_3(x) = 5 - 3(x-1) + 2(x-1)(x-2) - \frac{4}{3}(x-1)(x-2)(x-4)$

As another example, consider a pre-computed table for the nodes $x_0=-1, x_1=1, x_2=2$ :

| $i$ | $x_i$ | $f[x_i]$ | $f[x_i, x_{i+1}]$ | $f[x_0, x_1, x_2]$ |
|---|---|---|---|---|
| 0 | -1 | 4 | | |
| | | | -2 | |
| 1 | 1 | 0 | | 2 |
| | | | 4 | |
| 2 | 2 | 4 | | |

From the top diagonal, we identify the coefficients: $f[x_0]=4$, $f[x_0, x_1]=-2$, and $f[x_0, x_1, x_2]=2$.
The quadratic [interpolating polynomial](@entry_id:750764) in Newton form is:
$P_2(x) = f[x_0] + f[x_0, x_1](x-x_0) + f[x_0, x_1, x_2](x-x_0)(x-x_1)$
$P_2(x) = 4 + (-2)(x - (-1)) + 2(x - (-1))(x - 1)$
$P_2(x) = 4 - 2(x+1) + 2(x+1)(x-1)$

To express this in the standard [power series](@entry_id:146836) form $ax^2 + bx + c$, we expand the terms:
$P_2(x) = 4 - 2x - 2 + 2(x^2 - 1)$
$P_2(x) = 2 - 2x + 2x^2 - 2$
$P_2(x) = 2x^2 - 2x$

### Key Properties of Divided Differences

Divided differences possess several fundamental properties that are crucial for both theoretical understanding and practical application.

#### Symmetry

A remarkable and non-obvious property of [divided differences](@entry_id:138238) is their **symmetry**. The value of a divided difference $f[x_0, x_1, \dots, x_k]$ is independent of the order of the nodes $x_0, x_1, \dots, x_k$. For instance, $f[x_0, x_1, x_2] = f[x_1, x_0, x_2] = f[x_2, x_1, x_0]$, and so on for any permutation. This is not at all apparent from the [recursive definition](@entry_id:265514), which imposes a strict ordering.

We can verify this property with a direct calculation. Consider the data points $(1, 5), (3, 11), (4, 21)$ . Let's calculate the second-order divided difference in two different orders.

1.  Calculate $A = f[x_0, x_1, x_2] = f[1, 3, 4]$:
    $f[1, 3] = \frac{11 - 5}{3 - 1} = 3$
    $f[3, 4] = \frac{21 - 11}{4 - 3} = 10$
    $A = f[1, 3, 4] = \frac{f[3, 4] - f[1, 3]}{4 - 1} = \frac{10 - 3}{3} = \frac{7}{3}$

2.  Calculate $B = f[x_2, x_0, x_1] = f[4, 1, 3]$:
    $f[4, 1] = \frac{5 - 21}{1 - 4} = \frac{-16}{-3} = \frac{16}{3}$
    $f[1, 3] = 3$ (as calculated before)
    $B = f[4, 1, 3] = \frac{f[1, 3] - f[4, 1]}{3 - 4} = \frac{3 - \frac{16}{3}}{-1} = \frac{\frac{9-16}{3}}{-1} = \frac{-\frac{7}{3}}{-1} = \frac{7}{3}$

As shown, $A=B$, verifying the symmetry. This property is powerful because it allows us to compute any divided difference $f[x_i, \dots, x_j]$ even if it's not on the top diagonal of a specific table, provided we have enough information to reconstruct the necessary sub-problems .

#### Divided Differences of Polynomials

A second profound property emerges when we apply the divided difference operator to a polynomial function. Let's consider a general quadratic function, $f(x) = ax^2 + bx + c$, with $a \neq 0$ .

The first-order divided difference between any two distinct points $x_i$ and $x_j$ is:
$f[x_i, x_j] = \frac{(ax_j^2 + bx_j + c) - (ax_i^2 + bx_i + c)}{x_j - x_i} = \frac{a(x_j^2 - x_i^2) + b(x_j - x_i)}{x_j - x_i}$
$f[x_i, x_j] = a(x_j + x_i) + b$

Now, let's compute the second-order divided difference for three distinct points $x_0, x_1, x_2$:
$f[x_0, x_1, x_2] = \frac{f[x_1, x_2] - f[x_0, x_1]}{x_2 - x_0} = \frac{(a(x_2 + x_1) + b) - (a(x_1 + x_0) + b)}{x_2 - x_0}$
$f[x_0, x_1, x_2] = \frac{a(x_2 - x_0)}{x_2 - x_0} = a$

The second-order divided difference of a quadratic polynomial is a constant, equal to its leading coefficient, $a$. This result generalizes:

**Theorem:** For a polynomial $P(x)$ of degree $n$ with leading coefficient $a_n$, the $n$-th order divided difference $P[x_0, x_1, \dots, x_n]$ is constant and equal to $a_n$ for any set of $n+1$ distinct points. As a direct consequence, any divided difference of order $n+1$ or higher is identically zero.

This theorem has significant implications. For example, if we are told that for some unknown function $f(x)$, the fourth-order divided difference $f[x_0, x_1, x_2, x_3, x_4]$ is zero for any choice of five distinct points, this implies that the function must be a polynomial of degree at most 3 . This is because the error term for a cubic interpolating polynomial, which is proportional to the fourth-order divided difference, would be zero everywhere, meaning the function is identical to its cubic interpolant.

### The Link to Calculus and Error Analysis

The structure of [divided differences](@entry_id:138238) hints at a deep connection with the concept of derivatives from calculus. This connection provides both theoretical insight and a framework for [error analysis](@entry_id:142477).

#### The Mean Value Theorem for Divided Differences

The link between [divided differences](@entry_id:138238) and derivatives is formalized by the following theorem:

**Theorem:** If a function $f$ is $n$ times continuously differentiable on an interval $[a, b]$, and $x_0, x_1, \dots, x_n$ are distinct points in $[a, b]$, then there exists a number $\xi$ in the [open interval](@entry_id:144029) spanned by these points such that:
$f[x_0, x_1, \dots, x_n] = \frac{f^{(n)}(\xi)}{n!}$

This theorem states that the $n$-th order divided difference is equal to the $n$-th derivative evaluated at some intermediate point, scaled by $n!$. The first-order difference $f[x_0, x_1]$ is a discrete analogue of the first derivative, and this theorem is a generalization of the Mean Value Theorem from calculus.

Let's revisit the case of the quadratic $f(x) = ax^2 + bx + c$ . Its derivatives are $f'(x) = 2ax + b$ and $f''(x) = 2a$. According to the theorem, the second-order divided difference is:
$f[x_0, x_1, x_2] = \frac{f''(\xi)}{2!} = \frac{2a}{2} = a$
This provides an elegant confirmation of our previous algebraic derivation. The theorem also allows us to determine the constant ratio between the second-order divided difference and the second derivative for any quadratic:
$\frac{f[x_0, x_1, x_2]}{f''(x)} = \frac{a}{2a} = \frac{1}{2}$

#### Error Propagation in the Divided Difference Table

In practical applications, the initial function values $y_i = f(x_i)$ often come from measurements and are subject to error. It is crucial to understand how a single error propagates through the [divided difference table](@entry_id:177983).

Because the divided difference calculation is a linear operation (i.e., $(f+g)[x_0, x_1] = f[x_0, x_1] + g[x_0, x_1]$), we can analyze the propagation of the error itself. Let's assume a single measurement, $y_k$, has an error of $\epsilon_y$, while all other measurements are exact.

Consider a scenario with five points $x_0, \dots, x_4$ where only $y_2$ is faulty, with an error $E[x_2] = \epsilon_y = 0.48$. All other initial errors $E[x_i]$ are zero . Let's trace this error. The nodes are $x_0=0, x_1=1, x_2=3, x_3=4, x_4=7$.

The error propagates according to the same [recursive formula](@entry_id:160630): $E[x_i, \dots, x_{i+k}] = \frac{E[x_{i+1}, \dots, x_{i+k}] - E[x_i, \dots, x_{i+k-1}]}{x_{i+k} - x_i}$.

- **Errors in 1st Order Differences**: Only the differences that "straddle" $x_2$ are affected.
  $E[x_1, x_2] = \frac{E[x_2] - E[x_1]}{x_2 - x_1} = \frac{\epsilon_y - 0}{3 - 1} = \frac{\epsilon_y}{2}$
  $E[x_2, x_3] = \frac{E[x_3] - E[x_2]}{x_3 - x_2} = \frac{0 - \epsilon_y}{4 - 3} = -\epsilon_y$
  All other first-order errors ($E[x_0, x_1]$, $E[x_3, x_4]$) are zero.

- **Errors in 2nd Order Differences**: The error spreads further into a triangular pattern.
  $E[x_0, x_1, x_2] = \frac{E[x_1, x_2] - E[x_0, x_1]}{x_2 - x_0} = \frac{\epsilon_y/2 - 0}{3 - 0} = \frac{\epsilon_y}{6}$
  $E[x_1, x_2, x_3] = \frac{E[x_2, x_3] - E[x_1, x_2]}{x_3 - x_1} = \frac{-\epsilon_y - \epsilon_y/2}{4 - 1} = -\frac{\epsilon_y}{2}$
  $E[x_2, x_3, x_4] = \frac{E[x_3, x_4] - E[x_2, x_3]}{x_4 - x_2} = \frac{0 - (-\epsilon_y)}{7 - 3} = \frac{\epsilon_y}{4}$

- **Errors in 3rd Order Differences**:
  $E[x_0, x_1, x_2, x_3] = \frac{E[x_1, x_2, x_3] - E[x_0, x_1, x_2]}{x_3 - x_0} = \frac{-\epsilon_y/2 - \epsilon_y/6}{4 - 0} = -\frac{\epsilon_y}{6}$
  $E[x_1, x_2, x_3, x_4] = \frac{E[x_2, x_3, x_4] - E[x_1, x_2, x_3]}{x_4 - x_1} = \frac{\epsilon_y/4 - (-\epsilon_y/2)}{7 - 1} = \frac{\epsilon_y}{8}$

The sum of the absolute values of the errors in the third-order differences is $|-\frac{\epsilon_y}{6}| + |\frac{\epsilon_y}{8}| = \frac{\epsilon_y}{6} + \frac{\epsilon_y}{8} = \frac{7\epsilon_y}{24}$. With $\epsilon_y=0.48$, the total error is $\frac{7 \times 0.48}{24} = 7 \times 0.02 = 0.14$.

This analysis demonstrates that a single [local error](@entry_id:635842) in the input data propagates and affects an expanding "triangle" of values in the table. Furthermore, the denominators $(x_{i+k} - x_i)$ can amplify or diminish the error's magnitude. This makes higher-order [divided differences](@entry_id:138238) particularly sensitive to [measurement noise](@entry_id:275238), a critical consideration in their practical use.