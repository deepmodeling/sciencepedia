## Introduction
Polynomial interpolation is a cornerstone of numerical analysis, providing a powerful method to construct a function that precisely fits a set of data points. While various algorithms exist to create such a polynomial, a more fundamental question often precedes construction: Is the resulting polynomial guaranteed to be unique? This article addresses this crucial question, exploring the Uniqueness Theorem of Polynomial Interpolation, a principle that underpins the reliability of countless models in science and engineering.

Throughout the following sections, you will gain a comprehensive understanding of this pivotal theorem. The first section, **"Principles and Mechanisms,"** delves into the formal statement of the theorem, presents a classic [proof by contradiction](@entry_id:142130), and examines the critical conditions—such as distinct data points—required for uniqueness. We will also explore this concept from a linear algebra perspective using the Vandermonde matrix. The second section, **"Applications and Interdisciplinary Connections,"** demonstrates the far-reaching impact of uniqueness, from ensuring consistency in numerical software to enabling modeling in fields like physics, finance, and engineering, and its connection to advanced topics like [numerical integration](@entry_id:142553). Finally, **"Hands-On Practices"** provides a set of targeted problems designed to solidify your understanding of how the number and arrangement of points affect the uniqueness and degree of the resulting interpolant in both one and two dimensions.

## Principles and Mechanisms

In the study of numerical analysis and approximation theory, [polynomial interpolation](@entry_id:145762) stands as a foundational concept. The core objective is to construct a polynomial that passes precisely through a given set of data points. While methods for constructing such a polynomial are varied, a more fundamental question concerns its existence and, crucially, its uniqueness. This section delves into the principles and mechanisms that guarantee the uniqueness of the interpolating polynomial, exploring the conditions under which this uniqueness holds, the theoretical frameworks that prove it, and the practical implications of this powerful theorem.

### The Uniqueness Theorem of Polynomial Interpolation

The central tenet of this topic can be stated formally as the **Uniqueness Theorem for Polynomial Interpolation**:

*Given a set of $n+1$ data points $(x_0, y_0), (x_1, y_1), \dots, (x_n, y_n)$ where all the abscissas (the $x_i$ values) are distinct, there exists a unique polynomial $P(x)$ of degree at most $n$ that satisfies the interpolation conditions $P(x_i) = y_i$ for all $i = 0, 1, \dots, n$.*

Before delving into a formal proof, it is instructive to build intuition from a simple geometric case. Consider the task of finding a polynomial of degree at most one—a straight line of the form $P(x) = ax + b$—that passes through two distinct points, $(x_1, y_1)$ and $(x_2, y_2)$, where $x_1 \neq x_2$. Geometrically, it is a fundamental axiom that two distinct points in a plane define exactly one line. The algebraic reasoning mirrors this intuition perfectly. The slope of the line is unequivocally determined by the two points as $a = \frac{y_2 - y_1}{x_2 - x_1}$. Since $x_1 \neq x_2$, the denominator is non-zero, and the slope $a$ is unique. Once this slope is fixed, the [y-intercept](@entry_id:168689) $b$ is also uniquely determined by substituting one of the points, for instance, $b = y_1 - ax_1$. As both parameters $a$ and $b$ are uniquely determined, the polynomial $P(x)$ itself must be unique [@problem_id:2224823]. This simple case for $n=1$ is a specific instance of the general theorem.

### A Formal Proof of Uniqueness

The proof for the general case is elegant and relies on a classic proof by contradiction, leveraging a fundamental property of polynomials. The argument proceeds by assuming that uniqueness is false and then demonstrating that this assumption leads to a logical inconsistency.

Let us assume that for a given set of $n+1$ distinct points $(x_i, y_i)$, there exist two *different* polynomials, $P(x)$ and $Q(x)$, both of degree at most $n$, that interpolate these points. By the definition of interpolation, this means:
$P(x_i) = y_i$ and $Q(x_i) = y_i$ for all $i \in \{0, 1, \dots, n\}$.

Now, let's define a new polynomial, $D(x)$, as the difference between $P(x)$ and $Q(x)$:
$$ D(x) = P(x) - Q(x) $$
What can we deduce about $D(x)$? First, since $P(x)$ and $Q(x)$ are both polynomials of degree at most $n$, their difference, $D(x)$, must also be a polynomial of degree at most $n$.

Second, let's evaluate $D(x)$ at each of the interpolation nodes $x_i$:
$$ D(x_i) = P(x_i) - Q(x_i) = y_i - y_i = 0 $$
This holds for all $i = 0, 1, \dots, n$. This means that $D(x)$ has at least $n+1$ distinct roots: $x_0, x_1, \dots, x_n$.

Herein lies the contradiction. A fundamental result from algebra (a consequence of the Fundamental Theorem of Algebra) states that a *non-zero* polynomial of degree $k$ can have at most $k$ distinct roots. Our polynomial $D(x)$ has a degree of at most $n$, yet it possesses at least $n+1$ distinct roots. This is impossible if $D(x)$ is a non-zero polynomial. The only way to resolve this contradiction is to conclude that our initial assumption—that $D(x)$ is a non-zero polynomial because $P(x)$ and $Q(x)$ are different—must be false. Therefore, $D(x)$ must be the zero polynomial, i.e., $D(x) = 0$ for all $x$. If $P(x) - Q(x) = 0$, it directly implies that $P(x) = Q(x)$.

This proves that no two distinct polynomials of degree at most $n$ can pass through the same $n+1$ distinct points. The interpolating polynomial is, therefore, unique [@problem_id:2224838] [@problem_id:2224835].

### Essential Conditions for Uniqueness

The proof of uniqueness hinges on two critical conditions stated in the theorem: the number of points must be $n+1$ for a polynomial of degree at most $n$, and the $x$-coordinates (nodes) of these points must be distinct. Violating either of these conditions breaks the guarantee of uniqueness.

#### The Role of the Number of Points

The theorem requires $n+1$ points to uniquely define a polynomial of degree at most $n$. What happens if we have fewer points? Consider attempting to find a quadratic polynomial, $P(x) = ax^2 + bx + c$ (where $n=2$), that passes through only two points ($n+1=3$ are required), for instance $(0, 0)$ and $(1, 1)$.

The condition $P(0)=0$ implies $c=0$. The condition $P(1)=1$ implies $a+b+c=1$, which simplifies to $a+b=1$. This gives a relationship, $b=1-a$, but it does not uniquely determine the coefficients. Any value for $a$ will yield a valid quadratic polynomial. For example, if we choose $a=3$, then $b=-2$, giving $P_1(x) = 3x^2 - 2x$. If we choose $a=-4$, then $b=5$, giving $P_2(x) = -4x^2 + 5x$. Both are distinct quadratic polynomials, yet both pass through $(0, 0)$ and $(1, 1)$. This illustrates that with fewer than $n+1$ points, the problem is under-determined, and an infinite family of solutions exists [@problem_id:2224801].

#### The Role of Distinct Interpolation Nodes

The requirement that all $x_i$ be distinct is equally crucial. Let's examine what happens to our proof if this condition is violated. Suppose we have $n+1$ data points, but two of the nodes are the same, for example, $x_i = x_j$ for some $i \neq j$. This means we only have $n$ distinct $x$-coordinates in total.

Let's revisit the difference polynomial $D(x) = P(x) - Q(x)$. As before, its degree is at most $n$. However, it is now guaranteed to have roots only at the $n$ *distinct* nodes. So, $D(x)$ is a polynomial of degree at most $n$ with $n$ distinct roots. According to the [fundamental theorem of algebra](@entry_id:152321), a non-zero polynomial of degree $n$ *can* have $n$ roots. The contradiction we relied on previously vanishes. It is now possible for $D(x)$ to be a non-zero polynomial. For instance, if $P(x)$ and $Q(x)$ are two distinct polynomials of degree at most $n$ that interpolate the data, their difference $D(x)$ could be of the form $D(x) = C \prod_{k=1}^{n} (x-t_k)$, where $\{t_k\}_{k=1}^n$ are the $n$ distinct nodes and $C$ is a non-zero constant. Thus, the uniqueness proof fails, and multiple interpolating polynomials may exist [@problem_id:2224791].

### Alternative Perspectives on Uniqueness

The uniqueness of the interpolating polynomial can be understood from several theoretical standpoints, each offering a different and valuable insight.

#### The Linear Algebra Viewpoint: Non-Singularity of the Vandermonde Matrix

Finding an interpolating polynomial can be framed as a problem in linear algebra. Let the polynomial be $P(x) = c_0 + c_1x + c_2x^2 + \dots + c_nx^n$. The $n+1$ interpolation conditions $P(x_i) = y_i$ form a system of $n+1$ [linear equations](@entry_id:151487) for the $n+1$ unknown coefficients $c_0, c_1, \dots, c_n$:
$$
\begin{cases}
c_0 + c_1x_0 + c_2x_0^2 + \dots + c_nx_0^n  = y_0 \\
c_0 + c_1x_1 + c_2x_1^2 + \dots + c_nx_1^n  = y_1 \\
\vdots  \\
c_0 + c_1x_n + c_2x_n^2 + \dots + c_nx_n^n  = y_n
\end{cases}
$$
This system can be written in matrix form as $V\mathbf{c} = \mathbf{y}$, where:
$$ V = \begin{pmatrix} 1  x_0  x_0^2  \dots  x_0^n \\ 1  x_1  x_1^2  \dots  x_1^n \\ \vdots  \vdots  \vdots  \ddots  \vdots \\ 1  x_n  x_n^2  \dots  x_n^n \end{pmatrix}, \quad \mathbf{c} = \begin{pmatrix} c_0 \\ c_1 \\ \vdots \\ c_n \end{pmatrix}, \quad \mathbf{y} = \begin{pmatrix} y_0 \\ y_1 \\ \vdots \\ y_n \end{pmatrix} $$
The matrix $V$ is known as the **Vandermonde matrix**. From linear algebra, we know that this system has a unique solution for the coefficient vector $\mathbf{c}$ if and only if the matrix $V$ is non-singular, which is equivalent to its determinant being non-zero. The determinant of a Vandermonde matrix has a well-known formula:
$$ \det(V) = \prod_{0 \le i \lt j \le n} (x_j - x_i) $$
This formula makes it clear that $\det(V) \neq 0$ if and only if all the nodes $x_i$ are distinct. Therefore, the existence of a unique set of coefficients, and thus a unique interpolating polynomial, is directly equivalent to the non-singularity of the Vandermonde matrix, which in turn depends on the distinctness of the interpolation nodes [@problem_id:2224830]. The algebraic proof using the difference polynomial and the linear algebra proof are two sides of the same coin: the impossibility of a non-zero polynomial of degree $\le n$ having $n+1$ roots is equivalent to the [homogeneous system](@entry_id:150411) $V\mathbf{d}=\mathbf{0}$ having only the trivial solution $\mathbf{d}=\mathbf{0}$.

#### Invariance to Construction Method and Basis

The uniqueness theorem has a profound practical implication: no matter which valid algorithm or basis representation one chooses to construct the interpolating polynomial, the resulting function will be identical. For instance, one might use the **Lagrange interpolation** formula, which builds the polynomial from a weighted sum of special basis polynomials $L_i(x)$ that are 1 at $x_i$ and 0 at other nodes. Another might use the **Newton form**, which uses [divided differences](@entry_id:138238) to build the polynomial incrementally. Although the resulting algebraic expressions, say $P_A(x)$ from Lagrange and $P_B(x)$ from Newton, may appear very different, the uniqueness theorem guarantees that they are algebraically equivalent. That is, $P_A(x) = P_B(x)$ for all $x$ [@problem_id:2224808].

This [principle of invariance](@entry_id:199405) extends to the choice of basis for the [polynomial space](@entry_id:269905). The standard monomial basis {1, $x$, $x^2$, \dots, $x^n$} is just one option. One could use a basis of Chebyshev polynomials {$T_0(x)$, $T_1(x)$, \dots, $T_n(x)$} or a shifted power basis like {1, $(z-z_0)$, $(z-z_0)^2$, \dots, $(z-z_0)^n$}. The unique interpolating polynomial remains the same object; only its coordinates (the coefficients) change with the basis. For example, if one interpolates three points using the monomial basis to get $P(x) = a_0 + a_1 x + a_2 x^2$, and another person interpolates the same points using the Chebyshev basis to get $P(x) = c_0 T_0(x) + c_1 T_1(x) + c_2 T_2(x)$, the two expressions represent the very same quadratic function. One can always convert one representation to the other through algebraic substitution (e.g., using $T_2(x) = 2x^2-1$) [@problem_id:2224813].

### Generalizations and Practical Implications

#### Uniqueness in the Complex Plane

The uniqueness theorem is not confined to real-valued functions of a real variable. The entire theoretical apparatus—both the difference polynomial proof and the Vandermonde matrix argument—carries over directly to interpolation in the complex plane. Given $n+1$ points $(z_0, w_0), \dots, (z_n, w_n)$ in $\mathbb{C}^2$ with distinct nodes $z_i$, there exists a unique polynomial $P(z)$ with complex coefficients of degree at most $n$ such that $P(z_i) = w_i$ for all $i$. The core requirement is that the underlying algebraic structure (a field) supports the property that a non-zero polynomial of degree $k$ has at most $k$ roots, which is true for complex numbers. This allows for the modeling of phenomena such as system responses at complex frequencies, with the full confidence of a unique solution [@problem_id:2224840].

#### Theoretical Uniqueness versus Computational Reality

While the interpolating polynomial is mathematically unique in exact arithmetic, this theoretical purity confronts the finite-precision world of computation. Different algorithms for computing the [interpolating polynomial](@entry_id:750764), though theoretically equivalent, exhibit vastly different behaviors in the presence of [floating-point rounding](@entry_id:749455) errors.

For instance, directly solving the Vandermonde system $V\mathbf{c} = \mathbf{y}$ is notoriously unstable for even moderately large $n$, as the Vandermonde matrix becomes severely ill-conditioned. The standard Lagrange formula, while conceptually simple, can suffer from [subtractive cancellation](@entry_id:172005) when evaluating the basis polynomials. A more robust method is the **[barycentric interpolation formula](@entry_id:176462)**, which is often mathematically rearranged from the Lagrange form but provides superior [numerical stability](@entry_id:146550).

In a practical scenario, computing an interpolated value using the Lagrange formula and the barycentric formula on a computer might yield slightly different results. This discrepancy does not contradict the uniqueness theorem. Rather, it highlights that the polynomials being computed are approximations of the true unique polynomial, with the differences arising from the accumulation and propagation of [rounding errors](@entry_id:143856) specific to each algorithm's sequence of operations [@problem_id:2224833]. This distinction between theoretical uniqueness and computational results is a central theme in numerical analysis, emphasizing that the choice of algorithm is critical for achieving accurate results in practice.