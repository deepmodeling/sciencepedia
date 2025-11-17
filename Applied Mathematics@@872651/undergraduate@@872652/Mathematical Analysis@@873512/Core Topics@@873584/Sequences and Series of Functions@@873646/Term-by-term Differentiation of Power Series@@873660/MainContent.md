## Introduction
Power series offer a powerful way to represent functions, bridging the discrete world of infinite sequences with the continuous realm of calculus. However, this representation raises a critical question: how do the familiar operations of calculus, particularly differentiation, apply to a function defined as an infinite sum? The ability to differentiate a function by operating on each term of its series individually—a process known as [term-by-term differentiation](@entry_id:142985)—is not guaranteed but, where valid, unlocks a suite of powerful analytical and problem-solving techniques. This article provides a comprehensive guide to this fundamental concept.

The first chapter, "Principles and Mechanisms," will lay the theoretical groundwork. We will explore the main theorem that permits [term-by-term differentiation](@entry_id:142985), investigate its effect on the radius and [interval of convergence](@entry_id:146678), and uncover the profound link between a function's derivatives and the coefficients of its [series expansion](@entry_id:142878). Following this, "Applications and Interdisciplinary Connections" will demonstrate the method's utility, showcasing how it can be used to evaluate complex infinite series, solve challenging differential equations, and establish connections to fields like physics, probability, and [combinatorics](@entry_id:144343). Finally, "Hands-On Practices" will offer guided problems to help you master these techniques and solidify your understanding.

## Principles and Mechanisms

The representation of functions as [power series](@entry_id:146836) unlocks a remarkable synergy between the discrete world of infinite sequences and the continuous world of [differential calculus](@entry_id:175024). A central pillar of this connection is the ability to differentiate a power series, not as a monolithic entity, but by operating on each of its infinite terms individually. This chapter elucidates the principles governing this process, known as **[term-by-term differentiation](@entry_id:142985)**, explores its profound consequences, and demonstrates its utility in solving a wide array of mathematical problems.

### The Fundamental Theorem of Differentiation for Power Series

The primary result that enables the calculus of power series is both powerful and elegant. It states that a function represented by a power series is infinitely differentiable within its [interval of convergence](@entry_id:146678), and its derivatives can be found by differentiating the series term by term.

Formally, if a function $f(x)$ is defined by a power series centered at $x=c$ with a [radius of convergence](@entry_id:143138) $R > 0$,
$$ f(x) = \sum_{n=0}^{\infty} a_n (x-c)^n = a_0 + a_1(x-c) + a_2(x-c)^2 + \dots $$
for all $x$ in the [open interval](@entry_id:144029) $(c-R, c+R)$, then $f$ is differentiable on this interval. Its derivative, $f'(x)$, is given by:
$$ f'(x) = \frac{d}{dx} \sum_{n=0}^{\infty} a_n (x-c)^n = \sum_{n=0}^{\infty} \frac{d}{dx} [a_n (x-c)^n] = \sum_{n=1}^{\infty} n a_n (x-c)^{n-1} $$
Notice that the summation for the derivative starts at $n=1$, as the derivative of the constant term $a_0$ is zero.

A crucial, and perhaps surprising, aspect of this theorem is that the resulting [power series](@entry_id:146836) for the derivative has the **same radius of convergence** $R$ as the original series [@problem_id:1325204]. While a full proof requires advanced tools, the intuition can be grasped by examining the Cauchy-Hadamard formula for the [radius of convergence](@entry_id:143138), $R = 1 / (\limsup_{n\to\infty} |a_n|^{1/n})$. The coefficients of the derivative series are $b_n = (n+1)a_{n+1}$. The term $(n+1)^{1/n}$ approaches 1 as $n \to \infty$. This factor's negligible effect in the limit is what preserves the radius of convergence. Therefore, if a function is analytic (representable by a power series) in an interval, its derivative is also analytic in the same interval. This process can be repeated indefinitely, establishing that a function represented by a power series is infinitely differentiable within its open [interval of convergence](@entry_id:146678).

For instance, consider the series for $f(x) = \arctan(x)$, which is $\sum_{n=0}^{\infty} \frac{(-1)^n}{2n+1} x^{2n+1}$. By applying the Ratio Test, one can determine its radius of convergence is $R_S=1$. Differentiating term by term gives the series $g(x) = f'(x) = \sum_{n=0}^{\infty} (-1)^n x^{2n}$. This is a geometric series which is known to converge for $|x^2|  1$, or $|x|  1$, giving it a [radius of convergence](@entry_id:143138) $R_D=1$. This confirms the general theorem for this specific case [@problem_id:2317499].

However, the guarantee of an identical radius of convergence does not extend to the behavior at the **endpoints** of the interval. Differentiation can weaken convergence at the boundaries. A classic illustration involves the function $f(x) = \sum_{n=1}^{\infty} \frac{x^n}{n^2}$. The series for $f(x)$ converges for $x=1$ (the [p-series](@entry_id:139707) $\sum 1/n^2$) and for $x=-1$ (the [alternating series](@entry_id:143758) $\sum (-1)^n/n^2$), giving it an [interval of convergence](@entry_id:146678) of $[-1, 1]$. Its term-by-term derivative is $g(x) = f'(x) = \sum_{n=1}^{\infty} \frac{x^{n-1}}{n}$. While this new series still converges at $x=-1$ (the [alternating harmonic series](@entry_id:140965)), it diverges at $x=1$ (the [harmonic series](@entry_id:147787)). Thus, the [interval of convergence](@entry_id:146678) for the derivative is $[-1, 1)$ [@problem_id:231784, @problem_id:1325179]. This leads to a more subtle theorem: if the derivative series converges at an endpoint, the original series must also converge there. The converse, as we have just seen, is not true [@problem_id:2317505].

### The Link Between Coefficients and Derivatives

The ability to differentiate a power series term by term establishes a fundamental relationship between the coefficients of the series and the derivatives of the function it represents. Let's start with a function $f(x)$ represented by a Maclaurin series (a [power series](@entry_id:146836) centered at $c=0$):
$$ f(x) = a_0 + a_1 x + a_2 x^2 + a_3 x^3 + \dots $$
Evaluating at $x=0$, we immediately find $f(0) = a_0$. Now, let's differentiate term by term:
$$ f'(x) = a_1 + 2a_2 x + 3a_3 x^2 + 4a_4 x^3 + \dots $$
Evaluating this at $x=0$ yields $f'(0) = a_1$. Differentiating again:
$$ f''(x) = 2a_2 + (3 \cdot 2)a_3 x + (4 \cdot 3)a_4 x^2 + \dots $$
Evaluating at $x=0$ gives $f''(0) = 2a_2$, or $a_2 = f''(0)/2$. One more time:
$$ f'''(x) = (3 \cdot 2 \cdot 1)a_3 + (4 \cdot 3 \cdot 2)a_4 x + \dots $$
This gives $f'''(0) = 3! a_3$, or $a_3 = f'''(0)/3!$. By continuing this process, we can derive a general formula for the $n$-th coefficient [@problem_id:1325182]:
$$ a_n = \frac{f^{(n)}(0)}{n!} $$
This celebrated formula is the cornerstone of Taylor and Maclaurin series. It tells us that the coefficients of a [power series](@entry_id:146836) are uniquely determined by the derivatives of the function at the center of expansion.

This relationship is extraordinarily useful. It allows us to compute [higher-order derivatives](@entry_id:140882) of complex functions at a point by first finding their [power series expansion](@entry_id:273325). For instance, calculating the 8th derivative of $f(x) = \frac{x^2}{1+x-2x^2}$ at $x=0$ by direct differentiation would be an arduous task. However, by using [partial fraction decomposition](@entry_id:159208), we can expand $f(x)$ into a sum of [geometric series](@entry_id:158490) and find the coefficient of the $x^8$ term, $a_8$. The derivative is then simply $f^{(8)}(0) = 8! \cdot a_8$ [@problem_id:2317474]. Similarly, to find $f^{(4)}(0)$ for a function like $f(x) = (1 - x + 3x^2)\exp(-x^2/2)$, one can find the first few terms of the Maclaurin series for $\exp(-x^2/2)$, multiply by the polynomial, identify the coefficient $c_4$ of the $x^4$ term, and compute the derivative as $f^{(4)}(0) = 4! \cdot c_4$ [@problem_id:2317483].

### Applications of Term-by-Term Differentiation

The principles outlined above are not mere theoretical curiosities; they are powerful tools for solving concrete problems.

#### Evaluating Numerical Series

Some numerical series that are difficult to sum directly can be recognized as a particular value of a [power series](@entry_id:146836) that is the derivative of a known function. For example, to find the sum of $S = \sum_{n=1}^{\infty} \frac{n}{5^n}$, we can start with the well-known [geometric series](@entry_id:158490):
$$ f(x) = \sum_{n=0}^{\infty} x^n = \frac{1}{1-x}, \quad |x|  1 $$
Differentiating term by term gives:
$$ f'(x) = \sum_{n=1}^{\infty} n x^{n-1} = \frac{1}{(1-x)^2} $$
Multiplying by $x$ gives a series whose terms are $n x^n$:
$$ xf'(x) = \sum_{n=1}^{\infty} n x^n = \frac{x}{(1-x)^2} $$
The original series $S$ is this power series evaluated at $x = 1/5$. Since $|1/5|  1$, the evaluation is valid, and the sum can be computed directly by substituting $x=1/5$ into the [closed-form expression](@entry_id:267458) [@problem_id:2317507].

#### Solving Differential Equations

One of the most significant applications of this theory is the **[power series method](@entry_id:160913) for [solving ordinary differential equations](@entry_id:635033) (ODEs)**. For linear ODEs with analytic coefficients, we can assume the solution is an analytic function and thus can be written as a power series $y(x) = \sum_{n=0}^{\infty} c_n x^n$. By differentiating this series term by term and substituting it into the ODE, we can determine a **recurrence relation** that defines the coefficients $c_n$.

Consider the ODE $y''(x) - x y'(x) - y(x) = 0$ with [initial conditions](@entry_id:152863) $y(0) = 1$ and $y'(0) = 0$ [@problem_id:2317501]. We assume a solution $y(x) = \sum_{n=0}^{\infty} c_n x^n$. The derivatives are:
$$ y'(x) = \sum_{n=1}^{\infty} n c_n x^{n-1} \quad \text{and} \quad y''(x) = \sum_{n=2}^{\infty} n(n-1) c_n x^{n-2} $$
Substituting these into the ODE and manipulating the indices of summation to combine terms under a single sum yields a [power series](@entry_id:146836) that is identically zero. By the [uniqueness of power series](@entry_id:139951) representations, every coefficient of this combined series must be zero. This provides a [recurrence relation](@entry_id:141039) linking the coefficients, such as $c_{n+2} = \frac{c_n}{n+2}$ for this particular equation. The [initial conditions](@entry_id:152863) give $c_0 = y(0) = 1$ and $c_1 = y'(0) = 0$. The recurrence relation then allows us to compute all subsequent coefficients, uniquely determining the series solution.

#### Verifying and Discovering Identities

Term-by-term differentiation can also be used to confirm the consistency of calculus with the series representations of [elementary functions](@entry_id:181530). For example, differentiating the Maclaurin series for $\sin(x)$ term by term produces precisely the Maclaurin series for $\cos(x)$, elegantly confirming the familiar rule $\frac{d}{dx}\sin(x) = \cos(x)$ at the level of their [infinite series](@entry_id:143366) representations [@problem_id:2317469]. Similar exercises confirm that the derivative of the series for $\cosh(x)$ is the series for $\sinh(x)$ [@problem_id:2317497] [@problem_id:1325193], and the derivative of the series for $\arctan(x)$ is the geometric series for $\frac{1}{1+x^2}$ [@problem_id:2317490].

### Theoretical Consequences and Uniqueness

The rigid structure imposed by the requirement of analyticity leads to several profound theoretical consequences.

#### Symmetry

The rules of differentiation for [even and odd functions](@entry_id:157574) are beautifully reflected in their power series. An [even function](@entry_id:164802), $f(x) = f(-x)$, has a power series consisting only of even powers of $x$. When differentiated term by term, each term $a_{2n}x^{2n}$ becomes $(2n)a_{2n}x^{2n-1}$, an odd power of $x$. The resulting series thus represents an [odd function](@entry_id:175940) [@problem_id:2317460]. Conversely, differentiating the odd-powered series of an odd function yields a series with only even powers, representing an [even function](@entry_id:164802) [@problem_id:2317490].

#### Uniqueness and the Identity Theorem

The relationship $a_n = f^{(n)}(c)/n!$ implies that if two [power series](@entry_id:146836) are equal on an [open interval](@entry_id:144029), their corresponding coefficients must be identical. This uniqueness has strong implications. For example, if a function's derivative $f'(x)$ is identically zero within the [interval of convergence](@entry_id:146678), then the coefficients of its series, $n a_n$, must all be zero for $n \ge 1$. This forces $a_n = 0$ for all $n \ge 1$, meaning the series reduces to its constant term $a_0$. Thus, the function $f(x)$ must be constant on its [interval of convergence](@entry_id:146678) [@problem_id:1325163]. As a direct corollary, if two functions $f(x)$ and $g(x)$ have the same derivative, $f'(x) = g'(x)$, throughout their common [interval of convergence](@entry_id:146678), then their series coefficients must be equal for all terms of degree one or higher. This implies that the functions can differ only by a constant: $f(x) - g(x) = a_0 - b_0$ [@problem_id:1325196]. An even stronger statement can be made: if the derivative $f'(x)$ of a globally convergent [power series](@entry_id:146836) is a polynomial, then the function $f(x)$ itself must be a polynomial [@problem_id:1325172].

This rigidity is captured most powerfully by the **Identity Theorem** for analytic functions. It states that if two functions, analytic on a connected open domain, are equal on a set of points that has an accumulation point within that domain, then the functions must be identical everywhere in the domain. In the context of a [power series](@entry_id:146836) $f(x)$ centered at $c$, if $f(x_k)=0$ for a sequence of distinct points $\{x_k\}$ that converges to a point inside the [interval of convergence](@entry_id:146678) (including the center $c$), then the function must be identically zero, meaning all its coefficients are zero [@problem_id:1325168]. This theorem underscores the extraordinary structural integrity of [analytic functions](@entry_id:139584): their behavior in an arbitrarily small neighborhood dictates their behavior everywhere.

In summary, the principle of [term-by-term differentiation](@entry_id:142985) is not merely a computational convenience; it is a gateway to understanding the deep structure of analytic functions, providing tools for solving equations, evaluating sums, and revealing the profound connection between a function's local properties and its global identity.