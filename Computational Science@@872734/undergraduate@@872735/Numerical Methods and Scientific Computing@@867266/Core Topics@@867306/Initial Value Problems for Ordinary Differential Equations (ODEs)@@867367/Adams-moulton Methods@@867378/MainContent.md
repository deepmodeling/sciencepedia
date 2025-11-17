## Introduction
The numerical solution of [ordinary differential equations](@entry_id:147024) (ODEs) is a fundamental task in science and engineering, modeling everything from [planetary motion](@entry_id:170895) to chemical reactions. While simple methods provide a starting point, the demand for greater accuracy and efficiency, especially for challenging "stiff" systems, leads us to more advanced techniques. This article addresses this need by providing a comprehensive exploration of the Adams-Moulton methods, a powerful family of implicit multistep solvers renowned for their excellent stability and [high-order accuracy](@entry_id:163460).

## Principles and Mechanisms

Following our introduction to [linear multistep methods](@entry_id:139528), this chapter delves into the principles and mechanisms of a particularly important family: the Adams-Moulton methods. These methods are renowned for their high accuracy and excellent stability properties, which make them a cornerstone of modern [numerical solvers](@entry_id:634411) for ordinary differential equations (ODEs). We will explore their derivation, their inherent implicitness, practical implementation strategies, and their fundamental theoretical properties.

### Derivation from Integral Form: Interpolation vs. Extrapolation

The foundation for all Adams-type methods lies in the exact integral form of a first-order [initial value problem](@entry_id:142753), $y'(t) = f(t, y(t))$:

$$y(t_{n+1}) = y(t_n) + \int_{t_n}^{t_{n+1}} f(t, y(t)) dt$$

The core idea is to approximate the integral by replacing the potentially complicated function $f(t, y(t))$ with a simpler function that is easy to integrate: a polynomial, $P(t)$. The manner in which this polynomial is constructed defines the method. Let us consider two distinct strategies for constructing $P(t)$, assuming we have already computed a sequence of approximations $y_i \approx y(t_i)$ and corresponding derivative estimates $f_i = f(t_i, y_i)$ for $i \le n$.

First, one could construct a polynomial that interpolates a set of *previously computed* data points, such as $\{(t_n, f_n), (t_{n-1}, f_{n-1}), \dots, (t_{n-k+1}, f_{n-k+1})\}$. This polynomial is then integrated over the interval $[t_n, t_{n+1}]$. Because all the points used for constructing the polynomial lie to the left of or at the start of the integration interval, this approach effectively *extrapolates* the behavior of $f$ into the future. This strategy leads to the family of **explicit Adams-Bashforth methods**.

In contrast, the **Adams-Moulton (AM) methods** employ a more ambitious strategy. The polynomial $P(t)$ is constructed to pass through the same set of previous points but also includes the *unknown future point*, $(t_{n+1}, f_{n+1})$. This means the approximation is based on *interpolation* across the entire integration interval $[t_n, t_{n+1}]$. This inclusion of the future point, while seeming to pose a challenge, is precisely what gives Adams-Moulton methods their superior accuracy and stability. This defining characteristic, however, means the resulting formula for $y_{n+1}$ will depend on itself, a property known as implicitness.

### The Implicit Nature of Adams-Moulton Methods

A numerical method is **implicit** if the equation for the new state, $y_{n+1}$, cannot be solved by direct evaluation and instead involves $y_{n+1}$ on both sides. Let's examine the general form of a $k$-step Adams-Moulton method:

$$y_{n+1} = y_n + h \sum_{j=0}^{k-1} \beta_j f(t_{n+1-j}, y_{n+1-j})$$

Here, $h$ is the step size and the $\beta_j$ are constants determined by the method's order. The summation term is the result of integrating the [interpolating polynomial](@entry_id:750764). The key to the method's implicitness lies in the $j=0$ term of the sum: $\beta_0 f(t_{n+1}, y_{n+1})$. Since the function $f$ is evaluated at the future time $t_{n+1}$ with the unknown solution $y_{n+1}$, the value we are trying to compute, $y_{n+1}$, appears on the right-hand side of the equation. For any Adams-Moulton method, the coefficient $\beta_0$ is non-zero.

To make this concrete, let's consider the three-step Adams-Moulton method (which has order four):

$$y_{n+1} = y_n + \frac{h}{24} \left( 9 f(t_{n+1}, y_{n+1}) + 19 f(t_n, y_n) - 5 f(t_{n-1}, y_{n-1}) + f(t_{n-2}, y_{n-2}) \right)$$

When computing $y_{n+1}$, the values $y_n$, $y_{n-1}$, and $y_{n-2}$ are known from previous steps. Consequently, $f(t_n, y_n)$, $f(t_{n-1}, y_{n-1})$, and $f(t_{n-2}, y_{n-2})$ are also known. The term that prevents a direct calculation is precisely $9 f(t_{n+1}, y_{n+1})$, as it depends on the yet-to-be-determined $y_{n+1}$.

Perhaps the most fundamental example is the one-step Adams-Moulton method, which interpolates $f$ using just two points: $(t_n, f_n)$ and $(t_{n+1}, f_{n+1})$. Integrating the resulting linear polynomial yields the formula:

$$y_{n+1} = y_n + \frac{h}{2} \left( f(t_n, y_n) + f(t_{n+1}, y_{n+1}) \right)$$

This may be recognized as the well-known **Trapezoidal Rule** for numerical integration applied to ODEs. This second-order method is one of the most important implicit methods due to its simplicity and excellent stability properties, which we will discuss later.

### Implementation: Solving the Implicit Equation

The implicit nature of Adams-Moulton methods means that each time step requires solving a (generally nonlinear) algebraic equation for $y_{n+1}$. Let's represent the AM formula abstractly as $y_{n+1} = G(y_{n+1})$. We need to find the value of $y_{n+1}$ that satisfies this equation.

A common approach is to reframe this as a [root-finding problem](@entry_id:174994). If we define a function $g(w)$ such that $g(w) = w - G(w)$, then our goal is to find the root of $g(w)=0$, where $w$ is our stand-in for $y_{n+1}$. For instance, using the third-order AM method to solve $y'(t) = t - \cos(y(t))$, with known values at steps $i$ and $i-1$, the equation for $y_{i+1}$ can be rearranged into the form $g(y_{i+1}) = 0$, where $g(w)$ is a function of the single variable $w=y_{i+1}$. Once in this form, any standard [root-finding algorithm](@entry_id:176876), such as Newton's method, can be applied.

However, a simpler and more common technique for this class of problems is **[fixed-point iteration](@entry_id:137769)**. The AM formula itself provides a natural [iterative map](@entry_id:274839). Given an initial guess for the solution, which we denote $y_{i+1}^{(0)}$, we can generate a sequence of improved approximations:

$$ y_{i+1}^{(k+1)} = y_i + \frac{h}{2} \left[ f(t_i, y_i) + f(t_{i+1}, y_{i+1}^{(k)}) \right] $$

This example shows the [fixed-point iteration](@entry_id:137769) for the Trapezoidal Rule (second-order AM). We iterate this formula for $k=0, 1, 2, \dots$ until the value of $y_{i+1}^{(k)}$ converges.

The efficiency of this iteration hinges on a good initial guess, $y_{i+1}^{(0)}$. A poor guess might require many iterations or even cause the iteration to diverge. This is where **[predictor-corrector schemes](@entry_id:637533)** come into play. The primary role of a "predictor" is to provide a high-quality initial estimate for the unknown $y_{n+1}$. Typically, an explicit method, such as an Adams-Bashforth method of the same order, is used for this purpose. For example, to solve the implicit second-order AM equation, one might first "predict" a value using the explicit second-order Adams-Bashforth formula:

$$y_{n+1}^{(0)} = y_n + h\left( \frac{3}{2} f(t_n, y_n) - \frac{1}{2} f(t_{n-1}, y_{n-1}) \right) \quad (\text{Predictor})$$

This predicted value $y_{n+1}^{(0)}$ is then used as the initial guess in the [fixed-point iteration](@entry_id:137769) for the AM formula, which now acts as a "corrector":

$$y_{n+1}^{(k+1)} = y_n + \frac{h}{2} \left( f(t_n, y_n) + f(t_{n+1}, y_{n+1}^{(k)}) \right) \quad (\text{Corrector})$$

In many practical implementations, the corrector step is applied only once or twice (a PECE or PEC scheme) rather than iterating to full convergence, providing a good balance between accuracy and computational cost.

### Accuracy and Stability Properties

The widespread use of Adams-Moulton methods stems from their favorable theoretical properties, namely their high accuracy and superior stability compared to their explicit counterparts.

#### Local Truncation Error and Order

The **Local Truncation Error (LTE)** is the error incurred in a single step, assuming the exact solution was known at all previous steps. For a method of order $p$, the LTE is proportional to $h^{p+1}$. A key result for Adams-Moulton methods is that a $k$-step method, which uses an [interpolating polynomial](@entry_id:750764) through $k+1$ points, achieves an [order of accuracy](@entry_id:145189) $p = k+1$. The leading term of its LTE has the general form:

$$\tau_{n+1}(h) = C_{p+1} h^{p+1} y^{(p+1)}(\xi_n) + O(h^{p+2})$$

where $C_{p+1}$ is a method-specific error constant and $\xi_n$ is a point within the step interval. It is noteworthy that the error constants for AM methods are significantly smaller than those for Adams-Bashforth methods of the same order. This means that for a given step size $h$, AM methods are generally more accurate.

#### Zero-Stability

For any [linear multistep method](@entry_id:751318) to be convergent, it must be **zero-stable**. This property ensures that the numerical solution does not grow uncontrollably as the step size $h$ approaches zero. Zero-stability depends only on the coefficients $\alpha_j$ that multiply the solution values $y_{n+j}$. These are captured in the **first [characteristic polynomial](@entry_id:150909)**, $\rho(z)$. For a $k$-step Adams-Moulton method, the formula $y_{n+1} - y_n = h(\dots)$ implies that $\alpha_k=1$, $\alpha_{k-1}=-1$, and all other $\alpha_j$ are zero (in a shifted index formulation). This yields the polynomial:

$$\rho(z) = z^k - z^{k-1} = z^{k-1}(z-1)$$

A method is zero-stable if all roots of $\rho(z)$ have a magnitude less than or equal to 1, and any root with magnitude exactly 1 is simple (has multiplicity 1). The roots of the AM polynomial are $z=1$ (with multiplicity 1) and $z=0$ (with multiplicity $k-1$). Since the only root on the unit circle, $z=1$, is simple, the root condition is satisfied. Therefore, all Adams-Moulton methods are zero-stable, a crucial prerequisite for their use.

#### Absolute Stability and A-Stability

The most compelling reason to use implicit methods like Adams-Moulton is their superior **[absolute stability](@entry_id:165194)**. This property governs the method's behavior when applied to **[stiff equations](@entry_id:136804)**—problems where the solution has components that decay at vastly different rates. The stability is analyzed using the test equation $y' = \lambda y$, where $\lambda$ is a complex number. A method is stable for a given step size $h$ if the numerical solution does not grow for values of $z = h\lambda$ that lie in the method's **region of [absolute stability](@entry_id:165194)**.

For [stiff problems](@entry_id:142143), $\lambda$ has a large negative real part, so we desire methods whose [stability regions](@entry_id:166035) contain as much of the left half of the complex plane as possible. Explicit methods, like Adams-Bashforth, have strictly bounded [stability regions](@entry_id:166035). In contrast, implicit Adams-Moulton methods have much larger [stability regions](@entry_id:166035).

The most desirable property for stiff solvers is **A-stability**, where the region of [absolute stability](@entry_id:165194) includes the entire left half of the complex plane ($\Re(z) \le 0$). The second-order Adams-Moulton method (Trapezoidal Rule) is A-stable. The second-order Adams-Bashforth method is not. This is a fundamental trade-off: the AM2 method requires solving an implicit equation at each step, but it is [unconditionally stable](@entry_id:146281) for any stable linear ODE, allowing for much larger step sizes than the explicit AB2 method.

### Theoretical Limitations: The Dahlquist Stability Barriers

Given the excellent properties of the A-stable Trapezoidal Rule (AM, order 2), a natural question arises: can we construct A-stable Adams-Moulton methods of arbitrarily high order? The answer, unfortunately, is no. This is a consequence of the famous **Dahlquist stability barriers**.

The second Dahlquist barrier states that the maximum order of an A-stable [linear multistep method](@entry_id:751318) is two. The Trapezoidal Rule achieves this limit. Why can't higher-order AM methods be A-stable? The reason lies in their behavior for large, negative values of $z=h\lambda$, which corresponds to the "infinitely stiff" limit. In this limit, the roots of the method's full characteristic stability polynomial, $\rho(\xi) - z\sigma(\xi) = 0$, converge to the roots of the **second characteristic polynomial**, $\sigma(\xi)$. For A-stability, it is necessary that all roots of $\sigma(\xi)$ lie within or on the unit circle.

For the Adams-Moulton family, this condition holds only for the methods of order 1 (Backward Euler) and order 2 (Trapezoidal Rule). For any AM method with order $p > 2$, the corresponding polynomial $\sigma(\xi)$ has at least one root with magnitude greater than 1. Consequently, as $\Re(z) \to -\infty$, at least one root of the stability polynomial will grow beyond the unit circle, violating the condition for A-stability. This profound result establishes a hard limit on the achievable combination of order and stability for this family of methods, cementing the unique and important role of the second-order Trapezoidal Rule in the numerical solution of [stiff differential equations](@entry_id:139505).