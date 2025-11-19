## Introduction
Power series are a cornerstone of real analysis, offering a powerful way to represent complex functions as infinite polynomials. This representation bridges the worlds of discrete algebra and continuous calculus, but it also raises a fundamental question: can we manipulate these infinite sums with the same freedom as their finite counterparts? Specifically, can we interchange the operations of integration and infinite summation? The ability to integrate a [power series](@entry_id:146836) term by term is not a given, yet its validation unlocks a remarkably effective toolkit for solving problems that are otherwise intractable.

This article delves into the theory and application of [term-by-term integration](@entry_id:138696). It addresses the conditions under which this operation is valid and demonstrates its profound utility. Over the next three chapters, you will gain a comprehensive understanding of this essential technique. The journey begins in **Principles and Mechanisms**, where we will establish the fundamental theorem of [term-by-term integration](@entry_id:138696) and explore its theoretical underpinnings, such as [uniform convergence](@entry_id:146084) and the invariance of the [radius of convergence](@entry_id:143138). Next, **Applications and Interdisciplinary Connections** will showcase how this method is used to derive new series, evaluate [complex integrals](@entry_id:202758), solve differential equations, and connect analysis to fields like physics and statistics. Finally, **Hands-On Practices** will provide you with the opportunity to solidify your understanding by working through targeted problems.

## Principles and Mechanisms

Power series provide a remarkably powerful framework for representing functions, bridging the gap between discrete algebra and continuous analysis. Once a function is expressed as a power series, we can often manipulate it with the same ease as a polynomial. One of the most significant analytic operations we can perform is integration. This chapter will establish the foundational theorem for term-by-term [integration of [power serie](@entry_id:200139)s](@entry_id:146836), explore its theoretical underpinnings, and demonstrate its utility in deriving new series representations and evaluating complex [definite integrals](@entry_id:147612).

### The Fundamental Theorem of Term-by-Term Integration

The ability to interchange the operations of infinite summation and integration is not universally granted for all [series of functions](@entry_id:139536). However, [power series](@entry_id:146836) exhibit exceptional regularity within their [domain of convergence](@entry_id:165028), which permits this interchange. This leads to a central theorem that is both elegant in its formulation and profound in its consequences.

**Theorem:** Suppose a function $f(x)$ is represented by a [power series](@entry_id:146836) centered at $x=c$ with a [radius of convergence](@entry_id:143138) $R > 0$:
$$ f(x) = \sum_{n=0}^{\infty} a_n (x-c)^n $$
Then, for any $x$ within the [interval of convergence](@entry_id:146678) $(c-R, c+R)$, an [antiderivative](@entry_id:140521) of $f(x)$ can be found by integrating the [power series](@entry_id:146836) term-by-term:
$$ \int f(x) \,dx = C + \sum_{n=0}^{\infty} a_n \frac{(x-c)^{n+1}}{n+1} $$
where $C$ is the constant of integration. Furthermore, the resulting power series has the same [radius of convergence](@entry_id:143138), $R$.

For simplicity, let us consider a [power series](@entry_id:146836) centered at $x=0$, given by $f(x) = \sum_{n=0}^{\infty} a_n x^n$. According to the theorem, its antiderivative, $F(x)$, where $F'(x) = f(x)$, is represented by the series:
$$ F(x) = C + \sum_{n=0}^{\infty} \frac{a_n}{n+1} x^{n+1} = C + a_0 x + \frac{a_1}{2}x^2 + \frac{a_2}{3}x^3 + \dots $$
This formula provides a direct method for determining the coefficients of the integrated series from the coefficients of the original series [@problem_id:1325332].

### The Invariance of the Radius of Convergence

A critical and perhaps surprising aspect of the theorem is that [term-by-term integration](@entry_id:138696) does not alter the [radius of convergence](@entry_id:143138). While this may seem counter-intuitive at first, it underscores the robust nature of power [series convergence](@entry_id:142638). Integration is fundamentally a "smoothing" operation, and it stands to reason that it would preserve, rather than degrade, the convergence properties of the series.

We can establish this fact more rigorously. Let the radius of the original series $\sum a_n x^n$ be $R_f$. The integrated series is $\sum_{n=0}^{\infty} \frac{a_n}{n+1} x^{n+1}$, and its [radius of convergence](@entry_id:143138) $R_F$ is determined by its coefficients $b_{n+1} = a_n/(n+1)$. Using the Cauchy-Hadamard formula, we find that the reciprocal of the radius is given by:
$$ \frac{1}{R_F} = \limsup_{n \to \infty} \left| \frac{a_n}{n+1} \right|^{1/(n+1)} $$
It is a standard result from analysis that $\lim_{k \to \infty} k^{1/k} = 1$. This implies that the [asymptotic behavior](@entry_id:160836) is governed solely by the original coefficients $a_n$. Formally, one can show that $\limsup_{n \to \infty} |a_n/(n+1)|^{1/(n+1)} = \limsup_{n \to \infty} |a_n|^{1/n}$. Therefore, the radii of convergence are identical: $R_F = R_f$.

This principle holds even when dealing with sums of series. For instance, if we have two functions $f(x)$ and $g(x)$ with radii of convergence $R_f$ and $R_g$ respectively, the [radius of convergence](@entry_id:143138) for their sum, $h(x) = f(x) + g(x)$, is at least $\min(R_f, R_g)$. If $R_f \neq R_g$, the radius is exactly $\min(R_f, R_g)$. Since integrating $h(x)$ does not change its radius of convergence, the series for $H(x) = \int_0^x h(t) dt$ will also have a radius of convergence of $\min(R_f, R_g)$ [@problem_id:2317645].

As a concrete example, consider the function $f(x) = \sum_{n=0}^{\infty} (n+1) (5x)^n$. Its coefficients are $a_n = (n+1)5^n$. The [radius of convergence](@entry_id:143138) $R_f$ is $1/\lim_{n\to\infty} |(n+1)5^n|^{1/n} = 1/5$. The series for its antiderivative, $g(x)$, can be found by [term-by-term integration](@entry_id:138696). This yields the series $\sum_{n=0}^\infty 5^n x^{n+1}$ (plus a constant of integration). The radius of convergence $R_g$ for this series, which can be written as $x\sum_{n=0}^\infty (5x)^n$, is also easily calculated as $1/5$. This directly confirms that $R_f = R_g$, as predicted by the theorem [@problem_id:2317701].

### Applications in Analysis

The power of [term-by-term integration](@entry_id:138696) lies in its wide-ranging applications, from constructing series representations of functions to evaluating seemingly intractable integrals.

#### Finding Antiderivatives and Solving Initial Value Problems

A direct application of the theorem is to determine the [power series](@entry_id:146836) for a function $g(x)$ when the series for its derivative, $g'(x)$, is known. If we are also given an initial condition, such as the value of $g(0)$, we can determine the constant of integration and find the unique power series for $g(x)$.

For example, suppose the derivative of a function is given by $g'(x) = \sum_{n=1}^{\infty} \frac{n}{4^n} x^{n-1}$, and we know that $g(0) = 5$. We can find the series for $g(x)$ by integrating the series for $g'(x)$ term by term:
$$ g(x) = \int \left( \sum_{n=1}^{\infty} \frac{n}{4^n} x^{n-1} \right) dx = C + \sum_{n=1}^{\infty} \frac{n}{4^n} \frac{x^n}{n} = C + \sum_{n=1}^{\infty} \frac{x^n}{4^n} $$
Using the initial condition $g(0)=5$, we find that $C=5$. Thus, the power [series representation](@entry_id:175860) for $g(x)$ is:
$$ g(x) = 5 + \sum_{n=1}^{\infty} \left(\frac{x}{4}\right)^n $$
This demonstrates how an [initial value problem](@entry_id:142753) can be solved within the framework of [power series](@entry_id:146836) [@problem_id:1325307].

#### Deriving New Series and Evaluating Integrals

One of the most elegant applications of [term-by-term integration](@entry_id:138696) is the derivation of new power series from known ones. A canonical example is the Maclaurin series for the arctangent function. We begin with the well-known geometric series:
$$ \frac{1}{1-u} = \sum_{n=0}^{\infty} u^n, \quad |u|  1 $$
By substituting $u = -t^2$, we obtain the series for the derivative of $\arctan(t)$:
$$ \frac{d}{dt} \arctan(t) = \frac{1}{1+t^2} = \sum_{n=0}^{\infty} (-t^2)^n = \sum_{n=0}^{\infty} (-1)^n t^{2n}, \quad |t|  1 $$
Integrating both sides from $0$ to $x$ (with $|x|1$) and using $\arctan(0)=0$, we can swap the integral and summation:
$$ \arctan(x) = \int_0^x \frac{1}{1+t^2} dt = \sum_{n=0}^{\infty} (-1)^n \int_0^x t^{2n} dt = \sum_{n=0}^{\infty} \frac{(-1)^n}{2n+1} x^{2n+1} $$
This powerful technique allows us to generate a [series representation](@entry_id:175860) for a [transcendental function](@entry_id:271750) starting from a simple algebraic one.

This new series can, in turn, be used to evaluate [definite integrals](@entry_id:147612) that are difficult to compute by other means. Consider the integral $I = \int_0^{1/2} \frac{\arctan(x)}{x} dx$. A closed-form antiderivative for the integrand is not elementary. However, we can represent the integrand as a [power series](@entry_id:146836):
$$ \frac{\arctan(x)}{x} = \frac{1}{x} \sum_{n=0}^{\infty} \frac{(-1)^n}{2n+1} x^{2n+1} = \sum_{n=0}^{\infty} \frac{(-1)^n}{2n+1} x^{2n} $$
Since the interval $[0, 1/2]$ is well within the [interval of convergence](@entry_id:146678) $(-1,1)$, we can integrate term-by-term:
$$ I = \int_0^{1/2} \left( \sum_{n=0}^{\infty} \frac{(-1)^n}{2n+1} x^{2n} \right) dx = \sum_{n=0}^{\infty} \frac{(-1)^n}{2n+1} \left[ \frac{x^{2n+1}}{2n+1} \right]_0^{1/2} = \sum_{n=0}^{\infty} \frac{(-1)^n}{(2n+1)^2} \left(\frac{1}{2}\right)^{2n+1} $$
This transforms the problem of evaluating an integral into the problem of summing a rapidly converging [alternating series](@entry_id:143758), which is highly effective for numerical approximation [@problem_id:1342727].

Sometimes, integrating a series term-by-term leads to a new series that can be recognized and summed to a closed form. For instance, to evaluate $\int_0^x t \cos(t) dt$, we can start with the series for $\cos(t)$, multiply by $t$, and integrate term-by-term. The resulting series can be ingeniously decomposed into the known series for $x\sin(x)$ and $\cos(x)-1$, yielding the closed-form result $x\sin(x) + \cos(x) - 1$ [@problem_id:1325289]. This highlights the deep interplay between series manipulation and closed-form identities.

### Theoretical Justification and Endpoint Behavior

#### Uniform Convergence as the Foundation

The theoretical cornerstone that permits the interchange of integration and infinite summation for [power series](@entry_id:146836) is **[uniform convergence](@entry_id:146084)**. A power series $\sum a_n (x-c)^n$ with radius of convergence $R  0$ converges uniformly on any [closed and bounded interval](@entry_id:136474) $[a, b]$ contained strictly within its [interval of convergence](@entry_id:146678) $(c-R, c+R)$. It is a fundamental theorem of [real analysis](@entry_id:145919) that if a sequence of functions converges uniformly, the limit of the integrals is the integral of the limit. This theorem extends to [series of functions](@entry_id:139536) and provides the rigorous justification for the [term-by-term integration](@entry_id:138696) we have been using.

For scenarios where [uniform convergence](@entry_id:146084) is not immediately applicable or for a more fundamental justification, one might turn to the more powerful theorems of [measure theory](@entry_id:139744). For example, by applying the **Monotone Convergence Theorem** or the **Dominated Convergence Theorem**, one can justify [term-by-term integration](@entry_id:138696) even over an open interval where uniform convergence arguments are more subtle. This illustrates that the validity of [term-by-term integration](@entry_id:138696) is a very deep and robust property.

#### Convergence at the Endpoints: Abel's Theorem

Our discussion has so far focused on the open [interval of convergence](@entry_id:146678). The behavior of a [power series](@entry_id:146836) at the endpoints $x = c \pm R$ is more delicate and must be analyzed on a case-by-case basis. A series may converge at both, one, or neither endpoint. Integration can improve convergence at the endpoints, but a careful check is always required.

A pivotal result for understanding endpoint behavior is **Abel's Theorem**. It states that if a power series converges at an endpoint of its [interval of convergence](@entry_id:146678), then the function represented by the series is continuous at that endpoint. This means the value of the series at the endpoint is simply the limit of the function as $x$ approaches that endpoint.

Consider the function $F(x) = \int_0^x \arctan(t) dt$. We previously derived the Maclaurin series for $\arctan(t)$, which is known to converge for $t \in [-1, 1]$. By integrating, we find the series for $F(x)$:
$$ F(x) = \sum_{n=0}^{\infty} \frac{(-1)^n}{(2n+1)(2n+2)} x^{2n+2} $$
The [interval of convergence](@entry_id:146678) is $[-1, 1]$. At the endpoint $x=1$, the series becomes $\sum \frac{(-1)^n}{(2n+1)(2n+2)}$, which converges by the Alternating Series Test. By Abel's Theorem, the sum of this series is equal to $F(1) = \int_0^1 \arctan(t) dt$. This integral can be evaluated using [integration by parts](@entry_id:136350) to be $\frac{\pi}{4} - \frac{1}{2}\ln(2)$. Thus, we have found the exact sum of a non-trivial [alternating series](@entry_id:143758) by relating it back to a [definite integral](@entry_id:142493) [@problem_id:1325283].

The variety of endpoint behaviors is vast. The series for $-\ln(1-x) = \sum_{n=1}^\infty \frac{x^n}{n}$ has an [interval of convergence](@entry_id:146678) of $[-1, 1)$. It diverges at $x=1$ (the harmonic series) but converges conditionally at $x=-1$ (the [alternating harmonic series](@entry_id:140965)). In contrast, the series for the [dilogarithm function](@entry_id:181405), $\text{Li}_2(x) = \sum_{n=1}^\infty \frac{x^n}{n^2}$, converges absolutely at both endpoints $x=1$ and $x=-1$, as the series of [absolute values](@entry_id:197463) is a convergent [p-series](@entry_id:139707) ($\sum 1/n^2$) [@problem_id:2317695]. These examples serve as a crucial reminder that while the interior of the [interval of convergence](@entry_id:146678) is a domain of predictable, "polynomial-like" behavior, the boundaries demand individual and careful examination.