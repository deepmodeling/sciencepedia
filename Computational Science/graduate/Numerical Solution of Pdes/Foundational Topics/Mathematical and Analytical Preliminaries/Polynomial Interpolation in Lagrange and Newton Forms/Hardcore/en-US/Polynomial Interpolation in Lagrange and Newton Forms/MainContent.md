## Introduction
Polynomial interpolation is a cornerstone of numerical science, providing the essential capability to approximate complex functions from a [finite set](@entry_id:152247) of data points. Its significance is particularly profound in the numerical solution of partial differential equations (PDEs), where it underpins many advanced [discretization](@entry_id:145012) techniques. However, while the existence of a unique [interpolating polynomial](@entry_id:750764) is guaranteed, its representation is not. The choice between different forms, such as the Lagrange and Newton bases, involves critical trade-offs in computational efficiency, [numerical stability](@entry_id:146550), and algorithmic flexibility. This article demystifies these choices and their consequences. In the following chapters, we will first delve into the **Principles and Mechanisms** of the Lagrange and Newton forms, exploring their construction and inherent properties. Next, we will survey their extensive **Applications and Interdisciplinary Connections**, demonstrating their role in creating powerful PDE solvers and their links to fields like machine learning. Finally, a series of **Hands-On Practices** will provide concrete exercises to translate these theoretical concepts into practical computational skills.

## Principles and Mechanisms

Polynomial interpolation is a cornerstone of numerical analysis, providing a foundational tool for approximating functions from a [finite set](@entry_id:152247) of sample points. In the numerical solution of [partial differential equations](@entry_id:143134) (PDEs), this technique is indispensable for tasks such as constructing high-order flux reconstructions, imposing boundary conditions on complex geometries, and implementing semi-Lagrangian advection schemes. Given a set of $n+1$ distinct points, or **nodes**, $x_0, x_1, \dots, x_n$ and corresponding data values $f_0, f_1, \dots, f_n$, the goal of polynomial interpolation is to find a polynomial $p(x)$ of the lowest possible degree that satisfies the conditions $p(x_j) = f_j$ for all $j=0, \dots, n$. It is a [fundamental theorem of algebra](@entry_id:152321) that there exists a unique polynomial of degree at most $n$ that fulfills these conditions. While this polynomial is unique, its representation is not. The choice of basis for the [polynomial space](@entry_id:269905) $\mathbb{P}_n$ leads to different formulations, each with distinct computational properties and stability characteristics. This chapter elucidates the principles and mechanisms of the most common forms: the monomial (Vandermonde) basis, the Lagrange basis, and the Newton basis.

### Representations of the Interpolating Polynomial

The uniqueness of the interpolating polynomial implies that any valid construction method must yield the same mathematical object. The differences between methods lie in their algebraic formulation, computational cost, and numerical stability. To explore these differences, we will frequently refer to the concrete problem of finding the unique quadratic polynomial ($n=2$) that passes through the three data points $(0, 1), (1, 0),$ and $(2, 3)$ .

#### The Monomial Basis and the Vandermonde Matrix

The most straightforward representation of a polynomial is in the **monomial basis** $\{1, x, x^2, \dots, x^n\}$. The interpolant $p(x)$ is written as:
$p(x) = a_0 + a_1 x + a_2 x^2 + \dots + a_n x^n = \sum_{k=0}^{n} a_k x^k$.

The interpolation conditions $p(x_j) = f_j$ for each node $j=0, \dots, n$ generate a system of $n+1$ [linear equations](@entry_id:151487) for the unknown coefficients $a_0, \dots, a_n$:
$$
\begin{cases}
a_0 + a_1 x_0 + a_2 x_0^2 + \dots + a_n x_0^n  = f_0 \\
a_0 + a_1 x_1 + a_2 x_1^2 + \dots + a_n x_1^n  = f_1 \\
\vdots  \vdots \\
a_0 + a_1 x_n + a_2 x_n^2 + \dots + a_n x_n^n  = f_n
\end{cases}
$$
This system can be written in matrix form as $V\mathbf{a} = \mathbf{f}$, where $\mathbf{a} = [a_0, \dots, a_n]^T$, $\mathbf{f} = [f_0, \dots, f_n]^T$, and $V$ is the **Vandermonde matrix** with entries $V_{jk} = x_j^k$.

For our illustrative example with nodes $x_0=0, x_1=1, x_2=2$ and data $f_0=1, f_1=0, f_2=3$, the system becomes:
$$
\begin{pmatrix}
1  0  0 \\
1  1  1 \\
1  2  4
\end{pmatrix}
\begin{pmatrix}
a_0 \\ a_1 \\ a_2
\end{pmatrix}
=
\begin{pmatrix}
1 \\ 0 \\ 3
\end{pmatrix}
$$
Solving this system yields the coefficients $\begin{pmatrix} a_0  a_1  a_2 \end{pmatrix} = \begin{pmatrix} 1  -3  2 \end{pmatrix}$, so the polynomial is $p(x) = 1 - 3x + 2x^2$ .

While conceptually simple, this approach has severe practical drawbacks. The cost of solving this dense linear system with a general method like Gaussian elimination is $\Theta(n^3)$ operations, which is computationally expensive for large $n$ . More importantly, Vandermonde matrices are notoriously ill-conditioned, especially for nodes clustered together. This numerical instability makes the monomial basis unsuitable for high-degree interpolation in [floating-point arithmetic](@entry_id:146236).

#### The Lagrange Basis

The Lagrange formulation circumvents the need to solve a linear system by constructing a [basis of polynomials](@entry_id:148579) tailored to the specific set of nodes. The **Lagrange basis polynomials** $\ell_j(x)$ for $j=0, \dots, n$ are defined by the property:
$$
\ell_j(x_k) = \delta_{jk} = \begin{cases} 1  \text{if } j=k \\ 0  \text{if } j \neq k \end{cases}
$$
Each $\ell_j(x)$ is a polynomial of degree $n$ that is equal to one at its corresponding node $x_j$ and zero at all other nodes. This is achieved with the explicit formula:
$$
\ell_j(x) = \prod_{\substack{k=0 \\ k \neq j}}^{n} \frac{x-x_k}{x_j-x_k}
$$
The [interpolating polynomial](@entry_id:750764) $p(x)$ is then immediately given by a [linear combination](@entry_id:155091) of these basis polynomials, with the coefficients being the data values themselves:
$$
p(x) = \sum_{j=0}^{n} f_j \ell_j(x)
$$
Verification is trivial: at any node $x_k$, $p(x_k) = \sum_{j=0}^{n} f_j \ell_j(x_k) = \sum_{j=0}^{n} f_j \delta_{jk} = f_k$.

In the semi-Lagrangian context of numerically solving the [advection equation](@entry_id:144869) $u_t + a u_x = 0$, one might need to find the value of the solution at an off-grid point by interpolating from known grid data. For example, with nodes $x_0=-1, x_1=0, x_2=1$ and data $f(-1)=0, f(0)=1, f(1)=2$, we can construct the Lagrange basis polynomials and evaluate the interpolant at $x^\star = \frac{1}{2}$ . The resulting polynomial is simply $p(x) = x+1$, so $p(\frac{1}{2}) = \frac{3}{2}$.

The Lagrange form is elegant and theoretically important. However, direct evaluation using the product formula is computationally inefficient. A more practical variant is the **barycentric Lagrange interpolation formula**, which allows evaluation in $\Theta(n)$ operations after an initial $\Theta(n^2)$ setup cost to compute a set of [barycentric weights](@entry_id:168528) . A significant drawback of the Lagrange form is its inflexibility: if a new data point is added, all basis polynomials must be recomputed from scratch.

#### The Newton Form and Divided Differences

The Newton form offers a powerful compromise between computational efficiency and adaptability. It employs a basis constructed from the nodes themselves: $\{1, (x-x_0), (x-x_0)(x-x_1), \dots, \prod_{j=0}^{n-1}(x-x_j)\}$. The [interpolating polynomial](@entry_id:750764) is written as:
$$
p(x) = c_0 + c_1(x-x_0) + c_2(x-x_0)(x-x_1) + \dots + c_n \prod_{j=0}^{n-1}(x-x_j)
$$
The coefficients $c_k$ are known as **[divided differences](@entry_id:138238)**. They are denoted by $c_k = f[x_0, x_1, \dots, x_k]$ and are defined by a fundamental [recurrence relation](@entry_id:141039) :
*   **Zeroth order**: $f[x_i] = f_i$
*   **Higher orders ($k \ge 1$)**: $f[x_i, \dots, x_{i+k}] = \frac{f[x_{i+1}, \dots, x_{i+k}] - f[x_i, \dots, x_{i+k-1}]}{x_{i+k} - x_i}$

This [recursive definition](@entry_id:265514) allows for the efficient computation of all necessary coefficients by constructing a **[divided difference table](@entry_id:177983)**. The construction cost is $\Theta(n^2)$ operations. For instance, to convert an interpolant from Lagrange to Newton form for the data $(-1, 3), (0, -2), (2, 5)$, one computes the [divided differences](@entry_id:138238) to find the Newton coefficients $a_0 = 3, a_1 = -5, a_2 = \frac{17}{6}$ . The interpolant is thus $p(x) = 3 - 5(x+1) + \frac{17}{6}(x+1)x$.

Once the coefficients are known, evaluation at a point $x^\star$ can be performed efficiently in $\Theta(n)$ operations using a nested scheme analogous to Horner's method:
$y = c_n$
For $k = n-1, \dots, 0$:
$y = c_k + (x^\star - x_k) \cdot y$

### Properties and Extensions of the Newton Form

The Newton representation possesses several advantageous properties that make it a preferred choice in many practical applications, particularly in adaptive algorithms.

#### Extensibility

A key advantage of the Newton form is its extensibility. Suppose we have an $n$-th degree interpolant $p_n(x)$ for the points $(x_0,f_0), \dots, (x_n,f_n)$. If a new data point $(x_{n+1}, f_{n+1})$ is added, the new [interpolating polynomial](@entry_id:750764) $p_{n+1}(x)$ can be obtained by simply adding one more term to $p_n(x)$:
$$
p_{n+1}(x) = p_n(x) + f[x_0, \dots, x_{n+1}] \prod_{j=0}^{n} (x-x_j)
$$
Crucially, the original coefficients $c_0, \dots, c_n$ remain unchanged. Only the new coefficient $c_{n+1} = f[x_0, \dots, x_{n+1}]$ needs to be computed. This can be done efficiently in two ways :
1.  By evaluating the old polynomial at the new point: $c_{n+1} = \frac{f_{n+1} - p_n(x_{n+1})}{\prod_{j=0}^{n} (x_{n+1} - x_j)}$.
2.  By extending the divided difference computation: $c_{n+1}$ can be found by recursively applying the [divided difference formula](@entry_id:637971), using the previously computed values.

This property is invaluable in adaptive methods where the number of interpolation points may change during a computation, as it avoids the complete re-computation required by the Vandermonde and Lagrange forms.

#### Connection to Derivatives and Hermite Interpolation

Divided differences are deeply connected to the derivatives of the underlying function. The **Mean Value Theorem for Divided Differences** states that if $f$ is sufficiently smooth, there exists a point $\xi$ in the interval spanned by the nodes $\{x_0, \dots, x_n\}$ such that:
$$
f[x_0, \dots, x_n] = \frac{f^{(n)}(\xi)}{n!}
$$
This relationship can be formally justified using Rolle's theorem. For $n=2$, if we define an error function $e(x) = f(x) - p_2(x)$, this function has three roots at $x_0, x_1, x_2$. By Rolle's theorem, its derivative $e'(x)$ must have at least two roots, and consequently its second derivative $e''(x)$ must have at least one root, say at $\xi$. Since $p_2''(x) = 2f[x_0, x_1, x_2]$ is a constant, we find $e''(\xi) = f''(\xi) - 2f[x_0, x_1, x_2] = 0$, which proves the result . For the function $f(x) = \ln(1+x)$ and nodes $0, \frac{1}{2}, 1$, the second divided difference is $2\ln(\frac{8}{9})$, and the theorem guarantees a $\xi \in (0,1)$ such that this value equals $-\frac{1}{2(1+\xi)^2}$.

This connection allows the Newton framework to be generalized to **Hermite interpolation**, where the interpolant must match not only function values but also derivative values at the nodes. Given derivative data up to order $m_j$ at each node $x_j$, we seek a polynomial $p(x)$ that satisfies $p^{(r)}(x_j) = f^{(r)}(x_j)$ for $r=0, \dots, m_j$. This problem can be solved by creating a "confluent" sequence of nodes where each $x_j$ is repeated $m_j+1$ times. The divided difference definition is extended to these repeated nodes by taking a limit, which results in the rule :
$$
f[\underbrace{x_j, \dots, x_j}_{r+1 \text{ times}}] = \frac{f^{(r)}(x_j)}{r!}
$$
The standard Newton machinery can then be applied to this extended node sequence and the corresponding generalized [divided differences](@entry_id:138238).

### Stability of Polynomial Interpolation

While a unique interpolating polynomial always exists for distinct nodes, its practical utility depends critically on the stability of the interpolation process. Stability concerns how sensitive the resulting polynomial $p(x)$ is to small perturbations in the data values $f_j$. Such perturbations are ubiquitous in [scientific computing](@entry_id:143987), arising from [measurement error](@entry_id:270998), [round-off error](@entry_id:143577), or truncation error from previous computational steps.

The stability of interpolation is quantified by the **Lebesgue function** $\Lambda_n(x)$ and the **Lebesgue constant** $\lambda_n$. The Lebesgue function is defined as the sum of the absolute values of the Lagrange basis polynomials:
$$
\Lambda_n(x) = \sum_{j=0}^{n} |\ell_j(x)|
$$
The Lebesgue constant is the maximum value of this function over the interpolation interval $[a,b]$:
$$
\lambda_n = \max_{x \in [a,b]} \Lambda_n(x)
$$
The Lebesgue constant is precisely the operator norm of the interpolation operator $I_n: C([a,b]) \to C([a,b])$ in the supremum norm. It represents the maximum amplification factor for perturbations in the input data. Specifically, if the data values $f_j$ are perturbed by amounts $\delta_j$ such that $|\delta_j| \le \varepsilon$ for all $j$, the resulting perturbation in the interpolant is bounded by $\lVert I_n \delta \rVert_\infty \le \lambda_n \varepsilon$ . A smaller Lebesgue constant implies better stability. It is important to note that $\lambda_n$ depends only on the choice of nodes, not on the polynomial representation (Lagrange vs. Newton).

The [interpolation error](@entry_id:139425) itself is linked to stability through the famous **Lebesgue inequality**:
$$
\lVert f - p_n \rVert_\infty \le (1 + \lambda_n) \inf_{q \in \mathbb{P}_n} \lVert f - q \rVert_\infty
$$
This inequality states that the error of the [interpolating polynomial](@entry_id:750764) $p_n$ is at most a factor of $(1+\lambda_n)$ larger than the error of the best possible [polynomial approximation](@entry_id:137391) of the same degree. A large Lebesgue constant can therefore lead to an interpolant that is a poor approximation, even if the function is very smooth and well-approximable by polynomials.

The magnitude of $\lambda_n$ depends dramatically on the distribution of the interpolation nodes.
*   For **[equispaced nodes](@entry_id:168260)** on an interval, the Lebesgue constant grows exponentially with $n$. This leads to the infamous **Runge phenomenon**, where high-degree interpolation can diverge wildly from the true function, especially near the interval boundaries.
*   For **Chebyshev nodes** (the roots of Chebyshev polynomials), the Lebesgue constant exhibits slow, logarithmic growth, $\lambda_n = \mathcal{O}(\ln n)$.

This stark difference highlights the critical importance of node selection in high-order interpolation. A numerical experiment for $n=4$ shows that the Lebesgue constant for [equispaced nodes](@entry_id:168260) is approximately 2.21, while for Chebyshev nodes it is about 1.99. However, for $n=10$, the equispaced value has surged to approximately 29.16, whereas the Chebyshev value has only grown to approximately 2.40 . For any choice of nodes, it can be shown that $\lambda_n \ge 1$ always holds.

In summary, for [high-degree polynomial interpolation](@entry_id:168346), which is common in spectral methods for PDEs, the use of [equispaced nodes](@entry_id:168260) is numerically unstable and should be avoided. Node distributions that cluster near the interval endpoints, such as Chebyshev nodes, are essential for maintaining stability and ensuring the convergence of the approximation.