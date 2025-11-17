## Introduction
Many differential equations encountered in science and engineering, especially those with variable coefficients, resist solution by elementary techniques. This presents a significant challenge, as these equations often model complex physical systems. The [power series method](@entry_id:160913) provides a robust and systematic approach to constructing solutions for a broad class of these problems. This article explores how to find series solutions centered around an [ordinary point](@entry_id:164624), where the equation's coefficients are well-behaved.

In the first chapter, **Principles and Mechanisms**, we will lay the theoretical groundwork, defining [ordinary and singular points](@entry_id:177825) and establishing the theorem that guarantees the existence and convergence of series solutions. We will then detail the step-by-step process for deriving [recurrence relations](@entry_id:276612) to determine the solution's coefficients. Following this, the **Applications and Interdisciplinary Connections** chapter will demonstrate the method's versatility, showing how it provides insight into physical phenomena like [energy quantization](@entry_id:145335), solves systems of equations, and even offers a path to analyzing challenging nonlinear problems in physics and engineering. Finally, the **Hands-On Practices** section provides targeted exercises to solidify your understanding and build practical skills in applying these powerful techniques.

## Principles and Mechanisms

Many differential equations that arise in science and engineering, particularly those with variable coefficients, cannot be solved using elementary methods. However, for a broad and important class of linear differential equations, we can construct solutions in the form of power series. This chapter delves into the principles governing such solutions, focusing on the case where the series is expanded around a so-called **[ordinary point](@entry_id:164624)** of the differential equation. We will explore the theoretical guarantees for the existence and convergence of these solutions and detail the practical mechanism for their construction.

### Ordinary and Singular Points

Consider a general second-order linear [homogeneous differential equation](@entry_id:176396) of the form:
$$ A(x)y'' + B(x)y' + C(x)y = 0 $$
To analyze the behavior of its solutions, it is advantageous to write it in the **standard form**:
$$ y'' + p(x)y' + q(x)y = 0 $$
where $p(x) = B(x)/A(x)$ and $q(x) = C(x)/A(x)$.

The nature of the solutions near a point $x = x_0$ is fundamentally determined by the behavior of the coefficient functions $p(x)$ and $q(x)$ at that point.

A point $x_0$ is called an **[ordinary point](@entry_id:164624)** of the differential equation if both $p(x)$ and $q(x)$ are **analytic** at $x_0$. This means that both functions can be represented by a Taylor series expansion that converges in some neighborhood of $x_0$. For [rational functions](@entry_id:154279) $p(x)$ and $q(x)$, this condition simplifies: $x_0$ is an [ordinary point](@entry_id:164624) if the denominators of $p(x)$ and $q(x)$ are non-zero at $x_0$.

Conversely, a point $x_0$ is called a **[singular point](@entry_id:171198)** if it is not an [ordinary point](@entry_id:164624). That is, at least one of the functions $p(x)$ or $q(x)$ fails to be analytic at $x_0$. For equations with polynomial coefficients $A(x), B(x), C(x)$, the singular points are simply the roots of the leading coefficient $A(x)$.

For example, consider the equation $(x^2 - 9)y'' + y' + y = 0$ [@problem_id:2198591]. In standard form, we have $p(x) = \frac{1}{x^2 - 9}$ and $q(x) = \frac{1}{x^2 - 9}$. These functions are analytic everywhere except where the denominator is zero, i.e., $x^2 - 9 = 0$, which gives $x = 3$ and $x = -3$. Therefore, $x=3$ and $x=-3$ are the singular points of the equation. Every other point, such as $x=0$ or $x=1$, is an [ordinary point](@entry_id:164624).

Similarly, for the equation $(x^2 - x)y'' + \frac{1}{x+2}y' + y = 0$ [@problem_id:2198579], we put it in standard form by dividing by $A(x) = x^2-x$:
$$ p(x) = \frac{1}{(x+2)(x^2-x)} \quad \text{and} \quad q(x) = \frac{1}{x^2-x} $$
The functions $p(x)$ and $q(x)$ fail to be analytic where their denominators are zero. The singular points are thus the solutions to $(x+2)(x^2-x) = 0$, which are $x = 0$, $x = 1$, and $x = -2$. Any other point in the complex plane is an [ordinary point](@entry_id:164624).

### Existence and Radius of Convergence

The distinction between [ordinary and singular points](@entry_id:177825) is crucial because of the following fundamental theorem regarding the existence of power series solutions.

**Theorem:** If $x_0$ is an [ordinary point](@entry_id:164624) of the differential equation $y'' + p(x)y' + q(x)y = 0$, then its general solution can be expressed as $y(x) = \sum_{n=0}^{\infty} c_n (x-x_0)^n = c_0 y_1(x) + c_1 y_2(x)$, where $c_0$ and $c_1$ are arbitrary constants and $y_1(x)$ and $y_2(x)$ are two linearly independent series solutions that are analytic at $x_0$.

Furthermore, the theorem provides a guarantee on the [interval of convergence](@entry_id:146678) for these series solutions. The **radius of convergence**, $R$, of any series solution centered at $x_0$ is at least as large as the distance from $x_0$ to the nearest [singular point](@entry_id:171198) in the complex plane.

This distance is the radius of the largest open disk centered at $x_0$ within which both $p(x)$ and $q(x)$ are analytic. The [singular points](@entry_id:266699) act as barriers beyond which a convergent [series representation](@entry_id:175860) is not guaranteed.

Let's illustrate this powerful result.
- For the equation $(x^2 - 9)y'' + y' + y = 0$ with [singular points](@entry_id:266699) at $\pm 3$ [@problem_id:2198591]:
    - If we seek a solution centered at the [ordinary point](@entry_id:164624) $x_0 = 0$, the distance to the nearest singularity (either $3$ or $-3$) is $|0-3| = 3$. Thus, the [radius of convergence](@entry_id:143138) is guaranteed to be at least $R=3$.
    - If we instead center the solution at $x_0 = 1$, the distances to the singularities are $|1-3|=2$ and $|1-(-3)|=4$. The nearest singularity is at $x=3$. Therefore, the minimum guaranteed radius of convergence is $R=2$. This shows that the radius of convergence depends critically on the choice of the center $x_0$.

The singular points need not be real numbers. This is a critical aspect of the theory. Consider the equation $(x^2 - 4x + 13)y'' - 3xy' + 5y = 0$ [@problem_id:2198633]. The leading coefficient is zero when $x^2 - 4x + 13 = 0$. Using the quadratic formula, the singular points are $x = \frac{4 \pm \sqrt{16-52}}{2} = 2 \pm 3i$. These are points in the complex plane. If we want to find a series solution centered at the [ordinary point](@entry_id:164624) $x_0 = 1$, we must calculate the distance from $x_0=1$ to these complex singularities. The distance from a point $z_0 = a+bi$ to $z_1 = c+di$ is $|z_1 - z_0| = \sqrt{(c-a)^2 + (d-b)^2}$.
The distance from $x_0 = 1$ (or $1+0i$) to $2+3i$ is $\sqrt{(2-1)^2 + (3-0)^2} = \sqrt{1^2 + 3^2} = \sqrt{10}$. The distance to $2-3i$ is the same. Thus, the lower bound for the radius of convergence of a series solution centered at $x=1$ is $R = \sqrt{10}$. This means the series solution will converge for all $x$ such that $|x-1|  \sqrt{10}$.

### The Power Series Method: Finding the Recurrence Relation

The theorem guarantees the existence of a series solution, but it does not provide the coefficients $c_n$. The core mechanism for finding these coefficients is to assume the form of the solution, substitute it into the differential equation, and determine a relationship that the coefficients must satisfy. This relationship is known as a **[recurrence relation](@entry_id:141039)**.

The procedure is as follows:
1.  Assume a solution of the form $y(x) = \sum_{n=0}^{\infty} c_n (x-x_0)^n$ around an [ordinary point](@entry_id:164624) $x_0$.
2.  Differentiate the series term-by-term to find expressions for $y'(x)$ and $y''(x)$.
3.  Substitute the series for $y$, $y'$, and $y''$ into the original differential equation.
4.  Algebraically manipulate the resulting equation. This usually involves distributing any polynomial coefficients into the sums and shifting the indices of summation so that all series are expressed in terms of the same power, $(x-x_0)^k$.
5.  Combine all terms into a single [power series](@entry_id:146836). By the [identity principle](@entry_id:162041) for power series, if a series sums to zero over an interval, all of its coefficients must be zero.
6.  Setting the general coefficient of the combined series to zero yields the recurrence relation, which defines each coefficient $c_n$ in terms of preceding coefficients.

Let's apply this method to the celebrated **Airy's equation**, $y'' - xy = 0$, around the [ordinary point](@entry_id:164624) $x_0=0$ [@problem_id:2198597].
1.  Assume $y(x) = \sum_{n=0}^{\infty} c_n x^n$.
2.  The derivatives are $y'(x) = \sum_{n=1}^{\infty} n c_n x^{n-1}$ and $y''(x) = \sum_{n=2}^{\infty} n(n-1) c_n x^{n-2}$.
3.  Substituting into the ODE gives:
    $$ \sum_{n=2}^{\infty} n(n-1) c_n x^{n-2} - x \sum_{n=0}^{\infty} c_n x^n = 0 $$
    $$ \sum_{n=2}^{\infty} n(n-1) c_n x^{n-2} - \sum_{n=0}^{\infty} c_n x^{n+1} = 0 $$
4.  To combine these series, we must have the same power of $x$ in each. Let $k$ be the new index.
    - For the first sum, let $k = n-2$, so $n = k+2$. As $n$ goes from $2$ to $\infty$, $k$ goes from $0$ to $\infty$. The sum becomes $\sum_{k=0}^{\infty} (k+2)(k+1) c_{k+2} x^k$.
    - For the second sum, let $k = n+1$, so $n = k-1$. As $n$ goes from $0$ to $\infty$, $k$ goes from $1$ to $\infty$. The sum becomes $\sum_{k=1}^{\infty} c_{k-1} x^k$.
5.  The equation is now:
    $$ \sum_{k=0}^{\infty} (k+2)(k+1) c_{k+2} x^k - \sum_{k=1}^{\infty} c_{k-1} x^k = 0 $$
    To combine them, we separate the $k=0$ term from the first sum:
    $$ (2)(1)c_2 + \sum_{k=1}^{\infty} (k+2)(k+1) c_{k+2} x^k - \sum_{k=1}^{\infty} c_{k-1} x^k = 0 $$
    $$ 2c_2 + \sum_{k=1}^{\infty} \left[ (k+2)(k+1)c_{k+2} - c_{k-1} \right] x^k = 0 $$
6.  By the [identity principle](@entry_id:162041), all coefficients must be zero.
    - From the constant term ($k=0$): $2c_2 = 0 \implies c_2 = 0$.
    - From the coefficient of $x^k$ for $k \ge 1$: $(k+2)(k+1)c_{k+2} - c_{k-1} = 0$.

This gives the recurrence relation: $c_{k+2} = \frac{c_{k-1}}{(k+2)(k+1)}$ for $k \ge 1$. Adopting the convention that $c_j=0$ for $j0$, we can express this as a single relation for all $k \ge 0$: $(k+2)(k+1)c_{k+2} = c_{k-1}$ [@problem_id:2198597].

### Constructing the General Solution

The [recurrence relation](@entry_id:141039) is a formula for generating the series coefficients. The first two coefficients, $c_0$ and $c_1$, are not determined by the relation. Instead, they are determined by the [initial conditions](@entry_id:152863) of the problem: $c_0 = y(x_0)$ and $c_1 = y'(x_0)$. These two constants become the arbitrary constants in the general solution. All other coefficients, $c_n$ for $n \ge 2$, are determined in terms of $c_0$ and $c_1$.

Let's find the first few terms of the solution for $y'' - xy' - 2y = 0$ centered at $x_0=0$, with initial conditions $y(0)=c_0$ and $y'(0)=c_1$ [@problem_id:2198609].
Assuming $y(x)=\sum_{k=0}^{\infty} a_k x^k$ and substituting into the ODE leads to the recurrence relation (after re-indexing and combining terms):
$$ (k+2)(k+1)a_{k+2} - k a_k - 2a_k = 0 $$
$$ (k+2)(k+1)a_{k+2} = (k+2)a_k \implies a_{k+2} = \frac{a_k}{k+1} \quad \text{for } k \ge 0 $$
We start with the given initial conditions $a_0 = y(0) = c_0$ and $a_1 = y'(0) = c_1$. We can now generate subsequent coefficients:
- For $k=0$: $a_2 = \frac{a_0}{0+1} = a_0 = c_0$
- For $k=1$: $a_3 = \frac{a_1}{1+1} = \frac{a_1}{2} = \frac{c_1}{2}$
- For $k=2$: $a_4 = \frac{a_2}{2+1} = \frac{a_2}{3} = \frac{c_0}{3}$
- For $k=3$: $a_5 = \frac{a_3}{3+1} = \frac{a_3}{4} = \frac{c_1/2}{4} = \frac{c_1}{8}$

The solution up to the $x^5$ term is thus:
$y(x) = a_0 + a_1 x + a_2 x^2 + a_3 x^3 + a_4 x^4 + a_5 x^5 + \dots$
$y(x) = c_0 + c_1 x + c_0 x^2 + \frac{c_1}{2} x^3 + \frac{c_0}{3} x^4 + \frac{c_1}{8} x^5 + \dots$

We can group the terms based on $c_0$ and $c_1$:
$y(x) = c_0 \left(1 + x^2 + \frac{1}{3}x^4 + \dots\right) + c_1 \left(x + \frac{1}{2}x^3 + \frac{1}{8}x^5 + \dots\right)$
This explicitly shows the structure of the general solution, $y(x) = c_0 y_1(x) + c_1 y_2(x)$, where $y_1(x)$ and $y_2(x)$ are the two [fundamental solutions](@entry_id:184782). The first, $y_1(x)$, corresponds to initial conditions $y(0)=1, y'(0)=0$, and the second, $y_2(x)$, corresponds to $y(0)=0, y'(0)=1$.

In some cases, the recurrence may lead to many zero coefficients. For $(x^2+1) y'' + x y' - y = 0$ with $y(0)=2, y'(0)=3$, the recurrence is $a_{k+2} = - \frac{k^2-1}{(k+2)(k+1)} a_k$ [@problem_id:2198643]. With $a_0=2, a_1=3$:
- $a_2 = -\frac{-1}{2 \cdot 1}a_0 = \frac{1}{2}(2)=1$
- $a_3 = -\frac{0}{3 \cdot 2}a_1 = 0$. Since $a_3=0$, all subsequent odd coefficients ($a_5, a_7, \dots$) will also be zero.
- $a_4 = -\frac{3}{4 \cdot 3}a_2 = -\frac{1}{4}(1) = -\frac{1}{4}$
- $a_6 = -\frac{15}{6 \cdot 5}a_4 = -\frac{1}{2}(-\frac{1}{4}) = \frac{1}{8}$
The solution begins $y(x) = 2 + 3x + x^2 - \frac{1}{4}x^4 + \frac{1}{8}x^6 + \dots$.

The calculation of any specific coefficient, for example $c_5$ for $y'' + (x+1)y' - y = 0$ with $y(0)=A, y'(0)=B$, simply requires iterative application of the recurrence relation, starting from $c_0=A$ and $c_1=B$ [@problem_id:2198622].

### Deeper Connections and Reverse Engineering

The link between a differential equation and its series solution is profound, allowing us to reason in both directions.

#### From Solution to Equation

If we know the first few terms of a solution's series expansion, we can infer properties of the differential equation itself. Consider the general equation $y'' + p(x)y' + q(x)y = 0$, where $p(x)$ and $q(x)$ are analytic at $x=0$. Evaluating the ODE at $x=0$ gives a fundamental relationship:
$$ y''(0) + p(0)y'(0) + q(0)y(0) = 0 $$
Suppose we have determined from experiments two fundamental solutions [@problem_id:2198577]:
$y_1(x) = 1 + \frac{3}{2}x^2 - x^3 + O(x^4)$
$y_2(x) = x - x^2 + \frac{7}{6}x^3 + O(x^4)$

From the series, we can read the values of the functions and their derivatives at $x=0$. Recall that for a Maclaurin series $y(x) = \sum \frac{y^{(n)}(0)}{n!}x^n$.
- For $y_1(x)$: $y_1(0)=1$, $y_1'(0)=0$, $y_1''(0)/2! = 3/2 \implies y_1''(0)=3$.
- For $y_2(x)$: $y_2(0)=0$, $y_2'(0)=1$, $y_2''(0)/2! = -1 \implies y_2''(0)=-2$.

Now, we substitute each solution into the fundamental relationship:
- For $y_1$: $3 + p(0) \cdot 0 + q(0) \cdot 1 = 0 \implies q(0) = -3$.
- For $y_2$: $-2 + p(0) \cdot 1 + q(0) \cdot 0 = 0 \implies p(0) = 2$.
Thus, by knowing the local behavior of the solutions, we have determined the values of the system's coefficient functions at the origin: $p(0)=2$ and $q(0)=-3$.

#### From Recurrence to Equation

We can also work backward from a recurrence relation to find the differential equation it came from [@problem_id:2198601]. Suppose we discover that the coefficients of a solution satisfy $(n+1)c_{n+2} + (n-1)c_n = 0$. We want to find the polynomials $P(x), Q(x), R(x)$ in $P(x)y'' + Q(x)y' + R(x)y = 0$.

The structure of the recurrence gives clues. It links $c_{n+2}$ with $c_n$. Let's consider how terms in the ODE produce coefficients in the final series.
- $y'' = \sum (n+2)(n+1)c_{n+2}x^n$. This gives the $c_{n+2}$ term.
- $x^2 y'' = \sum n(n-1)c_n x^n$. This produces a $c_n$ term involving $n^2$.
- $x y' = \sum n c_n x^n$. This produces a $c_n$ term involving $n$.
- $y = \sum c_n x^n$. This produces a $c_n$ term.

The given recurrence $(n+1)c_{n+2} + (n-1)c_n = 0$ can be rewritten as $(n+2)(n+1)c_{n+2} + (n+2)(n-1)c_n = 0$ (multiplying by $n+2$, assuming $n+2 \neq 0$). The term $(n+2)(n+1)c_{n+2}$ is the coefficient of $x^n$ from $y''$. The term $(n+2)(n-1)c_n = (n^2+n-2)c_n$ must arise from a combination of $P(x), Q(x), R(x)$. A systematic analysis reveals that the combination $(1+x^2)y'' + (2x)y' - 2y = 0$ yields exactly this recurrence.

#### Connection to the Wronskian

The [power series method](@entry_id:160913) is also consistent with other fundamental theories of differential equations, such as Abel's theorem for the Wronskian. The Wronskian of two solutions $y_1, y_2$ is $W(x) = y_1 y_2' - y_1' y_2$. Abel's theorem states that for $y''+p(x)y'+q(x)y=0$, the Wronskian satisfies $W(x) = W(x_0)\exp(-\int_{x_0}^x p(t)dt)$.

For an equation like $y'' + \alpha x y = 0$ [@problem_id:2198605], we have $p(x)=0$. Abel's theorem predicts that the Wronskian must be a constant. We can verify this directly. By finding the series solutions for $y_1$ (with $y_1(0)=1, y_1'(0)=0$) and $y_2$ (with $y_2(0)=0, y_2'(0)=1$), and then computing the series for their Wronskian, we find:
$y_1(x) = 1 - \frac{\alpha}{6}x^3 + \dots$
$y_2(x) = x - \frac{\alpha}{12}x^4 + \dots$
$y_1'(x) = -\frac{\alpha}{2}x^2 + \dots$
$y_2'(x) = 1 - \frac{\alpha}{3}x^3 + \dots$

$W(x) = y_1 y_2' - y_1' y_2 = (1 - \frac{\alpha}{6}x^3 + \dots)(1 - \frac{\alpha}{3}x^3 + \dots) - (-\frac{\alpha}{2}x^2 + \dots)(x - \frac{\alpha}{12}x^4 + \dots)$
$W(x) = (1 - \frac{\alpha}{3}x^3 - \frac{\alpha}{6}x^3 + \dots) - (-\frac{\alpha}{2}x^3 + \dots)$
$W(x) = 1 - \frac{\alpha}{2}x^3 + \frac{\alpha}{2}x^3 + \dots = 1 + O(x^6)$
The lower-order terms cancel perfectly. In fact, all higher-order terms also cancel, leaving $W(x)=1$ for all $x$, consistent with Abel's theorem and the initial condition $W(0) = y_1(0)y_2'(0) - y_1'(0)y_2(0) = (1)(1)-(0)(0) = 1$. This demonstrates the beautiful internal consistency of the theory of differential equations.