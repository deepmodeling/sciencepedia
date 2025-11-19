## Introduction
The representation of functions as [power series](@entry_id:146836) is a cornerstone of mathematical analysis, transforming complex functions into infinite polynomials that are far easier to manipulate. While differentiating these series term-by-term is a relatively intuitive process, the same must be rigorously justified for integration. This article addresses the fundamental question: When and how can we integrate a power series by simply integrating each of its terms? It provides a comprehensive exploration of this powerful method, from its theoretical underpinnings to its diverse applications.

Over the next three sections, you will build a solid understanding of this essential technique.
-   **Principles and Mechanisms** will introduce the fundamental theorem of [term-by-term integration](@entry_id:138696), examining the conditions under which it holds, its effect on the radius and [interval of convergence](@entry_id:146678), and the critical role of Abel's theorem for analyzing series at their boundaries.
-   **Applications and Interdisciplinary Connections** will showcase the method's utility in practice. You will learn how it is used to derive series for non-[elementary functions](@entry_id:181530), approximate intractable integrals, solve differential equations common in physics and engineering, and find the exact sum of complex numerical series.
-   **Hands-On Practices** will provide opportunities to apply these concepts through guided problems, reinforcing your ability to manipulate and integrate power series to solve concrete mathematical challenges.

By the end of this article, you will not only understand the mechanics of [term-by-term integration](@entry_id:138696) but also appreciate its role as a vital tool connecting calculus, infinite series, and applied mathematics.

## Principles and Mechanisms

The representation of functions as [power series](@entry_id:146836) is one of the most powerful tools in mathematical analysis. It allows us to approximate, differentiate, and, as we shall see in this chapter, integrate functions by performing these operations on their much simpler polynomial terms. This chapter explores the foundational theorem that justifies the term-by-term [integration of [power serie](@entry_id:200139)s](@entry_id:146836), investigates its consequences for convergence, and demonstrates its wide-ranging applications in deriving new series representations and evaluating [complex integrals](@entry_id:202758) and sums.

### The Fundamental Theorem of Term-by-Term Integration

A [power series](@entry_id:146836) is, in essence, a polynomial of infinite degree. Our experience with finite polynomials suggests that integration can be performed term by term. The central theorem of this section provides rigorous justification for extending this intuition to infinite series.

**Theorem (Term-by-Term Integration of Power Series):** Let a function $f(x)$ be represented by a [power series](@entry_id:146836) centered at $x=c$ with a radius of convergence $R > 0$:
$$ f(x) = \sum_{n=0}^{\infty} a_n (x-c)^n $$
For any $x$ within the [interval of convergence](@entry_id:146678), i.e., for $|x-c| < R$, the indefinite integral of $f(x)$ can be found by integrating the series term by term:
$$ \int f(x) \,dx = C + \sum_{n=0}^{\infty} a_n \frac{(x-c)^{n+1}}{n+1} $$
where $C$ is the constant of integration. Similarly, the [definite integral](@entry_id:142493) from $c$ to $x$ is given by:
$$ \int_c^x f(t) \,dt = \sum_{n=0}^{\infty} a_n \frac{(x-c)^{n+1}}{n+1} $$

The validity of this theorem hinges on the [uniform convergence](@entry_id:146084) of power series on any closed subinterval within their open [interval of convergence](@entry_id:146678). This uniformity ensures that the integral of the sum is indeed the sum of the integrals.

Let's examine the structure of the resulting series for an [antiderivative](@entry_id:140521), $F(x)$, where $F'(x) = f(x)$. If $f(x) = \sum_{n=0}^{\infty} a_n x^n$, integrating each term $a_n x^n$ yields $\frac{a_n}{n+1} x^{n+1}$. Summing these and including the constant of integration gives the general form for the [antiderivative](@entry_id:140521)'s [power series](@entry_id:146836) [@problem_id:1325332]:
$$ F(x) = C + \sum_{n=0}^{\infty} \frac{a_n}{n+1} x^{n+1} = C + a_0 x + \frac{a_1}{2} x^2 + \frac{a_2}{3} x^3 + \dots $$

The constant of integration, $C$, is determined by an initial condition. For instance, if we know the value of the function at the center of the series, $F(c)$, then $C = F(c)$. A common scenario is when a function is defined by a definite integral starting from the center of the series, $F(x) = \int_c^x f(t) \,dt$, in which case $F(c) = 0$ and the constant $C$ is zero. In other cases, a specific condition, such as $g(0)=5$, must be used to solve for $C$. If a function's derivative is given by a [power series](@entry_id:146836), say $g'(x) = \sum_{n=1}^{\infty} \frac{n}{4^n} x^{n-1}$, and we know $g(0)=5$, we integrate term-by-term to find $g(x) = C + \sum_{n=1}^{\infty} \frac{x^n}{4^n}$. The condition $g(0)=5$ immediately implies $C=5$ [@problem_id:1325307].

### The Radius and Interval of Convergence

A remarkable and convenient property of [term-by-term integration](@entry_id:138696) is its effect on convergence. While differentiation can degrade convergence at the endpoints of the interval, integration often improves it.

**Theorem (Radius of Convergence):** If the [power series](@entry_id:146836) for $f(x)$ has a [radius of convergence](@entry_id:143138) $R$, then the [power series](@entry_id:146836) for its integral, $\int f(x) \,dx$, also has a [radius of convergence](@entry_id:143138) $R$.

Let's briefly examine why this is true. The radius of convergence is governed by the limiting behavior of the coefficients. If the original series is $\sum a_n x^n$, the integrated series has coefficients $b_{n+1} = \frac{a_n}{n+1}$. Let's consider the [ratio test](@entry_id:136231) for the new series, $\sum b_k x^k$:
$$ \lim_{k \to \infty} \left| \frac{b_{k+1}}{b_k} \right| = \lim_{n \to \infty} \left| \frac{a_n/(n+1)}{a_{n-1}/n} \right| = \left( \lim_{n \to \infty} \left| \frac{a_n}{a_{n-1}} \right| \right) \cdot \left( \lim_{n \to \infty} \frac{n}{n+1} \right) $$
The second limit is 1, so the limit of the ratios is unchanged. This means the radius of convergence, which is the reciprocal of this limit, is also unchanged [@problem_id:2317645] [@problem_id:2317701].

While the **radius of convergence** remains invariant, the **[interval of convergence](@entry_id:146678)** may not. The behavior at the endpoints $x = c \pm R$ can change. Specifically, [term-by-term integration](@entry_id:138696) can cause a series to converge at an endpoint where it previously diverged. Consider the geometric series $\sum_{n=0}^\infty x^n = \frac{1}{1-x}$, which has $R=1$ and diverges at both endpoints $x=1$ and $x=-1$. Integrating this series yields the series for $-\ln(1-x)$, which is $\sum_{n=0}^\infty \frac{x^{n+1}}{n+1}$. This new series still has $R=1$, but it now converges at $x=-1$ (the [alternating harmonic series](@entry_id:140965)) while still diverging at $x=1$ (the harmonic series) [@problem_id:1325316] [@problem_id:2317695].

This phenomenon can be observed systematically. If we integrate again, we obtain the series for the [dilogarithm function](@entry_id:181405), $\text{Li}_2(x) = \sum_{n=1}^\infty \frac{x^n}{n^2}$. At the endpoints, we examine $\sum \frac{1}{n^2}$ and $\sum \frac{(-1)^n}{n^2}$. Both of these series are absolutely convergent (the first by the [p-series test](@entry_id:190675) with $p=2$, the second by comparison with the first). Thus, after two integrations, the original series, which converged on $(-1,1)$, now converges on the closed interval $[-1,1]$ [@problem_id:2317695] [@problem_id:2317692]. This "smoothing" effect of integration, which enhances convergence at the boundaries, is a key feature of the operation.

### Applications in Deriving and Evaluating Series

One of the most significant uses of [term-by-term integration](@entry_id:138696) is to generate power series for new functions from the series of known functions. This technique elegantly connects functions through their calculus relationships.

#### Generating New Series Representations

Many fundamental [power series](@entry_id:146836) can be derived by integrating the geometric series $\sum_{n=0}^{\infty} t^n = \frac{1}{1-t}$, which converges for $|t|<1$.

-   **Logarithmic Functions**: To find the series for $\ln(1-x)$, we note that its derivative is $-\frac{1}{1-x}$. We can integrate the series for the derivative from $0$ to $x$:
    $$ \ln(1-x) = \int_0^x \left( -\frac{1}{1-t} \right) dt = \int_0^x \left( -\sum_{n=0}^{\infty} t^n \right) dt $$
    $$ = -\sum_{n=0}^{\infty} \int_0^x t^n dt = -\sum_{n=0}^{\infty} \frac{x^{n+1}}{n+1} = -\sum_{k=1}^{\infty} \frac{x^k}{k} $$
    The constant of integration is zero because $\ln(1-0)=0$. This classic derivation gives us a powerful tool for working with logarithms [@problem_id:1325316] [@problem_id:1325290].

-   **Inverse Trigonometric Functions**: The series for $\arctan(x)$ can be found similarly. We start with the derivative, $\frac{d}{dx}\arctan(x) = \frac{1}{1+x^2}$. By substituting $-t^2$ for $t$ in the [geometric series formula](@entry_id:159114), we get:
    $$ \frac{1}{1+t^2} = \sum_{n=0}^{\infty} (-t^2)^n = \sum_{n=0}^{\infty} (-1)^n t^{2n} $$
    Integrating this from $0$ to $x$ yields the celebrated series for the arctangent function [@problem_id:1325280]:
    $$ \arctan(x) = \int_0^x \left( \sum_{n=0}^{\infty} (-1)^n t^{2n} \right) dt = \sum_{n=0}^{\infty} (-1)^n \frac{x^{2n+1}}{2n+1} $$

-   **Trigonometric and Hyperbolic Functions**: The deep connection between trigonometric and hyperbolic functions is beautifully reflected in their [power series](@entry_id:146836). Integrating the series for $\cos(t) = \sum_{n=0}^\infty \frac{(-1)^n t^{2n}}{(2n)!}$ term-by-term from $0$ to $x$ gives:
    $$ \int_0^x \cos(t) dt = \sum_{n=0}^{\infty} \frac{(-1)^n}{(2n)!} \int_0^x t^{2n} dt = \sum_{n=0}^{\infty} \frac{(-1)^n x^{2n+1}}{(2n+1)!} $$
    This resulting series is precisely the Maclaurin series for $\sin(x)$, confirming that $\int \cos(x) dx = \sin(x) + C$ [@problem_id:2317647]. An identical procedure shows that integrating the series for $\cosh(x)$ produces the series for $\sinh(x)$ [@problem_id:1325313].

#### Evaluating Integrals and Sums

The method can also be applied to evaluate [definite integrals](@entry_id:147612) that are difficult to compute with standard techniques or to find the exact sum of certain numerical series.

For example, to find the value of the [definite integral](@entry_id:142493) $I(x) = \int_0^x t \cos(t) dt$, we can first write the series for the integrand $t \cos(t)$ and then integrate.
$$ t \cos(t) = t \sum_{n=0}^{\infty} \frac{(-1)^n t^{2n}}{(2n)!} = \sum_{n=0}^{\infty} \frac{(-1)^n t^{2n+1}}{(2n)!} $$
Integrating term-by-term gives a series for $I(x)$, which can then, with some algebraic manipulation, be recognized as the series for $x\sin(x) + \cos(x) - 1$ [@problem_id:1325289].

Conversely, a numerical series can sometimes be recognized as a specific value of a [power series](@entry_id:146836) obtained through integration. To calculate the sum $S = \sum_{k=1}^{\infty} \frac{1}{k \cdot 2^k}$, we can write it as $\sum_{k=1}^{\infty} \frac{(1/2)^k}{k}$. This perfectly matches the series we derived for $-\ln(1-x)$, evaluated at $x = 1/2$. Therefore, the sum is $-\ln(1-1/2) = -\ln(1/2) = \ln(2)$ [@problem_id:2317624].

### Convergence at the Boundary and Abel's Theorem

Some of the most elegant results in analysis arise from evaluating these series at the endpoints of their [interval of convergence](@entry_id:146678). This step is not trivial and requires justification, which is provided by **Abel's Theorem**.

**Abel's Theorem (simplified):** If a power series converges at an endpoint of its [interval of convergence](@entry_id:146678), say at $x=R$, then the value of the series at that point is equal to the limit of the function represented by the series as $x$ approaches $R$ from within the interval.
$$ \text{If } \sum_{n=0}^\infty a_n R^n \text{ converges, then } \sum_{n=0}^\infty a_n R^n = \lim_{x \to R^-} f(x) $$

This theorem allows us to equate the sum of a numerical series with the value of a known continuous function, opening the door to remarkable calculations.

-   **The Leibniz Formula for $\pi$**: The series for $\arctan(x)$ is $\sum_{n=0}^{\infty} (-1)^n \frac{x^{2n+1}}{2n+1}$. At $x=1$, this becomes the series $1 - \frac{1}{3} + \frac{1}{5} - \dots$. This series converges by the Alternating Series Test. By Abel's Theorem, its sum is equal to $\lim_{x \to 1^-} \arctan(x) = \arctan(1) = \frac{\pi}{4}$. This provides a stunning connection between an [infinite series](@entry_id:143366) of rational numbers and the constant $\pi$ [@problem_id:1325309].

-   **The Alternating Harmonic Series**: The series for $\ln(1+x)$ is $\sum_{n=1}^\infty (-1)^{n-1} \frac{x^n}{n}$. At $x=1$, this gives the [alternating harmonic series](@entry_id:140965) $1 - \frac{1}{2} + \frac{1}{3} - \dots$. This series converges, and by Abel's theorem, its sum is $\ln(1+1) = \ln(2)$ [@problem_id:1325303].

This principle can be used to find exact values for [definite integrals](@entry_id:147612) up to the boundary. For example, the value of $\int_0^1 \arctan(t) dt$ can be found by integrating the series for $\arctan(t)$ and evaluating the resulting series at $x=1$. Using Abel's theorem, this sum is equal to the value of the integral, which can be computed via integration by parts to be $\frac{\pi}{4} - \frac{1}{2}\ln(2)$ [@problem_id:1325283].

### Advanced Perspectives

The principle of [term-by-term integration](@entry_id:138696) is a gateway to more advanced mathematical concepts.

-   **Special Functions**: Many special functions in mathematics and physics are defined by integrals that are not expressible in terms of [elementary functions](@entry_id:181530). Power series provide a crucial method for computing and analyzing them. For example, the Beta function, $B(x,y) = \int_0^1 t^{x-1}(1-t)^{y-1} dt$, can be represented as an infinite series by expanding the $(1-t)^{y-1}$ term using the [generalized binomial theorem](@entry_id:262225) and integrating term by term. This requires careful justification, but it yields a computable [series representation](@entry_id:175860) for the function for given $x > 0$ and $y > 0$ [@problem_id:2317681].

-   **Integral Representations and Generating Functions**: The process can be reversed. Sometimes, a difficult coefficient in a series can be re-written as an integral, which facilitates summation. The expression $\frac{1}{n+2}$ can be written as $\int_0^1 t^{n+1} dt$. Substituting this into a series allows one to interchange summation and integration, turning a sum over discrete indices into a more tractable integral of a continuous function [@problem_id:2317672]. This is a fundamental idea behind the theory of [generating functions](@entry_id:146702) and [integral transforms](@entry_id:186209).

-   **Connection to Taylor Coefficients**: The relationship between the series for a function $F(x)$ and its derivative $F'(x)$ provides a powerful link between their Taylor coefficients. If $F(x) = \sum a_n x^n$ and $F'(x) = \sum c_n x^n$, we know that $a_{n+1} = \frac{c_n}{n+1}$. Since the coefficients are related to derivatives at the origin by $a_n = \frac{F^{(n)}(0)}{n!}$, this method becomes a tool for calculating [higher-order derivatives](@entry_id:140882) of functions defined by integrals, sometimes in cases where direct differentiation would be prohibitively complex [@problem_id:2317655].

In summary, [term-by-term integration](@entry_id:138696) is not merely a computational shortcut; it is a deep structural property of [analytic functions](@entry_id:139584) that reveals the intricate connections between algebra, calculus, and the infinite. Its mastery provides access to a vast landscape of mathematical analysis and its applications.