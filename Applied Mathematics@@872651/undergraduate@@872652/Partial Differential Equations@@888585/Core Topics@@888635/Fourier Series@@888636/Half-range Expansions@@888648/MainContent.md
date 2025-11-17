## Introduction
In the study of physical phenomena on finite domains, such as the vibration of a guitar string or heat flow in a rod, we often need to represent an initial state or boundary condition using a series of [trigonometric functions](@entry_id:178918). While the standard theory of Fourier series is designed for [periodic functions](@entry_id:139337) on symmetric intervals like $[-L, L]$, many problems are naturally defined on a "half-range" interval, such as $[0, L]$. This presents a knowledge gap: how do we apply Fourier's powerful tools to these non-periodic functions on asymmetric intervals? The answer lies in the technique of **half-range expansions**.

This article provides a comprehensive guide to constructing and applying these crucial mathematical tools. By extending a function from $[0, L]$ to $[-L, L]$ as either an even or an [odd function](@entry_id:175940), we can generate a pure cosine or pure sine series, respectively. This choice is not arbitrary but is fundamentally linked to the physical constraints, or boundary conditions, of the problem at hand.

Throughout this text, you will learn the core principles of this method, its profound connections to other areas of science and engineering, and how to apply it yourself. First, the chapter on **Principles and Mechanisms** will detail the construction of [even and odd extensions](@entry_id:167036) and derive the formulas for the [sine and cosine series](@entry_id:164557) coefficients from the property of orthogonality. Next, **Applications and Interdisciplinary Connections** will explore how these series are indispensable for [solving partial differential equations](@entry_id:136409) and have surprising uses in [mathematical analysis](@entry_id:139664) and numerical methods. Finally, a series of **Hands-On Practices** will allow you to solidify your understanding by working through concrete examples and exploring the analytical properties of these expansions.

## Principles and Mechanisms

In the context of [solving partial differential equations](@entry_id:136409) (PDEs) on finite domains, we are often faced with the task of representing a function $f(x)$, defined on an interval $[0, L]$, as a Fourier series. However, the standard theory of Fourier series applies to [periodic functions](@entry_id:139337) defined over a symmetric interval such as $[-L, L]$. To bridge this gap, we introduce the concept of **half-range expansions**, which involve extending the function $f(x)$ from its original domain $[0, L]$ to the interval $[-L, L]$ in a specific manner, and then constructing the standard Fourier series for this extended function. The nature of this extension determines the type of series we obtain. The two most important extensions are the [even and odd extensions](@entry_id:167036), which give rise to the half-range cosine and sine series, respectively.

### The Even Extension and Half-Range Cosine Series

A natural way to extend a function $f(x)$ from $[0, L]$ to $[-L, L]$ is to create an **[even extension](@entry_id:172762)**, denoted $f_{even}(x)$. This function is constructed to be symmetric with respect to the y-axis.

**Definition: Even Extension**
The [even extension](@entry_id:172762) of a function $f(x)$ defined on $[0, L]$ is the function $f_{even}(x)$ defined on $[-L, L]$ by:
$$
f_{even}(x) = 
\begin{cases} 
f(x)  &\text{if } 0 \le x \le L \\
f(-x) &\text{if } -L \le x  0 
\end{cases}
$$
This can be written more compactly as $f_{even}(x) = f(|x|)$ for $x \in [-L, L]$. By construction, $f_{even}(-x) = f(|-x|) = f(|x|) = f_{even}(x)$, confirming it is an even function.

The full Fourier series of any even function on $[-L, L]$ contains only cosine terms (and a constant term), as the sine coefficients, which involve integrating an even function times an odd function (sine), are all zero. This specialized series is called the **half-range cosine series** of the original function $f(x)$.

**Definition: Half-Range Cosine Series**
The half-range cosine series of $f(x)$ on $[0, L]$ is given by:
$$
f(x) \sim \frac{A_0}{2} + \sum_{n=1}^\infty A_n \cos\left(\frac{n\pi x}{L}\right)
$$
where the coefficients are calculated as:
$$
A_n = \frac{2}{L} \int_0^L f(x) \cos\left(\frac{n\pi x}{L}\right) dx, \quad \text{for } n = 0, 1, 2, \dots
$$
It is a crucial insight that these coefficients are identical to the Fourier cosine coefficients for the full Fourier series of $f_{even}(x)$ on $[-L, L]$. This is because the integrand $f_{even}(x) \cos(\frac{n\pi x}{L})$ is an even function, and for any [even function](@entry_id:164802) $g(x)$, $\int_{-L}^L g(x) dx = 2 \int_0^L g(x) dx$ [@problem_id:2123865].

The series converges to a [periodic function](@entry_id:197949), let's call it $g(x)$, which is the [periodic extension](@entry_id:176490) of $f_{even}(x)$ with period $2L$. For any $x \in \mathbb{R}$, the value of $g(x)$ can be found by first mapping $x$ back to the fundamental interval $[-L, L]$ and then using the even symmetry.

For example, consider the function $f(x) = 3x$ on the interval $[0, 2]$. Here, $L=2$. The half-range cosine series represents its even, [periodic extension](@entry_id:176490), $g(x)$, which has a [fundamental period](@entry_id:267619) of $2L=4$. The function $g(x)$ is even, so $g(-x) = g(x)$. To find the value at $x=3$, we use its [periodicity](@entry_id:152486): $g(3) = g(3-4) = g(-1)$. By the [even extension](@entry_id:172762) rule, $g(-1) = g(1)$, and since $1$ is in the original interval, $g(1) = f(1) = 3 \cdot 1 = 3$. Thus, the series converges to $3$ at $x=3$ [@problem_id:2109595]. Similarly, if we construct the cosine series for $f(x)=x(2-x)$ on $[0,2]$ and wish to find its value $S(5.5)$, we use the period $4$: $S(5.5) = S(5.5 - 4) = S(1.5)$. Since $1.5 \in [0,2]$, $S(1.5) = f(1.5) = 1.5(2-1.5) = 0.75$ [@problem_id:2109615].

### The Odd Extension and Half-Range Sine Series

Alternatively, we can extend $f(x)$ to an **odd extension**, denoted $f_{odd}(x)$, which is constructed to have rotational symmetry about the origin.

**Definition: Odd Extension**
The odd extension of a function $f(x)$ defined on $[0, L]$ is the function $f_{odd}(x)$ defined on $[-L, L]$ by:
$$
f_{odd}(x) = 
\begin{cases} 
f(x)  \text{if } 0  x \le L \\
0  \text{if } x = 0 \\
-f(-x) \text{if } -L \le x  0 
\end{cases}
$$
This can be written compactly as $f_{odd}(x) = \text{sgn}(x)f(|x|)$ for $x \in [-L, L]$, where $\text{sgn}(x)$ is the sign function. By construction, $f_{odd}(-x) = -f_{odd}(x)$, confirming it is an [odd function](@entry_id:175940).

The full Fourier series of any odd function on $[-L, L]$ contains only sine terms, as the cosine coefficients (including $A_0$) are all zero. This gives rise to the **half-range sine series**.

**Definition: Half-Range Sine Series**
The half-range sine series of $f(x)$ on $[0, L]$ is given by:
$$
f(x) \sim \sum_{n=1}^\infty B_n \sin\left(\frac{n\pi x}{L}\right)
$$
where the coefficients are calculated as:
$$
B_n = \frac{2}{L} \int_0^L f(x) \sin\left(\frac{n\pi x}{L}\right) dx, \quad \text{for } n = 1, 2, 3, \dots
$$
As with the cosine series, these coefficients are identical to those for the full Fourier series of $f_{odd}(x)$ on $[-L, L]$, since the integrand $f_{odd}(x) \sin(\frac{n\pi x}{L})$ is an even function [@problem_id:2123865]. The sine series converges to the $2L$-[periodic extension](@entry_id:176490) of $f_{odd}(x)$.

### Orthogonality: The Foundation of Half-Range Expansions

The formulas for the coefficients $A_n$ and $B_n$ are not arbitrary; they are a direct consequence of the **orthogonality** of the [sine and cosine functions](@entry_id:172140) on the interval $[0, L]$. Two functions, $g(x)$ and $h(x)$, are said to be orthogonal on an interval $[a, b]$ if their inner product, defined as $\int_a^b g(x)h(x) dx$, is zero.

For the half-range cosine series, the set of basis functions $\{1, \cos(\frac{\pi x}{L}), \cos(\frac{2\pi x}{L}), \dots \}$ is orthogonal on $[0, L]$. This means:
$$
\int_0^L \cos\left(\frac{n\pi x}{L}\right) \cos\left(\frac{m\pi x}{L}\right) dx = 0, \quad \text{for } n \neq m
$$
The "length" or norm-squared of each basis function is:
$$
\int_0^L \cos^2\left(\frac{n\pi x}{L}\right) dx = \begin{cases} L/2 \text{if } n > 0 \\ L \text{if } n = 0 \end{cases}
$$
This orthogonality is the key. For example, to find a specific coefficient $A_m$, we multiply the entire cosine series by $\cos(\frac{m\pi x}{L})$ and integrate from $0$ to $L$. Due to orthogonality, every term in the infinite sum vanishes except for the one where $n=m$, allowing us to isolate and solve for $A_m$.

A physical analogy for orthogonality can be found in the concept of energy. Consider a function that is a superposition of two distinct modes, $f(x) = A \cos(\frac{n \pi x}{L}) + B \cos(\frac{m \pi x}{L})$, where $n \neq m$. The total "energy" of this signal over $[0, L]$ is $E = \int_0^L [f(x)]^2 dx$. Expanding the square leads to three integrals. The integrals of the squared terms yield $\frac{L}{2}A^2$ and $\frac{L}{2}B^2$, while the cross-term integral, $\int_0^L 2AB \cos(\frac{n \pi x}{L}) \cos(\frac{m \pi x}{L}) dx$, is zero due to orthogonality. Thus, the total energy is simply the sum of the energies of the individual components: $E = \frac{L}{2}(A^2 + B^2)$. There is no interference or cross-talk between the modes, which is a defining feature of an [orthogonal basis](@entry_id:264024) [@problem_id:2109565]. A similar orthogonality relationship holds for the sine basis functions, $\{\sin(\frac{n\pi x}{L})\}_{n=1}^\infty$, on the interval $[0, L]$.

### Applications and the Choice of Series in PDEs

The existence of two different series for the same function $f(x)$ on $[0, L]$ is not a redundancy but a powerful tool. The choice between a sine or cosine series is dictated by the **boundary conditions** of the physical problem being modeled, most commonly in the solution of PDEs like the heat equation or wave equation.

Consider the [one-dimensional heat equation](@entry_id:175487), $u_t = \kappa u_{xx}$, on a rod of length $L$. The solution methodology of separation of variables, $u(x,t) = X(x)T(t)$, leads to a spatial [boundary value problem](@entry_id:138753) for $X(x)$. The initial temperature distribution is given by $u(x,0) = f(x)$.

1.  **Homogeneous Dirichlet Conditions**: If the ends of the rod are held at zero temperature, we have $u(0,t) = u(L,t) = 0$. This imposes the conditions $X(0)=0$ and $X(L)=0$ on the spatial [eigenfunctions](@entry_id:154705). The functions that satisfy these are $\sin(\frac{n\pi x}{L})$. Therefore, to represent the initial condition $f(x)$, we must use a **half-range sine series**. The coefficients of this series become the initial amplitudes for each mode in the time-evolution solution. For instance, finding the coefficients for an initial profile like $f(x) = U_0$ for $0 \lt x \lt L/2$ and $0$ otherwise requires computing the sine series coefficients $B_n = \frac{2U_{0}}{n\pi}[1-\cos(\frac{n\pi}{2})]$ [@problem_id:2109575]. For a smoother initial profile like $f(x) = A(x-x^3)$ on $[0,1]$, the coefficients $B_n = -\frac{12A(-1)^{n}}{n^{3}\pi^{3}}$ determine the solution [@problem_id:2109622].

2.  **Homogeneous Neumann Conditions**: If the ends of the rod are insulated, there is zero heat flux, which translates to the conditions $u_x(0,t) = u_x(L,t) = 0$. This requires spatial [eigenfunctions](@entry_id:154705) with zero slope at the boundaries: $X'(0)=0$ and $X'(L)=0$. The functions that satisfy this are $\cos(\frac{n\pi x}{L})$. Consequently, for insulated boundaries, we must represent the initial condition $f(x)$ using a **half-range cosine series** [@problem_id:2095050].

As a practical example of calculating cosine coefficients, one might be tasked with representing $f(x) = \sin(x)$ on $[0, \pi]$ using cosines. This is not paradoxical; it is merely a representation valid *within that interval*. The calculation yields a series $\frac{2}{\pi} - \frac{4}{\pi} \sum_{k=1}^{\infty} \frac{\cos(2 k x)}{4 k^{2} - 1}$, demonstrating that any reasonably well-behaved function can be expressed in either form on the half-range [@problem_id:2103621].

### Convergence and Smoothness

The convergence properties of a half-range series on $[0, L]$ are inherited from the properties of the full Fourier series of its corresponding [periodic extension](@entry_id:176490).

The **Fourier Convergence Theorem** states that at any point where the [periodic extension](@entry_id:176490) is continuous, the series converges to the function's value. At a point of jump discontinuity, the series converges to the average of the left- and right-hand limits. For a half-range sine series of a function $f(x)$ with a jump from $V_1$ to $V_2$ at $x=a$, the series will converge to $\frac{V_1 + V_2}{2}$ at that point. This is because the odd extension preserves this jump within the interval $(0, L)$ [@problem_id:2109617].

Furthermore, the **smoothness** of the [periodic extension](@entry_id:176490) dictates the **rate of convergence** of the Fourier coefficients. A smoother function has faster-decaying coefficients, meaning fewer terms are needed for an accurate approximation.

Consider the function $f(x) = \pi - x$ on $[0, \pi]$.
*   Its **[even extension](@entry_id:172762)** results in a continuous, triangular-wave-like function. Since the function is continuous but its derivative is not (it has "corners"), its cosine coefficients $A_n$ will decay as $1/n^2$.
*   Its **odd extension** results in a discontinuous sawtooth-wave-like function, with jumps at $x=0, \pm \pi, \dots$. Because of these jumps, its sine coefficients $B_n$ will decay more slowly, as $1/n$.
The [periodic extension](@entry_id:176490) of the even case is continuous, while the [periodic extension](@entry_id:176490) of the odd case is not [@problem_id:2103635].

This principle can be explored quantitatively. Consider the function $f(x) = V_0(1-x/L)$ on $[0, L]$. Its odd extension has a jump discontinuity at $x=0$, whereas its [even extension](@entry_id:172762) is continuous but has a corner at $x=0$. A direct calculation reveals that the sine coefficients are $b_n = \frac{2V_0}{n\pi}$, decaying as $O(1/n)$. The cosine coefficients (for odd $n=2k-1$) are $a_{2k-1} = \frac{4V_0}{((2k-1)\pi)^2}$, decaying as $O(1/n^2)$. The faster decay of the cosine coefficients is a direct result of the superior smoothness of the even [periodic extension](@entry_id:176490). The precise relationship between these decay rates can even be captured in a limit, showing that for large odd indices $n$, the ratio $|a_n|/|b_n|$ behaves like $2/(n\pi)$, confirming the one-order-of-magnitude faster convergence for the cosine series in this case [@problem_id:2109569]. This connection between smoothness and convergence rate is a cornerstone of Fourier analysis.