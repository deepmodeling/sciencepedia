## Introduction
Fractional calculus, the extension of [differentiation and integration](@entry_id:141565) to non-integer orders, has emerged from a historical mathematical curiosity into an indispensable tool for scientists and engineers. Its unique strength lies in the ability of fractional operators to describe "memory" and [hereditary properties](@entry_id:153191), where the future state of a system depends on its entire past history. Standard integer-order differential equations often fall short in modeling such complex phenomena, which are ubiquitous in fields ranging from viscoelasticity to anomalous diffusion. Fractional differential equations (FDEs) fill this knowledge gap, providing a more nuanced and accurate language to describe the real world.

This article provides a comprehensive introduction to the principles and methods for solving simple FDEs. Across the following chapters, you will gain a solid foundation in this fascinating subject. The journey begins in the **Principles and Mechanisms** chapter, where we will rigorously define the fractional integral and the various [fractional derivatives](@entry_id:177809), explore their properties, and uncover the critical differences between them. Next, the **Applications and Interdisciplinary Connections** chapter will showcase the remarkable utility of FDEs by exploring their role in modeling complex systems across physics, engineering, biology, and more. Finally, you will apply your knowledge in the **Hands-On Practices** section, working through guided problems that reinforce key concepts and solution techniques. By the end, you will be equipped to understand and begin solving fundamental problems in the world of [fractional calculus](@entry_id:146221).

## Principles and Mechanisms

Having established the historical context and broad applications of fractional calculus in the preceding chapter, we now turn to a rigorous examination of its foundational principles and operational mechanics. This chapter will construct the essential tools of the field, beginning with the fractional integral and proceeding to the various definitions of the fractional derivative. We will explore the subtle yet critical differences between these definitions, the rules governing their composition, and their application in solving elementary [fractional differential equations](@entry_id:175430) (FDEs).

### The Fractional Integral and its Properties

The most natural entry point into [fractional calculus](@entry_id:146221) is through the generalization of repeated integration. An $n$-fold [iterated integral](@entry_id:138713) of a function $f(t)$, starting from $0$, can be expressed concisely by Cauchy's formula for repeated integration:

$$
(I^n f)(t) = \int_0^t \int_0^{\tau_{n-1}} \cdots \int_0^{\tau_1} f(\tau_0) \,d\tau_0 \cdots d\tau_{n-1} = \frac{1}{(n-1)!} \int_0^t (t-\tau)^{n-1} f(\tau) \,d\tau
$$

The insight of Riemann and Liouville was to replace the integer $n$ in this formula with an arbitrary positive real number $\alpha$, and the [factorial](@entry_id:266637) $(n-1)!$ with its continuous generalization, the Gamma function $\Gamma(n)$. This leads to the definition of the **Riemann-Liouville (RL) fractional integral** of order $\alpha > 0$.

**Definition: Riemann-Liouville Fractional Integral**
For a [locally integrable function](@entry_id:175678) $f(t)$, the left-sided Riemann-Liouville fractional integral of order $\alpha > 0$ is defined as:
$$
(I_{0+}^{\alpha} f)(t) \equiv ({}_{RL}I_{0+}^{\alpha} f)(t) = \frac{1}{\Gamma(\alpha)} \int_0^t (t-\tau)^{\alpha-1} f(\tau) \,d\tau
$$
The notation $I_{0+}^{\alpha}$ indicates an integration of fractional order $\alpha$ with a lower limit of $0$.

A fundamental property that validates this definition as a consistent extension of integer-order integration is the **[semigroup property](@entry_id:271012)**. This law states that applying a fractional integral of order $\beta$ followed by an integral of order $\alpha$ is equivalent to a single integration of order $\alpha+\beta$.

**Property: Semigroup Law for Fractional Integrals**
For $\alpha, \beta > 0$ and a suitable function $f(t)$, the following identity holds:
$$
I_{0+}^{\alpha} (I_{0+}^{\beta} f)(t) = I_{0+}^{\alpha+\beta} f(t)
$$

This property can be verified directly. As a demonstration, let us verify the semigroup law for the monomial function $f(t) = t^p$, where $p > -1$ [@problem_id:1146861]. The fractional integral of a [power function](@entry_id:166538) is a standard result, which can be derived using the Beta function, $B(x,y) = \int_0^1 u^{x-1}(1-u)^{y-1}du = \frac{\Gamma(x)\Gamma(y)}{\Gamma(x+y)}$.
$$
I_{0+}^{\alpha} t^p = \frac{1}{\Gamma(\alpha)} \int_0^t (t-\tau)^{\alpha-1} \tau^p \,d\tau
$$
By letting $\tau = tu$, we obtain:
$$
I_{0+}^{\alpha} t^p = \frac{t^{\alpha+p}}{\Gamma(\alpha)} \int_0^1 (1-u)^{\alpha-1} u^p \,du = \frac{t^{\alpha+p}}{\Gamma(\alpha)} B(p+1, \alpha) = \frac{\Gamma(p+1)}{\Gamma(p+\alpha+1)} t^{p+\alpha}
$$
Using this formula, the left-hand side of the [semigroup property](@entry_id:271012) becomes:
$$
I_{0+}^{\alpha} (I_{0+}^{\beta} t^p) = I_{0+}^{\alpha} \left( \frac{\Gamma(p+1)}{\Gamma(p+\beta+1)} t^{p+\beta} \right) = \frac{\Gamma(p+1)}{\Gamma(p+\beta+1)} I_{0+}^{\alpha} (t^{p+\beta})
$$
Applying the formula again with the new power $p+\beta$:
$$
= \frac{\Gamma(p+1)}{\Gamma(p+\beta+1)} \frac{\Gamma(p+\beta+1)}{\Gamma(p+\beta+\alpha+1)} t^{p+\beta+\alpha} = \frac{\Gamma(p+1)}{\Gamma(p+\alpha+\beta+1)} t^{p+\alpha+\beta}
$$
This is precisely the result of applying the right-hand side of the [semigroup property](@entry_id:271012), $I_{0+}^{\alpha+\beta} t^p$, directly. The difference between the two sides is thus zero, confirming the property for this class of functions.

### Definitions of the Fractional Derivative

While the fractional integral has a relatively straightforward and universally accepted definition, the fractional derivative can be defined in several non-equivalent ways. Each definition possesses distinct properties and is suited for different types of applications. We will discuss the three most prominent definitions.

#### The Grünwald-Letnikov Derivative

Perhaps the most intuitive approach is to generalize the finite-difference definition of a derivative. The Grünwald-Letnikov (GL) derivative does precisely this. Recalling that for an integer derivative, $f'(t) = \lim_{h\to 0} \frac{f(t)-f(t-h)}{h}$, the generalization to order $\alpha$ involves a weighted sum of past function values.

**Definition: Grünwald-Letnikov Derivative**
For an order $\alpha > 0$, the GL derivative is defined as:
$$
D_t^\alpha f(t) = \lim_{h\to 0^+} \frac{1}{h^\alpha} \sum_{k=0}^{\lfloor t/h \rfloor} (-1)^k \binom{\alpha}{k} f(t-kh)
$$
where $\binom{\alpha}{k} = \frac{\Gamma(\alpha+1)}{k! \Gamma(\alpha-k+1)}$ is the generalized binomial coefficient.

This definition elegantly demonstrates that the fractional derivative is a "local" operator in time, but one with memory, as its value at time $t$ depends on the entire history of the function $f$ from $0$ to $t$.

An important feature of fractional derivative operators is their effect on exponential functions. For ordinary derivatives, $d/dt(e^{ct}) = c e^{ct}$, meaning $e^{ct}$ is an [eigenfunction](@entry_id:149030) of the derivative operator. Let's examine if this property extends to the GL fractional derivative [@problem_id:1146810]. Applying the GL definition to $f(t) = e^{ct}$:
$$
D_t^\alpha e^{ct} = \lim_{h\to 0^+} \frac{1}{h^\alpha} \sum_{k=0}^{\lfloor t/h \rfloor} (-1)^k \binom{\alpha}{k} e^{c(t-kh)} = e^{ct} \lim_{h\to 0^+} \frac{1}{h^\alpha} \sum_{k=0}^{\lfloor t/h \rfloor} \binom{\alpha}{k} (-e^{-ch})^k
$$
In the limit $h \to 0$, the sum becomes the generalized binomial series for $(1-x)^\alpha$ with $x=e^{-ch}$.
$$
D_t^\alpha e^{ct} = e^{ct} \lim_{h\to 0^+} \frac{(1-e^{-ch})^\alpha}{h^\alpha} = e^{ct} \left( \lim_{h\to 0^+} \frac{1-e^{-ch}}{h} \right)^\alpha
$$
The limit inside the parentheses is the definition of the derivative of $e^{-cx}$ at $x=0$, which evaluates to $c$. Thus, we arrive at the remarkable result:
$$
D_t^\alpha e^{ct} = c^\alpha e^{ct}
$$
The exponential function remains an eigenfunction of the fractional derivative operator, with the eigenvalue being $c^\alpha$.

#### The Riemann-Liouville and Caputo Derivatives

The other two major definitions, Riemann-Liouville (RL) and Caputo, are both built upon the RL fractional integral. Their distinction lies in the order of application of integer-order differentiation and fractional-order integration. Let $n = \lceil \alpha \rceil$ be the smallest integer greater than or equal to $\alpha$.

**Definition: Riemann-Liouville Fractional Derivative**
The RL derivative is defined by performing fractional integration first, then integer-order differentiation:
$$
({}_{RL}D_{0+}^\alpha f)(t) = \frac{d^n}{dt^n} (I_{0+}^{n-\alpha} f)(t) = \frac{1}{\Gamma(n-\alpha)} \frac{d^n}{dt^n} \int_0^t (t-\tau)^{n-\alpha-1} f(\tau) \,d\tau
$$

**Definition: Caputo Fractional Derivative**
The Caputo derivative is defined by performing integer-order differentiation first, then fractional integration:
$$
({}_{C}D_{0+}^\alpha f)(t) = (I_{0+}^{n-\alpha} f^{(n)})(t) = \frac{1}{\Gamma(n-\alpha)} \int_0^t (t-\tau)^{n-\alpha-1} f^{(n)}(\tau) \,d\tau
$$
For this definition to be valid, $f(t)$ must be sufficiently differentiable.

### The Critical Distinction: RL vs. Caputo Derivatives

The decision to use the RL or Caputo derivative is one of the most important in modeling physical phenomena with FDEs. The difference is not merely syntactic; it has profound implications for how [initial conditions](@entry_id:152863) are treated. The relationship between the two for $n-1  \alpha  n$ is given by:
$$
({}_{RL}D_{0+}^\alpha f)(t) = ({}_{C}D_{0+}^\alpha f)(t) + \sum_{k=0}^{n-1} \frac{f^{(k)}(0)}{\Gamma(k-\alpha+1)} t^{k-\alpha}
$$
The Caputo derivative is identical to the RL derivative if and only if the function and its first $n-1$ derivatives are zero at $t=0$. This key difference makes the Caputo derivative particularly appealing for [initial value problems](@entry_id:144620) in physics and engineering, as it allows for the use of initial conditions $f(0), f'(0), \dots, f^{(n-1)}(0)$ in the same form as for integer-order differential equations. In contrast, [initial conditions](@entry_id:152863) for RL-formulated problems must be specified for fractional integrals of the function, such as $\lim_{t\to 0} (I_{0+}^{1-\alpha}f)(t)$.

Let's illustrate this with concrete examples.

For an order $\alpha \in (0,1)$, we have $n=1$. The relationship simplifies to:
$$
({}_{RL}D_{0+}^\alpha f)(t) - ({}_{C}D_{0+}^\alpha f)(t) = \frac{f(0)}{\Gamma(1-\alpha)} t^{-\alpha}
$$
This formula reveals that the two derivatives differ by a term that depends only on the function's initial value, $f(0)$. If one were given that the difference between the two derivatives for a function $y(x)$ is $K x^{-\alpha}$ for some constant $K$, comparing this to the formula immediately implies that $\frac{y(0)}{\Gamma(1-\alpha)} = K$, or $y(0) = K\Gamma(1-\alpha)$. The simplest non-constant polynomial satisfying this is the linear function $y(x) = x + K\Gamma(1-\alpha)$ [@problem_id:1146796].

This concept extends to higher orders. For $\alpha \in (1,2)$, we have $n=2$, and the relationship involves two initial value terms:
$$
({}_{RL}D_{0+}^\alpha f)(t) - ({}_{C}D_{0+}^\alpha f)(t) = \frac{f(0)}{\Gamma(1-\alpha)} t^{-\alpha} + \frac{f'(0)}{\Gamma(2-\alpha)} t^{1-\alpha}
$$
Suppose we wish to find a polynomial $p(t)$ such that a new function $g(t) = f(t) + p(t)$ has identical RL and Caputo derivatives [@problem_id:1146616]. For ${}_{RL}D_{0+}^\alpha g(t)$ to equal ${}_{C}D_{0+}^\alpha g(t)$, the summation term involving the initial conditions of $g(t)$ must vanish for all $t>0$. This requires the coefficients of $t^{-\alpha}$ and $t^{1-\alpha}$ to be zero, which in turn necessitates $g(0)=0$ and $g'(0)=0$. If we are given an arbitrary function $f(t)$, we can construct such a $g(t)$ by choosing $p(t)$ to cancel out the initial conditions of $f(t)$. Specifically, we need $p(0) = -f(0)$ and $p'(0) = -f'(0)$. The minimal degree polynomial satisfying these two constraints is the linear polynomial $p(t) = p(0) + p'(0)t = -f(0) - f'(0)t$. For example, if $f(t) = A\cosh(\lambda t) + B\sinh(\lambda t)$, then $f(0)=A$ and $f'(0)=B\lambda$, so the required polynomial is $p(t) = -A - B\lambda t$. This exercise powerfully demonstrates that the difference between the two derivatives is entirely encoded in the initial conditions.

### Operator Compositions and Properties

The rules for composing fractional operators are more complex than their integer-order counterparts and reveal further subtleties of the theory.

#### Composing Integrals and Derivatives

While differentiating a fractional integral of the same order, $D^\alpha I^\alpha f(t)$, recovers the original function $f(t)$, the reverse operation, $I^\alpha D^\alpha f(t)$, does not, due to the non-local nature of the operators. A particularly useful composition law involves applying a Caputo derivative to a Riemann-Liouville integral [@problem_id:1146580]. For $\alpha > \beta > 0$, it can be shown that:
$$
({}^C D^\beta (I^\alpha f))(t) = (I^{\alpha-\beta} f)(t)
$$
This means that applying a Caputo derivative of order $\beta$ to a function that has been fractionally integrated to order $\alpha$ is equivalent to simply reducing the order of integration to $\alpha-\beta$. This property simplifies many calculations. For instance, if we take $f(t) = t^{3/2}$, $\alpha=7/2$, and $\beta=3/2$, the direct calculation of $h(t) = I^{7/2} t^{3/2}$ yields $h(t) = \frac{\sqrt{\pi}}{160} t^5$. Subsequently applying the Caputo derivative of order $\beta=3/2$ (for which $m=2$) to $h(t)$ gives ${}^C D^{3/2} h(t) = \frac{4}{35}t^{7/2}$. This same result can be obtained more directly by calculating $I^{\alpha-\beta} f(t) = I^{7/2 - 3/2} t^{3/2} = I^2 t^{3/2}$, which also yields $\frac{4}{35}t^{7/2}$.

#### The Failure of the Semigroup Law for Derivatives

A critical departure from integer calculus is the general failure of the [semigroup property](@entry_id:271012) for [fractional derivatives](@entry_id:177809). That is,
$$
{}^C D^\alpha ({}^C D^\beta f)(t) \neq {}^C D^{\alpha+\beta} f(t)
$$
This identity only holds if the function $f(t)$ satisfies certain zero initial conditions. The non-commutativity arises because the Caputo derivative annihilates constant terms and other low-order polynomials. Let's analyze the correction term $E(t) = {}^CD^\alpha({}^CD^\beta y(t)) - {}^CD^{\alpha+\beta}y(t)$ for the function $y(t) = A + Bt + Ct^2$, with constraints $0  \alpha  1$, $1  \beta  2$, and $2  \alpha+\beta  3$ [@problem_id:1146660].
1.  First, we compute ${}^CD^\beta y(t)$. Since $1  \beta  2$, we have $\lceil\beta\rceil=2$. The Caputo derivative annihilates terms $t^k$ for $k  2$. Thus, ${}^CD^\beta(A+Bt) = 0$. We are left with:
    ${}^CD^\beta y(t) = C \cdot {}^CD^\beta t^2 = C \frac{\Gamma(3)}{\Gamma(3-\beta)} t^{2-\beta}$.
2.  Next, we compute ${}^CD^\alpha$ of this result. Since the inner function vanishes at $t=0$, its Caputo and RL derivatives are identical. Using the power rule gives:
    ${}^CD^\alpha({}^CD^\beta y(t)) = C \frac{2}{\Gamma(3-\beta)} \cdot D^\alpha t^{2-\beta} = \frac{2C}{\Gamma(3-\beta)} \frac{\Gamma(3-\beta)}{\Gamma(3-\beta-\alpha)} t^{2-\beta-\alpha} = \frac{2C}{\Gamma(3-\alpha-\beta)} t^{2-\alpha-\beta}$.
3.  Finally, we compute ${}^CD^{\alpha+\beta} y(t)$. Since $2  \alpha+\beta  3$, we have $\lceil\alpha+\beta\rceil=3$. The Caputo derivative annihilates all terms $t^k$ for $k  3$. As $y(t)$ is a polynomial of degree 2, we have ${}^CD^{\alpha+\beta}y(t) = 0$.
The correction term is therefore $E(t) = \frac{2C}{\Gamma(3-\alpha-\beta)} t^{2-\alpha-\beta} - 0$, which is non-zero. This discrepancy arises because the term $Ct^2$ is not annihilated by ${}^CD^\beta$, but the [entire function](@entry_id:178769) $y(t)$ is annihilated by ${}^CD^{\alpha+\beta}$.

### Solving Canonical Fractional Differential Equations

The tools developed above allow us to approach the solution of FDEs. The role played by the exponential function in [ordinary differential equations](@entry_id:147024) is taken over by a more general class of functions in [fractional calculus](@entry_id:146221).

#### The Mittag-Leffler Function: The Fractional Exponential

Consider the simple homogeneous linear FDE with a Caputo derivative:
$$
{}^C D^\alpha_t y(t) + \lambda y(t) = 0, \quad t \ge 0, \quad y(0)=y_0
$$
where $0  \alpha \le 1$. The solution to this equation is not an exponential function, but rather the **Mittag-Leffler function**, defined by the series:
$$
E_{\alpha, \beta}(z) = \sum_{k=0}^{\infty} \frac{z^k}{\Gamma(\alpha k + \beta)}
$$
The solution to the FDE is given by $y_\alpha(t) = y_0 E_{\alpha,1}(-\lambda t^\alpha)$. Let's verify this by applying the operator $L \equiv {}^C D^\alpha + \lambda$ to the function $y(t) = E_{\alpha,1}(-\lambda t^\alpha)$, assuming $y_0=1$ for simplicity [@problem_id:1146603]. We apply the operator term by term to the [series representation](@entry_id:175860):
$$
{}^C D^\alpha \left( \sum_{k=0}^{\infty} \frac{(-\lambda)^k t^{\alpha k}}{\Gamma(\alpha k + 1)} \right) = \sum_{k=0}^{\infty} \frac{(-\lambda)^k}{\Gamma(\alpha k + 1)} {}^C D^\alpha (t^{\alpha k})
$$
For $k=0$, the term is a constant, and its Caputo derivative (for $\alpha \in (0,1)$) is zero. For $k \ge 1$:
$$
{}^C D^\alpha t^{\alpha k} = \frac{\Gamma(\alpha k+1)}{\Gamma(\alpha k - \alpha + 1)} t^{\alpha k - \alpha} = \frac{\Gamma(\alpha k+1)}{\Gamma(\alpha(k-1) + 1)} t^{\alpha(k-1)}
$$
Substituting this back, the series becomes:
$$
\sum_{k=1}^{\infty} \frac{(-\lambda)^k}{\Gamma(\alpha k + 1)} \frac{\Gamma(\alpha k+1)}{\Gamma(\alpha(k-1) + 1)} t^{\alpha(k-1)} = \sum_{k=1}^{\infty} \frac{(-\lambda)^k t^{\alpha(k-1)}}{\Gamma(\alpha(k-1) + 1)}
$$
Re-indexing with $j = k-1$, this is $-\lambda \sum_{j=0}^{\infty} \frac{(-\lambda)^j t^{\alpha j}}{\Gamma(\alpha j + 1)} = -\lambda E_{\alpha,1}(-\lambda t^\alpha)$.
Therefore, $L[y(t)] = {}^C D^\alpha y(t) + \lambda y(t) = -\lambda E_{\alpha,1}(-\lambda t^\alpha) + \lambda E_{\alpha,1}(-\lambda t^\alpha) = 0$. This confirms that the Mittag-Leffler function is the [fundamental solution](@entry_id:175916) for this class of FDEs.

A crucial test of any generalized theory is that it must reduce to the well-known classical theory in the appropriate limit. This is the **correspondence principle**. For fractional calculus, we expect to recover standard calculus as $\alpha \to 1$. Let's test this on our solution [@problem_id:1146748]:
$$
\lim_{\alpha \to 1^-} y_\alpha(t) = \lim_{\alpha \to 1^-} y_0 E_{\alpha,1}(-\lambda t^\alpha) = y_0 \lim_{\alpha \to 1^-} \sum_{k=0}^{\infty} \frac{(-\lambda t^\alpha)^k}{\Gamma(\alpha k + 1)}
$$
As $\alpha \to 1$, we have $t^\alpha \to t$ and $\Gamma(\alpha k + 1) \to \Gamma(k+1) = k!$. The expression becomes:
$$
y_0 \sum_{k=0}^{\infty} \frac{(-\lambda t)^k}{k!} = y_0 e^{-\lambda t}
$$
This is exactly the solution to the first-order ODE $y'(t) + \lambda y(t) = 0$ with $y(0)=y_0$. The framework is consistent.

#### Action on Periodic Functions

The behavior of fractional operators on [periodic functions](@entry_id:139337) is of great interest in fields like [viscoelasticity](@entry_id:148045) and signal processing. Let us consider the action of a fractional integrator of order $\alpha$ on the function $f(t) = \sin(\omega t)$. The full solution contains transient terms that decay over time. The long-term behavior is captured by the **steady-state component**, which can be found efficiently using methods from linear time-invariant (LTI) [systems theory](@entry_id:265873) [@problem_id:1146876]. The fractional integral is a [convolution operator](@entry_id:276820) with the kernel $k(t) = t^{\alpha-1}/\Gamma(\alpha)$. The Laplace transform of this kernel gives the system's transfer function, $H(s) = \mathcal{L}\{k(t)\} = s^{-\alpha}$.
For a sinusoidal input $\sin(\omega t)$, the steady-state output is given by $|H(i\omega)| \sin(\omega t + \arg H(i\omega))$. We evaluate the transfer function at $s=i\omega$:
$$
H(i\omega) = (i\omega)^{-\alpha} = (\omega e^{i\pi/2})^{-\alpha} = \omega^{-\alpha} e^{-i\alpha\pi/2}
$$
From this, we extract the magnitude and phase:
$$
|H(i\omega)| = \omega^{-\alpha}, \quad \arg H(i\omega) = -\frac{\alpha\pi}{2}
$$
The [steady-state response](@entry_id:173787) of the fractional integrator is therefore:
$$
y_{ss}(t) = \omega^{-\alpha} \sin\left(\omega t - \frac{\alpha\pi}{2}\right)
$$
Fractional integration of a sinusoid results in a [sinusoid](@entry_id:274998) of the same frequency, but with its amplitude scaled by $\omega^{-\alpha}$ and its phase shifted by a constant $-\alpha\pi/2$.

#### Connecting RL and Caputo Initial Value Problems

As a final point, we bridge the gap between the two main formulations of [initial value problems](@entry_id:144620). An IVP for an RL-FDE typically involves an initial condition on a fractional integral, e.g., $\lim_{t\to 0^+} [ {}_{0}D_{t}^{-\beta} y(t) ] = b$. The solution to such a problem is often singular at $t=0$, for example, containing a term proportional to $t^{-\beta}$. A Caputo-based IVP, on the other hand, starts with a finite initial value $y(0)=c$. How are $b$ and $c$ related?

Consider the RL-FDE ${}_{0}D_{t}^{1/2} y(t) + \lambda y(t) = 0$ with the initial condition $\lim_{t\to 0^+} [ {}_{0}D_{t}^{-1/2} y(t) ] = b$. The solution is $y(t) = b t^{-1/2} E_{1/2, 1/2}(-\lambda t^{1/2})$. To find an equivalent regular initial condition, we can analyze the small-$t$ behavior of this solution [@problem_id:1146802]. Expanding the Mittag-Leffler series:
$$
y(t) = b t^{-1/2} \sum_{k=0}^{\infty} \frac{(-\lambda t^{1/2})^k}{\Gamma(k/2 + 1/2)} = b \left( \frac{t^{-1/2}}{\Gamma(1/2)} - \frac{\lambda t^0}{\Gamma(1)} + \frac{\lambda^2 t^{1/2}}{\Gamma(3/2)} - \cdots \right)
$$
The solution behaves as $y(t) \approx \frac{b}{\sqrt{\pi}}t^{-1/2} - b\lambda$ for small $t$. The singular part is $\frac{b}{\Gamma(1/2)}t^{-1/2}$. If we define a "regularized" function $z(t)$ by subtracting this singularity, we get:
$$
z(t) = y(t) - \frac{b}{\Gamma(1/2)}t^{-1/2} = -b\lambda + O(t^{1/2})
$$
The initial value of this regularized function is $c = z(0) = \lim_{t\to 0^+} z(t) = -b\lambda$. This establishes a direct algebraic link between the initial condition $b$ for the RL problem and the initial condition $c$ for an equivalent regularized problem that could be modeled using the Caputo framework. This connection is vital for translating between the mathematical formalism of RL equations and the physically intuitive [initial conditions](@entry_id:152863) used in Caputo equations.