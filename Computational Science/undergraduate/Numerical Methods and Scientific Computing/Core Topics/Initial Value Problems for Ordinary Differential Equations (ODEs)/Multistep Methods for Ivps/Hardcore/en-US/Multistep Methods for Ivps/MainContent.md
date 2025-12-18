## Introduction
When modeling dynamic systems, from the orbit of a planet to the firing of a neuron, we often turn to [initial value problems](@entry_id:144620) (IVPs). While [single-step methods](@entry_id:164989) provide a robust way to find numerical solutions, they can be computationally intensive. Multistep methods offer a powerful and often more efficient alternative by leveraging information from several previous time steps to predict the next. This approach, however, introduces a new layer of complexity concerning stability and implementation. This article addresses the fundamental question: how do we construct, analyze, and intelligently apply [multistep methods](@entry_id:147097) to solve a wide range of [ordinary differential equations](@entry_id:147024), including the challenging "stiff" problems that arise frequently in science and engineering?

Across the following chapters, you will gain a deep understanding of these powerful numerical tools.
-   **Principles and Mechanisms** will introduce the general form of [linear multistep methods](@entry_id:139528), explore their derivation, and delve into the critical theories of convergence and stability, including the famous Dahlquist barriers.
-   **Applications and Interdisciplinary Connections** will demonstrate the practical utility of these methods by solving problems in physics, engineering, biology, and economics, highlighting the crucial choice between explicit and [implicit schemes](@entry_id:166484) for stiff and non-[stiff systems](@entry_id:146021).
-   **Hands-On Practices** will provide interactive exercises to solidify your understanding of method derivation, stability analysis, and the practical consequences of choosing the right method for a given problem.

Let's begin by exploring the foundational principles and mechanisms that govern the behavior of [multistep methods](@entry_id:147097).

## Principles and Mechanisms

In the numerical solution of [initial value problems](@entry_id:144620) (IVPs), [multistep methods](@entry_id:147097) offer a powerful alternative to the single-step techniques discussed previously. Whereas [single-step methods](@entry_id:164989), such as those of the Runge-Kutta family, compute the solution at the next time step, $y_{n+1}$, using only information from the current step, $y_n$, [multistep methods](@entry_id:147097) leverage a history of previously computed values—$y_n, y_{n-1}, y_{n-2}, \dots$—to achieve higher accuracy and [computational efficiency](@entry_id:270255). This chapter delves into the principles governing the construction, implementation, and analysis of these important numerical tools.

### The General Form of Linear Multistep Methods

A general **$k$-step [linear multistep method](@entry_id:751318) (LMM)** for the IVP $y'(t) = f(t, y(t))$ is defined by the difference equation:
$$
\sum_{j=0}^{k} \alpha_j y_{n+j} = h \sum_{j=0}^{k} \beta_j f_{n+j}
$$
where $y_{n+j}$ is the [numerical approximation](@entry_id:161970) to the solution $y(t_{n+j})$ at the grid point $t_{n+j} = t_0 + (n+j)h$, $h$ is the constant step size, and $f_{n+j} = f(t_{n+j}, y_{n+j})$. The coefficients $\alpha_j$ and $\beta_j$ are constants that define the specific method. By convention, we set $\alpha_k=1$ to ensure $y_{n+k}$ can be isolated.

This general form gives rise to two major families of methods:
1.  **Explicit Methods**: If $\beta_k = 0$, the formula for $y_{n+k}$ does not depend on $f_{n+k}$. The value of $y_{n+k}$ can be computed directly from past values, making the calculation straightforward.
2.  **Implicit Methods**: If $\beta_k \neq 0$, the unknown value $y_{n+k}$ appears on both sides of the equation, as it is embedded within the term $f_{n+k} = f(t_{n+k}, y_{n+k})$. This creates an equation, often nonlinear, that must be solved for $y_{n+k}$ at each step.

While explicit methods are simpler to implement, we will see that implicit methods possess significantly superior stability properties, making them indispensable for certain classes of problems.

### Derivation of Multistep Methods

The coefficients $\alpha_j$ and $\beta_j$ are not arbitrary; they are chosen to ensure the method accurately approximates the behavior of the differential equation. There are two primary approaches to deriving these coefficients.

#### Derivation from Numerical Integration

One of the most intuitive ways to construct LMMs is to start from the [fundamental theorem of calculus](@entry_id:147280), which gives the exact relation:
$$
y(t_{n+1}) - y(t_n) = \int_{t_n}^{t_{n+1}} y'(t) \, dt = \int_{t_n}^{t_{n+1}} f(t, y(t)) \, dt
$$
The core idea is to approximate the integral on the right-hand side. We can do this by replacing the function $f(t, y(t))$ with a polynomial, $P(t)$, that interpolates the function at a set of previously computed points. The choice of interpolation points and the interval of integration defines the method.

The **Adams-Bashforth** family of explicit methods arises from this approach. To derive the $k$-step Adams-Bashforth (AB) method, we construct a polynomial $P_{k-1}(t)$ of degree $k-1$ that passes through the $k$ known values $(t_n, f_n), (t_{n-1}, f_{n-1}), \dots, (t_{n-k+1}, f_{n-k+1})$. The next solution value, $y_{n+1}$, is then approximated by integrating this polynomial from $t_n$ to $t_{n+1}$:
$$
y_{n+1} = y_n + \int_{t_n}^{t_{n+1}} P_{k-1}(t) \, dt
$$
For instance, to construct the 4-step Adams-Bashforth (AB4) method, we interpolate $f$ at the four nodes $\{t_n, t_{n-1}, t_{n-2}, t_{n-3}\}$ with a degree-3 polynomial. Integrating this interpolant over $[t_n, t_{n+1}]$ yields the well-known formula :
$$
y_{n+1} = y_n + \frac{h}{24} \left( 55f_n - 59f_{n-1} + 37f_{n-2} - 9f_{n-3} \right)
$$
The **Adams-Moulton** family of [implicit methods](@entry_id:137073) is derived similarly, but the interpolating polynomial includes the future, unknown point $(t_{n+1}, f_{n+1})$. This makes the method implicit but typically yields a higher [order of accuracy](@entry_id:145189) and better stability for the same number of steps.

#### Derivation from Taylor Series Expansions

A more analytical approach is the [method of undetermined coefficients](@entry_id:165061), which relies on Taylor series. We postulate a general form for the method and choose the coefficients to cancel as many terms as possible in the Taylor expansion of the **[local truncation error](@entry_id:147703) (LTE)**. The LTE is the residual that remains when the exact solution $y(t)$ is substituted into the method's formula.

Let's derive the 2-step Adams-Bashforth method as an example . We seek a method of the form:
$$
y_{n+1} = y_n + h \left( \alpha f_n + \beta f_{n-1} \right)
$$
The local truncation error $T_{n+1}$ is:
$$
T_{n+1} = y(t_{n+1}) - y(t_n) - h \left( \alpha y'(t_n) + \beta y'(t_{n-1}) \right)
$$
We expand $y(t_{n+1})$ and $y'(t_{n-1})$ in Taylor series around $t_n$:
$$
y(t_{n+1}) = y(t_n+h) = y(t_n) + h y'(t_n) + \frac{h^2}{2} y''(t_n) + O(h^3)
$$
$$
y'(t_{n-1}) = y'(t_n-h) = y'(t_n) - h y''(t_n) + O(h^2)
$$
Substituting these into the expression for $T_{n+1}$ and collecting terms by powers of $h$:
$$
T_{n+1} = (1 - \alpha - \beta) h y'(t_n) + \left( \frac{1}{2} + \beta \right) h^2 y''(t_n) + O(h^3)
$$
To make the method as accurate as possible, we set the coefficients of the lowest powers of $h$ to zero.
-   Coefficient of $h^1$: $1 - \alpha - \beta = 0$
-   Coefficient of $h^2$: $\frac{1}{2} + \beta = 0$

Solving this system gives $\beta = -\frac{1}{2}$ and $\alpha = \frac{3}{2}$. The resulting method is the second-order Adams-Bashforth method:
$$
y_{n+1} = y_n + h \left( \frac{3}{2} f_n - \frac{1}{2} f_{n-1} \right)
$$
The LTE is of order $O(h^3)$, making the method second-order. This procedure can be generalized to derive methods of any desired order and provides a systematic framework for analyzing accuracy. The collection of equations that the coefficients must satisfy to achieve a certain order are known as the **order conditions** .

### Practical Aspects of Implementation

#### The Starting Problem

A $k$-step method requires $k$ previous values ($y_n, \dots, y_{n-k+1}$) to compute the next value. However, an IVP only provides a single starting value, $y_0 = y(t_0)$. This raises a fundamental question: how do we compute $y_1, y_2, \dots, y_{k-1}$? The multistep formula cannot be used for these initial steps because the required history of values does not exist .

The [standard solution](@entry_id:183092) is to employ a **starter method**. A single-step method, such as a Runge-Kutta method, is used to generate the first few points ($y_1, \dots, y_{k-1}$). To preserve the overall accuracy of the LMM, the starter method should have an order of accuracy at least as high as the LMM itself.

#### Predictor-Corrector Methods

As noted, [implicit methods](@entry_id:137073) have desirable stability properties but require solving an equation for $y_{n+1}$ at each step. For a nonlinear $f(t,y)$, this typically involves an iterative process like Newton's method. **Predictor-corrector methods** offer a compromise. At each step, they:
1.  **Predict**: Use an explicit method (the predictor) to produce a first estimate of the solution, $y_{n+1}^{(P)}$.
2.  **Evaluate**: Use this prediction to approximate the derivative at the next step: $f_{n+1}^{(P)} = f(t_{n+1}, y_{n+1}^{(P)})$.
3.  **Correct**: Use an implicit method (the corrector), with $f_{n+1}$ on the right-hand side replaced by $f_{n+1}^{(P)}$, to compute the final value, $y_{n+1}$.

This process avoids the need for an iterative solve, as the corrector is used in an explicit fashion. A classic example is the Milne-Simpson method, which pairs an explicit Milne predictor with an implicit Simpson's rule corrector . This approach often combines the stability benefits of the implicit corrector with the computational ease of an explicit method.

#### Adaptive Step-Size Control

In many applications, the solution of an ODE changes rapidly in some regions and slowly in others. An efficient solver should adapt its step size $h$, taking small steps in regions of rapid change and large steps where the solution is smooth.

For [single-step methods](@entry_id:164989) like Runge-Kutta, changing the step size is straightforward. The next step is computed using only information at the current point, so changing $h$ from one step to the next has no effect on the formula itself.

For [multistep methods](@entry_id:147097), this is a significant challenge. As seen in their derivation, standard LMMs rely on a history of points that are assumed to be equally spaced. If we change $h$, the basis for the fixed coefficients of the method is invalidated. An on-the-fly change to the step size requires either restarting the method (by generating a new history with a single-step method at the new step size) or using more complex variable-step-size formulations where the coefficients $\alpha_j$ and $\beta_j$ are recomputed at each step. This makes adaptive stepping algorithmically much more complex for [multistep methods](@entry_id:147097) than for [single-step methods](@entry_id:164989) .

### Convergence and Stability Theory

For a numerical method to be useful, the numerical solution must converge to the true solution as the step size $h$ approaches zero. The **Dahlquist Equivalence Theorem**, a cornerstone of LMM theory, states that a [linear multistep method](@entry_id:751318) is convergent if and only if it is **consistent** and **zero-stable**.

#### Consistency and Order

A method is **consistent** if its [local truncation error](@entry_id:147703) goes to zero faster than $h$ as $h \to 0$. This ensures that the difference equation correctly approximates the differential equation in the limit. For any LMM, consistency is equivalent to having an [order of accuracy](@entry_id:145189) $p \ge 1$.

The **order** of a method, $p$, is a key measure of its accuracy. A method of order $p$ has a [local truncation error](@entry_id:147703) of $O(h^{p+1})$. It might seem counter-intuitive, but this [local error](@entry_id:635842) accumulates over the integration steps to produce a **[global error](@entry_id:147874)** at a fixed time $T$ that is of order $O(h^p)$. This fundamental relationship, where the [global error](@entry_id:147874) order is one less than the local error order, can be readily verified numerically. For example, a third-order Adams-Bashforth method exhibits a local error that scales with $h^4$ and a global error that scales with $h^3$ .

#### Zero-Stability and Parasitic Modes

**Zero-stability** is a more subtle but critical concept. It relates to the behavior of the numerical solution in the limit as $h \to 0$. An LMM is a difference equation, and its solutions are governed by the roots of a characteristic polynomial. For a $k$-step method, this polynomial is the **first characteristic polynomial**, $\rho(\zeta)$, defined as:
$$
\rho(\zeta) = \sum_{j=0}^{k} \alpha_j \zeta^{k-j}
$$
(Note that the indexing convention may vary in literature). Zero-stability is guaranteed if the method satisfies the **root condition**:
1.  All roots of $\rho(\zeta) = 0$ must have a magnitude less than or equal to 1 ($|\zeta| \le 1$).
2.  Any root with magnitude equal to 1 must be a simple (non-repeated) root.

The root $\zeta=1$ is always present for a consistent method and is called the **[principal root](@entry_id:164411)**; it corresponds to the component of the numerical solution that approximates the true solution. All other roots are called **parasitic roots**. If any parasitic root has a magnitude greater than 1, it will introduce a component that grows exponentially, rendering the method useless. If a parasitic root lies on the unit circle but is not equal to 1, it can introduce persistent or growing oscillations.

Consider the leapfrog method, $y_{n+2} - y_n = 2h f_{n+1}$. This is a 2-step method with $\alpha_0=-1, \alpha_1=0, \alpha_2=1$. Its [characteristic polynomial](@entry_id:150909) (using a slightly different but equivalent formulation from ) is $\rho(\xi) = \xi^2 - 1 = 0$, which has roots $\xi = 1$ and $\xi = -1$. Both roots are simple and on the unit circle, so the method is zero-stable. However, the parasitic root at $\xi = -1$ introduces a non-physical component that behaves like $(-1)^n$. This manifests as a persistent, non-decaying odd-even oscillation in the solution if excited by starting errors or round-off .

A method that is zero-stable but has parasitic roots on the unit circle is sometimes called **weakly stable**. In long integrations, even small round-off errors can excite these parasitic modes, leading to oscillations that can corrupt the solution. The Milne-Simpson method is a famous example of a high-order method that suffers from this weak instability, where small numerical noise can trigger slowly growing oscillations over time .

### Stability for Stiff Problems

Many problems in science and engineering are **stiff**. A stiff system is one that involves multiple time scales, typically a rapidly decaying transient component and a slowly varying solution of interest. For the scalar test equation $y' = \lambda y$, stiffness corresponds to a large negative real part of $\lambda$.

For such problems, [zero-stability](@entry_id:178549) is not enough. We require **[absolute stability](@entry_id:165194)**. The **region of [absolute stability](@entry_id:165194)** of a method is the set of values $z = h\lambda$ in the complex plane for which the numerical solution $y_n$ decays to zero as $n \to \infty$.

A critical distinction emerges between [explicit and implicit methods](@entry_id:168763). Explicit methods, like Adams-Bashforth, have very small regions of [absolute stability](@entry_id:165194). For the stiff IVP $y'(t) = -1000(y - \cos(t))$, where the effective $\lambda$ is $-1000$, the fourth-order Adams-Bashforth method (AB4) is stable only for a maximum step size of about $h \le 0.0003$. Attempting to use a larger step size causes the numerical solution to blow up. In contrast, the fourth-order implicit Adams-Moulton method (AM4) is stable for $h \le 0.003$, a ten-fold improvement. This dramatic difference highlights a general principle: **explicit methods are unsuitable for [stiff problems](@entry_id:142143)**, as they are constrained to impractically small step sizes by stability, not accuracy .

For [stiff problems](@entry_id:142143), we desire methods with the largest possible [stability regions](@entry_id:166035).
- A method is **A-stable** if its region of [absolute stability](@entry_id:165194) contains the entire left half-plane ($\text{Re}(z) \leq 0$). This means the method will be stable for any stable stiff problem, regardless of the step size. The Trapezoidal Rule is a classic A-stable method.
- However, A-stability alone can be insufficient. For a stiff component where $\text{Re}(z)$ is large and negative, we want the numerical method to strongly damp that component. The amplification factor of the Trapezoidal Rule approaches $-1$ as $\text{Re}(z) \to -\infty$. This means it does not damp the stiffest components; instead, it causes them to oscillate, which is highly undesirable.
- A stronger property is **L-stability** (or stiff stability). A method is L-stable if it is A-stable and its amplification factor approaches zero as $\text{Re}(z) \to -\infty$. This property ensures that the fastest-decaying components of the true solution are also strongly damped in the numerical solution.

The **Backward Differentiation Formulas (BDF)** are a family of implicit LMMs that are renowned for their excellent stability properties for [stiff equations](@entry_id:136804). While not all are A-stable, the lower-order BDFs (up to order 6) have large [stability regions](@entry_id:166035) that make them ideal. In particular, BDF1 (Backward Euler) and BDF2 are L-stable. When applied to a stiff problem, the L-stable BDF-2 method effectively damps the transient component and produces a smooth, accurate solution. In contrast, the A-stable Trapezoidal Rule, while remaining bounded, exhibits spurious oscillations due to its failure to damp the high-frequency error components . This makes L-stable methods like BDF the preferred choice for a wide range of [stiff problems](@entry_id:142143).