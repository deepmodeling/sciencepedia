## Introduction
In the realm of high-order numerical simulations, Discontinuous Galerkin (DG) methods offer exceptional accuracy, but their efficiency with [explicit time integration](@entry_id:165797) is often hampered by a critical bottleneck. The need to adhere to a single, global time step, dictated by the most restrictive element in the mesh, means that most of the computational domain is evolved far more slowly than necessary, leading to significant inefficiency. Local Time Stepping (LTS) provides a powerful solution to this problem by allowing different parts of the mesh to advance with time steps tailored to their [local stability](@entry_id:751408) requirements, promising dramatic gains in performance.

This article provides a comprehensive exploration of LTS for DG discretizations. The first chapter, "Principles and Mechanisms," lays the theoretical groundwork, detailing the rationale behind LTS and the core challenges of maintaining conservation and accuracy at multi-rate interfaces. Building on this foundation, "Applications and Interdisciplinary Connections" explores the practical utility of LTS-DG schemes in diverse fields, from [geophysics](@entry_id:147342) to [multiphysics](@entry_id:164478), and discusses implementation on high-performance computing architectures. Finally, "Hands-On Practices" offers targeted exercises to solidify understanding and build practical implementation skills. By navigating these chapters, the reader will gain a deep understanding of how to design, analyze, and apply robust and efficient LTS schemes, transforming a theoretical concept into a practical tool for advanced [scientific computing](@entry_id:143987).

## Principles and Mechanisms

The efficiency of [explicit time integration](@entry_id:165797) schemes for Discontinuous Galerkin (DG) methods is fundamentally limited by the most restrictive element in the [computational mesh](@entry_id:168560). Local Time Stepping (LTS) methods overcome this limitation by allowing different elements to advance in time with different step sizes, tailored to their [local stability](@entry_id:751408) limits. This chapter elucidates the core principles and mechanisms that govern the design and analysis of LTS schemes, focusing on the critical challenges of maintaining conservation, accuracy, and stability at interfaces where time steps are discontinuous.

### The Rationale for Local Time Stepping

The motivation for [local time stepping](@entry_id:751411) stems directly from the stability constraints of [explicit time integration](@entry_id:165797) schemes when applied to the semi-discrete DG system. For [hyperbolic partial differential equations](@entry_id:171951), such as the advection equation $u_t + a u_x = 0$, the stability of an explicit scheme is governed by a Courant–Friedrichs–Lewy (CFL) condition. This condition dictates that the time step, $\Delta t$, must be small enough to ensure that information does not propagate across more than a fraction of an element within a single step.

For a DG [discretization](@entry_id:145012) on an element $K_e$ of size $h_e$ using polynomials of degree $p_e$, the maximum allowable time step for an explicit method is constrained by the spectral radius of the local DG spatial operator. A sharp stability analysis reveals a strong dependence on both mesh size and polynomial degree. For instance, in the case of one-dimensional [linear advection](@entry_id:636928), a [sufficient condition for stability](@entry_id:271243) often takes the form:

$$
\Delta t_e \le C \frac{h_e}{|a| \cdot f(p_e)}
$$

where $C$ is a constant depending on the specific [time integration](@entry_id:170891) scheme, $|a|$ is the wave speed, and $f(p_e)$ is a function that increases with the polynomial degree. A well-established result for many common DG formulations is that the [spectral radius](@entry_id:138984) scales quadratically with $p_e$, leading to a stability constraint of $\Delta t_e \propto h_e/p_e^2$. However, for the specific case of the 1D [linear advection](@entry_id:636928) operator, a sharper analysis shows a [linear scaling](@entry_id:197235) of the relevant eigenvalues, yielding the less restrictive bound:

$$
\Delta t_e \le \frac{C_{\text{RK}}}{|a|(2 p_e + 1)} h_e
$$

where $C_{\text{RK}}$ is a coefficient associated with the Runge-Kutta scheme used  .

This relationship highlights the core issue: in many practical simulations, computational meshes are highly non-uniform. They may contain very small elements in regions of [complex geometry](@entry_id:159080) or high gradients, alongside much larger elements elsewhere. Furthermore, adaptive methods may employ high-degree polynomials ($p$-adaptivity) in regions where the solution is smooth and low-degree polynomials where it is not. A conventional, global time-stepping scheme is forced to use a single $\Delta t$ for all elements, dictated by the minimum of all local $\Delta t_e$ across the entire mesh. This means that the vast majority of elements (the larger, lower-degree ones) are advanced with a time step that is far smaller than what their own stability would require, leading to profound computational inefficiency. Local time stepping directly addresses this by allowing each element, or groups of elements, to march forward in time with a step size appropriate to its local CFL condition, promising substantial gains in efficiency.

### The Fundamental Challenges: Interface Coupling, Conservation, and Accuracy

The principal difficulty in designing and implementing LTS schemes lies at the interfaces between elements that take different time steps. Consider a "slow" element $K_c$ taking a large step $\Delta t_c$ and an adjacent "fast" element $K_f$ taking $r$ smaller substeps, $\Delta t_f = \Delta t_c / r$. When the DG spatial operator for element $K_f$ is evaluated at one of its intermediate substep times, it requires the state of its neighbor $K_c$ at that exact moment. However, the state of $K_c$ is only naturally computed at the beginning and end of its large step $\Delta t_c$. This temporal misalignment necessitates a mechanism for predicting or interpolating states in time, which in turn raises two fundamental questions:

1.  **Conservation:** How can we ensure that the scheme remains conservative, meaning that the total mass, momentum, or energy is conserved by the discrete operator?
2.  **Accuracy:** How can we ensure that the temporal interpolation and flux evaluation at the interface are performed with sufficient accuracy to avoid degrading the [high-order accuracy](@entry_id:163460) of the underlying DG scheme?

A successful LTS method must provide a satisfactory answer to both of these questions.

### Ensuring Discrete Conservation

A cornerstone of the DG method is its [local conservation](@entry_id:751393) property, which is achieved by ensuring that the [numerical flux](@entry_id:145174) leaving one element is precisely the same as the flux entering its neighbor. For an LTS scheme to be conservative, this balance must be maintained over a common synchronization interval. For a coarse-fine interface, this means that the total flux exchanged between elements $K_c$ and $K_f$ over the coarse time step $[t^n, t^n + \Delta t_c]$ must sum to zero .

Mathematically, if $\widehat{\boldsymbol{F}}(t)$ is the [numerical flux](@entry_id:145174) vector at the interface, the conservation requirement is:
$$
\int_{t^n}^{t^n + \Delta t_c} \widehat{\boldsymbol{F}}_{c \to f}(t) \, dt = - \int_{t^n}^{t^n + \Delta t_c} \widehat{\boldsymbol{F}}_{f \to c}(t) \, dt
$$
where the subscripts denote the direction of flux transfer. Given that numerical fluxes are defined to be conservative (e.g., $\widehat{\boldsymbol{F}}(\boldsymbol{U}_A, \boldsymbol{U}_B) = - \widehat{\boldsymbol{F}}(\boldsymbol{U}_B, \boldsymbol{U}_A)$), this condition is satisfied if and only if both elements use the *same* time-integrated flux value for their updates.

However, the "fast" and "coarse" elements naturally compute this integral differently. The fast element $K_f$ computes it as a sum over its $r$ substeps, while the coarse element $K_c$ computes it in a single go. Due to differences in temporal quadrature, these two values will generally not be identical, leading to a conservation defect.

#### The Flux-Correction Method

A robust and widely used technique to enforce exact discrete conservation is the **flux-correction** (or flux-accumulation) method. The logic is as follows  :

1.  The fine element $K_f$ is advanced through its $r$ substeps. At each substep $m$, it computes an approximation to the time-averaged interface flux, $\boldsymbol{\phi}_{f}^{(m)}$, and uses it for its update.
2.  The total time-integrated flux from the perspective of the fine element is accumulated by summing these contributions: $\boldsymbol{\mathcal{F}}_{\text{fine}} = \sum_{m=1}^{r} \Delta t_f \boldsymbol{\phi}_{f}^{(m)}$.
3.  The coarse element $K_c$ is advanced using its own approximation of the time-integrated flux, $\boldsymbol{\mathcal{F}}_{\text{coarse}} = \Delta t_c \boldsymbol{\phi}_{c}$.
4.  A conservation error, $\boldsymbol{\mathcal{E}}_{\text{flux}} = \boldsymbol{\mathcal{F}}_{\text{coarse}} - \boldsymbol{\mathcal{F}}_{\text{fine}}$, arises because $\boldsymbol{\mathcal{F}}_{\text{coarse}} \neq \boldsymbol{\mathcal{F}}_{\text{fine}}$ in general.
5.  To correct this, the scheme enforces conservation by ensuring the coarse element's update effectively uses the flux calculated by the fine element. An a posteriori correction is applied to the coarse element's state. The correction increment to the cell-average state, $\Delta \overline{\boldsymbol{U}}_{c}^{\mathrm{corr}}$, is precisely the amount needed to account for the flux mismatch :

    $$
    \Delta \overline{\boldsymbol{U}}_{c}^{\mathrm{corr}} = \frac{1}{|K_{c}|} \left( \Delta t_{c} \boldsymbol{\phi}_{c} - \sum_{m=1}^{r} \Delta t_{f} \boldsymbol{\phi}_{f}^{(m)} \right)
    $$

This procedure ensures that the total change in the conserved quantities over the combined domain $K_c \cup K_f$ is zero to machine precision.

This process can be viewed through the lens of [numerical quadrature](@entry_id:136578). The goal is to compute the integral $\int_{t^n}^{t^{n+1}} \widehat{\boldsymbol{F}}(t) dt$. The fine side approximates this with a composite rule, while the coarse side uses a single-panel rule. The flux correction reconciles these two different numerical quadratures. A simple but illuminating thought experiment involves assuming the interface flux is held piecewise-constant over each of the $r$ fine substeps. To compute the total time integral exactly under this assumption, one would need exactly one quadrature point for each of the $r$ substeps. The fine side's summation naturally provides this, so the minimal number of temporal quadrature evaluations needed to exactly preserve the discrete mass is $r$ .

### Maintaining High-Order Accuracy

While conservation is paramount, the [interface coupling](@entry_id:750728) must also be accurate enough not to contaminate the high-order convergence of the DG scheme. A $q$-th order scheme must have a local truncation error (LTE) of $O(\Delta t^{q+1})$. Any additional error introduced by the LTS [interface coupling](@entry_id:750728) must be of this order or higher.

The interface error arises primarily from the mismatch in how the time-integrated flux is approximated on the two sides. Let's analyze this for a hypothetical scheme where both elements use the [trapezoidal rule](@entry_id:145375) for [time integration](@entry_id:170891), which is a second-order method ($p_t=2$). The coarse element uses a single trapezoidal step of size $\Delta t_2$, while the fine element uses a [composite trapezoidal rule](@entry_id:143582) over $q$ substeps of size $\Delta t_1 = \Delta t_2/q$. The error in approximating the integral of a smooth flux function $f(t)$ for the single step is known to be $-\frac{\Delta t_2^3}{12} f''(t) + O(\Delta t_2^4)$. For the composite rule, the error is $-\frac{\Delta t_2 \Delta t_1^2}{12} f''(t) + O(\Delta t_2^4) = -\frac{\Delta t_2^3}{12q^2} f''(t) + O(\Delta t_2^4)$.

The mismatch between the two quadrature approximations, which manifests as a conservation error before correction, is the difference between these two error terms :
$$
\mathcal{E}_{\text{iface}} = T_{\Delta t_{2}}[f] - T_{\Delta t_{1}}^{(q)}[f] \approx \left( \frac{\Delta t_2^3}{12} - \frac{\Delta t_2^3}{12q^2} \right) f''(t_n) = \frac{q^2-1}{12q^2} \Delta t_2^3 f''(t_n)
$$
Crucially, this interface mismatch error is $O(\Delta t_2^3)$. Since the intrinsic LTE of the second-order trapezoidal rule is already $O(\Delta t^3)$, this interface error does not introduce a lower-order pollution. Therefore, the global [second-order accuracy](@entry_id:137876) of the scheme is maintained .

This principle generalizes. For a scheme to achieve a global [order of accuracy](@entry_id:145189) $q$, the following conditions must be met :
1.  The time integrator used within each element must be at least $q$-th order accurate.
2.  The states of neighboring elements needed for flux calculations must be provided by a temporal interpolation or prediction method that is itself of order $q$.
3.  The quadrature rule used to approximate the time-integrated interface flux must introduce an error of order $O(\Delta t^{q+1})$ or smaller. If the solution trace is represented by a temporal polynomial of degree at most $q-1$ (a natural result of a $q$-th order RK method), the [quadrature rule](@entry_id:175061) must be exact for polynomials of degree at least $q-1$.

### A Survey of Local Time Stepping Strategies

Several families of LTS methods have been developed, each employing a different strategy for [interface coupling](@entry_id:750728) .

*   **Subcycling:** This is the classic approach, typically using integer time step ratios ($r \in \mathbb{N}$). To compute fluxes, the state of the coarse neighbor is predicted forward in time using a high-order polynomial. Conservation is enforced via flux accumulation and correction, as described above.

*   **Multirate Runge-Kutta (MRK):** These sophisticated [single-step methods](@entry_id:164989) are designed to handle non-integer time step ratios. They couple elements at all required RK stage times. When one element requires a state from a neighbor at a time that is not one of the neighbor's own stage times, the neighbor provides the state using a high-order polynomial interpolant known as a **[dense output](@entry_id:139023)** or [continuous extension](@entry_id:161021). Conservation and accuracy are achieved by ensuring the [quadrature rules](@entry_id:753909) for the time-integrated flux, defined by the RK coefficients, are consistent across the interface .

*   **Multirate Adams-Bashforth (MRAB):** These multi-step methods use an [extrapolation](@entry_id:175955) polynomial constructed from the solution's history to advance in time. At an LTS interface, an element must evaluate its [extrapolation](@entry_id:175955) polynomial using flux data that depends on the neighbor's state history, which requires interpolation of the neighbor's non-aligned history.

*   **Multirate Spectral Deferred Correction (MRSDC):** This is an iterative approach that achieves high order by successively correcting a provisional solution defined on a set of collocation nodes within a time step. At an LTS interface, neighboring elements have different sets of collocation nodes. They exchange data by evaluating their respective solution polynomials (which interpolate their own collocation point values) at the times requested by their neighbor.

### Advanced Considerations

#### Nonlinear Problems

For [nonlinear conservation laws](@entry_id:170694), such as the Euler or Burgers' equations, the interface flux itself is a nonlinear function of the left and right states. In an LTS context, the predicted states $u_L(t)$ and $u_R(t)$ are time-dependent polynomials. This means that at each point in time $t$ within the step, a new Riemann problem with states $(u_L(t), u_R(t))$ must be solved to find the Godunov flux.

Consider, for example, Burgers' equation $u_t + \partial_x(u^2/2) = 0$ at an interface where the left and right states are given by linear functions of time, $u_L(t) = 1 + 0.4t$ and $u_R(t) = -0.2 + 0.1t$ for $t \in [0, 0.5]$. To find the time-averaged Godunov flux, one must first determine the wave structure for all $t$. In this case, $u_L(t) > u_R(t)$, indicating a shock. The shock speed $s(t) = (u_L(t) + u_R(t))/2$ is also a function of time. Since $s(t) > 0$, the state at the interface is always $u_L(t)$. The Godunov flux is then $F(t) = \frac{1}{2} [u_L(t)]^2$. The final step is to compute the integral $\frac{1}{\tau} \int_0^\tau \frac{1}{2}[1+0.4t]^2 dt$ . This example illustrates the significant added complexity of applying LTS to nonlinear problems.

#### Strong Stability Preservation

For hyperbolic problems, it is often critical that the numerical scheme preserves certain nonlinear stability properties, such as being [total variation diminishing](@entry_id:140255) (TVD) or positivity-preserving. **Strong Stability Preserving (SSP)** [time integrators](@entry_id:756005) are designed to guarantee such properties, provided the simple forward Euler method is stable under some time step $\Delta t_{\text{FE}}$. An SSP method can be viewed as a convex combination of forward Euler steps.

When using LTS, preserving the SSP property is a delicate task. The entire numerical update over a full coarse step, including all substeps and interface couplings, must be decomposable into a grand convex combination of valid forward Euler steps. The main challenge is the [interface coupling](@entry_id:750728). If the state provided by a neighbor (e.g., through temporal prediction) cannot be expressed as a convex combination of valid states, the SSP property can be violated. Therefore, a key condition for an LTS scheme to be SSP is that all interface states used to evaluate fluxes at substep times must themselves be convex combinations of admissible states from the neighboring partition . Designing [coupling strategies](@entry_id:747985) that satisfy this stringent requirement is an active area of research.