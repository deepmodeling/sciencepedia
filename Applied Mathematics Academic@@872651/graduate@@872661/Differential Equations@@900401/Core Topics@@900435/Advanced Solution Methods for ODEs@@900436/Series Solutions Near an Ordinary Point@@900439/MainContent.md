## Introduction
Many differential equations with variable coefficients, which are essential for modeling real-world phenomena, cannot be solved using [elementary functions](@entry_id:181530). This creates a significant gap in our ability to analyze and predict the behavior of complex systems. The method of series solutions provides a powerful and systematic approach to bridge this gap by representing the solution as an infinite power series. This article serves as a comprehensive guide to mastering this indispensable technique, focusing on solutions centered around an [ordinary point](@entry_id:164624) of an equation.

The section "Principles and Mechanisms" lays the theoretical groundwork. It covers the identification of ordinary points, the theorem that guarantees the existence and convergence of a series solution, and the step-by-step process for deriving the crucial recurrence relation that generates the solution's coefficients. Following this, "Applications and Interdisciplinary Connections" explores the vast utility of the method, showing how it is used to define [special functions](@entry_id:143234), solve complex nonlinear and coupled systems, and provide critical insights in fields ranging from astrophysics to quantum mechanics. Finally, "Hands-On Practices" offers a selection of guided problems to solidify understanding and build practical skills in applying these concepts to a variety of challenging scenarios.

## Principles and Mechanisms

Many differential equations that arise in science and engineering, particularly those with variable coefficients, cannot be solved in terms of [elementary functions](@entry_id:181530). For these cases, an invaluable technique is to seek a solution in the form of an infinite [power series](@entry_id:146836). This chapter delineates the principles that guarantee the existence of such solutions and the mechanisms by which they can be constructed. We will focus on series solutions centered around an **[ordinary point](@entry_id:164624)** of the differential equation.

### Ordinary Points and the Guarantee of Convergence

Consider a general second-order linear [homogeneous differential equation](@entry_id:176396):
$$
A(x)y'' + B(x)y' + C(x)y = 0
$$
To analyze its solutions, we first write it in **standard form** by dividing by the leading coefficient, $A(x)$:
$$
y'' + p(x)y' + q(x)y = 0
$$
where $p(x) = \frac{B(x)}{A(x)}$ and $q(x) = \frac{C(x)}{A(x)}$.

The behavior of solutions is critically dependent on the properties of the coefficient functions $p(x)$ and $q(x)$. A point $x_0$ is called an **[ordinary point](@entry_id:164624)** of the differential equation if both $p(x)$ and $q(x)$ are analytic at $x_0$. A function is analytic at a point if it can be represented by a power series that converges in a neighborhood of that point. For [rational functions](@entry_id:154279) $p(x)$ and $q(x)$, this is equivalent to the denominator not being zero at $x_0$. If a point is not ordinary, it is called a **[singular point](@entry_id:171198)**.

The significance of ordinary points is captured in the following fundamental theorem:

**Theorem:** If $x_0$ is an [ordinary point](@entry_id:164624) of the differential equation $y'' + p(x)y' + q(x)y = 0$, then its general solution can be expressed as a [power series](@entry_id:146836) centered at $x_0$:
$$
y(x) = \sum_{n=0}^{\infty} c_n (x-x_0)^n = c_0 y_1(x) + c_1 y_2(x)
$$
where $c_0$ and $c_1$ are arbitrary constants, and $y_1(x)$ and $y_2(x)$ are two [linearly independent](@entry_id:148207) series solutions. Furthermore, the **[radius of convergence](@entry_id:143138)** of these series solutions is at least as large as the distance from $x_0$ to the nearest [singular point](@entry_id:171198) in the complex plane.

This theorem provides a powerful guarantee. Before embarking on the process of finding a series solution, we can determine a lower bound for its radius of convergence simply by locating the [singular points](@entry_id:266699) of the equation.

Let's illustrate this principle. Consider the equation $(x^2 - 9)y'' + y' + y = 0$. In standard form, $p(x) = q(x) = \frac{1}{x^2-9}$. The [singular points](@entry_id:266699) are the values of $x$ where the denominator is zero, namely $x=3$ and $x=-3$.
- If we seek a solution centered at the [ordinary point](@entry_id:164624) $x_0 = 0$, the nearest [singular points](@entry_id:266699) are at a distance of $|3-0|=3$ and $|-3-0|=3$. Thus, the guaranteed minimum radius of convergence is $\rho_0 = 3$.
- If we instead center the solution at $x_1 = 1$, the distances to the singularities are $|3-1|=2$ and $|-3-1|=4$. The nearest singularity is $x=3$, so the guaranteed radius is $\rho_1 = 2$.
This demonstrates that the [radius of convergence](@entry_id:143138) depends on the choice of the center $x_0$. [@problem_id:2198591]

The singular points need not be real numbers. The theorem requires us to consider the complex plane. For instance, take the equation $(x^2 - 4x + 13)y'' - 3xy' + 5y = 0$. The [singular points](@entry_id:266699) are the roots of $x^2 - 4x + 13 = 0$. Using the quadratic formula, we find the roots to be $x = 2 \pm 3i$. If we want to find a series solution centered at the [ordinary point](@entry_id:164624) $x_0 = 1$, we must calculate the distance in the complex plane from $x_0=1$ to these singularities. The distance to both $2+3i$ and $2-3i$ is the same:
$$
R = |(2 \pm 3i) - 1| = |1 \pm 3i| = \sqrt{1^2 + (\pm 3)^2} = \sqrt{10}
$$
Therefore, any series solution centered at $x=1$ is guaranteed to converge for at least $|x-1| \lt \sqrt{10}$. [@problem_id:2198633]

This concept extends to equations with more complex coefficients and to expansion points in the complex plane. Let's analyze the equation $(x^2 - x)y'' + y' + \frac{1}{x+2}y = 0$. First, we write it in standard form:
$$
y'' + \frac{1}{x(x-1)} y' + \frac{1}{(x+2)x(x-1)} y = 0
$$
The coefficient functions $p(x)$ and $q(x)$ have singularities where their denominators are zero: at $x=0$, $x=1$, and $x=-2$. Suppose we are interested in a series solution centered at the complex [ordinary point](@entry_id:164624) $x_0 = \frac{1}{2} + i$. We find the distance from $x_0$ to each [singular point](@entry_id:171198):
- Distance to $x=0$: $|\frac{1}{2}+i - 0| = \sqrt{(\frac{1}{2})^2 + 1^2} = \frac{\sqrt{5}}{2}$
- Distance to $x=1$: $|\frac{1}{2}+i - 1| = |-\frac{1}{2}+i| = \sqrt{(-\frac{1}{2})^2 + 1^2} = \frac{\sqrt{5}}{2}$
- Distance to $x=-2$: $|\frac{1}{2}+i - (-2)| = |\frac{5}{2}+i| = \sqrt{(\frac{5}{2})^2 + 1^2} = \frac{\sqrt{29}}{2}$

The minimum of these distances is $\frac{\sqrt{5}}{2}$. This is the guaranteed minimum [radius of convergence](@entry_id:143138) for a series solution centered at $x_0 = \frac{1}{2} + i$. [@problem_id:2189878] [@problem_id:2198579]

### The Method for Finding Series Solutions

Once we have established that a series solution exists, we can find it using a procedure often called the [method of undetermined coefficients](@entry_id:165061). The process is systematic:

1.  **Assume a Solution:** Posit a solution of the form $y(x) = \sum_{n=0}^{\infty} c_n (x-x_0)^n$. For simplicity, we will often use $x_0=0$.
2.  **Differentiate:** Compute the series for $y'(x)$ and $y''(x)$ by [term-by-term differentiation](@entry_id:142985).
3.  **Substitute:** Substitute the series for $y$, $y'$, and $y''$ into the original differential equation.
4.  **Re-index:** Manipulate the summation indices so that the power of $x$ (or $x-x_0$) is the same in all sums, typically $x^k$.
5.  **Equate Coefficients:** Combine the sums into a single series. By the [identity principle](@entry_id:162041) for [power series](@entry_id:146836), if $\sum_{k=0}^{\infty} A_k x^k = 0$ for all $x$ in an interval, then every coefficient $A_k$ must be zero.
6.  **Find the Recurrence Relation:** Setting the total coefficient of $x^k$ to zero gives a **recurrence relation**, which is an equation that relates coefficients with different indices.

Let's apply this method to the classic **Airy's equation**, $y'' - xy = 0$, around the [ordinary point](@entry_id:164624) $x_0=0$.

1.  Assume $y(x) = \sum_{n=0}^{\infty} c_n x^n$.
2.  Differentiate: $y'(x) = \sum_{n=1}^{\infty} n c_n x^{n-1}$ and $y''(x) = \sum_{n=2}^{\infty} n(n-1) c_n x^{n-2}$.
3.  Substitute: $\sum_{n=2}^{\infty} n(n-1) c_n x^{n-2} - x \sum_{n=0}^{\infty} c_n x^n = 0$.
4.  Re-index:
    - For the first term, let $k=n-2$. When $n=2$, $k=0$. The sum becomes $\sum_{k=0}^{\infty} (k+2)(k+1) c_{k+2} x^k$.
    - For the second term, first bring $x$ inside: $- \sum_{n=0}^{\infty} c_n x^{n+1}$. Now, let $k=n+1$. When $n=0$, $k=1$. The sum is $- \sum_{k=1}^{\infty} c_{k-1} x^k$.
5.  The equation is now $\sum_{k=0}^{\infty} (k+2)(k+1) c_{k+2} x^k - \sum_{k=1}^{\infty} c_{k-1} x^k = 0$. To combine these, we separate the $k=0$ term from the first sum:
    $$ (2)(1)c_2 + \sum_{k=1}^{\infty} \left[ (k+2)(k+1) c_{k+2} - c_{k-1} \right] x^k = 0 $$
    By the [identity principle](@entry_id:162041), the coefficient of each power of $x$ must be zero. This gives $c_2 = 0$ and, for $k \ge 1$:
6.  The [recurrence relation](@entry_id:141039) is $(k+2)(k+1) c_{k+2} = c_{k-1}$. If we adopt the convention that $c_j=0$ for any negative index $j$, this single relation holds for all $k \ge 0$. [@problem_id:2198597]

The process is similar for more complex equations. For $y'' - y' + xy = 0$, we substitute the series for $y$, $y'$, and $y''$ and re-index all terms to the power $x^n$:
- $y''(x) = \sum_{n=0}^{\infty} (n+2)(n+1) a_{n+2} x^n$
- $-y'(x) = -\sum_{n=0}^{\infty} (n+1) a_{n+1} x^n$
- $xy(x) = \sum_{n=1}^{\infty} a_{n-1} x^n$
Combining these yields $\sum_{n=0}^{\infty} [(n+2)(n+1)a_{n+2} - (n+1)a_{n+1}]x^n + \sum_{n=1}^{\infty} a_{n-1}x^n = 0$.
We handle the $n=0$ case separately: $(2)(1)a_2 - (1)a_1 = 0 \implies a_2 = \frac{1}{2}a_1$.
For $n \ge 1$, we can combine everything: $(n+2)(n+1)a_{n+2} - (n+1)a_{n+1} + a_{n-1} = 0$. This gives the [three-term recurrence relation](@entry_id:176845):
$$
a_{n+2} = \frac{(n+1)a_{n+1} - a_{n-1}}{(n+2)(n+1)} \quad \text{for } n \ge 1
$$
This relation allows us to compute all coefficients $a_n$ for $n \ge 2$ in terms of the first two, $a_0$ and $a_1$. [@problem_id:2198604]

### Constructing Solutions from Recurrence Relations

The [recurrence relation](@entry_id:141039) is the engine for generating the solution. The coefficients $c_0$ and $c_1$ are not determined by the relation; they are the arbitrary constants corresponding to the initial conditions $y(x_0)=c_0$ and $y'(x_0)=c_1$. All subsequent coefficients, $c_2, c_3, \dots$, are determined in terms of $c_0$ and $c_1$.

By grouping terms involving $c_0$ and terms involving $c_1$, we can explicitly write the general solution as $y(x) = c_0 y_1(x) + c_1 y_2(x)$, where $y_1(x)$ and $y_2(x)$ are the two fundamental series solutions.

Consider the equation $y'' - xy' - 2y = 0$. Following the series solution method, we arrive at the remarkably simple recurrence relation $a_{k+2} = \frac{a_k}{k+1}$ for $k \ge 0$. Let the initial conditions be $y(0)=c_0$ and $y'(0)=c_1$, which means $a_0=c_0$ and $a_1=c_1$. We can now generate the subsequent coefficients:
- For even indices: $a_2 = \frac{a_0}{1} = c_0$, $a_4 = \frac{a_2}{3} = \frac{c_0}{3}$, ...
- For odd indices: $a_3 = \frac{a_1}{2} = \frac{c_1}{2}$, $a_5 = \frac{a_3}{4} = \frac{c_1}{8}$, ...
The solution up to the $x^5$ term is:
$$
y(x) = a_0 + a_1x + a_2x^2 + a_3x^3 + a_4x^4 + a_5x^5 + \dots
$$
$$
y(x) = c_0 + c_1x + c_0x^2 + \frac{c_1}{2}x^3 + \frac{c_0}{3}x^4 + \frac{c_1}{8}x^5 + \dots
$$
Grouping by $c_0$ and $c_1$:
$$
y(x) = c_0\left(1 + x^2 + \frac{1}{3}x^4 + \dots\right) + c_1\left(x + \frac{1}{2}x^3 + \frac{1}{8}x^5 + \dots\right)
$$
Here we see the two fundamental solutions, $y_1(x)$ and $y_2(x)$, emerging. [@problem_id:2198609] [@problem_id:2198631]

For an **[initial value problem](@entry_id:142753) (IVP)**, the values of $c_0$ and $c_1$ are specified. For example, let's solve $(x^2+1)y'' + xy' - y = 0$ with $y(0)=2$ and $y'(0)=3$. Here, $a_0=2$ and $a_1=3$. The recurrence relation is found to be $a_{k+2} = -\frac{k^2-1}{(k+2)(k+1)}a_k$.
- $k=0: a_2 = -\frac{-1}{2 \cdot 1}a_0 = \frac{1}{2}(2) = 1$.
- $k=1: a_3 = -\frac{1-1}{3 \cdot 2}a_1 = 0$. Since $a_3=0$, the recurrence implies $a_5, a_7, \dots$ will also be zero.
- $k=2: a_4 = -\frac{2^2-1}{4 \cdot 3}a_2 = -\frac{3}{12}(1) = -\frac{1}{4}$.
- $k=4: a_6 = -\frac{4^2-1}{6 \cdot 5}a_4 = -\frac{15}{30}(-\frac{1}{4}) = \frac{1}{8}$.
The first few terms of the unique solution are:
$$
y(x) = 2 + 3x + x^2 - \frac{1}{4}x^4 + \frac{1}{8}x^6 + \dots
$$
This polynomial provides a good approximation of the solution near $x=0$. [@problem_id:2198643]

Finally, properties of the equation can sometimes reveal properties of the solution. Consider $y'' + \alpha x^2 y = 0$ with $y(0)=0, y'(0)=1$. The coefficient function $\alpha x^2$ is an [even function](@entry_id:164802). One can show that for such an equation, if the [initial conditions](@entry_id:152863) correspond to an odd function (i.e., $y(0)=0, y'(0) \neq 0$), the solution itself must be an [odd function](@entry_id:175940). This implies that all even-powered coefficients, $a_{2k}$, must be zero. Let's verify this with the [recurrence relation](@entry_id:141039). The method yields:
- $a_2 = 0, a_3=0$.
- For $k \ge 2$, the recurrence is $a_{k+2} = -\frac{\alpha}{(k+2)(k+1)}a_{k-2}$.
Since $a_0 = y(0) = 0$ and $a_2 = 0$, the recurrence relation $a_{k+2} = -\frac{\alpha}{(k+2)(k+1)}a_{k-2}$ implies that all subsequent even-indexed coefficients ($a_4, a_6, \dots$) must also be zero. For example, $a_4$ is proportional to $a_0$ and $a_6$ is proportional to $a_2$. Thus, all even coefficients are zero. The non-zero coefficients are the odd ones starting from $a_1=1$:
- From $a_3=0$, we get $a_7=0, a_{11}=0, \dots$.
- The only non-zero coefficients arise from $a_1=1$. The recurrence connects indices that differ by 4:
$$
a_5 = -\frac{\alpha}{5 \cdot 4}a_1 = -\frac{\alpha}{20}
$$
$$
a_9 = -\frac{\alpha}{9 \cdot 8}a_5 = -\frac{\alpha}{72}\left(-\frac{\alpha}{20}\right) = \frac{\alpha^2}{1440}
$$
This demonstrates how an initial analysis of symmetry can provide a valuable check on the results derived from the recurrence mechanism. [@problem_id:2198640]

In summary, the method of series solutions provides a robust and universal tool for solving a wide class of [linear differential equations](@entry_id:150365), transforming the analytical problem of finding a function into the algebraic problem of finding its coefficients.