## Introduction
In computational science, a fundamental task is to model a continuous function from a set of discrete data points. Polynomial interpolation offers a classic solution to this problem by constructing a polynomial that passes exactly through each point. Among various forms, the Newton form of the interpolating polynomial stands out for its computational efficiency and deep theoretical insights. This article addresses the need for a robust framework to not only construct these polynomials but also to understand their properties, applications, and limitations.

This article will guide you through the theory and practice of Newton's [divided differences](@entry_id:138238). In "Principles and Mechanisms," we will build the Newton polynomial from the ground up, explore the properties of its divided-difference coefficients, and reveal their profound connection to the derivatives of a function. In "Applications and Interdisciplinary Connections," we will witness the method's versatility, from modeling physical systems and analyzing [time-series data](@entry_id:262935) to its foundational role in numerical calculus and modern data science. Finally, in "Hands-On Practices," you will solidify your knowledge by implementing these algorithms to solve practical problems and observe their behavior firsthand.

## Principles and Mechanisms

The Newton form of the interpolating polynomial provides not only a practical method for constructing a polynomial that passes through a given set of data points but also a profound theoretical framework that connects discrete data analysis with the continuous calculus of derivatives. This section elucidates the core principles and mechanisms of Newton's [divided differences](@entry_id:138238), from their fundamental definition and construction to their deeper theoretical properties and practical computational considerations.

### The Structure of the Newton Polynomial

Given a set of $n+1$ distinct data points $(x_0, y_0), (x_1, y_1), \dots, (x_n, y_n)$, our goal is to find the unique polynomial of degree at most $n$ that interpolates these points. While several forms exist for this polynomial, the Newton form is particularly insightful and computationally convenient. We express the polynomial, $P_n(x)$, as a sum of progressively higher-degree terms:

$P_n(x) = c_0 + c_1(x-x_0) + c_2(x-x_0)(x-x_1) + \dots + c_n \prod_{j=0}^{n-1} (x-x_j)$

The coefficients $c_k$ are determined by sequentially enforcing the interpolation conditions, $P_n(x_i) = y_i$. Let us assume the function values come from a function $f$, so $y_i = f(x_i)$.

For the first point, $(x_0, f(x_0))$, we must have $P_n(x_0) = f(x_0)$. Evaluating the polynomial at $x_0$ causes all terms after the first to vanish:
$P_n(x_0) = c_0 = f(x_0)$
Thus, the first coefficient is simply the value of the function at the starting node.

For the second point, $(x_1, f(x_1))$, the condition is $P_n(x_1) = f(x_1)$:
$P_n(x_1) = c_0 + c_1(x_1-x_0) = f(x_1)$
Substituting $c_0 = f(x_0)$ and solving for $c_1$ yields:
$c_1 = \frac{f(x_1) - f(x_0)}{x_1 - x_0}$

This quantity is the slope of the line connecting the first two points and is the first instance of a **divided difference**. We define the zeroth-order divided difference as $f[x_i] = f(x_i)$ and the first-order divided difference as:
$f[x_i, x_{i+1}] = \frac{f[x_{i+1}] - f[x_i]}{x_{i+1} - x_i}$

Proceeding to find $c_2$, we use the condition $P_n(x_2) = f(x_2)$:
$P_n(x_2) = c_0 + c_1(x_2-x_0) + c_2(x_2-x_0)(x_2-x_1) = f(x_2)$
Solving for $c_2$ gives:
$c_2 = \frac{f(x_2) - (c_0 + c_1(x_2-x_0))}{ (x_2-x_0)(x_2-x_1) }$
While this expression appears complex, it can be shown to correspond to the **second-order divided difference**, which is defined recursively:
$f[x_i, x_{i+1}, x_{i+2}] = \frac{f[x_{i+1}, x_{i+2}] - f[x_i, x_{i+1}]}{x_{i+2} - x_i}$

This pattern generalizes. The coefficient $c_k$ is the $k$-th order divided difference involving the nodes $x_0, \dots, x_k$. The general [recursive definition](@entry_id:265514) for the $k$-th order divided difference is:
$f[x_i, \dots, x_{i+k}] = \frac{f[x_{i+1}, \dots, x_{i+k}] - f[x_i, \dots, x_{i+k-1}]}{x_{i+k} - x_i}$

The Newton form of the interpolating polynomial is therefore :
$P_n(x) = f[x_0] + f[x_0, x_1](x-x_0) + \dots + f[x_0, \dots, x_n] \prod_{j=0}^{n-1} (x-x_j)$
This can be written compactly as:
$P_n(x) = \sum_{k=0}^{n} f[x_0, \dots, x_k] \prod_{j=0}^{k-1} (x-x_j)$
where the empty product for $k=0$ is defined to be $1$. The coefficients $f[x_0, \dots, x_k]$ are typically computed and stored in a **[divided difference table](@entry_id:177983)**.

### Divided Differences as Discrete Derivatives

The structure of the Newton polynomial bears a striking resemblance to a Taylor polynomial, $T_n(x) = \sum_{k=0}^n \frac{f^{(k)}(x_0)}{k!} (x-x_0)^k$. This is no coincidence; the divided difference is a discrete analog of the derivative.

The connection is most apparent for the first-order divided difference, $f[x_0, x_1] = \frac{f(x_1) - f(x_0)}{x_1 - x_0}$. This is precisely the [difference quotient](@entry_id:136462) used in the definition of the first derivative, $f'(x_0) = \lim_{x_1 \to x_0} \frac{f(x_1) - f(x_0)}{x_1 - x_0}$. Furthermore, the Mean Value Theorem states that if $f$ is continuously differentiable, there exists a point $\xi$ between $x_0$ and $x_1$ such that $f'(\xi) = f[x_0, x_1]$.

This relationship extends to all higher orders. A generalization of the Mean Value Theorem, derivable from repeated application of Rolle's Theorem, establishes a fundamental connection between [divided differences](@entry_id:138238) and derivatives :
If $f$ is $k$ times continuously differentiable on an interval containing the distinct nodes $x_0, x_1, \dots, x_k$, then there exists a number $\zeta$ in the open interval spanned by these nodes such that:
$$f[x_0, x_1, \dots, x_k] = \frac{f^{(k)}(\zeta)}{k!}$$

This identity is powerful. It states that the $k$-th order divided difference is exactly equal to the $k$-th derivative evaluated at some (unknown) intermediate point $\zeta$, scaled by $1/k!$. In the limit where all nodes $x_i$ converge to a single point $a$, the point $\zeta$ must also converge to $a$. If the derivative $f^{(k)}(x)$ is continuous, we have:
$$\lim_{x_i \to a \text{ for } i=0,\dots,k} f[x_0, x_1, \dots, x_k] = \frac{f^{(k)}(a)}{k!}$$

This limit confirms the interpretation of the Newton polynomial as a generalization of the Taylor polynomial. While a Taylor series builds a polynomial approximation using derivative information at a single point, the Newton polynomial builds an exact polynomial interpolant using function value information at a set of discrete, possibly non-uniform, points. The divided difference $f[x_0, \dots, x_k]$ serves as a discrete approximation to the scaled derivative $\frac{f^{(k)}(x_0)}{k!}$ . This convergence can be verified numerically. For a function like $f(x) = \sin(x)$, one can compute a third-order divided difference, e.g., $f[a, a+h, a+2h, a+3h]$, and observe that as the spacing $h$ decreases, the value rapidly converges to the theoretical limit $\frac{f^{(3)}(a)}{3!} = \frac{-\cos(a)}{6}$ .

### Fundamental Properties of Divided Differences

Divided differences possess several essential properties that are crucial for both theory and application.

#### Symmetry

Although not apparent from its [recursive definition](@entry_id:265514), the value of a divided difference $f[x_0, \dots, x_k]$ is a **symmetric function** of its nodes; it is invariant under any permutation of the nodes $x_0, \dots, x_k$. This property follows from the fact that the divided difference $f[x_0, \dots, x_k]$ is the leading coefficient of the unique polynomial of degree $k$ that interpolates the function $f$ at these $k+1$ nodes. Since this polynomial is unique regardless of how the points are ordered, its leading coefficient must also be independent of the node ordering. Computationally, one can verify for a set of three nodes that the values of $f[x_0, x_1, x_2]$, $f[x_1, x_0, x_2]$, $f[x_2, x_1, x_0]$, etc., are all equal, up to [floating-point precision](@entry_id:138433), across all $3!=6$ permutations .

#### Action on Polynomials

The behavior of [divided differences](@entry_id:138238) when applied to polynomials is particularly elegant and important. Let $p(x)$ be a polynomial of degree $m$.

First, the $k$-th order divided difference of $p(x)$ is a polynomial of degree $m-k$ in any one of its arguments, provided the others are held constant. An immediate and powerful consequence is that **if the order of the divided difference is greater than the degree of the polynomial, the result is zero**.
$p[x_0, \dots, x_k] = 0 \quad \text{if } k > m$
This can be proven by induction on the degree of the polynomial. This property can be demonstrated numerically by sampling a polynomial of known degree $m$ and computing its [divided difference table](@entry_id:177983); all entries for orders $k > m$ will be zero, or a very small number attributable to [floating-point rounding](@entry_id:749455) error .

Second, **the $m$-th order divided difference of a polynomial of degree $m$ is constant and equal to its leading coefficient**. Let $p(x) = a_m x^m + \dots + a_0$. Then for any set of $m+1$ distinct nodes $x_0, \dots, x_m$:
$p[x_0, \dots, x_m] = a_m$
This follows from the linearity of the divided difference operator and the fact that all differences of order $m$ for polynomials of degree less than $m$ are zero . For example, for the function $f(x) = x^3$, which is a polynomial of degree 3 with a leading coefficient of $a_3=1$, the third-order divided difference $f[x_0, x_1, x_2, x_3]$ will be exactly $1$ for any four distinct nodes, a fact that can be verified by direct calculation .

#### Relation to Finite Differences for Equispaced Nodes

In the special case where the interpolation nodes are equispaced, such that $x_i = x_0 + i h$ for a constant spacing $h > 0$, the [divided differences](@entry_id:138238) simplify and relate directly to the **forward [finite difference](@entry_id:142363) operator**, $\Delta$, defined by $\Delta f(x_i) = f(x_{i+1}) - f(x_i)$. By induction, it can be proven that the $k$-th order divided difference is directly proportional to the $k$-th order [forward difference](@entry_id:173829), $\Delta^k f(x_0) = \Delta(\Delta^{k-1} f(x_0))$ :
$$f[x_0, x_1, \dots, x_k] = \frac{\Delta^k f(x_0)}{k! h^k}$$
This result connects Newton's general formula to the Newton [forward difference](@entry_id:173829) formula, which is often introduced in the context of [finite difference methods](@entry_id:147158).

### Algorithmic and Computational Aspects

The Newton form is not just a theoretical construct; it possesses significant algorithmic advantages.

#### Efficient Incremental Updates

One of the most celebrated features of the Newton polynomial is the ease with which it can be updated when new data becomes available. Suppose we have constructed the interpolating polynomial $P_n(x)$ for the points $(x_0, y_0), \dots, (x_n, y_n)$. If a new data point $(x_{n+1}, y_{n+1})$ arrives, the new [interpolating polynomial](@entry_id:750764) $P_{n+1}(x)$ is simply:
$P_{n+1}(x) = P_n(x) + f[x_0, \dots, x_{n+1}] \prod_{j=0}^{n} (x-x_j)$

Critically, the existing coefficients $c_0, \dots, c_n$ remain unchanged. We only need to compute the single new coefficient $c_{n+1} = f[x_0, \dots, x_{n+1}]$ and append the new term. This new coefficient can be calculated efficiently without recomputing the entire [divided difference table](@entry_id:177983). The new coefficient $c_{n+1}$ can be expressed in terms of the new point $(x_{n+1}, y_{n+1})$ and the already-computed polynomial $P_n(x)$ by enforcing the condition $P_{n+1}(x_{n+1}) = y_{n+1}$:
$c_{n+1} = \frac{y_{n+1} - P_n(x_{n+1})}{\prod_{k=0}^{n}(x_{n+1} - x_k)}$
The term $P_n(x_{n+1})$ can be evaluated using the known coefficients $c_0, \dots, c_n$. This entire update process requires only $O(n)$ arithmetic operations, making the Newton form ideal for applications where data arrives sequentially  .

#### Conversion Between Bases

While the Newton form is excellent for construction, the monomial basis ($p(x) = \sum a_i x^i$) is often standard for analysis or evaluation. It is therefore useful to have a procedure to convert from Newton coefficients $\{c_k\}$ to monomial coefficients $\{a_m\}$. This can be done via a nested multiplication algorithm analogous to Horner's method. Starting with the innermost part of the nested Newton form, $Q_n(x) = c_n$, one iteratively builds up the polynomials $Q_k(x) = c_k + (x-x_k) Q_{k+1}(x)$, keeping track of the monomial coefficients at each step. This process requires $O(n^2)$ operations in total  . The reverse transformation, from monomial to Newton coefficients, is also possible and involves constructing the [divided difference table](@entry_id:177983) for the monomial basis functions.

#### Numerical Stability Considerations

In exact arithmetic, the order of nodes does not affect the value of a divided difference due to the symmetry property. However, in finite-precision floating-point arithmetic, the situation is more complex. The [recursive formula](@entry_id:160630) involves subtractions, which can lead to **[subtractive cancellation](@entry_id:172005)** and a significant loss of precision if the two numbers being subtracted are very close. This is often the case when interpolation nodes are clustered together.

Because different node orderings result in different sequences of subtractions and divisions in the construction of the [divided difference table](@entry_id:177983), the accumulated [rounding error](@entry_id:172091) can differ. Consequently, the computed value of the highest-order coefficient may exhibit a small "drift" when the node order is changed. This effect is most pronounced when swapping two very close nodes, as this directly alters a denominator in one of the earliest, most sensitive stages of the recursive calculation . The transformation between the Newton and monomial bases can also be ill-conditioned, meaning small changes in the coefficients in one basis can lead to large changes in the other. This conditioning depends on the specific locations of the nodes .

### Interpolation in the Presence of Noise

A crucial practical consideration is how interpolation behaves when the data are not exact but are contaminated with measurement noise. Suppose our data are of the form $y_i = f(x_i) + \varepsilon_i$, where $f(x)$ is the true underlying signal and $\varepsilon_i$ is random noise.

By its very definition, the [interpolating polynomial](@entry_id:750764) $P_n(x)$ passes exactly through each data point $(x_i, y_i)$. This means it fits not only the signal $f(x_i)$ but also the noise $\varepsilon_i$. When the number of data points $N$ is large, the resulting high-degree polynomial often exhibits wild oscillations between the nodes as it contorts itself to pass through every noisy data point. This phenomenon is known as **overfitting**. The model has high variance because its shape is excessively sensitive to the specific noise realization in the data.

In such scenarios, a more robust approach is often **[polynomial regression](@entry_id:176102)**. Instead of fitting a high-degree polynomial that passes through all points, one chooses a polynomial $q_m(x)$ of a much lower degree ($m \ll N-1$) and finds the coefficients that minimize the sum of the squared errors $\sum_{i=1}^N (q_m(x_i) - y_i)^2$. Because the model has fewer degrees of freedom than data points, it cannot fit the noise perfectly. Instead, it finds a "best-fit" curve that averages through the data, effectively smoothing out the noise. This results in a model with lower variance, which is often a much better approximation of the true underlying function $f(x)$, despite potentially having a small amount of bias .

It is important to recognize that if one were to perform a [polynomial regression](@entry_id:176102) with degree $m=N-1$, the resulting [least-squares solution](@entry_id:152054) would be identical to the [interpolating polynomial](@entry_id:750764), inheriting all its issues with noise. The key to successful modeling of noisy data is choosing a [model complexity](@entry_id:145563) that is justified by the data, avoiding the temptation to fit the noise that interpolation encourages. While Newton interpolation offers elegant mathematical properties and efficient algorithms, its application to real-world, noisy data requires significant caution.