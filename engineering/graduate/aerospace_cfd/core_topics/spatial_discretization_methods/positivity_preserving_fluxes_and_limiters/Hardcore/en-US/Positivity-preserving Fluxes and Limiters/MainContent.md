## Introduction
In computational physics and engineering, simulations governed by [hyperbolic conservation laws](@entry_id:147752) must often preserve the positivity of key physical quantities, such as mass density, species concentration, or internal energy. In computational fluid dynamics (CFD), for instance, quantities like density and pressure must remain positive to ensure physical realism and [numerical stability](@entry_id:146550). Standard high-order [numerical schemes](@entry_id:752822), while accurate, can generate unphysical negative values that cause a simulation to fail. This article provides a comprehensive overview of positivity-preserving fluxes and limiters—the essential numerical tools that allow for both high-fidelity and robust simulations across a range of scientific disciplines.

This article is structured to build your expertise from the ground up. You will learn:
*   **Principles and Mechanisms:** Delve into the mathematical definition of the physically admissible state space and understand why preserving it is non-negotiable. We will explore the robust foundation provided by first-order monotone fluxes and dissect the challenges posed by [high-order schemes](@entry_id:750306), introducing the systematic limiting techniques developed to overcome them.
*   **Applications and Interdisciplinary Connections:** Discover how these methods are not just theoretical constructs but are vital for solving real-world problems. We will examine their application from core [gas dynamics](@entry_id:147692) and [reactive flows](@entry_id:190684) to diverse fields like [geophysics](@entry_id:147342), plasma physics, and astrophysics, showcasing their remarkable versatility.
*   **Hands-On Practices:** Solidify your understanding by working through targeted problems that guide you from deriving the fundamental energy constraints to applying time-step conditions for advanced, [high-order schemes](@entry_id:750306).

By the end of this journey, you will have a deep appreciation for the principles and practices that ensure CFD simulations are not only accurate but also physically sound and numerically indestructible.

## Principles and Mechanisms

In the numerical simulation of fluid dynamics, particularly in the high-speed compressible flows characteristic of aerospace applications, the governing equations impose strict physical constraints on the solution. The density $\rho$ and thermodynamic pressure $p$ must remain positive to represent a physically realizable medium. A numerical scheme that fails to preserve these properties will not only produce nonsensical results but will also encounter catastrophic mathematical failure, leading to solver divergence. This chapter elucidates the fundamental principles underlying this requirement and details the primary mechanisms through which modern [numerical schemes](@entry_id:752822) are designed to enforce it, ensuring both robustness and high-fidelity results.

### The Invariant Domain of Admissible States

The compressible Euler equations govern the evolution of a fluid state described by the vector of [conserved variables](@entry_id:747720) $\boldsymbol{U} = (\rho, \rho\boldsymbol{u}, E)^T$, representing density, momentum, and total energy density, respectively. For a [calorically perfect gas](@entry_id:747099), the [thermodynamic state](@entry_id:200783) is closed by the [ideal gas law](@entry_id:146757), which connects pressure $p$, density $\rho$, and specific internal energy $e$ via $p = (\gamma - 1)\rho e$, where $\gamma > 1$ is the ratio of specific heats. The total energy density $E$ is the sum of the internal energy density and the kinetic energy density: $E = \rho e + \frac{1}{2}\rho |\boldsymbol{u}|^2$.

For a state to be physically meaningful, it must reside within a specific region of the state space known as the **admissible set**, denoted by $\mathcal{G}$. This set is defined by the constraints of positive density and positive internal energy.

$\mathcal{G} = \{ (\rho, \rho\boldsymbol{u}, E) \,:\, \rho > 0 \text{ and } e > 0 \}$

Let us derive the explicit conditions on the conservative variables that define this set . The requirement $\rho > 0$ is self-evident. The requirement $e > 0$, combined with the equation of state $p = (\gamma-1)\rho e$ and the physical fact that $\gamma > 1$, is equivalent to requiring $p > 0$. To express the condition $e > 0$ in terms of the conservative variables, we first solve for $e$ from the definition of total energy:
$e = \frac{E}{\rho} - \frac{1}{2}|\boldsymbol{u}|^2 = \frac{E}{\rho} - \frac{1}{2}\frac{|\rho\boldsymbol{u}|^2}{\rho^2}$.
Substituting this into the condition $e > 0$ yields:
$\frac{E}{\rho} - \frac{1}{2}\frac{(\rho\boldsymbol{u}) \cdot (\rho\boldsymbol{u})}{\rho^2} > 0$.

Multiplying by the positive density $\rho$, we obtain the crucial inequality:
$E > \frac{|\rho\boldsymbol{u}|^2}{2\rho}$.

This inequality states that the total energy density must be strictly greater than the kinetic energy density. The excess energy is precisely the internal energy density, which must be positive to ensure a positive pressure and temperature. Therefore, the admissible set is formally defined as:
$\mathcal{G} = \{ (\rho, \rho\boldsymbol{u}, E) \,:\, \rho > 0 \text{ and } E - \frac{|\rho\boldsymbol{u}|^2}{2\rho} > 0 \}$.
The boundary of this set, where $E = |\rho\boldsymbol{u}|^2/(2\rho)$, corresponds to a state of zero pressure and absolute zero temperature—a physical limit the numerical solution must not cross.

The preservation of this invariant domain is not merely a matter of physical fidelity; it is a fundamental mathematical necessity for the well-posedness of the problem . Many numerical operations, particularly in [high-order schemes](@entry_id:750306) that reconstruct primitive variables $(\rho, \boldsymbol{u}, p)^T$, involve division by $\rho$. If $\rho \to 0$ or becomes negative, these operations become numerically unstable or singular. More fundamentally, the hyperbolicity of the Euler equations depends on the system's flux Jacobian matrix having a full set of real eigenvalues. These eigenvalues, which represent the characteristic wave speeds of the flow (e.g., $u-c, u, u+c$ in one dimension), depend on the speed of sound, $c = \sqrt{\gamma p / \rho}$. If $\rho \le 0$ (while $p$ remains positive), or vice-versa, the quantity $p/\rho$ becomes negative, rendering the speed of sound $c$ an imaginary number. This leads to [complex eigenvalues](@entry_id:156384), transforming the character of the governing partial differential equations from hyperbolic to elliptic. A time-dependent initial-value problem for an elliptic system is ill-posed, meaning that infinitesimal perturbations can grow unboundedly, leading to immediate numerical divergence. Consequently, any robust numerical scheme must guarantee that its updated solution remains within the admissible set $\mathcal{G}$ at every step.

### Monotone Fluxes and First-Order Schemes: The Positivity-Preserving Foundation

The simplest [numerical schemes](@entry_id:752822), first-order [finite volume methods](@entry_id:749402), provide the theoretical foundation for [positivity preservation](@entry_id:1129981). A [first-order method](@entry_id:174104) updates the cell average $\boldsymbol{U}_i$ using a [numerical flux](@entry_id:145174) $\boldsymbol{F}^*$ that depends only on the constant states in the immediately adjacent cells, $\boldsymbol{U}_i$ and $\boldsymbol{U}_{i+1}$.
$\boldsymbol{U}_i^{n+1} = \boldsymbol{U}_i^n - \frac{\Delta t}{\Delta x} (\boldsymbol{F}^*_{i+1/2} - \boldsymbol{F}^*_{i-1/2})$

A key result, central to the theory of conservation laws, is that if the [numerical flux](@entry_id:145174) is a **monotone flux**, the updated state $\boldsymbol{U}_i^{n+1}$ can be expressed as a **convex combination** of the states at the previous time step, provided a Courant-Friedrichs-Lewy (CFL) condition is satisfied . For example, the update can be written in the form $\boldsymbol{U}_i^{n+1} = C_{-1}\boldsymbol{U}_{i-1}^n + C_0\boldsymbol{U}_i^n + C_1\boldsymbol{U}_{i+1}^n$, where the coefficients $C_j$ are non-negative and sum to one.

The admissible set $\mathcal{G}$ is a **[convex set](@entry_id:268368)**. This means that for any two states $\boldsymbol{U}_a, \boldsymbol{U}_b \in \mathcal{G}$, any [linear combination](@entry_id:155091) $\theta \boldsymbol{U}_a + (1-\theta)\boldsymbol{U}_b$ for $\theta \in [0,1]$ also lies in $\mathcal{G}$. This property extends to combinations of multiple states. Therefore, if the initial states $\boldsymbol{U}_{i-1}^n, \boldsymbol{U}_i^n, \boldsymbol{U}_{i+1}^n$ are all in $\mathcal{G}$, their convex combination $\boldsymbol{U}_i^{n+1}$ is guaranteed to be in $\mathcal{G}$ as well. This property is known as **invariant-domain preservation**.

A widely used example of a monotone flux is the **Local Lax-Friedrichs (LLF)** or **Rusanov flux** . Its formula at the interface between a left state $\boldsymbol{U}_L$ and a right state $\boldsymbol{U}_R$ is:
$\boldsymbol{F}_{LLF}(\boldsymbol{U}_L, \boldsymbol{U}_R) = \frac{1}{2}(\boldsymbol{F}(\boldsymbol{U}_L) + \boldsymbol{F}(\boldsymbol{U}_R)) - \frac{1}{2}\alpha(\boldsymbol{U}_R - \boldsymbol{U}_L)$

Here, $\alpha$ is a numerical dissipation parameter representing an estimate of the maximum signal speed at the interface. For the scheme to be monotone and thus positivity-preserving, $\alpha$ must be an upper bound on the spectral radii of the flux Jacobians for both the left and right states. For the 1D Euler equations, this means:
$\alpha_{i+1/2} \ge \max( |\boldsymbol{u}_L| + c_L, |\boldsymbol{u}_R| + c_R )$
where the velocities and sound speeds are evaluated from the states $\boldsymbol{U}_i^n$ and $\boldsymbol{U}_{i+1}^n$. A [global maximum](@entry_id:174153) over all cells also suffices but is more dissipative.

Because first-order schemes use a [piecewise-constant reconstruction](@entry_id:753441), the pointwise value of the solution within a cell is identical to its cell average. Therefore, if the cell-average update is positivity-preserving, the pointwise solution is automatically guaranteed to be positive everywhere . This makes first-order [monotone schemes](@entry_id:752159) unconditionally robust building blocks for more advanced methods.

### The Challenge of High-Order Accuracy

High-order schemes, such as MUSCL, WENO, or Discontinuous Galerkin (DG) methods, achieve superior accuracy by representing the solution within each cell using polynomials of degree one or higher. This non-constant reconstruction, however, is the primary source of positivity violations. The reconstructed polynomial can exhibit **overshoots and undershoots**, creating pointwise values that lie outside the range of the neighboring cell averages . These spurious oscillations can cause the reconstructed density or pressure at an interface or a quadrature point to become negative, even if all cell averages are strictly positive.

It is crucial to distinguish between different notions of numerical stability. A scheme can be **Total Variation Diminishing (TVD)** for the [conserved variables](@entry_id:747720)—meaning it does not create new [local extrema](@entry_id:144991) in the solution profiles of $\rho$, $\rho u$, and $E$—and still fail to be positivity-preserving . This is because the pressure is a nonlinear function of the conservative variables. A state vector $\boldsymbol{U}^*$ whose components lie within the bounds of its neighbors may still correspond to a [negative pressure](@entry_id:161198) $p(\boldsymbol{U}^*)  0$.

Furthermore, the choice of [time integration](@entry_id:170891) scheme is critical. **Strong Stability Preserving (SSP)** methods are specifically designed for evolving solutions with [monotonicity](@entry_id:143760) properties. An SSP Runge-Kutta method can be expressed as a convex combination of forward Euler steps. If the forward Euler step is positivity-preserving (when applied to a suitable [spatial discretization](@entry_id:172158)), then the full SSP-RK update will also be positivity-preserving under an appropriate CFL condition. In contrast, a non-SSP time integrator, such as the classical [explicit midpoint method](@entry_id:137018), cannot be written in this form. It may introduce negative coefficients into its combined stencil, which can create negative values from positive data even when the CFL condition for the forward Euler step is satisfied .

### Techniques for High-Order Positivity Preservation

To reconcile [high-order accuracy](@entry_id:163460) with the strict requirement of positivity, a limiting strategy is necessary. Modern methods do not resort to ad-hoc fixes like simply clipping negative values, as this approach is non-conservative and destroys accuracy . Instead, they employ systematic, conservative limiting procedures.

#### Fallback Strategies and A Posteriori Limiting

One class of methods, such as the **Multidimensional Optimal Order Detection (MOOD)** scheme, adopts an a posteriori approach . It first computes a candidate solution with a high-order, unlimited scheme. Then, it checks if the resulting cell averages satisfy the physical constraints ($\rho > 0, p > 0$). If a cell is found to be "troubled" (i.e., non-physical), its high-order update is rejected, and the solution for that cell is recomputed using a robust, first-order monotone scheme. This strategy leverages the [guaranteed positivity](@entry_id:1125838) of the [first-order method](@entry_id:174104) as a safe fallback.

#### Flux-Corrected Transport (FCT)

The **Flux-Corrected Transport (FCT)** method provides a systematic way to blend low- and [high-order schemes](@entry_id:750306) at the flux level . The procedure involves several steps:
1.  **Decomposition:** The [numerical flux](@entry_id:145174) is decomposed into a low-order monotone flux $\boldsymbol{F}^L$ (e.g., Rusanov) and a high-order antidiffusive correction $\boldsymbol{D}$, such that $\boldsymbol{F}^{H} = \boldsymbol{F}^L + \boldsymbol{D}$.
2.  **Low-Order Update:** A provisional, guaranteed-positive solution $\boldsymbol{U}^{n+1, L}$ is computed using only the low-order flux $\boldsymbol{F}^L$.
3.  **Limiting:** The antidiffusive fluxes $\boldsymbol{D}$ are limited to ensure they do not create any new undershoots or overshoots. The total amount of antidiffusive flux that can be removed from a cell is bounded by the "capacity" provided by the positive low-order solution $\boldsymbol{U}^{n+1, L}$.
4.  **Correction:** The final solution is computed by adding the limited antidiffusive fluxes to the low-order solution. The [limiting factors](@entry_id:196713) are calculated to be symmetric across cell faces, ensuring the correction step remains strictly conservative.

#### Scaling Limiters for Invariant-Domain Preservation

The most prevalent modern approach, pioneered by Zhang and Shu, is to apply a scaling limiter directly to the reconstructed states or fluxes to ensure they remain within the admissible set $\mathcal{G}$ before they are used in the update formula. This is an a priori method.

The core of this method relies on the insight that the updated cell average $\boldsymbol{\bar{U}}_j^{n+1}$ from a forward Euler step can be written as a convex combination of the solution values at the quadrature points used by the spatial discretization (e.g., in a DG scheme) . Therefore, if we can guarantee that the solution polynomial is positive at all quadrature points, the updated cell average will be positive.

The limiter enforces this condition by modifying the high-order polynomial reconstruction in any cell where a violation is detected. A common form of this **scaling limiter** is:
$\boldsymbol{U}_h^{\text{new}}(x) = \boldsymbol{\bar{U}}_j + \theta(\boldsymbol{U}_h(x) - \boldsymbol{\bar{U}}_j)$, where $\theta \in [0, 1]$.

This operation scales the oscillatory part of the polynomial, $(\boldsymbol{U}_h(x) - \boldsymbol{\bar{U}}_j)$, back towards the mean value $\boldsymbol{\bar{U}}_j$. The key properties of this limiter are:
1.  **Conservation:** It exactly preserves the cell average $\boldsymbol{\bar{U}}_j$ for any choice of $\theta$.
2.  **Accuracy Preservation:** In regions where the solution is smooth and strictly positive, the [high-order reconstruction](@entry_id:750305) $\boldsymbol{U}_h(x)$ will also be strictly positive for a sufficiently small mesh size $\Delta x$. In such cases, no limiting is required, $\theta$ is set to $1$, and the full [high-order accuracy](@entry_id:163460) of the scheme is retained .

The parameter $\theta$ is chosen as the largest value in $[0,1]$ that ensures the limited state $\boldsymbol{U}_h^{\text{new}}(x)$ is in the admissible set $\mathcal{G}$ at all relevant quadrature points. This involves solving a set of algebraic inequalities. For each quadrature point, we must satisfy:
1.  $\rho^{\text{new}} \ge \epsilon$
2.  $p(\boldsymbol{U}^{\text{new}}) \ge \epsilon$ (where $\epsilon$ is a small positive floor)

As illustrated in a sample calculation , if we consider the limited state as a function of $\theta$, the density constraint results in a [linear inequality](@entry_id:174297) for $\theta$. The pressure constraint, $E^{\text{new}} - |\rho\boldsymbol{u}^{\text{new}}|^2/(2\rho^{\text{new}}) \ge \epsilon'$, is a more complex [rational function](@entry_id:270841) of $\theta$ that can be shown to be equivalent to a concave quadratic inequality of the form $A\theta^2 + B\theta + C \ge 0$ with $A \le 0$. The smallest of the resulting [upper bounds](@entry_id:274738) on $\theta$ from all constraints and all quadrature points is chosen for the cell.

By combining this a priori scaling limiter with a monotone numerical flux and an SSP time integrator, one can construct a high-order scheme that provably preserves positivity for the Euler equations, providing a robust and accurate tool for the most demanding CFD simulations.