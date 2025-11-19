## Introduction
Solving [linear ordinary differential equations](@entry_id:276013) using power series is a cornerstone technique in [mathematical analysis](@entry_id:139664). While this method can yield solutions for a wide class of equations, a critical question arises before any calculation begins: for what values of the independent variable will the resulting series solution actually converge? This article addresses this knowledge gap by introducing a profound and elegant theorem that connects the convergence of a solution directly to the analytic structure of the differential equation's coefficients. By reading through, you will gain a powerful tool that often bypasses tedious algebraic computation.

The following chapters are designed to build your expertise systematically. In "Principles and Mechanisms," we will unveil the core theorem and the step-by-step procedure for finding the [radius of convergence](@entry_id:143138) by locating singularities in the complex plane. Next, "Applications and Interdisciplinary Connections" will broaden this perspective, showcasing how the theorem applies to higher-order equations, systems, and even problems in fields like differential geometry. Finally, "Hands-On Practices" will allow you to solidify your understanding through targeted exercises that challenge you to apply these concepts.

## Principles and Mechanisms

In the study of [linear ordinary differential equations](@entry_id:276013) (ODEs), seeking solutions in the form of power series, $y(x) = \sum_{n=0}^{\infty} a_n (x-x_0)^n$, is a powerful and versatile method. This approach is particularly effective when the coefficient functions of the ODE are **analytic** at the point of expansion, $x_0$. An essential question arises before one even attempts to calculate the coefficients $a_n$: for what range of $x$ values will this series solution converge? This chapter elucidates the fundamental principle that governs the radius of convergence of such solutions, a principle that connects the convergence properties of the solution to the analytic properties of the equation's coefficients.

### The Domain of Convergence and Singular Points

A foundational theorem in the theory of differential equations guarantees the existence of a power series solution around a point $x_0$ if the equation's coefficients are analytic at $x_0$. Let us consider a general second-order linear ODE written in its **standard form**:

$y'' + P(x)y' + Q(x)y = G(x)$

A point $x_0$ is called an **[ordinary point](@entry_id:164624)** if the functions $P(x)$, $Q(x)$, and (for [non-homogeneous equations](@entry_id:165356)) $G(x)$ are all analytic at $x_0$. If any of these functions fail to be analytic at a point, that point is called a **singular point** of the differential equation.

The central principle for determining the convergence of a [power series](@entry_id:146836) solution is remarkably geometric:

*The [radius of convergence](@entry_id:143138), $\rho$, for a power series solution centered at an [ordinary point](@entry_id:164624) $x_0$ is at least as large as the distance from $x_0$ to the nearest [singular point](@entry_id:171198) in the complex plane.*

This means the solution is guaranteed to converge for all $x$ within the open disk $|x - x_0|  \rho$. The "nearest singular point" is the crucial element, and its location must be determined by examining all coefficient functions, $P(x)$, $Q(x)$, and $G(x)$. A profound implication of this principle is that the behavior of the solution is dictated not just by real-valued singularities, but by singularities that may exist only in the **complex plane**.

### Calculating the Radius of Convergence: Rational Coefficients

The most common class of equations encountered in an introductory context involves coefficients that are rational functions. These typically arise from an equation originally in the polynomial form:

$p_2(x)y'' + p_1(x)y' + p_0(x)y = g(x)$

where $p_2(x)$, $p_1(x)$, and $p_0(x)$ are polynomials. In this case, the functions in standard form, $P(x) = p_1(x)/p_2(x)$ and $Q(x) = p_0(x)/p_2(x)$, are analytic everywhere except where the denominator $p_2(x)$ is zero. These zeros are the singular points of the differential equation.

To find the minimum guaranteed radius of convergence, $\rho$, the procedure is as follows:
1.  Identify the leading polynomial coefficient, $p_2(x)$.
2.  Find all roots of the equation $p_2(x) = 0$. These are the [singular points](@entry_id:266699). Note that these roots may be real or complex.
3.  For a given expansion center $x_0$, calculate the distance in the complex plane from $x_0$ to each singular point. The distance between two points $z_1 = a+bi$ and $z_2 = c+di$ is given by the modulus of their difference: $|z_1 - z_2| = \sqrt{(a-c)^2 + (b-d)^2}$.
4.  The minimum of these distances is the value of $\rho$.

Let's illustrate this with examples. Consider an equation of the form $(x^2 - 25) y'' + y' = 0$, for which we seek a solution centered at $x_0 = -4$. Here, the leading coefficient is $p_2(x) = x^2 - 25$. The [singular points](@entry_id:266699) are the roots of $x^2 - 25 = 0$, which are $x = 5$ and $x = -5$. These are both real. The distances from the center $x_0 = -4$ to these singularities are:

$|-4 - 5| = |-9| = 9$
$|-4 - (-5)| = |1| = 1$

The smaller of these two distances is 1. Therefore, the power series solution is guaranteed to converge for at least $|x - (-4)|  1$, giving a minimum radius of convergence $\rho = 1$ [@problem_id:2194791].

The true power of this method is revealed when the singularities are not real. Consider the equation $(x^2 + 4)y'' - 2xy' + 6y = 0$, with a series solution sought around $x_0 = 1$. The leading coefficient $x^2 + 4$ has no real roots. However, in the complex plane, the roots of $x^2 + 4 = 0$ are $x = \pm 2i$. These are the [singular points](@entry_id:266699). We must calculate the distance from the real-valued center $x_0 = 1$ (or $1+0i$) to these complex singularities:

$|1 - 2i| = \sqrt{(1-0)^2 + (0-2)^2} = \sqrt{1^2 + (-2)^2} = \sqrt{5}$
$|1 - (-2i)| = |1 + 2i| = \sqrt{(1-0)^2 + (0-(-2))^2} = \sqrt{1^2 + 2^2} = \sqrt{5}$

The nearest singularity is at a distance of $\sqrt{5}$. Thus, the guaranteed [radius of convergence](@entry_id:143138) is $\rho = \sqrt{5}$ [@problem_id:2194829]. This demonstrates that even for an ODE with real coefficients and a real expansion point, its convergence behavior is governed by its structure in the complex plane.

This principle holds for any polynomial coefficients and any expansion center. For an equation like $(x^2 - 4x + 13)y'' - 3xy' + 7y = 0$, centered at $x_0 = 1$, we find the singularities by solving $x^2 - 4x + 13 = 0$. Using the quadratic formula, we find the roots are $x = 2 \pm 3i$. The distance from $x_0 = 1$ to these points is:

$|1 - (2 \pm 3i)| = |-1 \mp 3i| = \sqrt{(-1)^2 + (\mp 3)^2} = \sqrt{1 + 9} = \sqrt{10}$

So, the [radius of convergence](@entry_id:143138) is $\rho = \sqrt{10}$ [@problem_id:2194812]. A similar calculation for the same equation but centered at $x_0 = -1$ would yield singular points at $2 \pm 3i$ and a distance of $|-1 - (2 \pm 3i)| = |-3 \mp 3i| = \sqrt{9+9} = 3\sqrt{2}$ [@problem_id:2194803]. This highlights that the [radius of convergence](@entry_id:143138) depends critically on the choice of the expansion center. This can be explored further by considering an ODE with singularities at $z = 3$, $z = 2i$, and $z = -2i$. For a solution centered at $z_0=0$, the nearest singularities are $\pm 2i$, at a distance $R_0 = 2$. For a solution centered at $z_0=2$, the nearest singularity is at $z=3$, at a distance $R_2 = |2-3|=1$. Thus, the choice of center directly impacts the [guaranteed convergence](@entry_id:145667) region [@problem_id:2194788].

We can even generalize this. For an equation of the form $(x^2 + a^2)y'' + \dots = 0$ with $a>0$, the singularities are always at $x = \pm ai$. For any real expansion center $x_0$, the distance to these singularities will be $\rho = |x_0 - (\pm ai)| = \sqrt{x_0^2 + a^2}$ [@problem_id:2194808].

### Generalizations and Broader Applications

The principle extends beyond equations with simple rational coefficients.

#### Transcendental Coefficients

Consider an equation where a coefficient is a [transcendental function](@entry_id:271750), such as $y'' + (\sec x) y' + y = 0$. We wish to find the radius of convergence for a series solution around $x_0=0$. The function $Q(x)=1$ is entire (analytic everywhere). The function $P(x) = \sec x = 1/\cos x$ has singularities wherever $\cos x = 0$. The roots of $\cos x = 0$ are $x = \frac{\pi}{2} + k\pi$ for any integer $k$. The singular points closest to the center $x_0 = 0$ are $x = \pi/2$ and $x = -\pi/2$. The distance from 0 to either of these is $\pi/2$. Therefore, the guaranteed radius of convergence is $\rho = \pi/2$ [@problem_id:2194770].

#### Non-Homogeneous Equations

The principle applies directly to [non-homogeneous equations](@entry_id:165356) of the form $y'' + P(x)y' + Q(x)y = G(x)$. The [radius of convergence](@entry_id:143138) of the [particular solution](@entry_id:149080)'s series is determined by the distance from $x_0$ to the nearest singularity of $P(x)$, $Q(x)$, *or* $G(x)$. For example, in the equation $(x^2 + 16)y'' + y = \frac{1}{x - 5}$, to find the radius of convergence for a series solution around $x_0=0$, we must consider all sources of non-analyticity.
After writing in standard form, we have:
$y'' + \frac{1}{x^2+16}y = \frac{1}{(x-5)(x^2+16)}$
The singularities arise from the zeros of the denominators:
- $x^2 + 16 = 0 \implies x = \pm 4i$
- $x - 5 = 0 \implies x = 5$

The set of all singular points is $\{5, 4i, -4i\}$. We calculate their distances from the center $x_0=0$:
$|0 - 5| = 5$
$|0 - 4i| = 4$
$|0 - (-4i)| = 4$

The minimum distance is 4. Thus, the radius of convergence for the [power series](@entry_id:146836) solution is guaranteed to be at least $\rho = 4$ [@problem_id:2194785].

#### Entire Coefficients and Infinite Radius of Convergence

What if the coefficient functions $P(x)$ and $Q(x)$ are analytic everywhere in the complex plane? Such functions are called **[entire functions](@entry_id:176232)**. Common examples include polynomials, $\exp(x)$, $\sin(x)$, and $\cos(x)$. If all coefficients in the standard form are entire, there are no singular points in the finite complex plane. In this case, the distance to the "nearest" singularity is infinite.

Consequently, the radius of convergence for a power series solution is infinite, meaning the series converges for all $x \in \mathbb{R}$ (or $z \in \mathbb{C}$). Famous examples include the **Airy equation**, $y'' - xy = 0$, and the **Hermite equation**, $y'' - 2xy' + 2\lambda y = 0$. In both cases, the coefficients in standard form are polynomials, which are entire. Therefore, any [power series](@entry_id:146836) solution to these equations centered at any point $x_0$ will have an infinite [radius of convergence](@entry_id:143138).

### A Deeper Connection

This geometric principle for finding the [radius of convergence](@entry_id:143138), $\rho$, is a remarkable theoretical shortcut. In the general theory of power series, the radius of convergence of $\sum a_n z^n$ can often be found using the [ratio test](@entry_id:136231) limit, $\rho = \lim_{n\to\infty} |a_n/a_{n+1}|$. For a [power series](@entry_id:146836) solution to an ODE, one could, in principle, derive the recurrence relation for the coefficients $a_n$, compute this limit, and find $\rho$. This would be a tedious algebraic task. For instance, for an equation like $(z^2 - 6z + 13) y'' + (z-3) y' + 2y = 0$ centered at $z_0=0$, one would have to substitute the series into the equation and solve for the $a_n$ recurrence. However, the theorem presented in this chapter allows us to bypass this entirely. We simply find the singularities at $z = 3 \pm 2i$, calculate their distance to the origin as $\rho = |3 \pm 2i| = \sqrt{13}$, and we have found the radius of convergence without ever computing a single coefficient $a_n$ [@problem_id:2189848]. This powerful result underscores a deep and beautiful connection between the analytic structure of a differential equation and the global behavior of its solutions.