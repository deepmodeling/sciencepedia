## Introduction
Simulating [nonlinear systems](@entry_id:168347) of [hyperbolic conservation laws](@entry_id:147752) is a cornerstone of modern computational science, enabling the study of phenomena from shock waves in aerospace to [plasma dynamics](@entry_id:185550) in fusion research. However, the mathematical nature of these systems permits non-unique, [weak solutions](@entry_id:161732), and standard numerical methods can suffer from catastrophic instabilities or generate physically incorrect results. To overcome this, a robust theoretical foundation is needed to guide the design of numerical schemes that are not just accurate, but provably stable.

This article addresses this fundamental challenge by introducing the framework of entropy conservative and entropy stable numerical methods. These techniques embed a discrete version of the second law of thermodynamics directly into the algorithm, providing a powerful mechanism for ensuring nonlinear stability. The reader will gain a comprehensive understanding of how to construct and apply these structure-preserving schemes. The article is structured to build knowledge progressively: "Principles and Mechanisms" will establish the theoretical groundwork, detailing the continuous [entropy condition](@entry_id:166346) and the algebraic construction of entropy conservative and stable fluxes. "Applications and Interdisciplinary Connections" will then showcase the versatility of these methods in complex, real-world problems across fluid dynamics, [geophysics](@entry_id:147342), and beyond. Finally, "Hands-On Practices" will provide concrete exercises to translate theory into practical implementation. We begin by delving into the core principles that link the physical concept of entropy to the mathematical stability of [numerical schemes](@entry_id:752822).

## Principles and Mechanisms

For nonlinear systems of [hyperbolic conservation laws](@entry_id:147752), the integral form of the equations admits [weak solutions](@entry_id:161732) that may contain discontinuities, such as shock waves. A fundamental challenge arises from the non-uniqueness of these [weak solutions](@entry_id:161732); the Rankine-Hugoniot [jump conditions](@entry_id:750965) alone are insufficient to distinguish physically relevant shocks from non-physical phenomena like expansion shocks. An additional admissibility criterion is required, which is provided by the second law of thermodynamics. This physical principle motivates the mathematical framework of entropy functions, which forms the bedrock of stability analysis for both the continuous equations and their numerical discretizations.

### The Continuous Entropy Condition

The concept of admissibility is formalized through the introduction of a mathematical **entropy pair**. An **entropy function**, denoted by $U(u)$, is a scalar, strictly [convex function](@entry_id:143191) of the vector of conserved state variables $u \in \mathbb{R}^m$. The [strict convexity](@entry_id:193965) of $U(u)$ is a crucial property that ensures the resulting analysis is meaningful. For any given entropy function, there exists a corresponding **entropy flux**, a vector-valued function $F^U(u) \in \mathbb{R}^d$, which is linked to $U(u)$ and the physical flux $f(u)$ of the conservation law.

To establish this link, consider a smooth solution $u(x,t)$ to the conservation law $\partial_t u + \nabla_x \cdot f(u) = 0$. The time evolution of the entropy density $U(u)$ is found via the [chain rule](@entry_id:147422):

$$
\partial_t U(u) = (\nabla_u U)^\top \partial_t u = -(\nabla_u U)^\top (\nabla_x \cdot f(u))
$$

For this expression to be part of a new conservation law, we must be able to write the right-hand side as the divergence of the entropy flux, $-\nabla_x \cdot F^U(u)$. By applying the [chain rule](@entry_id:147422) to the divergence of the entropy flux, $\nabla_x \cdot F^U(u) = \sum_j (\nabla_u F^U_j)^\top \partial_{x_j} u$, and comparing terms, we arrive at the **[compatibility condition](@entry_id:171102)** that defines $F^U(u)$ for a given $U(u)$:

$$
\nabla_u F^U_j(u) = (\nabla_u f_j(u))^\top v(u), \qquad j \in \{1, \dots, d\}
$$

Here, we have introduced the **entropy variables**, defined as the gradient of the entropy function with respect to the [conserved variables](@entry_id:747720): $v(u) = \nabla_u U(u)$. For any entropy pair $(U, F^U)$ satisfying this compatibility condition, all smooth solutions of the original conservation law also satisfy the local [entropy conservation](@entry_id:749018) law:

$$
\partial_t U(u) + \nabla_x \cdot F^U(u) = 0
$$

The true power of this framework becomes apparent when considering [weak solutions](@entry_id:161732). The physical admissibility criterion translates to the mathematical statement that physically relevant [weak solutions](@entry_id:161732) must satisfy the **[entropy inequality](@entry_id:184404)**:

$$
\partial_t U(u) + \nabla_x \cdot F^U(u) \le 0
$$

This inequality must hold in the sense of distributions. For a discrete shock discontinuity, it implies that the entropy flux entering the shock must be greater than or equal to the entropy flux leaving it, corresponding to a net production of entropy within the shock.

It is essential to distinguish a mathematical entropy function from other [conserved quantities](@entry_id:148503). Consider the one-dimensional compressible Euler equations. The total energy $E$ is a conserved variable, satisfying its own Rankine-Hugoniot [jump condition](@entry_id:176163) across a shock. However, because this is an equality, $E$ provides no selective power; it cannot be used to rule out unphysical expansion shocks. The [thermodynamic entropy](@entry_id:155885) $s$, in contrast, satisfies a strict inequality across a physical shock. The mathematical entropy $U(u) = -\rho s$ (where the negative sign ensures convexity) therefore also satisfies a strict inequality, making it a valid admissibility criterion. Total energy $E$ cannot serve this role.

### Discrete Entropy Analysis and Stability

The goal of a modern, structure-preserving numerical scheme is to satisfy a discrete analogue of this [entropy inequality](@entry_id:184404), thereby guaranteeing the nonlinear stability of the method. For a semi-discrete [finite volume](@entry_id:749401) or discontinuous Galerkin (DG) method, we can define the total discrete entropy as the sum of the entropy over all grid cells or elements, approximated by a suitable quadrature rule. For a one-dimensional [finite volume](@entry_id:749401) scheme on a uniform grid with spacing $\Delta x$, this is $E_h(t) = \Delta x \sum_i U(u_i(t))$. A scheme is defined as **entropy stable** if it guarantees that this total discrete entropy is non-increasing in time for periodic or isolated boundary conditions, i.e., $\frac{d}{dt} E_h(t) \le 0$.

Let's analyze the [time evolution](@entry_id:153943) of $E_h(t)$. Using the [chain rule](@entry_id:147422) and substituting the semi-discrete [finite volume](@entry_id:749401) update, $\frac{d u_i}{dt} = -\frac{1}{\Delta x}(\hat{f}_{i+1/2} - \hat{f}_{i-1/2})$, where $\hat{f}_{i+1/2}$ is the numerical flux at the interface between cells $i$ and $i+1$, we have:

$$
\frac{d E_h}{dt} = \Delta x \sum_i (\nabla_u U(u_i))^\top \frac{du_i}{dt} = \sum_i v_i^\top \left( -(\hat{f}_{i+1/2} - \hat{f}_{i-1/2}) \right)
$$

A [summation-by-parts](@entry_id:755630) manipulation (re-indexing the sum over $\hat{f}_{i-1/2}$) rearranges this into a sum over interfaces:

$$
\frac{d E_h}{dt} = \sum_i (v_{i+1} - v_i)^\top \hat{f}_{i+1/2} - (\text{boundary terms})
$$

This crucial result shows that the total rate of [entropy change](@entry_id:138294) is the sum of contributions from each internal interface. To achieve [entropy stability](@entry_id:749023), we must control the sign of these interface contributions.

### Entropy Conservative Fluxes

The first step in building an entropy-stable scheme is to design a baseline numerical flux that produces exactly zero numerical entropy at each interface. Such a flux is called **entropy conservative (EC)**. The condition for a flux $\hat{f}^{ec}$ to be entropy conservative is that its contribution to the entropy change, $(v_{i+1} - v_i)^\top \hat{f}^{ec}_{i+1/2}$, must itself have the structure of a perfect difference, allowing the global sum to telescope and cancel.

This is achieved if the flux satisfies Tadmor's identity:

$$
(v_R - v_L)^\top \hat{f}^{ec}(u_L, u_R) = \psi(u_R) - \psi(u_L)
$$

Here, $(u_L, u_R)$ are the states on the left and right of the interface, and $\psi(u)$ is the **entropy potential**, defined as $\psi(u) = v(u)^\top f(u) - F^U(u)$. If a numerical flux satisfies this condition at every interface, the total entropy change becomes a [telescoping sum](@entry_id:262349):

$$
\frac{d E_h}{dt} = \sum_i (\psi(u_{i+1}) - \psi(u_i)) - (\text{boundary terms})
$$

For periodic boundary conditions, this sum is exactly zero, meaning the discrete entropy is perfectly conserved.

The practical construction of EC fluxes is non-trivial. For the scalar Burgers' equation with entropy $U(u) = \frac{1}{2}u^2$, the unique symmetric EC flux can be found by solving Tadmor's identity, which yields:

$$
\hat{f}^{ec}(u_L, u_R) = \frac{\psi(u_R) - \psi(u_L)}{v(u_R) - v(u_L)} = \frac{\frac{1}{6}u_R^3 - \frac{1}{6}u_L^3}{u_R - u_L} = \frac{1}{6}(u_L^2 + u_L u_R + u_R^2)
$$

For systems like the compressible Euler equations, the entropy variables involve logarithms of density and pressure. Satisfying Tadmor's identity requires that the numerical flux be constructed using specific weighted averages. For a term like $[\ln(\rho)] \hat{f}_{\rho}$, to result in a desired jump $[\rho]$, the average used in $\hat{f}_{\rho}$ must be the **logarithmic mean**, $\mathcal{L}(a,b) = (b-a)/(\ln(b)-\ln(a))$. Using a simple [arithmetic mean](@entry_id:165355) would violate the identity and fail to conserve entropy. The renowned Ismail-Roe EC flux for the Euler equations is constructed by taking the [arithmetic mean](@entry_id:165355) for the velocity and the logarithmic mean for both density and pressure. It is important to note that this entropy-conservative framework is invariant under [linear transformations](@entry_id:149133) of the conservative variables but not under nonlinear transformations (e.g., to primitive variables).

### Entropy Stable Fluxes via Numerical Dissipation

Entropy conservative fluxes are centered, non-dissipative, and thus unstable in the presence of shocks. To build a physically correct and numerically robust scheme, we must introduce numerical dissipation in a way that is consistent with the second law of thermodynamics. This leads to the construction of **entropy stable (ES)** fluxes.

An ES flux is built by adding a carefully designed dissipation term to an EC flux:

$$
\hat{f}^{es}(u_L, u_R) = \hat{f}^{ec}(u_L, u_R) - \frac{1}{2} D(u_L, u_R) (v_R - v_L)
$$

The dissipation matrix $D$ must be symmetric and [positive semi-definite](@entry_id:262808). With this choice, the contribution to [entropy change](@entry_id:138294) at the interface becomes:

$$
(v_R - v_L)^\top \hat{f}^{es} = \left((v_R - v_L)^\top \hat{f}^{ec}\right) - \frac{1}{2}(v_R - v_L)^\top D (v_R - v_L) = (\psi_R - \psi_L) - \frac{1}{2}(v_R - v_L)^\top D (v_R - v_L)
$$

The rate of change of total entropy is now a sum of non-positive terms, ensuring [entropy stability](@entry_id:749023):

$$
\frac{d E_h}{dt} = -\frac{1}{2} \sum_i (v_{i+1} - v_i)^\top D_{i+1/2} (v_{i+1} - v_i) \le 0
$$

Critically, this construction maintains exact conservation for the underlying variables $(\rho, \rho u, \rho E)$. The dissipative term is equal and opposite for the two cells sharing an interface, so its contribution cancels out in the global balance of mass, momentum, and energy.

The choice of the dissipation matrix $D$ is crucial. A common approach is to relate it to the eigenvalues of the system Jacobian. For scalar problems, $D$ is a scalar $\alpha \ge 0$. A Rusanov-type (or local Lax-Friedrichs) dissipation sets $\alpha = \max(|\lambda(u_L)|, |\lambda(u_R)|)$, where $\lambda(u)$ is the characteristic speed. A Roe-type dissipation sets $\alpha$ proportional to an averaged wavespeed. While Roe-type dissipation is often less diffusive, it can fail at transonic shocks where the average wavespeed is near zero. In such cases, $\alpha$ vanishes, the scheme becomes entropy-conservative, and it fails to dissipate entropy as required by physics. A Rusanov-type dissipation, which depends on the maximum wavespeed, is more robust and ensures strict entropy dissipation even for stationary shocks.

### Application in High-Order Discontinuous Galerkin Methods

The principles of [entropy stability](@entry_id:749023) are particularly vital in high-order DG and spectral methods. In these methods, a naive collocation of the nonlinear flux term $\partial_x f(u)$ leads to **[aliasing](@entry_id:146322)** instabilities. Aliasing occurs because the nonlinear function $f(u_h)$, where $u_h$ is a degree-$N$ polynomial, is not itself a polynomial and contains higher-frequency modes. When this function is projected back onto the degree-$N$ [polynomial space](@entry_id:269905) (e.g., by evaluation at [nodal points](@entry_id:171339)), these high-frequency components are misinterpreted as low-frequency ones, which can spuriously inject energy into the system and cause it to blow up.

The modern solution to this problem is to use a **split-form** of the governing equations in conjunction with discrete operators that satisfy a **Summation-By-Parts (SBP)** property. The SBP property is a discrete analogue of integration-by-parts. By carefully designing the discrete [volume integral](@entry_id:265381) using a split form (such as a flux-differencing form built from an EC flux), it is possible to construct a DG-SBP scheme where the [volume integrals](@entry_id:183482)' contribution to the total [entropy change](@entry_id:138294) is exactly zero.

This powerful result implies that the [entropy stability](@entry_id:749023) of the entire high-order scheme is determined solely by the numerical fluxes used at the element interfaces. By employing the [entropy-stable fluxes](@entry_id:749015) $\hat{f}^{es}$ described above at all interfaces, one can construct a high-order DG-SBP scheme that is provably nonlinearly stable for general [hyperbolic systems](@entry_id:260647), elegantly taming the aliasing problem by enforcing a fundamental physical principle at the discrete level.