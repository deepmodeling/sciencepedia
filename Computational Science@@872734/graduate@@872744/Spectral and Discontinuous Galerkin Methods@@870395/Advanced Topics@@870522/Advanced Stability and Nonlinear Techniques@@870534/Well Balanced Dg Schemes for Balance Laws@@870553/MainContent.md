## Introduction
In the simulation of many physical phenomena, from ocean currents to [stellar atmospheres](@entry_id:152088), systems are governed by hyperbolic balance laws where flux gradients are in delicate equilibrium with source terms. Standard numerical schemes often struggle to maintain this balance, introducing spurious oscillations that corrupt long-term simulations of near-equilibrium states. This article addresses this critical challenge by providing a comprehensive exploration of well-balanced Discontinuous Galerkin (DG) schemes—methods specifically designed to preserve these physical steady states to machine precision. Across the following chapters, you will gain a deep understanding of this essential numerical property. The "Principles and Mechanisms" chapter will first establish the theoretical definition of the well-balanced property and detail the primary construction techniques, such as quadrature-based balancing and [hydrostatic reconstruction](@entry_id:750464). Next, "Applications and Interdisciplinary Connections" will showcase the far-reaching impact of these methods in fields like geophysics, astrophysics, and engineering. Finally, the "Hands-On Practices" section offers a series of targeted problems to translate theoretical knowledge into practical skill, guiding you through the analysis and design of a complete well-balanced solver.

## Principles and Mechanisms

In the [numerical simulation](@entry_id:137087) of systems governed by hyperbolic balance laws, a significant challenge arises when the solution approaches a steady state. In such states, the dynamics are dominated by a delicate equilibrium between flux gradients and source terms. Standard numerical methods, designed primarily for accuracy in transient regimes, often fail to preserve these equilibria. Discretization errors can introduce spurious forces or waves that overwhelm the delicate balance, leading to non-physical oscillations and a failure to capture the correct long-time behavior. A **[well-balanced scheme](@entry_id:756693)** is a numerical method specifically designed to overcome this limitation by preserving physically relevant steady states to machine precision. This chapter elucidates the fundamental principles defining this property and explores the primary mechanisms through which it is achieved in the context of Discontinuous Galerkin (DG) methods.

### The Well-Balanced Property: From Continuous to Discrete

A general one-dimensional hyperbolic system of balance laws can be written as:
$$
\partial_t \mathbf{u} + \partial_x \mathbf{f}(\mathbf{u}) = \mathbf{s}(x, \mathbf{u})
$$
where $\mathbf{u}(x,t)$ is the vector of conserved state variables, $\mathbf{f}(\mathbf{u})$ is the [flux vector](@entry_id:273577), and $\mathbf{s}(x, \mathbf{u})$ is a source term that may depend on both position and the state. A **steady state**, denoted $\mathbf{u}^\star(x)$, is a time-independent solution, satisfying $\partial_t \mathbf{u}^\star = 0$. This implies that the solution must satisfy the following [equilibrium equation](@entry_id:749057) at every point in space:
$$
\partial_x \mathbf{f}(\mathbf{u}^\star(x)) = \mathbf{s}(x, \mathbf{u}^\star(x))
$$
This equation expresses a precise, pointwise balance between the spatial gradient of the flux and the [source term](@entry_id:269111).

It is crucial to distinguish between two classes of steady states [@problem_id:3428755]. **Trivial steady states** are those where the solution $\mathbf{u}^\star$ is spatially constant and the source term is zero. For example, for the inviscid Burgers' equation, $u_t + \partial_x(\frac{1}{2}u^2) = 0$, any constant state $u^\star(x) = c$ is a steady state because both the flux gradient and the source are zero. Such states are typically easy for [numerical schemes](@entry_id:752822) to preserve.

The more challenging and physically interesting cases are **nontrivial steady states**. These are solutions where $\mathbf{u}^\star(x)$ is not constant, and its spatial variation is a direct consequence of a non-zero [source term](@entry_id:269111) or geometric effects. A canonical example is the "lake at rest" equilibrium in the one-dimensional [shallow water equations](@entry_id:175291) [@problem_id:3428823]. These equations model the evolution of water depth $h$ and momentum $hu$ over a variable bottom topography $b(x)$:
$$
\begin{aligned}
\partial_t h + \partial_x (h u) = 0 \\
\partial_t (h u) + \partial_x \left(h u^2 + \frac{1}{2} g h^2 \right) = -g h \partial_x b
\end{aligned}
$$
Here, $g$ is the gravitational acceleration, and the term $-g h \partial_x b$ is a [source term](@entry_id:269111) arising from the gravitational force component along the bed slope. A lake at rest is characterized by zero velocity ($u=0$) and a flat free-surface elevation. The free-surface elevation is $\eta(x) = h(x) + b(x)$. The condition $\eta(x) = \text{const}$ implies that any change in bed elevation is exactly matched by a compensating change in water depth. Under these conditions ($u=0$), the momentum equation reduces to a balance between the pressure gradient and the bed-slope source:
$$
\partial_x \left( \frac{1}{2} g (h^\star)^2 \right) = -g h^\star \partial_x b
$$
This is a nontrivial equilibrium: the water depth $h^\star(x)$ varies spatially, and it is this variation that generates a pressure gradient to precisely counteract the gravitational force. Another important example is the [hydrostatic equilibrium](@entry_id:146746) in [gas dynamics](@entry_id:147692), where a pressure gradient in a column of gas balances a gravitational potential [@problem_id:3428755].

The failure of standard numerical schemes to preserve these states stems from the independent discretization of the flux and source terms. Truncation errors, though small, are sufficient to break the exact balance, leading to spurious numerical artifacts. The **well-balanced property** is a formal requirement that a numerical scheme be immune to this issue.

In the context of a DG method, where the solution is approximated by a [piecewise polynomial](@entry_id:144637) $u_h$, the definition is precise. Let $u^\star(x)$ be a continuous steady state, and let $u_h^\star$ be its representation in the DG space (e.g., its $L^2$-projection onto polynomials of degree at most $p$). The semi-discrete DG scheme can be written in [weak form](@entry_id:137295) as finding $u_h$ such that for every test function $v$ in the [polynomial space](@entry_id:269905) $\mathbb{P}^p(K_i)$ on each element $K_i$:
$$
\int_{K_i} (\partial_t u_h) v \, dx = \mathcal{R}_{K_i}(v; u_h)
$$
where $\mathcal{R}_{K_i}$ is the discrete spatial residual, which includes contributions from [volume integrals](@entry_id:183482) and numerical fluxes at element interfaces. A DG scheme is said to be well-balanced (or to satisfy the discrete C-property) if the projected steady state $u_h^\star$ is a [stationary point](@entry_id:164360) of the discrete evolution [@problem_id:3428762] [@problem_id:3428836]. This requires that the discrete residual vanishes entirely when evaluated at the steady state:
$$
\mathcal{R}_{K_i}(v; u_h^\star) = 0 \quad \text{for all test functions } v \in \mathbb{P}^p(K_i) \text{ and for all elements } K_i.
$$
This is a much stronger condition than simply preserving the cell average (which corresponds to the case $v=1$). For higher-order methods ($p \ge 1$), all polynomial moments of the solution must remain stationary, meaning the shape of the polynomial approximation within each element must not evolve in time. Achieving this requires that the discrete flux divergence and the discrete source term cancel each other out perfectly.

### Mechanisms for Achieving Well-Balancing

Several powerful techniques have been developed to construct well-balanced DG schemes. These methods hinge on carefully designing the [discretization](@entry_id:145012) of the flux and source terms so that they obey a discrete analogue of the continuous equilibrium condition.

#### Quadrature-Based Balancing

One of the most direct ways to achieve [well-balancing](@entry_id:756695) is to design a [source term discretization](@entry_id:755076) that mimics the integration-by-parts formula for the flux divergence at the discrete quadrature level. The standard DG [weak form](@entry_id:137295) on an element $K$, after integration by parts, involves terms like:
$$
\int_K f(u_h) \partial_x v \, dx \quad \text{and} \quad \int_K s(x, u_h) v \, dx
$$
The core idea is to ensure that when $u_h = u_h^\star$, the numerical approximations of these integrals, along with the interface flux terms, sum to zero.

A common pitfall is to approximate each integral with a standard high-order [quadrature rule](@entry_id:175061), chosen independently. This does not guarantee balance. The key is that the discrete terms must cancel. For a steady state $u^\star$ where $f(u^\star)_x = s(x, u^\star)$, the weak form requires that the numerical approximation of $\int_K f(u^\star)_x v \,dx$ must equal that of $\int_K s(x, u^\star) v \,dx$. To illustrate what happens when they are not treated consistently, suppose for a given test function $v$, both integrands happen to be $x^4$ on the interval $K=[-1,1]$. The exact integral for both is $\int_{-1}^1 x^4 dx = 2/5$. If the flux term integral is computed with a 3-point Gauss-Legendre rule (exact for polynomials up to degree 5), the result is exactly $2/5$. But if the source term integral is computed with a 2-point rule (only exact up to degree 3), the result is $(\frac{1}{\sqrt{3}})^4 + (-\frac{1}{\sqrt{3}})^4 = 2/9$. The mismatch creates a spurious numerical residual of $2/5 - 2/9 = 8/45$, destroying the well-balanced property due to inconsistent quadrature [@problem_id:3428767].

A constructive approach is to design the [source term discretization](@entry_id:755076) and quadrature rule in tandem. Suppose we have a known polynomial steady state $u^\star(x)$ of degree $d$ and a flux $f(u)$ that is a polynomial of degree $m$ in $u$. The continuous balance is $f(u^\star)_x = s(u^\star,x)$. Using the chain rule, this is $f'(u^\star)u_x^\star = s(u^\star,x)$. We can enforce this at the discrete level by defining a well-balanced source discretization $s^{\text{WB}}(u^\star,x) := f'(u^\star(x)) u_x^\star(x)$ [@problem_id:3428749]. The [well-balancing](@entry_id:756695) condition on the [volume integrals](@entry_id:183482) then becomes:
$$
\int_K (\partial_x v) f(u^\star) \,dx \approx \int_K v s^{\text{WB}}(u^\star,x) \,dx
$$
where the integrals are evaluated by the same $N$-point [quadrature rule](@entry_id:175061). This equality holds if the quadrature rule is *exact* for both integrands for any polynomial [test function](@entry_id:178872) $v \in \mathbb{P}^p(K)$. The integrand on the left, $(\partial_x v) f(u^\star)$, is a polynomial of degree at most $(p-1) + md$. The integrand on the right, $v s^{\text{WB}}$, is a polynomial of degree at most $p + (m-1)d + (d-1) = p + md - 1$. Both integrands have the same maximal degree. A Gauss-Legendre quadrature with $N$ points is exact for polynomials of degree up to $2N-1$. To ensure [exactness](@entry_id:268999), we need $2N-1 \ge p + md - 1$, which gives the minimal number of quadrature points as:
$$
N_{\min} = \left\lceil \frac{p + md}{2} \right\rceil
$$
This formula provides a concrete design principle: by using a sufficiently accurate [quadrature rule](@entry_id:175061), we can ensure that the discrete flux divergence and source terms balance exactly for a known class of polynomial steady states. More generally, the goal is to select a [quadrature rule](@entry_id:175061) for the source term that makes the discrete balance hold, which may sometimes involve specialized [quadrature rules](@entry_id:753909) whose nodes or weights are designed to enforce the balance condition [@problem_id:3428824].

#### Hydrostatic Reconstruction

For problems like the [shallow water equations](@entry_id:175291), where the [source term](@entry_id:269111) is related to discontinuous geometry (the bed topography $b(x)$), a powerful technique known as **[hydrostatic reconstruction](@entry_id:750464)** is often employed [@problem_id:3428798]. This method modifies the state variables at the element interfaces before they are used to compute the [numerical flux](@entry_id:145174). The goal is to create local states at the interface that are themselves in a [hydrostatic balance](@entry_id:263368).

The procedure at a DG interface with left ($L$) and right ($R$) traces of the solution $(h, u, b)$ is as follows:
1.  **Define an interface bed elevation $b_I$.** A robust choice that handles [wetting](@entry_id:147044) and drying is to take the maximum of the left and right bed elevations: $b_I = \max(b_L, b_R)$. This represents the highest point of the "weir" at the interface.
2.  **Define a common interface free-surface level $H_I$.** To ensure stability and prevent non-physical creation of water, the interface free surface is taken as the minimum of the left and right free-surface levels, $H_L = h_L + b_L$ and $H_R = h_R + b_R$. Thus, $H_I = \min(H_L, H_R)$.
3.  **Define reconstructed water depths $h_L^*$ and $h_R^*$.** Based on the common bed and free-surface levels, a single water depth $h^*$ is defined at the interface, ensuring non-negativity: $h^* = \max(0, H_I - b_I)$. This same depth is used for both left and right reconstructed states: $h_L^* = h_R^* = h^*$.
4.  **Define reconstructed momenta $(hu)_L^*$ and $(hu)_R^*$.** The original velocities are applied to the reconstructed depths: $(hu)_L^* = h_L^* u_L$ and $(hu)_R^* = h_R^* u_R$.

When this reconstruction is applied to a "lake at rest" state where $u_L=u_R=0$ and $H_L=H_R=H_0$, the reconstructed momenta $(hu)^*$ are zero and the reconstructed depths $h_L^*$ and $h_R^*$ are identical. These identical reconstructed states are then passed to a consistent numerical flux function (for a flat-bottom system). Since the input states are identical, the [numerical flux](@entry_id:145174) simply evaluates to the physical flux, and the contribution to the DG residual correctly balances the discretized source term, preserving the equilibrium.

#### Reconstruction in Equilibrium Variables

For [high-order schemes](@entry_id:750306) ($p \ge 1$) and equilibria that are not simple polynomials, representing the steady state within the polynomial DG space can introduce approximation errors that break the balance. A more sophisticated strategy is to change the variables that are being approximated. Instead of reconstructing the conservative variables (e.g., density $\rho$ and momentum $\rho u$), one can reconstruct a set of **equilibrium variables** chosen such that one of them is constant in the [equilibrium state](@entry_id:270364) [@problem_id:3428757].

Consider the barotropic Euler equations with a gravitational potential $\Phi(x)$, where the hydrostatic equilibrium is defined by $u=0$ and the balance $\partial_x p(\rho) = -\rho \partial_x \Phi$. This is equivalent to the condition $h(\rho) + \Phi(x) = \text{const}$, where $h(\rho)$ is the [specific enthalpy](@entry_id:140496). Instead of using a polynomial to approximate the generally non-polynomial [density profile](@entry_id:194142) $\rho(x)$, we can define an equilibrium variable $\Pi = h(\rho) + \Phi(x)$ and reconstruct the pair $(\rho u, \Pi)$.

The advantage of this approach is that the [equilibrium state](@entry_id:270364) ($u=0, \Pi = \text{const}$) can be represented *exactly* in the [polynomial approximation](@entry_id:137391) space, regardless of the complexity of $\rho(x)$ or $\Phi(x)$. The polynomial for $\Pi$ is simply a constant (a degree-0 polynomial), and its derivative is identically zero. Since the momentum balance can be rewritten in terms of $\rho \partial_x \Pi$, the discrete residual evaluated at the quadrature points will be exactly zero because the term $\partial_x \Pi_h$ is zero everywhere. This elegant change of variables bypasses the projection errors associated with conservative variable reconstruction and leads to exceptionally robust [well-balanced schemes](@entry_id:756694), even in the presence of strong source terms and sharp gradients in the [equilibrium state](@entry_id:270364).

### Advanced Considerations and Pitfalls

Achieving and maintaining the well-balanced property requires careful implementation, and some common numerical strategies can inadvertently destroy it. A prominent example is the use of **[operator splitting](@entry_id:634210)** for [time integration](@entry_id:170891) [@problem_id:3428772].

For a system $\partial_t U = F(U) + S(U)$, it is tempting to separately integrate the hyperbolic part (governed by the vector field $F$) and the source part (governed by $S$). A typical splitting method, such as Lie-Trotter or Strang splitting, approximates the true solution by composing the individual flows. However, this approach is generally not well-balanced.

The error introduced by splitting can be analyzed using the Baker-Campbell-Hausdorff formula. The leading error term that causes a drift away from an [equilibrium state](@entry_id:270364) $U^\star$ (where $F(U^\star) + S(U^\star) = 0$) is proportional to the **Lie commutator** of the vector fields, $[S,F] = DS(U)F(U) - DF(U)S(U)$, evaluated at the equilibrium. For the linearized [shallow water equations](@entry_id:175291), this commutator can be shown to be non-zero for a non-flat bathymetry. For a non-symmetric splitting scheme (like Godunov splitting), the drift from equilibrium is of order $\mathcal{O}(\Delta t^2)$, meaning the scheme is not even first-order well-balanced. For a symmetric scheme (like Strang splitting), the $\mathcal{O}(\Delta t^2)$ drift term vanishes, but higher-order error terms involving nested commutators remain.

The conclusion is stark: [operator splitting](@entry_id:634210), while convenient, breaks the fundamental coupling between flux and source that defines the equilibrium. To construct a truly [well-balanced scheme](@entry_id:756693), the flux and source terms must be treated in a coupled, monolithic manner within the [spatial discretization](@entry_id:172158) and time-stepping algorithm.