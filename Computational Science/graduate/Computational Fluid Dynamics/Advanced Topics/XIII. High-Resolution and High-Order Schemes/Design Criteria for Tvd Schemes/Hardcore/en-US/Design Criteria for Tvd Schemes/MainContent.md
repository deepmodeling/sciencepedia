## Introduction
The numerical solution of [hyperbolic conservation laws](@entry_id:147752), which model everything from shock waves in [gas dynamics](@entry_id:147692) to [traffic flow](@entry_id:165354), presents a classic dilemma: how can we capture sharp discontinuities without introducing [spurious oscillations](@entry_id:152404), while simultaneously maintaining high accuracy in smooth regions? Low-order schemes are robust but diffusive, smearing out important features, while high-order linear schemes are accurate but prone to creating non-physical oscillations. Total Variation Diminishing (TVD) schemes offer a powerful and elegant solution to this long-standing challenge in computational science. By introducing a data-dependent nonlinearity, these methods intelligently adapt to the local solution, providing the best of both worlds—sharp, non-oscillatory profiles and [high-order accuracy](@entry_id:163460).

This article provides a comprehensive guide to the design criteria for TVD schemes, equipping you with the theoretical foundation and practical knowledge to understand and implement them.
*   In **Principles and Mechanisms**, we will dissect the core concepts, starting with Godunov's theorem, exploring the [flux limiter](@entry_id:749485) framework, and understanding the role of [artificial viscosity](@entry_id:140376).
*   **Applications and Interdisciplinary Connections** will broaden our view, examining how these principles are applied to complex systems like the Euler equations, extended to handle [physical invariants](@entry_id:197596), and connected to fields as diverse as [image processing](@entry_id:276975) and machine learning.
*   Finally, **Hands-On Practices** will ground these concepts in practical exercises, challenging you to apply the theory to concrete numerical problems.

By navigating through these chapters, you will gain a deep understanding of one of the foundational pillars of modern high-resolution numerical methods.

## Principles and Mechanisms

The accurate numerical simulation of [hyperbolic conservation laws](@entry_id:147752), which govern phenomena characterized by the propagation of waves and discontinuities such as shocks, presents a formidable challenge. First-order numerical schemes, while robust, introduce excessive numerical dissipation, smearing sharp features across many computational cells. Conversely, classical higher-order linear schemes, such as the Lax-Wendroff method, are dispersive and tend to produce non-physical oscillations, known as the Gibbs phenomenon, in the vicinity of discontinuities. The quest for methods that are both high-order accurate in smooth regions and non-oscillatory at discontinuities led to the development of [high-resolution schemes](@entry_id:171070), among which the Total Variation Diminishing (TVD) schemes are a foundational class. This chapter elucidates the core principles and mechanisms underpinning the design of TVD schemes.

### Godunov's Order Barrier and the Role of Nonlinearity

The fundamental difficulty in constructing [high-resolution schemes](@entry_id:171070) is encapsulated by **Godunov's order barrier theorem**. This theorem states that any linear numerical scheme that preserves the [monotonicity](@entry_id:143760) of an initially monotone profile (a property closely related to being non-oscillatory) can be at most first-order accurate. This represents a significant roadblock: it seems we must choose between the high accuracy of oscillatory schemes and the low accuracy of robust, non-oscillatory ones.

The critical insight that enables us to circumvent this barrier is the realization that Godunov's theorem applies only to **linear** schemes—that is, schemes where the updated value $u_i^{n+1}$ is a linear function of the values at the previous time step, $\{u_j^n\}$. By designing a scheme that is deliberately **nonlinear**, one can evade the premises of the theorem and achieve higher-order accuracy without sacrificing the non-oscillatory property . This nonlinearity is introduced by making the numerical scheme adaptive, meaning its behavior changes based on the local features of the solution itself.

A powerful mathematical framework for formalizing the "non-oscillatory" property is the concept of **Total Variation Diminishing (TVD)**. The [total variation](@entry_id:140383) of a discrete solution on a uniform grid is defined as the sum of the absolute differences between neighboring cell values:

$$
TV(u^n) = \sum_i |u_{i+1}^n - u_i^n|
$$

A numerical scheme is said to be TVD if the [total variation](@entry_id:140383) of the discrete solution is non-increasing from one time step to the next:

$$
TV(u^{n+1}) \le TV(u^n)
$$

This condition prevents the amplification of existing oscillations and, crucially, forbids the creation of new [local extrema](@entry_id:144991) in the solution. A scheme that satisfies the TVD property is guaranteed to be stable and will produce sharp, oscillation-free profiles. The challenge, therefore, shifts to designing nonlinear, data-dependent schemes that are second-order accurate in smooth regions of the flow while rigorously satisfying the TVD condition.

### The Flux Limiter Framework

The most common and successful strategy for constructing TVD schemes is the **[flux limiter](@entry_id:749485)** approach. This method intelligently combines a robust, first-order monotone flux with a more accurate, higher-order flux. There are two conceptually equivalent ways to view this construction.

One perspective is to view the final numerical flux, $F_{i+1/2}$, as a blend of a low-order (monotone) flux, $F^{LO}$, and a high-order flux, $F^{HO}$:

$$
F_{i+1/2} = F^{LO} + \chi \left( F^{HO} - F^{LO} \right)
$$

Here, $\chi$ is a **switching function** that depends on the local smoothness of the solution. In smooth regions, $\chi$ approaches $1$, activating the high-order flux to achieve high accuracy. Near discontinuities, $\chi$ approaches $0$, causing the scheme to revert to the robust, non-oscillatory low-order flux .

A more practical and widely analyzed formulation expresses the [numerical flux](@entry_id:145174) as a first-order monotone flux plus a limited correction or "anti-diffusive" term. For a [scalar conservation law](@entry_id:754531) $u_t + f(u)_x = 0$ and assuming [upwind differencing](@entry_id:173570) (e.g., [characteristic speed](@entry_id:173770) $f'(u) > 0$), the first-order [upwind flux](@entry_id:143931) is highly dissipative. A higher-order scheme like Lax-Wendroff can be constructed by adding a corrective term. The TVD approach introduces a limiter function, $\phi$, to modulate this correction. A [canonical form](@entry_id:140237) for the flux is:

$$
F_{i+1/2} = F_{i+1/2}^{\text{upwind}} + \frac{1}{2} a(1-\nu) \phi(r_i) (u_{i+1} - u_i)
$$

where $\nu = a \Delta t / \Delta x$ is the Courant number for [linear advection](@entry_id:636928) with speed $a$. The crucial new element is the **[flux limiter](@entry_id:749485) function** $\phi(r_i)$, which is a function of a **smoothness indicator**, $r_i$. This indicator is typically defined as the ratio of consecutive solution gradients. For an upwind-biased scheme considering the interface $i+1/2$, the relevant gradients are in the upwind direction (cell $i$) and the local direction (across cells $i$ and $i+1$):

$$
r_i = \frac{u_i - u_{i-1}}{u_{i+1} - u_i}
$$

When the solution is smooth, the gradients are nearly equal, and $r_i \approx 1$. If there is a local extremum at cell $i$, the gradients will have opposite signs, and $r_i  0$. Near a sharp change, $r_i$ will deviate significantly from $1$.

For a scheme of this form to be TVD, the [limiter](@entry_id:751283) function $\phi(r)$ must satisfy a set of conditions first systematically analyzed by Sweby. For $r  0$, the function must lie within the so-called **TVD region**:

$$
0 \le \phi(r) \le \min(2r, 2)
$$

Furthermore, to prevent the creation of new [extrema](@entry_id:271659), the [limiter](@entry_id:751283) must vanish when the gradient changes sign:

$$
\phi(r) = 0 \quad \text{for } r \le 0
$$

Finally, for the scheme to achieve [second-order accuracy](@entry_id:137876) in smooth regions where $r \approx 1$, the limiter must satisfy:

$$
\phi(1) = 1
$$

This framework provides a clear recipe for design: choose a function $\phi(r)$ that lies within the prescribed region and satisfies the endpoint conditions, and the resulting scheme will be a high-resolution TVD scheme  .

### A Deeper Look: Artificial Viscosity and the Modified Equation

To gain a more profound understanding of how [flux limiters](@entry_id:171259) work, we can perform a **[modified equation analysis](@entry_id:752092)**. This technique involves taking a discrete numerical scheme and, through Taylor series expansions, deriving the partial differential equation that it *actually* solves, including leading-order error terms.

Let us consider the simple [linear advection equation](@entry_id:146245), $u_t + a u_x = 0$, with $a  0$. The [first-order upwind scheme](@entry_id:749417) is $u_i^{n+1} = u_i^n - \nu(u_i^n - u_{i-1}^n)$, where $\nu = a \Delta t / \Delta x$. By performing a Taylor expansion of each term and eliminating higher-order time derivatives using the original PDE, one finds that the modified equation for the [upwind scheme](@entry_id:137305) is, to leading order:

$$
u_t + a u_x = \left[ \frac{a \Delta x}{2}(1-\nu) \right] u_{xx} + O(\Delta x^2)
$$

This reveals that the [first-order upwind scheme](@entry_id:749417) does not solve the pure advection equation, but rather a [convection-diffusion equation](@entry_id:152018). The term on the right-hand side, $D_{\mathrm{up}} = \frac{a \Delta x}{2}(1-\nu)$, is an **[artificial viscosity](@entry_id:140376)** or **[numerical diffusion](@entry_id:136300)** coefficient. It is this term, proportional to the grid spacing $\Delta x$, that is responsible for the excessive smearing of sharp profiles .

Now, if we perform the same analysis on the flux-limited scheme, we find a remarkable result. The modified equation becomes :

$$
u_t + a u_x = \left[ \frac{a \Delta x}{2}(1-\nu)(1 - \phi(r)) \right] u_{xx} + O(\Delta x^2)
$$

The effective [artificial viscosity](@entry_id:140376) is now $D_{\mathrm{eff}} = D_{\mathrm{up}}(1 - \phi(r))$. This expression perfectly illuminates the adaptive nature of the scheme.
-   In **smooth regions**, the solution varies gently, so $r \approx 1$. Since TVD limiters are designed with $\phi(1) = 1$, the term $(1 - \phi(r))$ approaches zero. The [artificial viscosity](@entry_id:140376) is effectively cancelled to leading order, and the scheme behaves as a higher-order, low-dissipation method.
-   Near **discontinuities or [extrema](@entry_id:271659)**, the ratio $r$ deviates from $1$. For an extremum, $r \le 0$, which means $\phi(r) = 0$. In this case, $D_{\mathrm{eff}} = D_{\mathrm{up}}$. The scheme automatically adds the full amount of first-order artificial viscosity, suppressing oscillations and robustly capturing the sharp feature.

The [flux limiter](@entry_id:749485) thus acts as an intelligent switch, turning off [numerical dissipation](@entry_id:141318) where it is not needed (to preserve accuracy) and turning it on where it is essential (to prevent oscillations).

### A Gallery of Common Flux Limiters

The TVD framework allows for a wide variety of limiter functions $\phi(r)$, each conferring different properties to the resulting scheme. The choice of [limiter](@entry_id:751283) represents a trade-off, typically between sharpness of captured discontinuities and robustness. A [limiter](@entry_id:751283) with larger values of $\phi(r)$ is considered more **compressive**, as it applies less dissipation and resolves shocks more sharply. Here are four classic examples :

-   **[minmod](@entry_id:752001):** $\phi(r) = \max(0, \min(1, r))$. This is the most dissipative of the common limiters and lies on the lower boundary of the TVD region. It is very robust but can smear discontinuities.

-   **van Leer:** $\phi(r) = \frac{r + |r|}{1 + |r|}$. For $r  0$, this simplifies to $\phi(r) = \frac{2r}{1+r}$. This [limiter](@entry_id:751283) is continuously differentiable (except at $r=0$) and is more compressive than [minmod](@entry_id:752001).

-   **Monotonized Central (MC):** $\phi(r) = \max(0, \min(2r, \frac{1+r}{2}, 2))$. This [limiter](@entry_id:751283) is designed to be more compressive than van Leer while remaining smooth in its definition.

-   **superbee:** $\phi(r) = \max(0, \min(2r, 1), \min(r, 2))$. This limiter lies on the upper boundary of the TVD region and is the most compressive of these examples. It is excellent for resolving [contact discontinuities](@entry_id:747781) but can sometimes "flatten" smooth peaks or cause "staircasing" of oblique shocks.

For all $r \ge 0$, the following ordering of compressiveness holds:

$$
\phi_{\text{superbee}}(r) \ge \phi_{\text{MC}}(r) \ge \phi_{\text{van Leer}}(r) \ge \phi_{\text{minmod}}(r)
$$

Consequently, for an identical problem, one expects the thickness of a numerically captured shock to follow the reverse order: superbee will produce the thinnest shock, and [minmod](@entry_id:752001) the thickest .

### TVD Schemes for Systems of Conservation Laws

Extending the TVD concept from scalar equations to [systems of conservation laws](@entry_id:755768), such as the Euler equations of gas dynamics, is a critical step. A naive approach of applying a scalar limiter to each component of the conserved variable vector (e.g., density, momentum, energy) independently is fundamentally flawed. This is because the components of the system are nonlinearly coupled and do not propagate independently. Such a procedure fails to respect the underlying wave physics and can generate severe, non-physical oscillations .

The correct and physically consistent approach is to apply the limiting procedure in **characteristic space**. For any hyperbolic system, it is possible to find a basis of eigenvectors in which the system locally decouples into a set of scalar advection equations. Each of these equations corresponds to a **characteristic field** that propagates at its own **[characteristic speed](@entry_id:173770)** (the corresponding eigenvalue). The TVD design criterion is then applied to each of these scalar characteristic fields independently.

The full procedure, often implemented within the Monotonic Upstream-centered Schemes for Conservation Laws (MUSCL) framework, proceeds as follows  :

1.  **Local Linearization:** At each cell interface $i+1/2$, the Jacobian matrix of the flux, $A(u) = \partial f / \partial u$, is evaluated at an appropriate local average of the states $u_i$ and $u_{i+1}$ (e.g., the Roe average). This provides the local eigenvalues $\lambda_p$ and the matrices of left ($L$) and right ($R$) eigenvectors.

2.  **Characteristic Projection:** The differences in the solution between neighboring cells (e.g., $\Delta u_i = u_{i+1} - u_i$) are projected onto the basis of left eigenvectors to obtain the jumps in the [characteristic variables](@entry_id:747282): $\Delta w_i = L \Delta u_i$. Each component $(\Delta w_i)_p$ represents the strength of the jump associated with the $p$-th characteristic wave.

3.  **Scalar Limiting:** For each characteristic field $p$, a smoothness ratio $r_p$ is computed from the characteristic jumps. A scalar [flux limiter](@entry_id:749485) $\phi(r_p)$ is then applied to compute a limited characteristic increment.

4.  **Reconstruction:** The limited characteristic increments are transformed back to physical space by multiplying with the right eigenvector matrix $R$. This yields a single, limited slope vector for the [conserved variables](@entry_id:747720), which is then used to reconstruct the high-order interface values $u_{L, i+1/2}$ and $u_{R, i+1/2}$.

5.  **Flux Evaluation:** The reconstructed states are used as input to an approximate Riemann solver to compute the [numerical flux](@entry_id:145174) $F_{i+1/2}$.

This characteristic-based limiting is built upon a robust first-order scheme. The foundation must be a **monotone base flux**, which is guaranteed to be TVD in its own right. Suitable choices are derived from monotone Riemann solvers such as the Godunov solver, the local Lax-Friedrichs (Rusanov) solver, or the Harten-Lax-van Leer (HLL) solver. Non-monotone solvers like the Roe solver without an [entropy fix](@entry_id:749021) are unsuitable as a base because they can generate non-physical waves on their own, a flaw that a [limiter](@entry_id:751283) cannot universally correct .

### The Role of Time Integration: Strong Stability Preservation

The discussion thus far has focused on the [spatial discretization](@entry_id:172158), which leads to a system of ordinary differential equations (ODEs) of the form $\frac{du}{dt} = L(u)$, where $L(u)$ is the TVD spatial operator. For the fully discrete scheme to be TVD, the [time integration](@entry_id:170891) method must also preserve this property.

A simple forward Euler step, $u^{n+1} = u^n + \Delta t L(u^n)$, is guaranteed to be TVD only if the time step $\Delta t$ is sufficiently small, i.e., $\Delta t \le \Delta t_{\mathrm{FE}}$, where $\Delta t_{\mathrm{FE}}$ is the maximum allowable forward Euler time step. To achieve higher-order accuracy in time, one might be tempted to use a standard Runge-Kutta (RK) method. However, not all higher-order RK methods will preserve the TVD property, even if the CFL condition is met.

Methods that do preserve the TVD property are known as **Strong Stability Preserving (SSP)** [time integrators](@entry_id:756005). The key insight behind SSP methods is that they can be expressed as a convex combination of forward Euler steps . A general explicit SSP Runge-Kutta method takes the form:

$$
u^{(k)} = \sum_{j=0}^{k-1} \left( \alpha_{kj} u^{(j)} + \beta_{kj} \Delta t L(u^{(j)}) \right), \quad \text{with } \alpha_{kj} \ge 0, \beta_{kj} \ge 0
$$

where $u^{(0)} = u^n$ and the final stage is $u^{n+1}$. By ensuring all coefficients are non-negative and each internal forward Euler-like step uses an effective time step that satisfies the first-order TVD constraint, the overall scheme can be proven to be TVD by a simple inductive argument using the convexity of the [total variation norm](@entry_id:756070). For such a method, the TVD property is maintained under a modified time step restriction $\Delta t \le c \cdot \Delta t_{\mathrm{FE}}$, where $c$ is the **SSP coefficient** of the method. For the popular third-order Shu-Osher RK method, the coefficient is $c=1$.

The necessity of using an SSP method cannot be overstated. If a non-SSP time integrator is coupled with a TVD spatial operator, the fully discrete scheme may fail to be TVD. It is possible to construct examples where such a combination leads to an *increase* in [total variation](@entry_id:140383), reintroducing the very oscillations the spatial limiter was designed to eliminate .

### Limitations and Advanced Topics

While the TVD framework has been enormously influential and successful, it is important to recognize its limitations, which have motivated further research and the development of even more advanced schemes.

#### Extension to Multiple Dimensions

Extending the TVD property to multiple spatial dimensions is notoriously difficult. A theorem by Goodman and LeVeque proves that any scheme for a 2D [linear advection equation](@entry_id:146245) that is TVD along all grid lines must be at most first-order accurate. Since [high-resolution schemes](@entry_id:171070) are second-order, they cannot be TVD in this strong sense.

In practice, a common approach is to apply the 1D characteristic-based limiting procedure dimension by dimension. While this works perfectly for flows aligned with the grid, it can fail for flows oblique to the grid. A canonical failure case involves advecting a discontinuity diagonally across a Cartesian mesh. The independent limiting in the $x$- and $y$-directions fails to correctly interpret the diagonal structure of the flow, leading to spurious "checkerboard" or "carbuncle" oscillations near cell corners . This highlights that robust multidimensional schemes require genuinely multidimensional limiters that constrain the gradient vector as a whole, rather than its components separately.

#### Entropy Satisfaction

A conservation law can admit multiple [weak solutions](@entry_id:161732), but only one is physically relevant—the one that satisfies the **[entropy condition](@entry_id:166346)**. This condition ensures that information flows correctly and prohibits non-physical phenomena like expansion shocks. A fundamental question is whether a TVD scheme is guaranteed to converge to the correct entropy solution.

The answer is subtle. The TVD property itself guarantees stability and convergence to *a* weak solution by suppressing oscillations. It does not, however, directly guarantee entropy satisfaction for every possible convex entropy function. For example, one can construct a scenario where the standard [upwind flux](@entry_id:143931)—which is part of a monotone and thus entropy-satisfying scheme—violates a specific algebraic condition (the "E-flux" condition) sufficient for entropy satisfaction for a non-standard entropy function like $U(u) = u^4/4$ .

In practice, the property that ensures entropy satisfaction for first-order schemes is **[monotonicity](@entry_id:143760)**, which is a stronger condition than being TVD. High-resolution TVD schemes are designed to revert to a monotone scheme near discontinuities. This mechanism is often sufficient to guide the solution toward the physically correct state. However, it is the underlying [monotonicity](@entry_id:143760), not the TVD property alone, that provides the more fundamental connection to the [entropy condition](@entry_id:166346).