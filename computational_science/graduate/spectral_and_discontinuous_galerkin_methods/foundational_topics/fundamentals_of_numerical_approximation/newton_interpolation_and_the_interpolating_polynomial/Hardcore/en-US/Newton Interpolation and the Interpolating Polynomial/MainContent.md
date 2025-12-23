## Introduction
Polynomial interpolation is a cornerstone of [numerical analysis](@entry_id:142637), enabling the approximation of complex functions with simpler, more manageable polynomials. While the [interpolating polynomial](@entry_id:750764) for a given set of data is unique, the form in which it is expressed has profound implications for both [computational efficiency](@entry_id:270255) and theoretical analysis. This article delves into one of the most versatile and powerful representations: the Newton form of the interpolating polynomial. It addresses the gap between simply knowing that an interpolant exists and understanding how to construct and leverage it for advanced applications, particularly in the realm of [high-order numerical methods](@entry_id:142601).

Across the following chapters, you will embark on a comprehensive exploration of this topic. The journey begins in **Principles and Mechanisms**, where we will systematically build the Newton polynomial using the calculus of [divided differences](@entry_id:138238) and explore its deep connections to derivatives and other interpolation forms. Next, **Applications and Interdisciplinary Connections** will showcase how these theoretical principles are put into practice to construct numerical operators, formulate sophisticated methods for solving differential equations, and build efficient [surrogate models](@entry_id:145436). Finally, **Hands-On Practices** will provide an opportunity to solidify these concepts through practical exercises that bridge theory with computational implementation in spectral and discontinuous Galerkin methods.

## Principles and Mechanisms

Polynomial interpolation is a cornerstone of numerical analysis, providing a means to approximate functions, construct [quadrature rules](@entry_id:753909), and formulate [numerical methods for differential equations](@entry_id:200837). While the uniqueness of the interpolating polynomial for a given set of distinct nodes is guaranteed, its representation is not. Different forms—such as the Lagrange, monomial, and Newton forms—offer distinct theoretical and computational advantages. This chapter delves into the principles and mechanisms of the Newton form of the [interpolating polynomial](@entry_id:750764), exploring its construction, its deep connections to differential and difference calculus, and its pivotal role in the analysis and implementation of modern [high-order numerical methods](@entry_id:142601).

### The Newton Form and Divided Differences

Given a set of $n+1$ distinct points or **nodes** $(x_0, y_0), (x_1, y_1), \dots, (x_n, y_n)$, where $y_i = f(x_i)$ for some function $f$, we seek the unique polynomial $P_n(x)$ of degree at most $n$ that passes through these points, i.e., $P_n(x_i) = y_i$ for all $i=0, \dots, n$.

The Newton form provides a systematic, constructive approach to building this polynomial. We begin with the simplest case, a zero-degree polynomial for the first point $(x_0, y_0)$:
$$ P_0(x) = y_0 $$
This polynomial correctly interpolates the first data point. To interpolate the second point $(x_1, y_1)$ as well, we seek a correction to $P_0(x)$. We construct a polynomial $P_1(x)$ of degree at most 1:
$$ P_1(x) = P_0(x) + c_1(x - x_0) $$
By construction, $P_1(x_0) = P_0(x_0) + c_1(x_0 - x_0) = y_0$, so the first interpolation condition is preserved. We enforce the second condition, $P_1(x_1) = y_1$, to determine the coefficient $c_1$:
$$ y_0 + c_1(x_1 - x_0) = y_1 \implies c_1 = \frac{y_1 - y_0}{x_1 - x_0} $$
This ratio is the familiar slope of the line connecting the two points. In the context of Newton interpolation, it is the **first-order divided difference** of $f$ with respect to the nodes $x_0$ and $x_1$.

This process is naturally extensible . Suppose we have constructed the polynomial $P_{k-1}(x)$ that interpolates the first $k$ points, $(x_0, y_0), \dots, (x_{k-1}, y_{k-1})$. We can construct $P_k(x)$ by adding a term that does not disturb the existing interpolation conditions. The polynomial $\prod_{i=0}^{k-1} (x - x_i)$ is zero at all nodes $x_0, \dots, x_{k-1}$. We can therefore write:
$$ P_k(x) = P_{k-1}(x) + c_k \prod_{i=0}^{k-1} (x - x_i) $$
Enforcing the new condition $P_k(x_k) = y_k$ allows us to solve for the coefficient $c_k$:
$$ c_k = \frac{y_k - P_{k-1}(x_k)}{\prod_{i=0}^{k-1} (x_k - x_i)} $$
This coefficient $c_k$ is defined as the **$k$-th order divided difference** of $f$ with respect to the nodes $x_0, \dots, x_k$, denoted by $f[x_0, x_1, \dots, x_k]$. The zeroth-order divided difference is simply the function value, $f[x_k] = f(x_k) = y_k$.

By repeated application of this procedure, we arrive at the **Newton form of the [interpolating polynomial](@entry_id:750764)**:
$$ P_n(x) = f[x_0] + f[x_0, x_1](x - x_0) + f[x_0, x_1, x_2](x - x_0)(x - x_1) + \dots + f[x_0, \dots, x_n] \prod_{i=0}^{n-1} (x - x_i) $$
This can be written more compactly as:
$$ P_n(x) = \sum_{k=0}^{n} f[x_0, \dots, x_k] \prod_{i=0}^{k-1} (x - x_i) $$
where the product for $k=0$ is defined to be 1. The set of polynomials $\left\{ \prod_{i=0}^{k-1} (x - x_i) \right\}_{k=0}^n$ is known as the **Newton basis**.

### Fundamental Properties of Divided Differences

The coefficients of the Newton form, the [divided differences](@entry_id:138238), possess several fundamental properties that make them a powerful analytical tool.

A more convenient, [recursive definition](@entry_id:265514) allows for their systematic computation:
$$ f[x_j, \dots, x_{j+k}] = \frac{f[x_{j+1}, \dots, x_{j+k}] - f[x_{j}, \dots, x_{j+k-1}]}{x_{j+k} - x_j} $$
This [recursion](@entry_id:264696) is the basis for constructing a **[divided difference table](@entry_id:177983)**, a triangular array that efficiently generates all necessary coefficients for the Newton polynomial. A key property, which can be proven by induction, is that the value of a divided difference is independent of the order of its arguments. For example, $f[x_0, x_1] = f[x_1, x_0]$. This **symmetry property** has a profound consequence: although our constructive definition of $P_n(x)$ depended on a specific ordering of the nodes, the resulting polynomial is identical regardless of the order chosen. This provides an alternative proof for the uniqueness of the interpolating polynomial .

**Connection to Derivatives**
Divided differences are intimately related to derivatives. Consider the first-order divided difference $f[x_0, x_1] = \frac{f(x_1) - f(x_0)}{x_1 - x_0}$. In the limit as $x_1 \to x_0$, this expression becomes the definition of the derivative $f'(x_0)$ . For instance, for the function $f(x) = \ln(\sin x)$ at $x_0 = \pi/3$, the limiting value of the divided difference is:
$$ \lim_{x_1 \to \pi/3} f[\pi/3, x_1] = f'(\pi/3) = \cot(\pi/3) = \frac{\sqrt{3}}{3} $$
This relationship generalizes. For a function $f$ that is $k$ times continuously differentiable, there exists a point $\xi$ in the interval spanned by $x_0, \dots, x_k$ such that:
$$ f[x_0, \dots, x_k] = \frac{f^{(k)}(\xi)}{k!} $$
This remarkable theorem establishes the divided difference as a discrete analogue of the derivative. In the limit of coalescing nodes, $x_i \to x_0$ for all $i$, we find $f[x_0, \dots, x_k] \to \frac{f^{(k)}(x_0)}{k!}$. This property is the foundation for **Hermite interpolation**, where the interpolant matches not only function values but also derivative values at the nodes.

**Connection to Finite Differences**
On a uniform grid where $x_j = x_0 + jh$ for some spacing $h$, [divided differences](@entry_id:138238) simplify to a scaled version of forward finite differences . The **[forward difference](@entry_id:173829) operator** $\Delta$ is defined by $\Delta f_j = f_{j+1} - f_j$, where $f_j = f(x_j)$, with higher powers defined recursively: $\Delta^r f_j = \Delta(\Delta^{r-1} f_j)$. Through induction, one can establish the identity:
$$ f[x_0, \dots, x_r] = \frac{\Delta^r f_0}{r! h^r} $$
This allows the Newton polynomial on a uniform grid to be rewritten as the **Newton [forward difference](@entry_id:173829) formula**:
$$ P_n(x) = \sum_{r=0}^{n} \frac{\Delta^r f_0}{r!} \left(\frac{x-x_0}{h}\right)^{\underline{r}} $$
where $(\xi)^{\underline{r}} = \xi(\xi-1)\cdots(\xi-r+1)$ is the **[falling factorial](@entry_id:265823)**. For example, if $f(x) = \exp(\lambda x)$, the $r$-th [forward difference](@entry_id:173829) at $x_0=0$ is $\Delta^r f_0 = (\exp(\lambda h)-1)^r$, and the coefficients of the [falling factorial](@entry_id:265823) basis become $\frac{(\exp(\lambda h) - 1)^r}{r!}$ .

### Relationship to Other Interpolation Forms and Computational Efficiency

The interpolating polynomial $P_n(x)$ is unique, but it can be expressed in different bases. By inspecting the Newton form, we can see that the term with the highest power of $x$, which is $x^n$, comes only from the last term in the sum. The coefficient of $x^n$ is therefore exactly the highest-order divided difference, $f[x_0, \dots, x_n]$. This means the **leading coefficient** of the interpolating polynomial in the monomial basis ($P_n(x) = a_n x^n + \dots + a_0$) is $a_n = f[x_0, \dots, x_n]$.

This fact provides a powerful link to the Lagrange form of the interpolating polynomial, $P_n(x) = \sum_{i=0}^n y_i \ell_i(x)$, where $\ell_i(x)$ are the Lagrange cardinal polynomials. By equating the leading coefficients in both the Newton and Lagrange forms, one can derive an explicit formula for the divided difference  :
$$ f[x_0, \dots, x_n] = \sum_{i=0}^{n} \frac{y_i}{\prod_{\substack{j=0 \\ j \neq i}}^{n} (x_i - x_j)} $$
This equivalence is particularly useful in theoretical analysis. For example, if we interpolate a polynomial $q(x)$ of degree at most $n$, the interpolant must be $q(x)$ itself. Thus, if $q(x)$ has degree less than $n$, its leading coefficient is zero, which implies that its $n$-th order divided difference must also be zero. This is a powerful property leveraged in problems such as , where the interpolation of $x^3$ by a degree-3 polynomial has a leading coefficient of 1, simplifying the overall calculation.

From a computational standpoint, the Newton and Lagrange forms have different performance characteristics .
*   **Evaluation of the Lagrange form:** $P_n(x) = \sum_{i=0}^n y_i \prod_{j \neq i} \frac{x-x_j}{x_i-x_j}$. Evaluating this at a new point $x$ requires recomputing each of the $n+1$ Lagrange basis polynomials. Each $\ell_i(x)$ requires $O(n)$ multiplications and divisions. The total cost is therefore $O(n^2)$ arithmetic operations.
*   **Evaluation of the Newton form:** The nested structure of the Newton form, $P_n(x) = c_0 + (x-x_0)(c_1 + (x-x_1)(\dots))$, lends itself to a highly efficient evaluation scheme known as **Horner's method**. The polynomial can be evaluated with only $n$ multiplications and $2n$ additions/subtractions, for a total cost of $O(n)$ operations.

Therefore, while constructing the Newton form requires computing the [divided difference table](@entry_id:177983) (an $O(n^2)$ process), it is far more efficient for repeated evaluations once the coefficients are known. This makes it preferable in applications where a single interpolant is evaluated at many points.

### Convergence and Stability of High-Order Interpolation

A critical question in approximation theory is whether the sequence of interpolating polynomials $P_n(x)$ converges to the function $f(x)$ as the number of nodes $n$ increases. The answer, perhaps surprisingly, is not always yes, and it depends profoundly on the choice of interpolation nodes.

The most intuitive choice, uniformly spaced nodes on an interval, can lead to disastrous results. For certain well-behaved, analytic functions, the interpolating polynomial develops large oscillations near the ends of the interval, and the error $\|f - P_n\|_\infty = \max_{x \in [-1,1]} |f(x) - P_n(x)|$ diverges as $n \to \infty$. This is the famous **Runge phenomenon** . For example, interpolating $f(x) = 1/(1+25x^2)$ on $[-1,1]$ with [equispaced nodes](@entry_id:168260) fails to converge. It is crucial to understand that this is a property of the node set, not the representation; reordering the nodes in the Newton form does not change the (unique) underlying polynomial and thus cannot mitigate the Runge phenomenon.

The stability of the interpolation process is quantified by the **Lebesgue constant**, $\Lambda_n$, which is the [operator norm](@entry_id:146227) of the interpolation map:
$$ \Lambda_n = \sup_{x \in [-1,1]} \sum_{j=0}^{n} |\ell_j(x)| $$
The [interpolation error](@entry_id:139425) is bounded by:
$$ \|f - P_n\|_\infty \le (1 + \Lambda_n) E_n(f) $$
where $E_n(f)$ is the error of the *best* possible [polynomial approximation](@entry_id:137391) of degree $n$. This inequality shows that convergence is a battle between the decay of the best approximation error $E_n(f)$ and the growth of the Lebesgue constant $\Lambda_n$. For [equispaced nodes](@entry_id:168260), $\Lambda_n$ grows exponentially ($\sim 2^n / (n \ln n)$), which overwhelms the geometric decay of $E_n(f)$ for [analytic functions](@entry_id:139584), causing divergence.

To ensure convergence, one must choose nodes that control the growth of $\Lambda_n$. Node sets that cluster near the endpoints of the interval, such as the **Chebyshev-Gauss-Lobatto** nodes ($x_j = \cos(j\pi/n)$) or **Legendre-Gauss-Lobatto** (LGL) nodes, are excellent choices. For these nodes, the Lebesgue constant grows only logarithmically, $\Lambda_n = O(\log n)$. If $f$ is analytic on a region in the complex plane containing the interval (specifically, a Bernstein ellipse), $E_n(f)$ decays geometrically. The slow growth of $\Lambda_n$ is not enough to spoil this convergence, and the [interpolation error](@entry_id:139425) $\|f - P_n\|_\infty$ decays geometrically as well .

The Lebesgue function, $\kappa(x) = \sum_{j=0}^n |\ell_j(x)|$, also serves as the local **absolute condition number** for [polynomial evaluation](@entry_id:272811) with respect to perturbations in the nodal data . It measures how much an error of size $\epsilon$ in the data values $y_i$ can be amplified in the computed value $P_n(x)$. For the degree-3 LGL nodes $\{-1, -1/\sqrt{5}, 1/\sqrt{5}, 1\}$ on $[-1,1]$, the condition number at the center is $\kappa(0) = |L_0(0)|+|L_1(0)|+|L_2(0)|+|L_3(0)| = |-1/8|+|5/8|+|5/8|+|-1/8| = 3/2$. The Lebesgue constant $\Lambda_n$ is the maximum value of this condition number over the entire interval.

### Interpolation as a Projection Operator in Spectral Methods

In the context of spectral and discontinuous Galerkin (DG) methods, interpolation plays a role that is deeply connected to the concept of projection. For a function space like $L^2([-1,1])$ and a polynomial subspace $\mathbb{P}_N$, we can define several operators that map a function $f$ to a polynomial in $\mathbb{P}_N$.

*   The **nodal interpolant** $I_N f \in \mathbb{P}_N$ is defined by $I_N f(x_i) = f(x_i)$ at a set of nodes $\{x_i\}_{i=0}^N$.
*   The **$L^2$ projection** $P_N f \in \mathbb{P}_N$ is the polynomial that is "closest" to $f$ in the $L^2$ norm. It is uniquely defined by the [orthogonality condition](@entry_id:168905): $\int_{-1}^1 (f - P_N f) q \, dx = 0$ for all $q \in \mathbb{P}_N$.

A fundamental property of the $L^2$ projection is that it provides the best approximation in the $L^2$ norm. Consequently, for any function $f$:
$$ \|f - P_N f\|_{L^2(-1,1)} \le \|f - I_N f\|_{L^2(-1,1)} $$
This is because $I_N f$ is just one particular polynomial in $\mathbb{P}_N$, while $P_N f$ is the one that minimizes the distance to $f$ .

The connection becomes even more profound when considering numerical quadrature. Let $\{x_i, w_i\}_{i=0}^N$ be the nodes and weights of a [quadrature rule](@entry_id:175061), such as the one associated with LGL nodes. We can define a **discrete $L^2$ projection**, $P_N^Q f \in \mathbb{P}_N$, using the discrete inner product associated with the quadrature:
$$ \sum_{i=0}^N w_i (f(x_i) - P_N^Q f(x_i)) q(x_i) = 0 \quad \text{for all } q \in \mathbb{P}_N $$
A remarkable result arises: for any set of nodes, the nodal interpolant $I_N f$ is identically equal to the discrete $L^2$ projection $P_N^Q f$  . We can see this by substituting $I_N f$ for $P_N^Q f$ in the defining equation. By definition, $f(x_i) - I_N f(x_i) = 0$ at every node $x_i$. Therefore, the sum is trivially zero, satisfying the condition. By uniqueness, $P_N^Q f = I_N f$.

This identity is a cornerstone of nodal spectral methods. It means that the simple and efficient procedure of collocating a function at the nodes is equivalent to performing a projection in a discrete norm. When these nodes are also quadrature points (like LGL nodes), this allows for the efficient and stable computation of integrals involving nonlinear terms, a process that mitigates [aliasing](@entry_id:146322) errors. However, it is essential to remember that this does not by itself prevent interpolation instability; the convergence of $I_N f$ to $f$ still depends on the function's regularity and the Lebesgue constant of the chosen nodes .