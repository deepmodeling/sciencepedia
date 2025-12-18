## Introduction
In the quantitative sciences, we often need to calculate [definite integrals](@entry_id:147612) for which no simple analytical solution exists. While basic methods like the [trapezoidal rule](@entry_id:145375) offer an approximation, their reliance on linear segments can be inefficient for functions with significant curvature. This article introduces Simpson's rule, a far more powerful and accurate [numerical integration](@entry_id:142553) technique that approximates functions using parabolas. By mastering this method, you gain a foundational tool for solving complex problems across finance, economics, and beyond.

This exploration is structured to build your expertise systematically. First, under "Principles and Mechanisms," we will delve into the mathematical theory behind the rule, analyze its high [order of accuracy](@entry_id:145189), and identify its limitations. Next, "Applications and Interdisciplinary Connections" will demonstrate its practical power in valuing assets, measuring inequality, and pricing derivatives. Finally, "Hands-On Practices" will allow you to apply this knowledge to solve realistic quantitative problems, cementing your understanding.

## Principles and Mechanisms

In the preceding chapter, we introduced the fundamental challenge of [numerical integration](@entry_id:142553): approximating the value of a [definite integral](@entry_id:142493) when an analytical solution is unavailable or impractical. We saw that the simplest methods, such as the [trapezoidal rule](@entry_id:145375), approximate the integrand with a straight line over each subinterval. While intuitive, this approach can require a very large number of subintervals to achieve high accuracy for functions with significant curvature. This chapter delves into a more sophisticated and powerful family of techniques known as Simpson's rule, which achieves higher accuracy by using quadratic and cubic approximations. We will explore the theoretical underpinnings of this method, analyze its sources of accuracy, investigate its limitations, and situate it within the broader landscape of [numerical integration](@entry_id:142553) techniques.

### The Foundation: Approximating with Parabolas

The core idea behind **Simpson's rule** is to improve upon the linear approximations of the [trapezoidal rule](@entry_id:145375) by using higher-degree polynomials. Instead of connecting two points with a line, we can define a curve more precisely by using three points. The simplest non-linear curve that can pass through any three points is a parabola, a polynomial of degree two.

Consider the integral $\int_a^b f(x) \, dx$. Let's take the simplest possible partition of this interval that involves three points: the endpoints $a$ and $b$, and the midpoint $m = (a+b)/2$. Let the step size be $h = (b-a)/2$. The three points are then $x_0 = a$, $x_1 = a+h$, and $x_2 = a+2h=b$. We can find the unique quadratic polynomial, $P_2(x)$, that passes through the points $(x_0, f(x_0))$, $(x_1, f(x_1))$, and $(x_2, f(x_2))$. By integrating this polynomial from $a$ to $b$, we can derive an approximation for the integral of $f(x)$:

$$
\int_a^b f(x) \, dx \approx \int_a^b P_2(x) \, dx = \frac{h}{3} [f(x_0) + 4f(x_1) + f(x_2)]
$$

This celebrated result is known as **Simpson's 1/3 rule**. The name "1/3" comes from the factor of $h/3$ in the formula. The weights applied to the function values at the left endpoint, midpoint, and right endpoint are $\frac{h}{3}$, $\frac{4h}{3}$, and $\frac{h}{3}$, respectively. Intuitively, the midpoint is given four times the weight of the endpoints, reflecting its central importance in defining the curvature of the approximating parabola.

A remarkable property of Simpson's 1/3 rule is that it is exact not only for quadratic polynomials (as expected by its construction) but also for any cubic polynomial. The symmetric nature of the approximation causes the error term associated with the cubic part of the function's local expansion to integrate to zero, providing a "free" order of accuracy.

### The Composite Simpson's Rule

The basic three-point rule is useful for a single parabolic segment, but to integrate a function over a larger domain with high accuracy, we must generalize it. The **composite Simpson's 1/3 rule** achieves this by dividing the integration interval $[a, b]$ into an even number of subintervals, $n$, of equal width $h = (b-a)/n$. This partition creates $n+1$ grid points $x_i = a + ih$ for $i = 0, 1, \dots, n$.

The rule then applies the basic three-point formula repeatedly to successive pairs of subintervals. The first application covers $[x_0, x_2]$, the next covers $[x_2, x_4]$, and so on, until the final pair $[x_{n-2}, x_n]$. Summing these individual approximations gives the composite formula:

$$
\int_a^b f(x) \, dx \approx \frac{h}{3} [f(x_0) + 4f(x_1) + 2f(x_2) + 4f(x_3) + \dots + 2f(x_{n-2}) + 4f(x_{n-1}) + f(x_n)]
$$

Notice the characteristic pattern of weights: the first and last points have a weight of $1$; the interior points with odd indices (the midpoints of each parabolic segment) have a weight of $4$; and the interior points with even indices (which are shared endpoints of adjacent parabolic segments) have a weight of $2$.

A practical application demonstrates the method's utility. Consider numerically verifying the Fundamental Theorem of Calculus for a function whose [antiderivative](@entry_id:140521) is non-elementary, such as the Gaussian function $f(x) = \exp(-x^2)$. The definite integral $\int_a^b \exp(-x^2) \, dx$ can be calculated exactly using the special error function, $\text{erf}(x)$. An implementation of the composite Simpson's rule allows us to approximate this integral and compare it to the exact value. For instance, to compute $\int_0^1 \exp(-x^2) \, dx$ using $n=100$ subintervals, we would apply the formula above. This approach proves robust even for unconventional intervals, such as one with reversed limits (e.g., from $1$ to $-1$), where the negative step size $h$ correctly computes the negative of the forward integral .

### The Source of Accuracy: Error Analysis

Why is Simpson's rule so much more accurate than the trapezoidal rule? For a smooth function, the global error of the [composite trapezoidal rule](@entry_id:143582) decreases in proportion to $h^2$, written as $\mathcal{O}(h^2)$. In contrast, the [global error](@entry_id:147874) of the composite Simpson's rule is $\mathcal{O}(h^4)$. This means that halving the step size $h$ reduces the error of the trapezoidal rule by a factor of 4, but for Simpson's rule, it reduces the error by a factor of 16. This dramatic improvement stems from a profound [error cancellation](@entry_id:749073) mechanism, which can be understood from two perspectives.

#### The Taylor Series Perspective

Let's analyze the [local error](@entry_id:635842) over a single panel of two subintervals, from $x-h$ to $x+h$, centered at a point $x$. We can express the function $f$ using a Taylor series expansion around $x$:

$$
f(x+t) = f(x) + t f'(x) + \frac{t^2}{2} f''(x) + \frac{t^3}{6} f'''(x) + \frac{t^4}{24} f^{(4)}(x) + \mathcal{O}(t^5)
$$

The exact integral over $[x-h, x+h]$ is found by integrating this series term by term. Due to the symmetric interval, all odd powers of $t$ integrate to zero:

$$
\int_{x-h}^{x+h} f(t) \, dt = 2h f(x) + \frac{h^3}{3} f''(x) + \frac{h^5}{60} f^{(4)}(x) + \mathcal{O}(h^7)
$$

Now, let's compute the Simpson's rule approximation on this same panel: $S = \frac{h}{3}[f(x-h) + 4f(x) + f(x+h)]$. Substituting the Taylor expansions for $f(x-h)$ and $f(x+h)$:

$$
S = \frac{h}{3} \left[ \left( f(x) - hf'(x) + \frac{h^2}{2}f''(x) - \frac{h^3}{6}f'''(x) + \frac{h^4}{24}f^{(4)}(x) \right) + 4f(x) + \left( f(x) + hf'(x) + \frac{h^2}{2}f''(x) + \frac{h^3}{6}f'''(x) + \frac{h^4}{24}f^{(4)}(x) \right) \right] + \mathcal{O}(h^7)
$$

Inside the brackets, the terms involving the first and third derivatives ($f'(x)$ and $f'''(x)$) cancel out perfectly. Collecting the remaining terms, we find:

$$
S = \frac{h}{3} \left[ 6f(x) + h^2 f''(x) + \frac{h^4}{12} f^{(4)}(x) \right] + \mathcal{O}(h^7) = 2h f(x) + \frac{h^3}{3} f''(x) + \frac{h^5}{36} f^{(4)}(x) + \mathcal{O}(h^7)
$$

The local error is the difference between the exact integral and the approximation. Notice that the first two terms match exactly! The leading error term is:

$$
\text{Error}_{\text{local}} = \left(\frac{h^5}{60} - \frac{h^5}{36}\right) f^{(4)}(x) + \mathcal{O}(h^7) = -\frac{h^5}{90} f^{(4)}(x) + \mathcal{O}(h^7)
$$

This is the key insight from : the symmetric $1,4,1$ weighting scheme is specifically designed to cancel not just the linear term's error (like the trapezoidal rule) but also the cubic term's error. The [local error](@entry_id:635842) is of order $\mathcal{O}(h^5)$. When we sum the errors from all $N/2 = \mathcal{O}(1/h)$ panels across the entire integration domain, the global error becomes $\mathcal{O}(h^4)$.

#### The Richardson Extrapolation Perspective

A second, equally powerful way to understand Simpson's rule is to view it as an instance of **Richardson [extrapolation](@entry_id:175955)**. This is a general technique for combining two lower-order estimates to produce a higher-order estimate.

Let $I$ be the true value of the integral, and let $T(h)$ be the approximation from the [composite trapezoidal rule](@entry_id:143582) with step size $h$. For a [smooth function](@entry_id:158037), the error of the [trapezoidal rule](@entry_id:145375) has a regular structure: $I - T(h) = c_2 h^2 + c_4 h^4 + \dots$.

Now, consider applying the trapezoidal rule with half the step size, $h/2$. The approximation is $T(h/2)$, and its error is $I - T(h/2) = c_2 (h/2)^2 + c_4 (h/2)^4 + \dots = \frac{c_2}{4} h^2 + \frac{c_4}{16} h^4 + \dots$.

We have two equations and can eliminate the leading error term, which is of order $\mathcal{O}(h^2)$. Multiplying the second equation by 4 and subtracting the first gives:

$$
4(I - T(h/2)) - (I - T(h)) = (c_2 h^2 + \frac{c_4}{4} h^4) - (c_2 h^2 + c_4 h^4) + \mathcal{O}(h^6)
$$

$$
3I - 4T(h/2) + T(h) = -\frac{3c_4}{4}h^4 + \mathcal{O}(h^6)
$$

Solving for $I$ yields a new, more accurate approximation:

$$
I \approx \frac{4T(h/2) - T(h)}{3}
$$

The error of this new approximation is $\mathcal{O}(h^4)$. Astonishingly, if one works through the algebra, this [linear combination](@entry_id:155091) of two trapezoidal approximations is identical to the composite Simpson's rule with step size $h/2$. Thus, Simpson's rule is not an arbitrary construction; it is the direct result of applying Richardson [extrapolation](@entry_id:175955) to the [trapezoidal rule](@entry_id:145375), systematically eliminating the leading source of error .

### Variations and Extensions

#### Simpson's 3/8 Rule

The 1/3 rule is based on fitting a quadratic polynomial through three points. We can extend this idea by fitting a cubic polynomial through four points. Integrating this cubic yields **Simpson's 3/8 rule**, which is applied over a panel of three subintervals. The basic formula is:

$$
\int_{x_0}^{x_3} f(x) \, dx \approx \frac{3h}{8} [f(x_0) + 3f(x_1) + 3f(x_2) + f(x_3)]
$$

For a composite version, the total number of subintervals $n$ must be a multiple of 3. Both the 1/3 rule and the 3/8 rule have a global error of order $\mathcal{O}(h^4)$. However, their error constants are different. For the 1/3 rule, the leading error term is proportional to $-\frac{h^4}{180}f^{(4)}(\xi)$, while for the 3/8 rule, it is proportional to $-\frac{h^4}{80}f^{(4)}(\xi)$. The 1/3 rule has a smaller error constant and is generally preferred for its simplicity and slightly higher accuracy. Nonetheless, in specific applications like pricing [financial derivatives](@entry_id:637037), both methods can be used and compared. For the same number of function evaluations on a grid where $n$ is a multiple of 6 (allowing both rules to be applied), one might observe that one rule slightly outperforms the other depending on the specific integrand .

#### Handling Non-Uniform Grids

A significant limitation of the standard composite formulas is their reliance on a uniformly spaced grid. In many applications, from finance to experimental science, data may be available only at irregular intervals. However, the fundamental principle of Simpson's rule—integrating a local [interpolating polynomial](@entry_id:750764)—can be adapted.

Given three consecutive points $(t_i, f(t_i))$, $(t_{i+1}, f(t_{i+1}))$, and $(t_{i+2}, f(t_{i+2}))$ that are not evenly spaced, one can still construct the unique quadratic polynomial passing through them (for instance, using Lagrange basis polynomials) and integrate it exactly from $t_i$ to $t_{i+2}$. The resulting formula will be a weighted sum $w_i f(t_i) + w_{i+1} f(t_{i+1}) + w_{i+2} f(t_{i+2})$, where the weights $w_k$ now depend on the specific spacing between the points. For example, in valuing a project with irregular cash flows, we can apply this generalized three-point rule to successive triplets of data points. If an even number of points leaves a final interval with only two points, we can simply fall back to the trapezoidal rule for that last segment. This hybrid approach provides a robust method for integrating non-uniformly sampled data .

### Limitations and Pathologies: When Simpson's Rule Struggles

The $\mathcal{O}(h^4)$ convergence of Simpson's rule is predicated on a critical assumption: that the integrand is sufficiently smooth (specifically, four times continuously differentiable, or $C^4$). When this condition is violated, the method's performance can degrade dramatically. Understanding these failure modes is as important as knowing the rule itself.

#### Non-Smooth Integrands

In [computational finance](@entry_id:145856), many integrands are not smooth. For example, the payoff of a standard call or put option, $(S_T - K)^+$ or $(K - S_T)^+$, has a "kink" at the strike price $K$.

*   **Kinks:** Consider an integrand like $f(x) = |x-K|w(x)$, where $w(x)$ is a [smooth function](@entry_id:158037). The first derivative of $f(x)$ has a [jump discontinuity](@entry_id:139886) at $x=K$. This violation of the smoothness requirement breaks the [error cancellation](@entry_id:749073) mechanism. The dominant error now comes from the single panel containing the kink, and the [global convergence](@entry_id:635436) rate drops from $\mathcal{O}(h^4)$ to $\mathcal{O}(h^2)$—the same as the much simpler trapezoidal rule . The standard, robust solution to this problem is to **split the integral at the point of non-smoothness**:
    $$
    \int_a^b f(x) \, dx = \int_a^K f(x) \, dx + \int_K^b f(x) \, dx
    $$
    By applying Simpson's rule to each sub-integral separately, we ensure that the integrand is smooth over each domain of integration, and the desired $\mathcal{O}(h^4)$ convergence is restored.

*   **Jumps:** A more severe violation is a [jump discontinuity](@entry_id:139886), as seen in the payoff of a digital option, which is an indicator function $\mathbf{1}_{\{s \ge K\}}$. When integrating a function like $g(s) = \mathbf{1}_{\{s \ge K\}} p(s)$, where $p(s)$ is a smooth probability density, the integrand itself has a jump at $s=K$. Without any special treatment, the error from the single interval containing the jump dominates, and the [global error](@entry_id:147874) degrades even further to $\mathcal{O}(h)$. Again, splitting the integral at the discontinuity is the correct remedy to recover the higher-order accuracy of the underlying [quadrature rule](@entry_id:175061) .

#### Singular Integrands (Improper Integrals)

Another common challenge arises when the integrand has a vertical asymptote at one of the endpoints, for instance, in computing the [improper integral](@entry_id:140191) $\int_0^1 \frac{1}{\sqrt{1-t}} dt$. The standard composite Simpson's rule (and [trapezoidal rule](@entry_id:145375)) cannot be applied directly because they require evaluating the function at the endpoint $t=1$, where it is infinite . Attempting to do so would halt the computation. There are two primary strategies for handling such [integrable singularities](@entry_id:634345):

1.  **Change of Variables:** A powerful technique is to use a variable substitution that removes the singularity. For the integral above, the substitution $t = 1 - y^2$ transforms the integral into $\int_0^1 2 \, dy$, which is trivial to evaluate. Simpson's rule would, in fact, compute it exactly.
2.  **Specialized Quadrature or Truncation:** One can use "open" [quadrature rules](@entry_id:753909) that do not evaluate the function at the endpoints. Alternatively, one can treat the integral by its definition, $\lim_{\varepsilon \to 0^+} \int_0^{1-\varepsilon} f(t) \, dt$, and apply Simpson's rule on the truncated interval $[0, 1-\varepsilon]$, though this can be numerically delicate.

#### A Counter-intuitive Case: Periodic Functions

While Simpson's rule is generally superior to the [trapezoidal rule](@entry_id:145375), there is a notable exception: integrating a smooth, periodic function over one full period. In this specific scenario, the [composite trapezoidal rule](@entry_id:143582) exhibits "super-convergence," meaning its error converges to zero faster than any power of $h$. Simpson's rule, surprisingly, does not share this property and can be less accurate.

This phenomenon can be understood through the Richardson [extrapolation](@entry_id:175955) lens. The exceptional accuracy of the [trapezoidal rule](@entry_id:145375) for periodic functions means its error $I-T(h)$ is extremely small. However, the term $T(h/2)$ might not be as accurate if the new grid points happen to alias a high-frequency component of the function. The formula $S(h) = (4T(h/2) - T(h))/3$ can then combine a very inaccurate $T(h/2)$ with a very accurate $T(h)$, resulting in an approximation $S(h)$ that is less accurate than $T(h)$ alone . This serves as a valuable reminder that there are no universally "best" methods; the choice of algorithm should always be informed by the properties of the problem at hand.

### Simpson's Rule in the Broader Landscape of Integration

Simpson's rule is a workhorse for one-dimensional integration, but it is essential to understand its place among other powerful techniques, especially when moving beyond one dimension or dealing with very [smooth functions](@entry_id:138942).

#### The Curse of Dimensionality: Simpson vs. Monte Carlo

How would we compute a multi-dimensional integral, such as the expected value of a basket option in finance, which may depend on dozens of assets? A naive extension of Simpson's rule is to create a tensor-product grid. If we use $N$ points in each of $d$ dimensions, the total number of function evaluations becomes $N^d$. The cost grows exponentially with the dimension, a phenomenon known as the **curse of dimensionality**. For even a modest dimension like $d=10$ and $N=100$ points, the cost becomes an astronomical $100^{10}$.

This is where **Monte Carlo integration** becomes indispensable. Its error decreases as $1/\sqrt{M}$, where $M$ is the number of random samples, *regardless of the dimension $d$*. To achieve an error of $\varepsilon$, Monte Carlo requires $M = \mathcal{O}(\varepsilon^{-2})$ evaluations. For Simpson's rule, the cost is $\mathcal{O}((\varepsilon^{-1/4})^d) = \mathcal{O}(\varepsilon^{-d/4})$.

The comparison is stark :
*   In low dimensions ($d=1, 2, 3$), the $\mathcal{O}(\varepsilon^{-d/4})$ cost of Simpson's rule is far superior to the $\mathcal{O}(\varepsilon^{-2})$ cost of Monte Carlo.
*   In high dimensions (e.g., $d=50$), the cost $\mathcal{O}(\varepsilon^{-12.5})$ for Simpson's is prohibitive, while the $\mathcal{O}(\varepsilon^{-2})$ cost for Monte Carlo remains manageable.

This trade-off is fundamental: grid-based methods like Simpson's are highly efficient in low dimensions, but Monte Carlo is the only feasible approach for high-dimensional problems.

#### Spectral Accuracy: Simpson vs. Chebyshev Methods

Even in one dimension, if the integrand is not just smooth but **analytic** (i.e., it can be represented by a convergent Taylor series), there are methods that can outperform Simpson's rule. **Spectral methods**, such as those based on Chebyshev polynomial approximation, represent the global function with a single high-degree polynomial. For [analytic functions](@entry_id:139584), the error of such an approximation decreases exponentially, or "spectrally," with the polynomial degree $m$: the error is $\mathcal{O}(\rho^{-m})$ for some $\rho > 1$.

This [exponential convergence](@entry_id:142080) leads to a dramatic efficiency gain. To achieve an error of $\varepsilon$, the required polynomial degree is $m = \mathcal{O}(\log(1/\varepsilon))$. In contrast, Simpson's rule requires $n = \mathcal{O}(\varepsilon^{-1/4})$ points. When function evaluations are computationally expensive, the total cost for the Chebyshev method is $\mathcal{O}(\log(1/\varepsilon))$, whereas for Simpson's rule it is $\mathcal{O}(\varepsilon^{-1/4})$. Because a logarithmic function grows much more slowly than any [power function](@entry_id:166538), the [spectral method](@entry_id:140101) will be vastly more efficient for achieving high accuracy on analytic functions .

In summary, Simpson's rule represents a sweet spot in [numerical integration](@entry_id:142553). It is simple to implement, far more accurate than the [trapezoidal rule](@entry_id:145375) for [smooth functions](@entry_id:138942), and serves as an excellent general-purpose tool for one-dimensional problems. Its true mastery, however, lies in recognizing the assumptions behind its power and knowing when the properties of the problem—non-smoothness, singularities, high dimensionality, or [analyticity](@entry_id:140716)—call for a different, more specialized approach.