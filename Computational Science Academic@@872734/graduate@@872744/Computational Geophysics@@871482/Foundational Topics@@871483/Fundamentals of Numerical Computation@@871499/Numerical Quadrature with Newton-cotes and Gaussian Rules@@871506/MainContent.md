## Introduction
In [computational geophysics](@entry_id:747618) and many other scientific fields, [definite integrals](@entry_id:147612) are fundamental to describing physical phenomena, from calculating a gravitational anomaly to modeling seismic wave travel times. However, finding an exact analytical solution for these integrals is often impossible. Numerical quadrature provides a robust and essential framework for approximating these integrals, replacing the continuous problem with a finite, weighted sum of function values. This article delves into the two cornerstone families of these methods: the intuitive, equispaced Newton-Cotes rules and the powerful, optimal Gaussian [quadrature rules](@entry_id:753909).

Our exploration is structured to build from fundamental theory to practical application. The first chapter, **"Principles and Mechanisms,"** lays the theoretical groundwork. We will derive familiar rules like the Trapezoidal and Simpson's rules, explore the concepts of algebraic accuracy and numerical stability, and uncover the profound connection between Gaussian quadrature and orthogonal polynomials. This section establishes why Gaussian methods offer superior accuracy and robustness for a given computational cost.

Next, **"Applications and Interdisciplinary Connections"** bridges theory and practice. We will see how these rules are applied to solve real-world problems in geophysics and how to devise advanced strategies for tackling challenging integrals involving singularities, infinite domains, or sharp features. This chapter highlights the versatility of quadrature techniques and their impact on fields ranging from [climate science](@entry_id:161057) to Bayesian inference.

Finally, the **"Hands-On Practices"** section provides an opportunity to translate theory into code, offering practical exercises that reinforce the core concepts and build essential implementation skills. Our journey begins by dissecting the fundamental mechanics that define and differentiate these powerful numerical tools.

## Principles and Mechanisms

### Fundamental Concepts of Numerical Quadrature

In many areas of [computational geophysics](@entry_id:747618), from [seismic modeling](@entry_id:754642) to potential [field theory](@entry_id:155241), we are confronted with the task of evaluating [definite integrals](@entry_id:147612). When an analytical solution for an integral is unavailable or impractical, we turn to numerical methods. **Numerical quadrature** provides a framework for approximating a [definite integral](@entry_id:142493) by a finite weighted sum of function values at specific points within the domain of integration.

Formally, a numerical quadrature rule for approximating the integral $I[f] = \int_a^b f(x) \,dx$ is a linear functional, denoted $Q[f]$, of the form:
$$
Q[f] = \sum_{i=1}^{n} w_i f(x_i)
$$
Here, the points $x_i \in [a, b]$ are called the **nodes** or **abscissas** of the rule, and the coefficients $w_i$ are the corresponding **weights**. The choice of these $n$ nodes and $n$ weights defines the specific [quadrature rule](@entry_id:175061). The linearity of this functional is evident, as for any scalars $\alpha, \beta$ and functions $f, g$, it holds that $Q[\alpha f + \beta g] = \alpha Q[f] + \beta Q[g]$ [@problem_id:3612187].

A primary metric for the quality of a [quadrature rule](@entry_id:175061) is its **[degree of exactness](@entry_id:175703)**, also known as **algebraic accuracy**. This is defined as the largest integer $m$ such that the rule exactly integrates every polynomial of degree less than or equal to $m$. That is, $Q[p] = I[p]$ for all polynomials $p(x)$ with $\deg(p) \le m$, but there exists at least one polynomial of degree $m+1$ for which the rule is not exact [@problem_id:3612187]. This focus on polynomials is not arbitrary; polynomial approximation is the bedrock of much of [numerical analysis](@entry_id:142637), and the ability of a rule to integrate polynomials exactly is a strong indicator of its performance on smooth functions that can be well-approximated by polynomials.

Many [quadrature rules](@entry_id:753909), including the Newton-Cotes family, are **interpolatory**. The core idea is to first approximate the integrand $f(x)$ by a polynomial $p_{n-1}(x)$ that interpolates $f(x)$ at the $n$ chosen nodes. The integral of the function is then approximated by the exact integral of this interpolating polynomial:
$$
\int_a^b f(x) \,dx \approx \int_a^b p_{n-1}(x) \,dx
$$
If $p_{n-1}(x) = \sum_{i=1}^{n} f(x_i) \ell_i(x)$, where $\ell_i(x)$ are the Lagrange basis polynomials, then the weights of the [quadrature rule](@entry_id:175061) are simply the [definite integrals](@entry_id:147612) of these basis polynomials: $w_i = \int_a^b \ell_i(x) \,dx$ [@problem_id:3612206]. A direct consequence of this construction is that an $n$-point interpolatory rule will have a [degree of exactness](@entry_id:175703) of at least $n-1$, because if $f(x)$ is itself a polynomial of degree at most $n-1$, its unique [interpolating polynomial](@entry_id:750764) of that degree is $f(x)$ itself, rendering the approximation exact [@problem_id:3612142].

### The Newton-Cotes Family: Rules Based on Equispaced Nodes

The simplest and most intuitive family of interpolatory [quadrature rules](@entry_id:753909) is the **Newton-Cotes** family, which is characterized by the use of equally spaced nodes over the integration interval $[a,b]$. These rules are categorized as **closed** if they include the endpoints $a$ and $b$ as nodes, and **open** if they do not.

#### Derivation and Properties of Basic Rules

We can derive the weights for any Newton-Cotes rule from first principles by enforcing the condition of exactness for a [basis of polynomials](@entry_id:148579). Let's demonstrate this for the two most common closed rules.

Consider the simplest case: a 2-node rule, which uses the endpoints $x_0=a$ and $x_1=b$. We seek weights $w_0$ and $w_1$ such that $\int_a^b f(x)\,dx \approx w_0 f(a) + w_1 f(b)$. We enforce [exactness](@entry_id:268999) for polynomials up to degree 1, using the basis $\{1, x\}$.
- For $f(x)=1$: $\int_a^b 1 \,dx = b-a$. The rule gives $w_0(1) + w_1(1) = w_0+w_1$. Thus, $w_0+w_1 = b-a$.
- For $f(x)=x$: $\int_a^b x \,dx = \frac{b^2-a^2}{2}$. The rule gives $w_0(a) + w_1(b)$. Thus, $aw_0+bw_1 = \frac{b^2-a^2}{2}$.
Solving this $2 \times 2$ system yields the weights $w_0 = w_1 = \frac{b-a}{2}$. This is the well-known **[trapezoidal rule](@entry_id:145375)**.
To find its [degree of exactness](@entry_id:175703), we test it on $f(x)=x^2$. The exact integral is $\frac{b^3-a^3}{3}$, while the rule gives $\frac{b-a}{2}(a^2+b^2)$. These are not equal in general, so the [degree of exactness](@entry_id:175703) is $1$ [@problem_id:3612142].

Next, consider the 3-node rule with nodes at $a$, the midpoint $\frac{a+b}{2}$, and $b$. This is **Simpson's rule**. Deriving the weights $w_0, w_1, w_2$ by enforcing exactness for $\{1, x, x^2\}$ is algebraically simpler on a reference interval, say $[-1, 1]$, with nodes at $-1, 0, 1$. The [integral transforms](@entry_id:186209) as $\int_a^b f(x) \,dx = \frac{b-a}{2} \int_{-1}^1 g(t) \,dt$, where $g(t) = f(x(t))$. Solving for the weights on $[-1,1]$ and scaling them by $\frac{b-a}{2}$ yields the weights for the interval $[a,b]$:
$$
w_0 = \frac{b-a}{6}, \quad w_1 = \frac{4(b-a)}{6} = \frac{2(b-a)}{3}, \quad w_2 = \frac{b-a}{6}
$$
By construction, Simpson's rule is exact for polynomials up to degree 2. However, a surprising result emerges when testing it on $f(x)=x^3$. On the interval $[0,1]$, for instance, the exact integral of $x^3$ is $\frac{1}{4}$. Simpson's rule gives $\frac{1}{6}(0^3 + 4(\frac{1}{2})^3 + 1^3) = \frac{1}{6}(0 + \frac{4}{8} + 1) = \frac{1}{4}$. The rule is exact for $x^3$ [@problem_id:3612187, @problem_id:3612186]. Testing on $x^4$ reveals it is not exact. Thus, the [degree of exactness](@entry_id:175703) of Simpson's rule is $3$. This "bonus" [degree of precision](@entry_id:143382) is a general feature of closed Newton-Cotes rules with an odd number of nodes ($n$ is odd, degree is $n$).

#### Composite Quadrature Rules

One might assume that to increase accuracy, one should simply use a Newton-Cotes rule with a very high number of nodes. However, as we will see later, this is a flawed strategy. The proper way to increase accuracy is to subdivide the integration interval $[a,b]$ into smaller panels and apply a simple, low-degree rule to each panel. This is the essence of **composite quadrature**.

Let the interval $[a,b]$ be divided into $N$ panels of uniform width $h = (b-a)/N$. The total integral is the sum of the integrals over each panel. A composite rule approximates the total integral by summing the results of a basic rule applied to each panel.

The error of such a scheme is analyzed in two parts. The **[local truncation error](@entry_id:147703)** is the error committed on a single panel of width $h$. The **[global truncation error](@entry_id:143638)** is the total error over the entire interval $[a,b]$, which is the sum of the $N$ local errors [@problem_id:3612199]. If the local error on a panel is proportional to some power of its width, say $O(h^{p+1})$, then the global error accumulates. Since there are $N = (b-a)/h$ panels, the global error is bounded by $N \times O(h^{p+1}) = O(h^p)$. The notation $E(h) = O(h^p)$ formally means that there exist constants $M > 0$ and $h_0 > 0$ such that the [global error](@entry_id:147874) magnitude $|E(h)|$ is bounded by $M h^p$ for all $h \le h_0$ [@problem_id:3612199].

For the composite Simpson's rule, the [local error](@entry_id:635842) on a panel of width $h$ is $O(h^5)$. The [global error](@entry_id:147874) over $[a,b]$ is therefore $O(h^4)$, provided the integrand is sufficiently smooth (specifically, $f \in C^4([a,b])$) [@problem_id:3612199]. This powerful scaling means that halving the panel width $h$ reduces the [global error](@entry_id:147874) by a factor of approximately $16$.

### The Gaussian Quadrature Family: Rules Based on Optimal Nodes

The Newton-Cotes approach fixes the node locations to be equispaced, leaving only the weights as free parameters. An $n$-point rule has $n$ free parameters, which allows us to enforce [exactness](@entry_id:268999) for polynomials up to degree $n-1$. A profound insight leads to a more powerful class of methods: what if we also treat the $n$ node locations as free parameters? This gives us $2n$ degrees of freedom ($n$ nodes and $n$ weights), which we can use to satisfy $2n$ constraints. This is the foundation of **Gaussian quadrature**.

The central result is that by optimally choosing both the nodes and weights, an $n$-point Gaussian [quadrature rule](@entry_id:175061) can achieve a **maximal [degree of exactness](@entry_id:175703) of $2n-1$** [@problem_id:3426593]. This is a remarkable improvement over Newton-Cotes rules. For example, a 2-point Gauss-Legendre rule has a [degree of exactness](@entry_id:175703) of $2(2)-1=3$, the same as the 3-point Simpson's rule, but using one fewer function evaluation.

#### Derivation and Properties

Let's derive the 2-point Gauss-Legendre rule on the interval $[-1,1]$ from first principles. We seek two nodes, $x_1, x_2$, and two weights, $w_1, w_2$, to exactly integrate polynomials up to degree $3$. We enforce exactness for the monomial basis $\{1, x, x^2, x^3\}$:
- $f(x)=1$: $\int_{-1}^1 1\,dx=2 \implies w_1+w_2=2$
- $f(x)=x$: $\int_{-1}^1 x\,dx=0 \implies w_1x_1+w_2x_2=0$
- $f(x)=x^2$: $\int_{-1}^1 x^2\,dx=\frac{2}{3} \implies w_1x_1^2+w_2x_2^2=\frac{2}{3}$
- $f(x)=x^3$: $\int_{-1}^1 x^3\,dx=0 \implies w_1x_1^3+w_2x_2^3=0$

This is a non-linear system of four equations. We can exploit the symmetry of the integration interval. For an optimal rule, we expect symmetric nodes, $x_1 = -x_2$, and equal weights, $w_1 = w_2$.
- From the first equation, $w_1+w_1=2 \implies w_1=1$, so $w_2=1$.
- The second and fourth equations are automatically satisfied by symmetry.
- The third equation becomes $1(-x_2)^2 + 1(x_2)^2 = \frac{2}{3} \implies 2x_2^2 = \frac{2}{3} \implies x_2^2 = \frac{1}{3}$.
Thus, the nodes are $x_1 = -1/\sqrt{3}$ and $x_2 = 1/\sqrt{3}$.
This 2-point rule, with nodes $\pm 1/\sqrt{3}$ and weights equal to 1, exactly integrates all polynomials up to degree 3, but fails for degree 4 [@problem_id:3612158, @problem_id:3612187]. For composite rules, an $n$-point Gauss-Legendre quadrature has a [local error](@entry_id:635842) of $O(h^{2n+1})$, leading to a [global error](@entry_id:147874) of $O(h^{2n})$ [@problem_id:3612199].

#### The Role of Orthogonal Polynomials

Solving large [non-linear systems](@entry_id:276789) for every rule is not practical. The general theory of Gaussian quadrature provides a beautiful and profound connection to **[orthogonal polynomials](@entry_id:146918)**. For an integral of the form $\int_a^b w(x) f(x) \,dx$, where $w(x)$ is a non-negative weight function, the $n$ optimal nodes for the corresponding Gaussian [quadrature rule](@entry_id:175061) are precisely the $n$ roots of the degree-$n$ polynomial that is orthogonal to all polynomials of lesser degree with respect to the inner product $\langle p,q \rangle = \int_a^b w(x) p(x) q(x) \,dx$. These roots are guaranteed to be real, distinct, and to lie within the interval $(a,b)$.

This insight leads to a "zoo" of powerful [quadrature rules](@entry_id:753909), each tailored to a specific integral structure by absorbing a key part of the integrand into the weight function $w(x)$ [@problem_id:3612207]. The three most common families are:
1.  **Gauss-Legendre Quadrature**: For the weight function $w(x)=1$ on the finite interval $\Omega=[-1,1]$. It is the method of choice for generic integrals over finite domains, which can always be mapped to $[-1,1]$ via a [linear transformation](@entry_id:143080). A typical geophysical application is integrating angle-dependent quantities, like [reflection coefficients](@entry_id:194350), over a finite range of angles.
2.  **Gauss-Laguerre Quadrature**: For the weight function $w(x)=e^{-x}$ on the semi-infinite interval $\Omega=[0, \infty)$. It excels at evaluating integrals with exponential decay, such as Laplace transforms or wavenumber integrals in attenuating media.
3.  **Gauss-Hermite Quadrature**: For the weight function $w(x)=e^{-x^2}$ on the entire real line $\Omega=(-\infty, \infty)$. This is ideal for integrals with a Gaussian decay factor, which arise in Fourier analysis, diffusion problems, and Gaussian beam modeling.

The general strategy is to identify the structure of the integral, perform a change of variables to match one of these [canonical forms](@entry_id:153058), and apply the corresponding highly-accurate Gaussian rule to the remaining smooth part of the integrand.

### Comparative Analysis and Practical Considerations

The choice between Newton-Cotes and Gaussian quadrature involves a fundamental trade-off between simplicity and power. For a fixed number of function evaluations, Gaussian quadrature is vastly superior in terms of algebraic accuracy. However, this power comes from a more complex theoretical foundation.

#### Stability and Weight Properties

A crucial difference between the two families lies in the behavior of their weights, which has profound implications for [numerical stability](@entry_id:146550).
For high-degree Newton-Cotes rules (specifically, for $n=8$ and for $n \ge 10$ in the closed case), some of the weights $w_i$ become **negative** [@problem_id:3426593]. The reason for this lies in the behavior of the Lagrange basis polynomials $\ell_i(x)$ for equally spaced nodes. For large $n$, these polynomials exhibit wild oscillations, especially near the endpoints of the interval—a manifestation of **Runge's phenomenon**. Since the weights are the integrals of these polynomials, $w_i = \int_a^b \ell_i(x) \,dx$, large negative lobes in $\ell_i(x)$ can lead to negative weights [@problem_id:3612206].

The presence of negative weights is a major cause of numerical instability. To see why, consider the sensitivity of the quadrature sum $Q[f] = \sum w_i f(x_i)$ to small perturbations in the function values. The absolute error in the sum due to perturbations $|\delta f(x_i)| \le \varepsilon$ is bounded by:
$$
|\Delta Q| \le \sum_{i=1}^n |w_i| |\delta f(x_i)| \le \varepsilon \sum_{i=1}^n |w_i|
$$
The quantity $\sum_{i=1}^n |w_i|$ is the **operator norm** of the quadrature functional and acts as a condition number for the summation [@problem_id:3612206]. If all weights are positive, this sum is simply $\sum w_i = b-a$ (since the rule is exact for $f(x)=1$). If some weights are negative, however, the sum of absolute values $\sum |w_i|$ will be strictly greater than $b-a$. For high-degree Newton-Cotes rules, this sum grows exponentially with $n$, leading to catastrophic amplification of any input noise or [rounding errors](@entry_id:143856).

In stark contrast, a cornerstone of Gaussian quadrature theory is that for any positive weight function $w(x)$, all the [quadrature weights](@entry_id:753910) $W_i$ are **strictly positive** [@problem_id:3426593, @problem_id:3612206]. This guarantees that the operator norm is minimal: $\sum |W_i| = \sum W_i = \int_a^b w(x)\,dx$. This property endows Gaussian quadrature with exceptional [numerical stability](@entry_id:146550), making it robust against perturbations in the function values.

#### The Meaning of Optimality

Gaussian quadrature is often called "optimal." It is crucial to understand that this optimality refers specifically to achieving the **maximal [degree of exactness](@entry_id:175703)** for a given number of nodes. It is the solution to a finite-dimensional moment-[matching problem](@entry_id:262218) in [polynomial space](@entry_id:269905). There are other notions of optimality, such as finding a rule that minimizes the [worst-case error](@entry_id:169595) for functions belonging to a certain [function space](@entry_id:136890) (e.g., $L^2$ or Sobolev spaces) with a specified norm. This is an infinite-dimensional problem of "optimal recovery," and Gaussian quadrature is generally not the solution to this different type of optimization problem [@problem_id:3612167].

#### Practical Computation of Gaussian Rules

The nodes and weights of Gaussian [quadrature rules](@entry_id:753909) are not found by solving large nonlinear systems. The modern, standard method is the **Golub-Welsch algorithm** [@problem_id:3612157]. This algorithm leverages the [three-term recurrence relation](@entry_id:176845) that all families of orthogonal polynomials satisfy. The coefficients of this [recurrence relation](@entry_id:141039) can be used to construct a real, symmetric, [tridiagonal matrix](@entry_id:138829) known as the **Jacobi matrix**, $J_n$.

The power of this approach lies in a remarkable result from numerical linear algebra:
- The **eigenvalues** of the $n \times n$ Jacobi matrix $J_n$ are precisely the $n$ Gaussian quadrature **nodes** $x_i$.
- The corresponding **weights** $w_i$ can be computed from the first components of the normalized eigenvectors of $J_n$. Specifically, $w_i = \mu_0 v_{1i}^2$, where $\mu_0 = \int_a^b w(x)\,dx$ is the total mass and $v_{1i}$ is the first component of the eigenvector associated with the eigenvalue $x_i$ [@problem_id:3612157].

Casting the problem this way is highly advantageous. Computing the [eigenvalues and eigenvectors](@entry_id:138808) of a [symmetric tridiagonal matrix](@entry_id:755732) is a standard, well-understood problem for which extremely fast and stable algorithms exist. The computational cost scales as $O(n^2)$, not $O(n^3)$ as for a general [symmetric matrix](@entry_id:143130). This makes the Golub-Welsch algorithm a backward-stable and highly robust procedure, far superior to attempting to find the roots of high-degree polynomials directly using methods like Newton's method, which would require excellent initial guesses to find all distinct roots [@problem_id:3612157]. For moderate $n$, this algorithm is the method of choice. Only for extremely large $n$ do specialized [asymptotic methods](@entry_id:177759) become competitive.