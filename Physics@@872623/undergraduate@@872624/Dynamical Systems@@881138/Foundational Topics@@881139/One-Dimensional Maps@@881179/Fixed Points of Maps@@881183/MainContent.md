## Introduction
In the study of systems that evolve over time, from planetary orbits to population fluctuations, a fundamental question arises: do equilibrium states exist, and are they stable? These states of balance, known as **fixed points**, are central to the field of dynamical systems. Understanding how to find these points and predict whether a system will converge to them or diverge is key to unlocking the long-term behavior of complex processes. This article provides a comprehensive introduction to this vital concept. The first chapter, **Principles and Mechanisms**, lays the mathematical groundwork for defining, locating, and classifying the [stability of fixed points](@entry_id:265683). Building on this foundation, the second chapter, **Applications and Interdisciplinary Connections**, demonstrates the power of this analysis by exploring real-world models in fields ranging from biology and economics to physics and engineering. Finally, the **Hands-On Practices** section allows you to apply these techniques to concrete problems. We begin by establishing the core principles that govern these points of equilibrium.

## Principles and Mechanisms

In the study of discrete-time dynamical systems, a central concept is that of the **fixed point**. A fixed point represents a state of equilibrium, a configuration of the system that remains unchanged as time evolves. Understanding where these equilibria are and whether they are stable or unstable is fundamental to characterizing the long-term behavior of any dynamical system. This chapter will lay out the principles for finding and [classifying fixed points](@entry_id:266290) in both one- and multi-dimensional maps.

### Defining and Locating Fixed Points

A [discrete-time dynamical system](@entry_id:276520) is described by a function, or **map**, $f$, that dictates the evolution of the system's state. If the state at step $n$ is $x_n$, the state at the next step is $x_{n+1} = f(x_n)$.

A **fixed point** of the map $f$ is a state $x^*$ that maps to itself. Mathematically, it is a solution to the equation:
$$
f(x^*) = x^*
$$
Graphically, for a [one-dimensional map](@entry_id:264951) $f: \mathbb{R} \to \mathbb{R}$, fixed points are the values of $x$ where the graph of the function $y = f(x)$ intersects the line $y = x$.

Finding fixed points typically reduces to solving this algebraic equation. Consider a map given by the function $f(x) = \frac{5}{x+1} - 1$. To find its fixed points, we set $f(x) = x$ and solve [@problem_id:1676391]:
$$
x = \frac{5}{x+1} - 1
$$
Assuming $x \neq -1$, we can rearrange the equation:
$$
x+1 = \frac{5}{x+1}
$$
$$
(x+1)^2 = 5
$$
Taking the square root of both sides gives $x+1 = \pm\sqrt{5}$, which yields two distinct fixed points: $x^* = -1 + \sqrt{5}$ and $x^* = -1 - \sqrt{5}$.

The concept of a fixed point is not limited to real-valued functions. It applies to any system with a well-defined state space and evolution rule. For instance, in [cryptography](@entry_id:139166), one might analyze a map on a [finite set](@entry_id:152247) of integers. Consider an encryption scheme on the set $S = \{0, 1, \dots, N-1\}$ defined by $f(k) = (B - (k+A)) \pmod N$. A fixed point is an integer $k$ that remains unchanged by the encryption. Setting $f(k)=k$ leads to a [linear congruence](@entry_id:273259) [@problem_id:1676377]:
$$
k \equiv B - (k+A) \pmod N
$$
$$
2k \equiv B-A \pmod N
$$
For a system with parameters $N=30$, $A=7$, and $B=13$, this becomes $2k \equiv 6 \pmod{30}$. This congruence has solutions $k=3$ and $k=18$, which are vulnerabilities in such a system as they represent messages that are not altered by the encryption.

### The Existence of Fixed Points

While we can solve for fixed points algebraically, a more profound question is: under what conditions can we guarantee that a fixed point exists at all? For [continuous maps](@entry_id:153855) on closed intervals, a powerful [existence theorem](@entry_id:158097) provides the answer.

Consider a continuous function $f$ that maps a closed interval $[a, b]$ into itself, denoted $f: [a, b] \to [a, b]$. This means that for any input $x \in [a, b]$, the output $f(x)$ is also guaranteed to be in $[a, b]$. To investigate the existence of a fixed point, we can define an auxiliary function $g(x) = f(x) - x$ [@problem_id:1676383]. A fixed point of $f$ corresponds to a root of $g$, since $f(c)=c$ is equivalent to $g(c) = f(c) - c = 0$.

Since $f$ maps into the interval $[a, b]$, we know that $a \le f(x) \le b$ for all $x \in [a, b]$. Let's evaluate $g(x)$ at the endpoints of the interval:
- At $x=a$: $g(a) = f(a) - a$. Because $f(a) \ge a$, we have $g(a) \ge 0$.
- At $x=b$: $g(b) = f(b) - b$. Because $f(b) \le b$, we have $g(b) \le 0$.

We have a continuous function $g(x)$ on $[a, b]$ such that $g(a)$ is non-negative and $g(b)$ is non-positive. The **Intermediate Value Theorem** states that if a continuous function takes on two values, it must also take on all values in between. Therefore, there must exist at least one value $c \in [a, b]$ for which $g(c) = 0$. This proves that every [continuous map](@entry_id:153772) from a closed interval to itself must have at least one fixed point. This result is a one-dimensional case of the celebrated **Brouwer's Fixed-Point Theorem**.

### Stability of Fixed Points in One-Dimensional Maps

Finding fixed points is only part of the story. The next crucial step is to determine their **stability**. A fixed point $x^*$ is **stable** (or **attracting**) if any iteration starting sufficiently close to $x^*$ converges towards it. It is **unstable** (or **repelling**) if any iteration starting arbitrarily close (but not exactly at) $x^*$ moves away from it.

The stability of a fixed point $x^*$ is determined by the local behavior of the map $f$, which is governed by its derivative, $f'(x^*)$. Let $x_n = x^* + \epsilon_n$ be a point near the fixed point, where $\epsilon_n$ is a small perturbation. The next state is:
$$
x_{n+1} = f(x_n) = f(x^* + \epsilon_n)
$$
Using a first-order Taylor expansion around $x^*$, we get:
$$
x_{n+1} \approx f(x^*) + f'(x^*) \epsilon_n
$$
Since $f(x^*) = x^*$, we have $x_{n+1} \approx x^* + f'(x^*) \epsilon_n$. The new perturbation is $\epsilon_{n+1} = x_{n+1} - x^* \approx f'(x^*) \epsilon_n$. The perturbation $\epsilon_n$ is multiplied by the factor $f'(x^*)$ at each step. This leads to the **Linear Stability Criterion**:

- If $|f'(x^*)|  1$, the perturbation shrinks at each step, $|\epsilon_{n+1}|  |\epsilon_n|$, and the iterates converge to $x^*$. The fixed point is **stable**.
- If $|f'(x^*)| > 1$, the perturbation grows, $|\epsilon_{n+1}| > |\epsilon_n|$, and the iterates move away from $x^*$. The fixed point is **unstable**.
- If $|f'(x^*)| = 1$, the linear analysis is inconclusive, and a more detailed, [nonlinear analysis](@entry_id:168236) is required. Such a point is called **non-hyperbolic**.

As a classic example, consider the **logistic map**, $f(x) = rx(1-x)$, a foundational model in population dynamics. For $r > 1$, it has a positive fixed point at $x^* = 1 - 1/r$. The derivative is $f'(x) = r(1-2x)$. Evaluating at the fixed point gives $f'(x^*) = r(1 - 2(1 - 1/r)) = 2-r$. The stability condition $|f'(x^*)|  1$ becomes $|2-r|  1$, which is equivalent to $-1  2-r  1$. This inequality holds for $1  r  3$. Thus, the positive fixed point of the [logistic map](@entry_id:137514) is stable for $r \in (1, 3)$ [@problem_id:1676393].

The value of the derivative not only determines stability but also the nature and [rate of convergence](@entry_id:146534) or divergence.
Consider two simple linear maps modeling decay processes: Process A, $f_A(x) = 0.5x$, and Process B, $f_B(x) = -0.75x$ [@problem_id:1676380]. Both have a [stable fixed point](@entry_id:272562) at $x^*=0$.
- For Process A, $f_A'(0) = 0.5$. Since $0  f_A'(0)  1$, iterates starting near 0 will converge to 0 **monotonically** (from the same side). The magnitude of the deviation from the fixed point is halved at each step.
- For Process B, $f_B'(0) = -0.75$. Since $-1  f_B'(0)  0$, iterates will also converge, but they will do so in an **oscillatory** manner, alternating sides of the fixed point at each step.
- The **[rate of convergence](@entry_id:146534)** is determined by $|f'(x^*)|$. A value closer to zero implies faster convergence. Here, $|0.5|  |-0.75|$, so Process A converges faster than Process B. The time to reach a certain fraction of the initial deviation depends on the logarithm of $|f'(x^*)|$.

Stability can also depend on a system parameter. For the map $f(x) = \lambda x \exp(-x^2)$, the non-trivial fixed points $x^* = \pm\sqrt{\ln\lambda}$ exist for $\lambda > 1$. The derivative at these points is $f'(x^*) = 1 - 2\ln\lambda$. Stability is lost when $|f'(x^*)| = 1$. This occurs when $1 - 2\ln\lambda = -1$, which implies $\ln\lambda = 1$, or $\lambda = \exp(1)$ [@problem_id:1708893]. At this parameter value, the system undergoes a **bifurcation**, where the qualitative nature of its dynamics changes.

When the linear stability test is inconclusive ($|f'(x^*)|=1$), we must examine the nonlinear terms. For the map $f(x) = x + x^2$, the only fixed point is $x^*=0$, and $f'(0) = 1$ [@problem_id:1676394]. To analyze its stability, we look at the sign of the displacement, $f(x)-x = x^2$.
- For any small $x > 0$, $f(x) - x = x^2 > 0$, meaning $f(x) > x$. Iterates move away from the fixed point on the right side.
- For any small $x  0$, $f(x) - x = x^2 > 0$, meaning $f(x) > x$. Since $x$ is negative, this means $f(x)$ is closer to 0 than $x$ is (e.g., if $x=-0.1$, $f(x)=-0.09$). Iterates move towards the fixed point from the left side.
This type of fixed point, which is attracting from one side and repelling from the other, is called **semi-stable**.

### Fixed Points in Higher Dimensions

The concepts of [fixed points and stability](@entry_id:268047) extend naturally to higher-dimensional systems, where the state is a vector $\vec{x} \in \mathbb{R}^n$. A fixed point $\vec{x}^*$ satisfies $\vec{x}^* = \vec{f}(\vec{x}^*)$.

The simplest multidimensional systems are **decoupled**. For example, consider a 2D system modeling two non-interacting species with populations $x$ and $y$ [@problem_id:1676569]:
$$
x_{k+1} = f(x_k) = 1.5 x_k(2 - x_k)
$$
$$
y_{k+1} = g(y_k) = 4 y_k^2
$$
A fixed point $(x^*, y^*)$ must satisfy $x^*=f(x^*)$ and $y^*=g(y^*)$ simultaneously. The fixed points of the 2D system are simply the Cartesian products of the fixed points of the individual 1D maps. For the map $f$, the fixed points are $x^*=0$ and $x^*=2-1/1.5 = 4/3$. For the map $g$, the fixed points are $y^*=0$ and $y^*=1/4$. Combining these yields the four fixed points of the 2D system: $(0,0)$, $(4/3, 0)$, $(0, 1/4)$, and $(4/3, 1/4)$.

For general, coupled systems, the stability analysis requires linearizing the vector-valued function $\vec{f}$ at the fixed point $\vec{x}^*$. This is accomplished using the **Jacobian matrix**, $J$, which is the multidimensional analogue of the derivative. For a 2D map $(x_{n+1}, y_{n+1}) = (f_1(x_n, y_n), f_2(x_n, y_n))$, the Jacobian matrix is:
$$
J(x,y) = \begin{pmatrix} \frac{\partial f_1}{\partial x}  \frac{\partial f_1}{\partial y} \\ \frac{\partial f_2}{\partial x}  \frac{\partial f_2}{\partial y} \end{pmatrix}
$$
The local dynamics near a fixed point $\vec{x}^*$ are governed by the linear map $\vec{\epsilon}_{n+1} \approx J(\vec{x}^*) \vec{\epsilon}_n$, where $\vec{\epsilon}_n = \vec{x}_n - \vec{x}^*$. The stability is determined by the **eigenvalues** ($\lambda_i$) of the Jacobian matrix evaluated at the fixed point.

A fixed point $\vec{x}^*$ is **stable** if and only if all eigenvalues of $J(\vec{x}^*)$ have a magnitude less than 1 (i.e., $|\lambda_i|  1$ for all $i$). If any eigenvalue has a magnitude greater than 1, the fixed point is **unstable**.

Let's classify the fixed point at $(0,0)$ for the map $x_{n+1} = \frac{7}{4}x_n - \frac{1}{2}y_n^2$, $y_{n+1} = \frac{1}{2}y_n + \frac{1}{4}x_n^2$ [@problem_id:1676565]. The Jacobian at the origin is:
$$
J(0,0) = \begin{pmatrix} 7/4  0 \\ 0  1/2 \end{pmatrix}
$$
The eigenvalues are the diagonal entries, $\lambda_1 = 7/4$ and $\lambda_2 = 1/2$. Since $|\lambda_1| = 1.75 > 1$ and $|\lambda_2| = 0.5  1$, there is one expanding direction and one contracting direction. This type of [unstable fixed point](@entry_id:269029) is called a **saddle point**. Iterates are repelled from the fixed point along the eigenvector associated with $\lambda_1$ but are attracted towards it along the eigenvector associated with $\lambda_2$.

The classification of fixed points in 2D is richer than in 1D:
- **Stable/Unstable Node**: Eigenvalues are real and satisfy $|\lambda_1|, |\lambda_2|  1$ (stable) or $|\lambda_1|, |\lambda_2| > 1$ (unstable).
- **Saddle Point**: Eigenvalues are real, with one having magnitude greater than 1 and the other less than 1.
- **Stable/Unstable Spiral (or Focus)**: Eigenvalues are a [complex conjugate pair](@entry_id:150139), with magnitude $|\lambda|  1$ (stable) or $|\lambda| > 1$ (unstable). Iterates spiral in or out.
- **Center**: Eigenvalues are a [complex conjugate pair](@entry_id:150139) with magnitude $|\lambda| = 1$. The [linear approximation](@entry_id:146101) predicts rotation on ellipses.

As in the 1D case, a fixed point is **non-hyperbolic** if any eigenvalue has a magnitude of exactly one. These points represent boundaries in parameter space where the stability of a fixed point can change, leading to bifurcations. For a 2D system, we can identify these boundaries in the plane of the Jacobian's trace $\tau = \text{tr}(J)$ and determinant $\Delta = \det(J)$, which relate to the eigenvalues by $\lambda_1+\lambda_2=\tau$ and $\lambda_1\lambda_2=\Delta$. A non-hyperbolic condition arises if [@problem_id:1676557]:
1.  An eigenvalue is $\lambda = 1$. The characteristic equation $\lambda^2 - \tau\lambda + \Delta = 0$ gives $1 - \tau + \Delta = 0$, or $\Delta = \tau - 1$.
2.  An eigenvalue is $\lambda = -1$. This gives $1 + \tau + \Delta = 0$, or $\Delta = -\tau - 1$.
3.  The eigenvalues are a [complex conjugate pair](@entry_id:150139) on the unit circle ($|\lambda|=1, \lambda \notin \mathbb{R}$). In this case, their product is $\Delta = \lambda\bar{\lambda} = |\lambda|^2 = 1$.

These three lines, $\Delta = \tau - 1$, $\Delta = -\tau - 1$, and $\Delta = 1$, form the critical boundaries in the [trace-determinant plane](@entry_id:163457) that separate regions of different dynamical behavior. Crossing one of these lines as a system parameter is varied corresponds to a fundamental change—a bifurcation—in the system's dynamics.