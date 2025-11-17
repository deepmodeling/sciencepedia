## Introduction
In [computational engineering](@entry_id:178146) and [numerical analysis](@entry_id:142637), the ability to approximate complex functions or model discrete data is fundamental. Polynomial interpolation provides a powerful way to construct a continuous function that passes exactly through a given set of data points. While several methods exist to find this unique polynomial, the Newton form, which is built upon the concept of [divided differences](@entry_id:138238), stands out for its computational elegance, efficiency, and profound theoretical insights. It addresses the need for a method that is not only fast but also easily updatable as new data becomes available.

This article provides a comprehensive exploration of [divided differences](@entry_id:138238) and their role in interpolation. In the "Principles and Mechanisms" chapter, you will learn the [recursive definition](@entry_id:265514) of [divided differences](@entry_id:138238), how to construct an interpolation table, and the fundamental properties that make this approach so advantageous. Following that, the "Applications and Interdisciplinary Connections" chapter will showcase the versatility of this method across diverse fields, from creating simulation models in engineering to processing experimental data in physics and even securing information in cryptography. Finally, the "Hands-On Practices" section will allow you to apply these concepts to solve practical problems, solidifying your understanding of this essential numerical tool.

## Principles and Mechanisms

In the study of numerical methods, [polynomial interpolation](@entry_id:145762) provides a foundational toolkit for approximating functions and modeling data. While several schemes exist for constructing the unique interpolating polynomial that passes through a given set of points, the Newton form, built upon the concept of [divided differences](@entry_id:138238), offers exceptional computational efficiency and deep theoretical insight. This chapter explores the principles of [divided differences](@entry_id:138238) and the mechanisms of constructing and utilizing the associated interpolation tables.

### The Newton Form of the Interpolating Polynomial

Given a set of $n+1$ distinct data points $(x_0, y_0), (x_1, y_1), \dots, (x_n, y_n)$, our goal is to find a polynomial $P_n(x)$ of degree at most $n$ such that $P_n(x_i) = y_i$ for all $i=0, \dots, n$. One of the most elegant and computationally practical representations for this polynomial is the **Newton form**:

$P_n(x) = a_0 + a_1(x-x_0) + a_2(x-x_0)(x-x_1) + \dots + a_n \prod_{j=0}^{n-1} (x-x_j)$

This can be written more compactly as:

$P_n(x) = \sum_{k=0}^{n} a_k \prod_{j=0}^{k-1} (x-x_j)$

where the empty product for $k=0$ is defined as 1. A key feature of this representation is its **nested structure**. The degree-$n$ polynomial $P_n(x)$ is constructed by adding a correction term to the degree-$(n-1)$ polynomial $P_{n-1}(x)$ that interpolates the first $n$ points. This structure proves immensely valuable, particularly when new data points are added sequentially, as we will see later.

The coefficients $a_k$ are known as **[divided differences](@entry_id:138238)**. Specifically, the coefficient $a_k$ is the $k$-th order divided difference of the function values with respect to the nodes $x_0, x_1, \dots, x_k$. We denote this as $a_k = f[x_0, x_1, \dots, x_k]$.

### Divided Differences: Definition and Computation

Divided differences are defined recursively. Let us associate the given data values $y_i$ with a function $f$, such that $y_i = f(x_i)$.

The **zeroth-order divided difference** is simply the function value itself:
$f[x_i] = y_i$

The **first-order divided difference** is the slope of the [secant line](@entry_id:178768) connecting two points:
$f[x_i, x_j] = \frac{f[x_j] - f[x_i]}{x_j - x_i}$

For higher orders, the [recursive definition](@entry_id:265514) provides a clear computational path. The **$k$-th order divided difference** is defined in terms of two $(k-1)$-th order differences:
$f[x_i, x_{i+1}, \dots, x_{i+k}] = \frac{f[x_{i+1}, \dots, x_{i+k}] - f[x_i, \dots, x_{i+k-1}]}{x_{i+k} - x_i}$

This recursive structure lends itself to a systematic computation organized in a **[divided difference table](@entry_id:177983)**. The table is typically arranged with nodes in the first column, function values (zeroth-order differences) in the second, first-order differences in the third, and so on.

Let's illustrate this with an example. Consider the three data points $(-1, 4), (1, 0), (2, 4)$. We can construct the [divided difference table](@entry_id:177983) as follows:

| $i$ | $x_i$ | $f[x_i]$ | $f[x_i, x_{i+1}]$ | $f[x_0, x_1, x_2]$ |
|:---:|:---:|:---:|:---:|:---:|
| 0 | -1 | 4 | | |
| | | | $f[x_0, x_1] = \frac{0-4}{1-(-1)} = -2$ | |
| 1 | 1 | 0 | | $f[x_0, x_1, x_2] = \frac{4 - (-2)}{2 - (-1)} = \frac{6}{3} = 2$ |
| | | | $f[x_1, x_2] = \frac{4-0}{2-1} = 4$ | |
| 2 | 2 | 4 | | |

The coefficients $a_0, a_1, a_2$ required for the Newton form of the [interpolating polynomial](@entry_id:750764) are found along the top diagonal of this table:
$a_0 = f[x_0] = 4$
$a_1 = f[x_0, x_1] = -2$
$a_2 = f[x_0, x_1, x_2] = 2$

Using these coefficients and the nodes $x_0=-1, x_1=1$, the Newton polynomial is:
$P_2(x) = a_0 + a_1(x-x_0) + a_2(x-x_0)(x-x_1)$
$P_2(x) = 4 + (-2)(x - (-1)) + 2(x - (-1))(x - 1)$
$P_2(x) = 4 - 2(x+1) + 2(x+1)(x-1)$

Expanding this expression yields the standard monomial form:
$P_2(x) = 4 - 2x - 2 + 2(x^2 - 1) = 2 - 2x + 2x^2 - 2 = 2x^2 - 2x$

### Fundamental Properties and Computational Advantages

The Newton form and [divided differences](@entry_id:138238) possess several properties that make them central to computational engineering.

#### Uniqueness versus Representation

A key point of potential confusion is the distinction between the interpolating polynomial itself and its representation. For any given set of distinct points, the interpolating polynomial is unique. However, its Newton form representation depends on the order in which the nodes are chosen.

For example, if we take the data set $\{(0, 1), (1, 2), (2, 7)\}$ and change the order of the points, the [divided difference table](@entry_id:177983) and the resulting Newton coefficients will change. However, the final, expanded polynomial will be identical in all cases, a consequence of the uniqueness theorem for [polynomial interpolation](@entry_id:145762). For instance, ordering the points as $(0,1), (1,2), (2,7)$ yields coefficients $a_0=1, a_1=1, a_2=2$, while ordering them as $(1,2), (2,7), (0,1)$ yields coefficients $a'_0=2, a'_1=5, a'_2=2$. Both representations, though constructed differently, expand to the same unique quadratic $P(x) = 2x^2 - x + 1$. An important related property is that the *highest-order* divided difference is independent of the permutation of its arguments (e.g., $f[x_0, x_1, x_2] = f[x_1, x_2, x_0]$), whereas the intermediate coefficients are not.

#### Efficiency of Updating and Computational Cost

The nested structure of the Newton polynomial is its greatest practical advantage. Suppose we have already computed the degree-$n$ interpolant $P_n(x)$ and its corresponding [divided difference table](@entry_id:177983), and a new data point $(x_{n+1}, y_{n+1})$ becomes available. To find the new interpolant $P_{n+1}(x)$, we do not need to start from scratch. We simply add one new term:

$P_{n+1}(x) = P_n(x) + a_{n+1} \prod_{j=0}^{n} (x - x_j)$

where $a_{n+1} = f[x_0, \dots, x_{n+1}]$. To find this new coefficient, we only need to compute the new entries along the bottom diagonal of the [divided difference table](@entry_id:177983), which is an operation of complexity $O(n)$. This is vastly more efficient than alternative methods, such as re-solving the $(n+2) \times (n+2)$ Vandermonde linear system for the monomial coefficients, which would require $O((n+2)^3)$ operations.

More generally, constructing the entire [divided difference table](@entry_id:177983) for $n+1$ points requires computing $\frac{n(n+1)}{2}$ entries, each taking a constant number of operations. The total cost is therefore $O(n^2)$. In contrast, forming and solving the Vandermonde system is an $O(n^3)$ process. A detailed analysis shows that the ratio of computational costs between the Vandermonde and Newton methods grows approximately linearly with $n$, making the divided difference approach overwhelmingly superior for anything beyond a few points.

### Theoretical Interpretation and Error Analysis

Divided differences are not merely computational tools; they have a deep connection to the theory of derivatives and provide a powerful mechanism for error analysis.

#### Relationship to Derivatives and Geometric Meaning

A foundational result, derived from the Mean Value Theorem, states that if a function $f$ is $n$ times continuously differentiable, then for any set of distinct nodes $x_0, \dots, x_n$ in its domain, there exists a number $\xi$ in the interval spanned by these nodes such that:

$f[x_0, \dots, x_n] = \frac{f^{(n)}(\xi)}{n!}$

This theorem establishes the divided difference as an approximation to the scaled $n$-th derivative of the function. It is a common error to omit the $n!$ term.

This relationship provides a clear geometric interpretation. For three points, the quadratic interpolant $p(x)$ has a constant second derivative, which can be shown to be $p''(x) = 2 f[x_0, x_1, x_2]$. Consequently, the sign of the second-order divided difference $f[x_0, x_1, x_2]$ directly determines the [concavity](@entry_id:139843) of the unique parabola passing through the three points: if the divided difference is positive, the parabola is concave up; if negative, it is concave down.

#### Error Estimation and Determining Polynomial Degree

One of the most elegant applications of the Newton form is in [error analysis](@entry_id:142477). The error of the [interpolating polynomial](@entry_id:750764) $P_n(x)$ is given by:

$E_n(x) = f(x) - P_n(x) = f[x_0, \dots, x_n, x] \prod_{j=0}^{n} (x-x_j)$

The term $f[x_0, \dots, x_n, x]$ involves the unknown value $f(x)$ and cannot be computed directly. However, if we have an additional data point $(x_{n+1}, f(x_{n+1}))$, we can approximate the error by assuming that the divided difference does not change much:
$f[x_0, \dots, x_n, x] \approx f[x_0, \dots, x_n, x_{n+1}]$

This means the next term in the Newton series, $f[x_0, \dots, x_{n+1}] \prod_{j=0}^{n} (x-x_j)$, serves as a practical estimate for the error of $P_n(x)$. For example, when modeling thermal conductivity with a quadratic polynomial $P_2(T)$ based on three temperature points, we can use a fourth data point to compute the third divided difference and estimate the [interpolation error](@entry_id:139425) $|E_2(T)|$ at an intermediate temperature.

Furthermore, if the underlying data is generated by a polynomial of degree $m$, then a direct consequence of the relationship to derivatives is that all [divided differences](@entry_id:138238) of order $m+1$ and higher will be exactly zero. This allows an analyst to inspect the [divided difference table](@entry_id:177983) and infer the degree of the underlying polynomial function. If a column of [divided differences](@entry_id:138238) is constant and non-zero, the data is consistent with a polynomial of that degree. If a column is entirely zero, the polynomial degree is less than that order.

### Practical Considerations and Extensions

While powerful, the application of [divided differences](@entry_id:138238) requires an awareness of potential numerical issues and offers avenues for elegant extensions.

#### Numerical Stability

The [recursive formula](@entry_id:160630) for [divided differences](@entry_id:138238) involves denominators of the form $(x_{i+k} - x_i)$. If two nodes, say $x_i$ and $x_j$, are very close to each other, the problem becomes **ill-conditioned**. The divided difference $f[x_i, x_j] = \frac{y_i - y_j}{x_i - x_j}$ can become very large unless $y_i$ is also very close to $y_j$. This can lead to large coefficients in the Newton polynomial and can cause the interpolant to exhibit large gradients and oscillations, especially between the clustered nodes. Small uncertainties in the input data can be greatly amplified, leading to unreliable results.

Similarly, an error in a single function value $y_k$ will propagate through the [divided difference table](@entry_id:177983). Due to the linearity of the divided difference operator, the effect of an error $\epsilon$ in $y_k$ can be tracked by computing the [divided differences](@entry_id:138238) for a data set where all values are zero except for a single $\epsilon$ at $y_k$. The error propagates in a triangular "[fan-out](@entry_id:173211)" pattern from its origin. The final perturbation induced in the highest-order divided difference $f[x_0, \dots, x_n]$ is given by $\epsilon / \prod_{j=0, j\neq k}^{n}(x_k - x_j)$. This highlights that the impact of an error is amplified if the nodes are clustered.

#### Extension to Hermite Interpolation

The framework of [divided differences](@entry_id:138238) can be elegantly extended to **Hermite interpolation**, where derivative values are specified at some nodes in addition to function values. If at a node $x_k$ we know both the function value $f(x_k)$ and its derivative $f'(x_k)$, we can incorporate this information by treating the node as if it appears twice in the list of nodes. To handle the resulting division by zero in the standard formula, we define the first-order divided difference for coalescing points as the derivative:

$f[x_k, x_k] \equiv f'(x_k)$

With this definition, the standard [divided difference table](@entry_id:177983) can be constructed as usual. For instance, to find a polynomial that matches $U(0)=3$, $U'(0)=2$, $U(1)=4$, and $U(2)=9$, we would set up the table with the node sequence $0, 0, 1, 2$ and use the function values $3, 3, 4, 9$, defining $f[0,0]=2$. This seamless integration of derivative data showcases the remarkable flexibility and conceptual power of the divided difference formalism.