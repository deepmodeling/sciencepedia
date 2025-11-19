## Introduction
Power series stand as a fundamental concept in mathematical analysis, creating a powerful link between the discrete world of sequences and the continuous domain of functions. They allow us to represent complex functions, like $\sin(x)$ or $\exp(x)$, as infinite polynomials. A natural and critical question then arises: how do the standard operations of calculus, particularly differentiation, apply to these infinite sums? Can we simply differentiate a [power series](@entry_id:146836) term by term, as we would a finite polynomial, and trust the result? This article provides a comprehensive answer to that question, establishing the theoretical bedrock for this essential technique.

Across the following chapters, you will embark on a journey from foundational theory to practical application.
*   **Principles and Mechanisms** establishes the core theorem of [term-by-term differentiation](@entry_id:142985), exploring the intimate relationship between a function's derivatives and its series coefficients, and proving the crucial fact that the radius of convergence remains unchanged after differentiation.
*   **Applications and Interdisciplinary Connections** demonstrates the theorem's immense utility, showing how it is used to solve complex differential equations, evaluate series sums, and serve as a foundational tool in fields like combinatorics and probability theory.
*   **Hands-On Practices** provides a set of targeted problems to solidify your understanding and build practical skills in applying these concepts.

By the end of this exploration, you will not only understand the formal justification for differentiating [power series](@entry_id:146836) but also master its application as a versatile problem-solving tool.

## Principles and Mechanisms

The representation of functions as [power series](@entry_id:146836) is a cornerstone of mathematical analysis, providing a bridge between the discrete world of sequences and the continuous world of functions. A central question that arises is how the fundamental operations of calculus, particularly differentiation, interact with these [infinite series](@entry_id:143366) representations. This chapter establishes the rigorous foundation for the term-by-term [differentiation of power series](@entry_id:183610), a powerful technique with far-reaching consequences in both pure and [applied mathematics](@entry_id:170283).

### The Intimate Link Between Coefficients and Derivatives

Before we explore the differentiation of a power series, it is essential to first appreciate the profound relationship between the coefficients of the series and the derivatives of the function it represents. This relationship is, in fact, the very basis for the Taylor and Maclaurin series expansions.

Consider a function $f(x)$ that can be represented by a power series centered at $x=c$ within an [interval of convergence](@entry_id:146678) $(c-R, c+R)$ where $R > 0$:
$$ f(x) = \sum_{n=0}^{\infty} a_n (x-c)^n = a_0 + a_1(x-c) + a_2(x-c)^2 + a_3(x-c)^3 + \dots $$
If we evaluate this function at the center $x=c$, every term involving $(x-c)$ vanishes, leaving us with:
$$ f(c) = a_0 $$
This gives us the zeroth coefficient. To find the next coefficient, $a_1$, let us assume for a moment that we can differentiate the series term-by-term, just as we would a finite polynomial:
$$ f'(x) = \sum_{n=1}^{\infty} n a_n (x-c)^{n-1} = a_1 + 2a_2(x-c) + 3a_3(x-c)^2 + \dots $$
Evaluating this derivative series at $x=c$ again eliminates all terms except the first:
$$ f'(c) = a_1 $$
Continuing this process, we compute the second derivative:
$$ f''(x) = \sum_{n=2}^{\infty} n(n-1) a_n (x-c)^{n-2} = 2a_2 + 3 \cdot 2 a_3(x-c) + \dots $$
Evaluating at $x=c$ yields:
$$ f''(c) = 2a_2 = 2! a_2 $$
By induction, after taking $k$ derivatives, we arrive at the expression:
$$ f^{(k)}(x) = \sum_{n=k}^{\infty} n(n-1)\cdots(n-k+1) a_n (x-c)^{n-k} $$
The summation term can be written using factorial notation as $\frac{n!}{(n-k)!}$. When we evaluate at $x=c$, only the first term of this series (where $n=k$) is non-zero:
$$ f^{(k)}(c) = k(k-1)\cdots(1) a_k = k! a_k $$
Solving for the coefficient $a_k$ gives us the celebrated formula [@problem_id:1325182]:
$$ a_k = \frac{f^{(k)}(c)}{k!} $$
This formula demonstrates that if a function has a power [series representation](@entry_id:175860), its coefficients are uniquely determined by the function's successive derivatives at the center of expansion.

This relationship is not merely a theoretical curiosity; it provides a remarkably efficient method for calculating [higher-order derivatives](@entry_id:140882) of complex functions at a specific point. Instead of performing tedious repeated differentiation, one can instead find the function's [power series expansion](@entry_id:273325) and identify the relevant coefficient.

For example, suppose we wish to find the value of $f^{(4)}(0)$ for the function $f(x) = (1 - x + 3x^2)\exp(-x^2/2)$ [@problem_id:2317483]. Direct computation would involve four applications of the [product rule](@entry_id:144424), a laborious and error-prone process. A more elegant approach is to use the Maclaurin series (a [power series](@entry_id:146836) centered at $c=0$). The series for $\exp(u)$ is $\sum_{k=0}^{\infty} u^k/k!$. Substituting $u = -x^2/2$, we get:
$$ \exp(-x^2/2) = 1 - \frac{x^2}{2} + \frac{1}{2!}\left(-\frac{x^2}{2}\right)^2 + \dots = 1 - \frac{1}{2}x^2 + \frac{1}{8}x^4 - O(x^6) $$
Now, we multiply this series by the polynomial $P(x) = 1 - x + 3x^2$:
$$ f(x) = (1 - x + 3x^2) \left(1 - \frac{1}{2}x^2 + \frac{1}{8}x^4 - \dots\right) $$
From the relation $a_4 = f^{(4)}(0)/4!$, we only need to find the coefficient of the $x^4$ term, $a_4$. We find this by collecting all products that result in a power of $x^4$:
$$ a_4 x^4 = (1)\left(\frac{1}{8}x^4\right) + (-x)(0 \cdot x^3) + (3x^2)\left(-\frac{1}{2}x^2\right) = \left(\frac{1}{8} - \frac{3}{2}\right)x^4 = -\frac{11}{8}x^4 $$
The coefficient is $a_4 = -11/8$. Therefore, the fourth derivative at $x=0$ is:
$$ f^{(4)}(0) = 4! \cdot a_4 = 24 \left(-\frac{11}{8}\right) = -33 $$
This method, which relies on algebraic manipulation of series (often using [partial fraction decomposition](@entry_id:159208) and known geometric series expansions), is frequently more tractable than direct differentiation [@problem_id:2317474].

### The Term-by-Term Differentiation Theorem

Our derivation of the coefficient formula $a_k = f^{(k)}(c)/k!$ was based on the assumption that a [power series](@entry_id:146836) can be differentiated term-by-term. We now state this fundamental result as a formal theorem.

**Theorem (Term-by-Term Differentiation):** Let $f(x) = \sum_{n=0}^{\infty} a_n (x-c)^n$ be a [power series](@entry_id:146836) with a [radius of convergence](@entry_id:143138) $R > 0$. Then the function $f$ is differentiable on the [open interval](@entry_id:144029) $(c-R, c+R)$. Furthermore, its derivative $f'(x)$ can be found by differentiating the series term-by-term:
$$ f'(x) = \frac{d}{dx} \sum_{n=0}^{\infty} a_n (x-c)^n = \sum_{n=1}^{\infty} n a_n (x-c)^{n-1} $$
Crucially, the resulting [power series](@entry_id:146836) for $f'(x)$ has the **same radius of convergence** $R$.

This theorem is immensely powerful. It not only validates our earlier exploration but also guarantees that the process of differentiation does not shrink the domain where the [series representation](@entry_id:175860) is valid (excluding the endpoints). Consequently, within its radius of convergence, a function defined by a [power series](@entry_id:146836) is infinitely differentiable.

### Invariance of the Radius of Convergence

A key claim of the theorem is that differentiation preserves the radius of convergence. Let's investigate why this is true [@problem_id:1325204]. The radius of convergence $R_S$ for a series $S(x) = \sum a_n (x-c)^n$ is given by the Cauchy-Hadamard formula:
$$ \frac{1}{R_S} = \limsup_{n\to\infty} |a_n|^{1/n} $$
The derivative series is $T(x) = \sum_{n=1}^{\infty} n a_n (x-c)^{n-1}$. To fit the standard [power series](@entry_id:146836) form, we re-index by letting $m = n-1$, so $n = m+1$. The coefficients of $T(x)$ are $b_m = (m+1)a_{m+1}$. The radius of convergence for $T(x)$, denoted $R_T$, is:
$$ \frac{1}{R_T} = \limsup_{m\to\infty} |b_m|^{1/m} = \limsup_{m\to\infty} |(m+1)a_{m+1}|^{1/m} $$
We can separate this limit:
$$ \frac{1}{R_T} = \left( \lim_{m\to\infty} (m+1)^{1/m} \right) \left( \limsup_{m\to\infty} |a_{m+1}|^{1/m} \right) $$
The first part of this product is a standard limit that evaluates to 1. One way to see this is by considering its logarithm: $\lim_{m\to\infty} \ln((m+1)^{1/m}) = \lim_{m\to\infty} \frac{\ln(m+1)}{m} = 0$ by L'Hôpital's Rule. Thus, $\lim_{m\to\infty} (m+1)^{1/m} = \exp(0) = 1$.

The second part, $\limsup |a_{m+1}|^{1/m}$, can be shown to be equal to $\limsup |a_m|^{1/m}$. This implies that the [asymptotic behavior](@entry_id:160836) governing convergence is unchanged. Therefore,
$$ \frac{1}{R_T} = 1 \cdot \left( \limsup_{m\to\infty} |a_m|^{1/m} \right) = \frac{1}{R_S} $$
This proves that $R_T = R_S$. The act of differentiation, which introduces a factor of $n$ into the coefficients, does not alter the [radius of convergence](@entry_id:143138) because the effect of this polynomial factor is asymptotically negligible compared to the [exponential growth](@entry_id:141869) or decay determined by the radius of convergence itself.

We can see this principle in action with the series for $\arctan(x)$, which is $S(x) = \sum_{n=0}^{\infty} \frac{(-1)^n}{2n+1} x^{2n+1}$. Applying the ratio or [root test](@entry_id:138735) shows its radius of convergence is $R_S=1$. Differentiating term-by-term gives:
$$ D(x) = S'(x) = \sum_{n=0}^{\infty} \frac{(-1)^n}{2n+1} \cdot (2n+1)x^{2n} = \sum_{n=0}^{\infty} (-1)^n (x^2)^n $$
This is the well-known [geometric series](@entry_id:158490) for $\frac{1}{1+x^2}$, which converges for $|x^2|  1$, or $|x|  1$. The radius of convergence for the derivative series is $R_D=1$, confirming that $R_D = R_S$ [@problem_id:2317499].

### A Cautionary Note on Endpoints

While the radius of convergence is invariant, the behavior of the series *at the endpoints* of the [interval of convergence](@entry_id:146678) can change upon differentiation. The theorem guarantees convergence only on the [open interval](@entry_id:144029). Convergence at the endpoints must always be checked independently for both the original series and its derivative.

Differentiation can "weaken" convergence. A factor of $n$ is introduced in the coefficients of the derivative series, which can be just enough to cause divergence at an endpoint where the original series converged.

Consider the function defined by $f(x) = \sum_{n=1}^{\infty} \frac{(-1)^n (x-2)^n}{n^2}$ [@problem_id:1325179].
The [radius of convergence](@entry_id:143138) is $R=1$, so the open [interval of convergence](@entry_id:146678) is $(1, 3)$.
*   At the right endpoint, $x=3$, the series is $\sum \frac{(-1)^n}{n^2}$, which converges by the [alternating series test](@entry_id:145882) (and absolutely).
*   At the left endpoint, $x=1$, the series is $\sum \frac{(-1)^n(-1)^n}{n^2} = \sum \frac{1}{n^2}$, a convergent [p-series](@entry_id:139707).
Thus, the [interval of convergence](@entry_id:146678) for $f(x)$ is the closed interval $I_f = [1, 3]$.

Now, let's examine its derivative, $g(x) = f'(x)$:
$$ g(x) = \sum_{n=1}^{\infty} \frac{(-1)^n n(x-2)^{n-1}}{n^2} = \sum_{n=1}^{\infty} \frac{(-1)^n(x-2)^{n-1}}{n} $$
The radius of convergence is still $R=1$. We check its endpoints:
*   At $x=3$, the series becomes $\sum \frac{(-1)^n}{n}$, the [alternating harmonic series](@entry_id:140965), which converges conditionally.
*   At $x=1$, the series is $\sum \frac{(-1)^n(-1)^{n-1}}{n} = \sum \frac{-1}{n}$, the negative of the [harmonic series](@entry_id:147787), which diverges.
Therefore, the [interval of convergence](@entry_id:146678) for the derivative series is $I_g = (1, 3]$. The convergence at the left endpoint $x=1$ was lost through differentiation.

### Applications and Consequences of the Theorem

The ability to differentiate [power series](@entry_id:146836) term-by-term unlocks a vast array of applications, from evaluating difficult series to solving differential equations.

#### Direct Calculation and Summation
The theorem allows for the direct evaluation of a function's derivative, even when the function is defined by a series. This can sometimes transform a complicated series into a simpler, recognizable one. For instance, consider the function $f(x) = \sum_{n=1}^{\infty} \frac{(-1)^{n+1}}{n 3^n} (x-1)^n$ [@problem_id:2317482]. Its [radius of convergence](@entry_id:143138) is $R=3$. To find $f'(2)$, we first differentiate the series term-by-term, which is valid since $|2-1|  3$:
$$ f'(x) = \sum_{n=1}^{\infty} \frac{(-1)^{n+1}}{n 3^n} \cdot n(x-1)^{n-1} = \sum_{n=1}^{\infty} \frac{(-1)^{n+1}}{3^n} (x-1)^{n-1} $$
Now, we evaluate at $x=2$:
$$ f'(2) = \sum_{n=1}^{\infty} \frac{(-1)^{n+1}}{3^n} (1)^{n-1} = \frac{1}{3} - \frac{1}{9} + \frac{1}{27} - \dots $$
This is a [geometric series](@entry_id:158490) with first term $a = 1/3$ and [common ratio](@entry_id:275383) $r = -1/3$. The sum is:
$$ f'(2) = \frac{a}{1-r} = \frac{1/3}{1 - (-1/3)} = \frac{1/3}{4/3} = \frac{1}{4} $$

#### Solving Differential Equations
One of the most significant applications of this theory is in finding solutions to [linear ordinary differential equations](@entry_id:276013) with non-constant coefficients. The "method of series solutions" assumes the solution can be written as a power series and uses [term-by-term differentiation](@entry_id:142985) to find the coefficients.

Let's find the solution to the differential equation $y''(x) - x y'(x) - y(x) = 0$ with initial conditions $y(0) = 1$ and $y'(0) = 0$ [@problem_id:2317501]. We assume an analytic solution of the form $y(x) = \sum_{n=0}^{\infty} c_n x^n$. We compute its derivatives:
$$ y'(x) = \sum_{n=1}^{\infty} n c_n x^{n-1} \quad \text{and} \quad y''(x) = \sum_{n=2}^{\infty} n(n-1) c_n x^{n-2} $$
Substituting these into the ODE requires careful manipulation of indices to combine the sums:
$$ \sum_{n=2}^{\infty} n(n-1) c_n x^{n-2} - x \sum_{n=1}^{\infty} n c_n x^{n-1} - \sum_{n=0}^{\infty} c_n x^n = 0 $$
$$ \sum_{k=0}^{\infty} (k+2)(k+1) c_{k+2} x^k - \sum_{n=1}^{\infty} n c_n x^n - \sum_{n=0}^{\infty} c_n x^n = 0 $$
By aligning the summation indices and combining terms, we get:
$$ \sum_{n=0}^{\infty} \left[ (n+2)(n+1)c_{n+2} - n c_n - c_n \right] x^n = 0 $$
For this [power series](@entry_id:146836) to be identically zero, every coefficient must be zero. This gives us the recurrence relation:
$$ (n+2)(n+1)c_{n+2} - (n+1)c_n = 0 \implies c_{n+2} = \frac{c_n}{n+2} \quad \text{for } n \ge 0 $$
The [initial conditions](@entry_id:152863) give us the first two coefficients: $c_0 = y(0) = 1$ and $c_1 = y'(0) = 0$. The [recurrence relation](@entry_id:141039) propagates these values. Since $c_1=0$, all odd coefficients ($c_3, c_5, \dots$) will be zero. For the even coefficients:
$$ c_2 = \frac{c_0}{2} = \frac{1}{2} $$
$$ c_4 = \frac{c_2}{4} = \frac{1}{2 \cdot 4} = \frac{1}{8} $$
$$ c_6 = \frac{c_4}{6} = \frac{1}{8 \cdot 6} = \frac{1}{48} $$
This method allows us to systematically construct the unique power series solution to the differential equation.

#### Uniqueness and Antiderivatives
The [term-by-term differentiation](@entry_id:142985) theorem has important consequences for the uniqueness of functions. Suppose the derivative of a [power series](@entry_id:146836) is zero everywhere inside its [interval of convergence](@entry_id:146678): $f'(x) = \sum n a_n (x-c)^{n-1} = 0$. By the [uniqueness of power series](@entry_id:139951) coefficients, this implies that $n a_n = 0$ for all $n \ge 1$. This forces $a_n=0$ for all $n \ge 1$. The series thus collapses to its constant term: $f(x) = a_0$. This is the [power series](@entry_id:146836) analogue of the familiar result from calculus that a function with a [zero derivative](@entry_id:145492) on an interval must be constant [@problem_id:1325163].

This leads directly to a result for antiderivatives. If two power series functions $f(x)$ and $g(x)$ have the same derivative, $f'(x) = g'(x)$, within their common [interval of convergence](@entry_id:146678), then their difference $h(x) = f(x) - g(x)$ must have a derivative $h'(x)=0$. Therefore, $f(x) - g(x)$ must be a constant [@problem_id:1325196]. This means that the antiderivative of a power series is unique up to an additive constant, just as with [elementary functions](@entry_id:181530). The constant can be determined by evaluating the functions at a single point within the [interval of convergence](@entry_id:146678).

In summary, the principle of [term-by-term differentiation](@entry_id:142985) is not merely a computational shortcut but a deep structural property of analytic functions. It guarantees that the realm of power series is closed under the operation of differentiation and provides the theoretical machinery to solve differential equations, evaluate derivatives, and understand the fundamental structure of functions defined by [infinite series](@entry_id:143366).