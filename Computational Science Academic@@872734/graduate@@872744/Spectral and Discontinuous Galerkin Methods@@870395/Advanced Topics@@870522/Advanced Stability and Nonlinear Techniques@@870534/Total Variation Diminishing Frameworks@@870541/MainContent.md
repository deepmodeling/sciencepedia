## Introduction
Simulating physical phenomena governed by [hyperbolic conservation laws](@entry_id:147752), such as shock waves in fluid dynamics or sharp fronts in [meteorology](@entry_id:264031), presents a significant challenge for numerical methods. While [high-order schemes](@entry_id:750306) like the Discontinuous Galerkin (DG) method promise exceptional accuracy for smooth solutions, they often produce spurious, non-physical oscillations near discontinuities. These oscillations can corrupt the entire solution and lead to numerical instability, creating a knowledge gap between the need for high fidelity and the demand for robustness. The Total Variation Diminishing (TVD) framework offers a powerful and systematic solution to this problem. It provides a set of mathematical principles and practical tools to design high-resolution [numerical schemes](@entry_id:752822) that capture sharp features without generating oscillations, ensuring the physical realism of the simulation.

This article provides a comprehensive exploration of TVD frameworks. The first chapter, **Principles and Mechanisms**, delves into the foundational theory, explaining the concept of [total variation](@entry_id:140383), the implications of Godunov's theorem, and the construction of TVD schemes using limiters and Strong Stability Preserving (SSP) [time integrators](@entry_id:756005). The second chapter, **Applications and Interdisciplinary Connections**, showcases the widespread impact of these methods, from advanced algorithms in computational fluid dynamics to novel uses in economics and uncertainty quantification. Finally, **Hands-On Practices** offers a set of targeted exercises to solidify understanding of key concepts like [total variation](@entry_id:140383) computation and limiter design.

## Principles and Mechanisms

In the numerical solution of [hyperbolic conservation laws](@entry_id:147752), particularly with [high-order methods](@entry_id:165413) like the Discontinuous Galerkin (DG) method, a central challenge is the accurate and stable representation of solutions containing sharp gradients or discontinuities. While high-order polynomial approximations offer superior accuracy in smooth regions, they are susceptible to producing non-physical, spurious oscillations near shocks—a phenomenon analogous to the Gibbs effect in Fourier series. The Total Variation Diminishing (TVD) framework provides a powerful set of principles and nonlinear mechanisms to suppress these oscillations, ensuring the robustness of the numerical solution. This chapter elucidates the foundational concepts of [total variation](@entry_id:140383), the mathematical formulation of the TVD property, and the practical construction of high-order TVD schemes.

### The Concept of Total Variation

To quantify and control oscillations, we must first introduce a suitable mathematical measure. The **total variation (TV)** of a function serves this purpose by measuring its total "up and down" movement over an interval. For a continuously differentiable scalar function $u(x)$ on an interval $[a,b]$, the [total variation](@entry_id:140383) is the integral of the absolute value of its derivative:

$$
\mathrm{TV}(u; [a,b]) = \int_a^b |u'(x)| \, dx
$$

This definition can be extended to functions that are not continuously differentiable, such as the piecewise smooth solutions containing jump discontinuities that arise in hyperbolic problems. For a piecewise continuously [differentiable function](@entry_id:144590) with a finite set of jump discontinuities $J = \{x_j\}$ in $(a,b)$, the [total variation](@entry_id:140383) is the sum of the variation in the smooth parts and the magnitude of the jumps [@problem_id:3424320]:

$$
\mathrm{TV}(u; [a,b]) = \int_a^b |u'(x)| \, dx + \sum_{x_j \in J} |u(x_j^+) - u(x_j^-)|
$$

Here, $u(x_j^\pm)$ denote the [one-sided limits](@entry_id:138326) at the jump location $x_j$. The space of functions for which this quantity is finite is known as the space of **[functions of bounded variation](@entry_id:144591)**, denoted $BV(a,b)$. Endowed with the norm $\|u\|_{BV(a,b)} = \|u\|_{L^1(a,b)} + \mathrm{TV}(u;[a,b])$, this [space forms](@entry_id:186145) a complete [normed vector space](@entry_id:144421) (a Banach space), which is the natural functional setting for the theory of [scalar conservation laws](@entry_id:754532) [@problem_id:3424320].

It is crucial to distinguish total variation from other measures of a function's size, such as the $L^1$ norm, $\|u\|_{L^1(a,b)} = \int_a^b |u(x)| \, dx$. The $L^1$ norm measures the average magnitude of the function, whereas total variation measures its oscillatory behavior. A function can have a small $L^1$ norm but an arbitrarily large total variation. Consider, for example, the sequence of functions $u_n(x) = \sin(2\pi n x)$ on $[0,1]$. For any integer $n$, the $L^1$ norm is constant: $\|u_n\|_{L^1(0,1)} = 2/\pi$. However, the total variation is $\mathrm{TV}(u_n; [0,1]) = \int_0^1 |2\pi n \cos(2\pi n x)| \, dx = 4n$, which grows linearly with the frequency $n$. This demonstrates that a more oscillatory function has a *larger* [total variation](@entry_id:140383), and that the TV [seminorm](@entry_id:264573) and the $L^1$ norm are not equivalent [@problem_id:3424320]. This property makes [total variation](@entry_id:140383) an ideal functional for penalizing or controlling oscillations.

### The Total Variation Diminishing (TVD) Property

The core idea of the TVD framework is to demand that the [total variation](@entry_id:140383) of the discrete numerical solution does not increase as it evolves in time. For a fully discrete scheme that advances the solution from time level $t^n$ to $t^{n+1}$ via an operator $G$, so that $U^{n+1} = G(U^n)$, the scheme is defined as **Total Variation Diminishing (TVD)** if for all initial data $U^n$ [@problem_id:3424360]:

$$
\mathrm{TV}(U^{n+1}) \le \mathrm{TV}(U^n)
$$

Here, $\mathrm{TV}(U)$ is a discrete analogue of the total variation, typically defined for a grid function of cell averages $\{U_i\}$ as the sum of the absolute differences between adjacent values: $\mathrm{TV}(U) = \sum_i |U_{i+1} - U_i|$.

For a semi-discrete scheme written as a system of [ordinary differential equations](@entry_id:147024), $\dot{U}(t) = L(U(t))$, the TVD property is expressed in continuous time [@problem_id:3424360]:

$$
\frac{d}{dt} \mathrm{TV}(U(t)) \le 0
$$

This condition ensures that the [total variation](@entry_id:140383) is a non-increasing function of time. A key consequence of the TVD property for one-dimensional scalar problems is that it is **[monotonicity](@entry_id:143760)-preserving**, meaning it cannot create new [local extrema](@entry_id:144991) in the solution [@problem_id:3424320]. If the solution at time $t^n$ is monotone over a certain range of cells, it will remain monotone at $t^{n+1}$. This property directly prevents the formation of spurious oscillations.

The need for such a strong condition becomes apparent when examining unmodified high-order methods. A high-order DG method, for instance, represents the solution within each element using a polynomial. The higher-order [modal coefficients](@entry_id:752057) of this polynomial can introduce non-monotonic, oscillatory behavior within an element, even if the cell averages are smooth. As demonstrated in [@problem_id:3424308], a DG solution with a large quadratic modal coefficient ($P^2$ mode) can exhibit significant sub-cell oscillations, which contribute to a large [total variation](@entry_id:140383). A TVD method must control or "limit" these [higher-order modes](@entry_id:750331) to prevent the total variation from growing.

### The Godunov Barrier and the Necessity of Nonlinearity

At first glance, one might hope to design a high-order numerical scheme that is both linear and satisfies the desirable TVD property. However, a fundamental result known as **Godunov's theorem** establishes a formidable barrier. The theorem, in its broader sense, states that any linear numerical scheme that is monotonicity-preserving (a property implied by being TVD for scalar problems) can be at most first-order accurate [@problem_id:3424352] [@problem_id:3424365].

This creates an "infeasibility frontier": for linear schemes, high accuracy and the non-oscillatory TVD property are mutually exclusive. Attempting to improve the accuracy of a linear scheme beyond first order will inevitably introduce oscillations. For example, the classical second-order Lax-Wendroff scheme is linear but notoriously oscillatory, while the [first-order upwind scheme](@entry_id:749417) is TVD but suffers from excessive [numerical diffusion](@entry_id:136300).

The profound implication of Godunov's theorem is that if we wish to construct a scheme that is both high-order accurate and TVD, the scheme *must* be **nonlinear**. The nonlinearity is introduced in an adaptive, data-dependent manner, allowing the scheme to behave like a high-order method in smooth regions of the solution and revert to a robust, non-oscillatory (often first-order) behavior near sharp gradients. This adaptive switching is the job of a **limiter**.

### Constructing High-Resolution TVD Schemes

A modern high-resolution TVD scheme is a sophisticated construction involving nonlinear spatial limiters and specialized [time integration methods](@entry_id:136323). The general strategy is to start with a [high-order spatial discretization](@entry_id:750307) and apply a limiter to its output to enforce the TVD condition, then evolve the resulting semi-discrete system with a time integrator that preserves this property.

#### Spatial Discretization: The MUSCL Approach and Flux Limiters

A popular framework for achieving [second-order accuracy](@entry_id:137876) in [finite volume](@entry_id:749401) and DG methods is the **Monotonic Upstream-centered Schemes for Conservation Laws (MUSCL)** approach. The core idea is to move beyond a piecewise-constant representation and reconstruct a piecewise-linear function within each cell before computing the [numerical fluxes](@entry_id:752791) at cell interfaces [@problem_id:3424365].

The slope of this linear reconstruction is critical. A naive choice, such as a [centered difference](@entry_id:635429), yields a high-order but oscillatory scheme. To enforce the TVD property, this slope must be "limited." This is achieved using a **[flux limiter](@entry_id:749485)** function, denoted $\phi(r)$. The [limiter](@entry_id:751283) function takes as input a measure of the local solution smoothness, typically the ratio of successive solution gradients, $r_i = (U_i - U_{i-1}) / (U_{i+1} - U_i)$, and returns a factor $\phi(r_i)$ that scales the slope.

The conditions on $\phi(r)$ that guarantee the resulting scheme is TVD can be visualized using the **Sweby diagram** [@problem_id:3618279]. This diagram plots $\phi(r)$ versus $r$. For a scheme to be second-order accurate and TVD for any stable time step, the function $\phi(r)$ must lie within a specific admissible region. This region, known as the second-order TVD region, is defined by the following inequalities:
$$
\begin{cases}
    \phi(r) = 0  \text{ if } r \le 0 \\
    0 \le \phi(r) \le 2r  \text{ if } 0 \le r \le 1 \\
    0 \le \phi(r) \le 2  \text{ if } r > 1
\end{cases}
$$
The condition $\phi(r)=0$ for $r \le 0$ is crucial; it "clips" developing oscillations at [local extrema](@entry_id:144991), where successive gradients have opposite signs. The mechanism by which these bounds ensure the TVD property is that they constrain the coefficients of the numerical update, guaranteeing that the new cell average is a convex combination of its neighbors from the previous time step, which is a [sufficient condition](@entry_id:276242) for monotonicity preservation. For [second-order accuracy](@entry_id:137876) in smooth regions (where $r \approx 1$), the [limiter](@entry_id:751283) must satisfy $\phi(1)=1$. A common example of a [limiter](@entry_id:751283) that satisfies these conditions is the `[minmod](@entry_id:752001)` limiter, defined as $\phi(r) = \max(0, \min(1, r))$ [@problem_id:3424365].

#### Temporal Discretization: Strong Stability Preserving (SSP) Methods

Once a nonlinear spatial operator $L(U)$ is designed such that the simple Forward Euler (FE) method, $U^{n+1} = U^n + \Delta t L(U^n)$, is TVD under some CFL time-step restriction $\Delta t \le \Delta t_{\mathrm{FE}}$, we need a high-order time integrator that preserves this property. Standard high-order Runge-Kutta methods do not, in general, preserve the TVD property.

The solution is to use **Strong Stability Preserving (SSP)** [time integration methods](@entry_id:136323), also known as TVD Runge-Kutta methods. The defining characteristic of an explicit SSP method is that it can be expressed as a convex combination of a sequence of Forward Euler steps [@problem_id:3424315] [@problem_id:3424360].

The TV [seminorm](@entry_id:264573), $\mathrm{TV}(U)$, is a convex functional. By Jensen's inequality, for any convex combination, we have $\mathrm{TV}(\sum_k \alpha_k U_k) \le \sum_k \alpha_k \mathrm{TV}(U_k)$. Since an SSP-RK step is a convex combination of operators (FE steps) that are themselves TVD, the convexity of the TV [seminorm](@entry_id:264573) guarantees that the full SSP-RK update is also TVD [@problem_id:3424352].

This preservation property holds under a modified time-step restriction, $\Delta t \le C \cdot \Delta t_{\mathrm{FE}}$, where $C$ is the **SSP coefficient** of the Runge-Kutta method. By analyzing the representation of the RK method as a convex combination of FE-like steps (the Shu-Osher form), one can derive a precise expression for this coefficient in terms of the RK coefficients $\alpha_{ij}$ and $\beta_{ij}$ [@problem_id:3424315]:
$$
C = \min_{\substack{1 \le i \le s \\ 0 \le j  i \\ \beta_{ij} > 0}} \frac{\alpha_{ij}}{\beta_{ij}}
$$
This elegant result provides a complete framework: a nonlinear TVD spatial operator combined with an SSP time integrator yields a fully discrete, high-order, non-oscillatory scheme.

### Limitations and Extensions

While powerful, the TVD framework is not without its limitations, and it exists within a landscape of related stability concepts.

#### TVD versus Other Stability Concepts

It is important not to confuse the TVD property with other stability criteria. For instance, a **Maximum-Principle Preserving (MPP)** scheme ensures that the solution values at grid nodes remain within the bounds of the initial data. While desirable, MPP is a weaker condition than TVD. A high-order polynomial can satisfy the maximum principle at a [discrete set](@entry_id:146023) of nodes while exhibiting wild oscillations between them, leading to a significant increase in the total variation. This shows that MPP alone is insufficient to control sub-cell oscillations that high-order DG methods can produce [@problem_id:3424346].

Another crucial concept is **[entropy stability](@entry_id:749023)**. For a physically relevant solution to a nonlinear conservation law, a mathematical entropy function must not increase in time. An entropy-stable scheme is one that satisfies a discrete version of this [entropy inequality](@entry_id:184404). TVD schemes for scalar laws are guaranteed to converge to the correct entropy solution. However, [entropy stability](@entry_id:749023) is a more general concept that extends more readily to [systems of conservation laws](@entry_id:755768) and can be achieved in [high-order methods](@entry_id:165413) with less intrusive modifications than the limiters required for TVD. Modern [entropy-stable schemes](@entry_id:749017) are often built from an underlying **entropy-conservative flux**, with carefully tailored numerical dissipation added to ensure entropy decay [@problem_id:3424363].

#### Order Degeneracy at Extrema and TVB Limiters

The most significant practical drawback of TVD schemes is their tendency to "clip" smooth [extrema](@entry_id:271659). At a smooth local maximum or minimum, the discrete slopes on either side will have opposite signs. A strict TVD [limiter](@entry_id:751283), designed to prevent the creation of new extrema, will interpret this as an incipient oscillation and force the local reconstruction to be flat (first-order accurate) [@problem_id:3424050]. This leads to a local degradation of accuracy to first order and a blunting of smooth peaks and valleys in the solution.

To remedy this, the concept of **Total Variation Bounded (TVB)** limiters was introduced. A TVB scheme relaxes the strict non-increasing condition, instead allowing the [total variation](@entry_id:140383) to increase by a small, controlled amount at each time step, such that the total variation remains uniformly bounded for all time, $\mathrm{TV}(U^n) \le B$. The allowed increase is calibrated to the local smoothness of the solution. Specifically, the [limiter](@entry_id:751283) is modified to permit slopes consistent with a smooth function (e.g., a parabola) by checking if the change in slope is smaller than a threshold proportional to $\Delta x^2$ and an estimate of the second derivative. This modification allows the TVB scheme to distinguish between the natural curvature of a smooth extremum and a genuine oscillation, thereby retaining [high-order accuracy](@entry_id:163460) in these critical regions where TVD schemes fail [@problem_id:3424050]. This represents a refinement of the TVD philosophy, sacrificing strict variation decay to achieve more uniform [high-order accuracy](@entry_id:163460).