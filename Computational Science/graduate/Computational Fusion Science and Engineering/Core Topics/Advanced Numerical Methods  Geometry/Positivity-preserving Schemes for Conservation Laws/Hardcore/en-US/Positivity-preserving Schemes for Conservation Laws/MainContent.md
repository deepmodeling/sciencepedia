## Introduction
In the computational modeling of physical systems governed by conservation laws, ensuring that simulated quantities respect fundamental physical constraints—such as the non-negativity of density and pressure—is not just a matter of correctness, but a prerequisite for [numerical stability](@entry_id:146550). Standard numerical methods can inadvertently produce physically meaningless negative values, often causing simulations to crash. Positivity-preserving schemes are a class of advanced numerical methods designed to rigorously prevent such failures, thereby guaranteeing the physical realism and robustness of a simulation.

This article provides a comprehensive overview of the design, analysis, and application of these crucial numerical techniques. It addresses the knowledge gap between basic numerical methods and the advanced, robust schemes required for cutting-edge research in fields like fusion energy and astrophysics. Across three chapters, you will gain a deep understanding of this topic. The "Principles and Mechanisms" chapter will lay the theoretical foundation, explaining how positivity is achieved through concepts like convex combinations and invariant regions. The "Applications and Interdisciplinary Connections" chapter will demonstrate how these principles are applied to complex systems like [magnetohydrodynamics](@entry_id:264274) and connected to diverse fields from combustion to oceanography. Finally, the "Hands-On Practices" will guide you through implementing and testing these methods, solidifying your theoretical knowledge with practical skill.

## Principles and Mechanisms

In the numerical simulation of physical systems governed by conservation laws, a fundamental requirement is that the computed solution must respect essential physical constraints. For many quantities encountered in fusion plasma modeling—such as particle number density, pressure, or internal energy—this implies a strict non-negativity constraint. A numerical scheme that generates negative values for these quantities is not only producing a physically meaningless result but is often on the verge of catastrophic failure, as the mathematical model itself (e.g., equations of state, reaction rates) may become ill-defined. Therefore, the design and analysis of **[positivity-preserving schemes](@entry_id:753612)** are of paramount importance in computational science. This chapter elucidates the core principles and mechanisms underpinning these methods.

### Defining Positivity for Scalar Conservation Laws

We begin by considering a one-dimensional [scalar conservation law](@entry_id:754531), a prototype for many transport phenomena:
$$
\frac{\partial u}{\partial t} + \frac{\partial f(u)}{\partial x} = 0
$$
where $u(x,t)$ is a conserved quantity, such as a particle density, that must remain non-negative, and $f(u)$ is the flux function. In a [finite volume method](@entry_id:141374), the solution is represented by cell averages, $\bar{u}_i^n \approx \frac{1}{\Delta x} \int_{x_{i-1/2}}^{x_{i+1/2}} u(x, t^n) dx$. A numerical scheme's primary task is to evolve these cell averages in time.

A numerical scheme is defined as **positivity-preserving** if, given non-negative initial cell averages, $\bar{u}_i^0 \ge 0$ for all cells $i$, the computed cell averages remain non-negative for all subsequent times, $\bar{u}_i^n \ge 0$ for all $n > 0$. This property is not guaranteed by default and typically holds only if the time step $\Delta t$ is restricted by a **Courant–Friedrichs–Lewy (CFL) condition**, whose specific form depends on the scheme and the flux function $f(u)$ .

It is crucial to distinguish this property from other desirable attributes of numerical schemes . A scheme is **monotone** if its update operator is a [non-decreasing function](@entry_id:202520) of each of its stencil inputs. For [scalar conservation laws](@entry_id:754532) in one dimension, a consistent monotone scheme is guaranteed to satisfy a **[discrete maximum principle](@entry_id:748510)**, which states that the updated value in a cell is bounded by the minimum and maximum values of its neighbors at the previous time step. This, in turn, implies that the scheme is positivity-preserving and also **Total Variation Diminishing (TVD)**, meaning the [total variation](@entry_id:140383) of the discrete solution, $\sum_i |\bar{u}_{i+1}^n - \bar{u}_i^n|$, does not increase in time. While [monotonicity](@entry_id:143760) provides a powerful pathway to proving positivity, it is a much stricter condition than positivity itself. Many modern [high-order schemes](@entry_id:750306) are not monotone but are engineered to preserve positivity. Furthermore, the TVD property alone does not guarantee positivity, nor does positivity imply that a scheme is TVD.

### The Core Mechanism: The Convex Combination

The most fundamental mechanism for achieving positivity in a wide range of explicit [finite volume](@entry_id:749401) schemes is to formulate the update in such a way that the new cell average is a **convex combination** of the old cell averages from a local stencil.

Consider a general explicit finite volume update for a cell $i$, which is coupled to its neighbors $j(f)$ across faces $f$:
$$
\bar{u}_i^{n+1} = \bar{u}_i^n - \frac{\Delta t}{V_i} \sum_{f \in \mathcal{N}(i)} A_f \hat{F}_f^n
$$
where $V_i$ is the cell volume (or area in 2D, length in 1D), $A_f$ is the face area (or length in 2D), and $\hat{F}_f^n$ is the [numerical flux](@entry_id:145174). If the [numerical flux](@entry_id:145174) is a linear function of the states in cell $i$ and its neighbor $j(f)$, say $\hat{F}_f^n = \alpha_f \bar{u}_i^n + \beta_f \bar{u}_{j(f)}^n$ , we can rearrange the update into the form:
$$
\bar{u}_i^{n+1} = C_i \bar{u}_i^n + \sum_{f \in \mathcal{N}(i)} C_{j(f)} \bar{u}_{j(f)}^n
$$
where the coefficients are given by:
$$
C_i = 1 - \frac{\Delta t}{V_i} \sum_{f \in \mathcal{N}(i)} A_f \alpha_f \quad \text{and} \quad C_{j(f)} = - \frac{\Delta t}{V_i} A_f \beta_f
$$
If we can ensure that all these coefficients are non-negative, $C_i \ge 0$ and $C_{j(f)} \ge 0$, then if all initial averages $\bar{u}_k^n$ are non-negative, the updated average $\bar{u}_i^{n+1}$ will also be non-negative. For consistent schemes, it can often be shown that these coefficients sum to one, i.e., $C_i + \sum_f C_{j(f)} = 1$. In such cases, the update is a true convex combination. The conditions for non-negativity of the coefficients invariably lead to a CFL-type restriction on the time step $\Delta t$.

For instance, for the linear advection equation $\partial_t U + \nabla \cdot (\mathbf{a} U) = 0$ with an [upwind flux](@entry_id:143931), this principle leads directly to the classic CFL condition. The update can be expressed as a convex combination of neighbor values, and the condition that all coefficients in the combination are non-negative yields the maximal time step . For a 3D Cartesian cell of dimensions $d_x, d_y, d_z$, this condition is:
$$
\Delta t \le \frac{1}{\frac{|a_x|}{d_x} + \frac{|a_y|}{d_y} + \frac{|a_z|}{d_z}}
$$

### Constructing Positivity-Preserving First-Order Schemes

This convex combination principle provides a constructive path to designing and analyzing schemes.

A classic example is the **first-order upwind scheme** for [linear advection](@entry_id:636928), $u_t + a u_x = 0$ with $a > 0$. The update is $\bar{u}_i^{n+1} = (1 - \lambda) \bar{u}_i^n + \lambda \bar{u}_{i-1}^n$, where $\lambda = a \Delta t / \Delta x$ is the CFL number. For the CFL condition $\lambda \le 1$, the coefficients $(1-\lambda)$ and $\lambda$ are both non-negative and sum to one. This guarantees that $\bar{u}_i^{n+1}$ is a convex combination of $\bar{u}_i^n$ and $\bar{u}_{i-1}^n$, thus preserving non-negativity .

Another cornerstone is the **Local Lax-Friedrichs (LLF) or Rusanov scheme**. This scheme can be viewed as adding a sufficient amount of numerical diffusion to a central flux to suppress oscillations and enforce positivity. For a general flux $f(u)$, the LLF [numerical flux](@entry_id:145174) between states $u_L$ and $u_R$ is:
$$
\hat{f}(u_L, u_R) = \frac{1}{2}\left( f(u_L) + f(u_R) \right) - \frac{\alpha}{2}\left( u_R - u_L \right)
$$
where $\alpha$ is a dissipation coefficient chosen to be an upper bound on the local [characteristic speed](@entry_id:173770), i.e., $\alpha \ge |f'(u)|$. By substituting this flux into the finite volume update, one can show that the scheme is positivity-preserving under the CFL condition $\Delta t \le \Delta x / \alpha$  . The analysis reveals that under this condition, the update is monotone and thus satisfies a [discrete maximum principle](@entry_id:748510), which is a stronger property that directly implies positivity .

A similar outcome can be achieved by explicitly adding a linear **artificial diffusion** term to a scheme that is not inherently positive, like a [central difference scheme](@entry_id:747203) . Consider an update of the form:
$$
\rho_i^{n+1} = \rho_i^{n} - \frac{\Delta t}{V_i} \sum_{f \in \partial i} A_f \left[ \text{Central Flux}_f - D (\rho_{j(f)}^{n} - \rho_i^{n}) \right]
$$
The added term, with coefficient $D > 0$, acts to damp gradients. By writing this update in the convex combination form, one can derive a minimal value $D_{\min}$ required to ensure all combination weights are non-negative, thereby guaranteeing positivity. For this to be possible, the time step $\Delta t$ must also be sufficiently small. This perspective highlights that sufficient numerical dissipation is a key ingredient for the positivity of many simple schemes.

### Generalization to Systems: Invariant-Region Preservation

For [systems of conservation laws](@entry_id:755768), such as the compressible Euler or magnetohydrodynamics (MHD) equations, the concept of positivity must be extended. The physical state is not defined by a single non-negative scalar but by a vector of conserved quantities $\boldsymbol{U} = (\rho, \boldsymbol{m}, E, \dots)^{\top}$ that must simultaneously satisfy a set of constraints.

For the Euler equations, for example, the state is physically admissible only if the mass density $\rho > 0$ and the [thermal pressure](@entry_id:202761) $p > 0$. The pressure is not a conserved variable itself but is derived from them. For an ideal gas, the pressure is given by $p = (\gamma-1)(E - \frac{|\boldsymbol{m}|^2}{2\rho})$, where $E$ is the total energy density . The condition $p>0$ is therefore equivalent to the nonlinear constraint $E > |\boldsymbol{m}|^2 / (2\rho)$, which means the total energy must exceed the kinetic energy.

The set of all physically admissible states is known as the **[invariant region](@entry_id:1126659)** or **admissible set**, denoted by $\mathcal{G}$. For a system like ideal MHD with multiple passive species, this set is defined by the intersection of multiple constraints :
$$
\mathcal{G} = \left\{ \boldsymbol{U} : \rho \ge 0, \quad p(\boldsymbol{U}) \ge 0, \quad 0 \le Y_k \le 1, \quad \sum_k Y_k = 1, \dots \right\}
$$
A scheme is called **Invariant-Region-Preserving (IRP)** if it guarantees that if $\overline{\boldsymbol{U}}_i^n \in \mathcal{G}$, then $\overline{\boldsymbol{U}}_i^{n+1} \in \mathcal{G}$, under a suitable CFL condition. This is the natural generalization of a [positivity-preserving scheme](@entry_id:1129980) to systems.

A critical property of the admissible set $\mathcal{G}$ for many [hyperbolic systems](@entry_id:260647) is its **[convexity](@entry_id:138568)**. A set is convex if the line segment connecting any two points within the set lies entirely within the set. The set $\mathcal{G}$ for the Euler and MHD equations is indeed convex, as it is defined by the intersection of superlevel sets of affine or [concave functions](@entry_id:274100) of the conservative variables (e.g., $\rho$ is affine, $p(\boldsymbol{U})$ is concave) . This [convexity](@entry_id:138568) is the key that enables the construction of high-order IRP schemes.

### High-Order Schemes and Stiff Source Terms

First-order schemes, while robustly positive, are too diffusive for most practical applications. Achieving high-order accuracy while rigorously maintaining physical constraints requires more sophisticated techniques.

A [dominant strategy](@entry_id:264280) for constructing high-order IRP schemes is through a **convex limiting** procedure . This typically involves:
1.  Computing a candidate update $\overline{\boldsymbol{U}}_{i,\text{HO}}^{n+1}$ using a high-order, but potentially non-IRP, method (e.g., WENO or DG).
2.  Computing a 'failsafe' update $\overline{\boldsymbol{U}}_{i,\text{LO}}^{n+1}$ using a robust first-order IRP scheme (like the LLF scheme).
3.  Forming the final update as a convex combination: $\overline{\boldsymbol{U}}_i^{n+1} = \theta_i \overline{\boldsymbol{U}}_{i,\text{HO}}^{n+1} + (1-\theta_i) \overline{\boldsymbol{U}}_{i,\text{LO}}^{n+1}$.
The blending factor $\theta_i \in [0, 1]$ is chosen to be the largest possible value that ensures $\overline{\boldsymbol{U}}_i^{n+1} \in \mathcal{G}$. Because $\mathcal{G}$ is convex and $\overline{\boldsymbol{U}}_{i,\text{LO}}^{n+1}$ is inside it, such a $\theta_i$ can always be found. This minimally invasive correction preserves the high-order accuracy as much as possible while strictly enforcing the physical constraints.

The [time discretization](@entry_id:169380) must also be chosen carefully. **Strong Stability Preserving (SSP)** [time integration methods](@entry_id:136323) are designed specifically to preserve convex functional constraints like positivity when coupled with a suitable [spatial discretization](@entry_id:172158). An $s$-stage SSP Runge-Kutta method can be written in a way that expresses the final update as a convex combination of intermediate stages, each of which is the result of a forward Euler step. For example, the popular third-order, three-stage SSPRK scheme preserves positivity if the time step $\Delta t$ is no larger than the maximum allowable time step for a single forward Euler step of the spatial operator, i.e., its SSP coefficient is 1 .

Finally, many physical problems are described by **balance laws**, which include source terms:
$$
\frac{\partial U}{\partial t} + \nabla \cdot F(U) = S(U)
$$
Source terms can represent effects like radiation, ionization, or recombination, and they can pose a significant threat to positivity, especially when they are **stiff** . A stiff source term is one that operates on a much faster timescale than the fluid transport. For example, a strong [radiative cooling](@entry_id:754014) term might be modeled as $S(e) = -\alpha e$ for the internal energy, with $\alpha \gg 1$.

If such a source is treated with an explicit forward Euler update, $e^{n+1} = e^* - \Delta t \alpha e^* = (1 - \Delta t \alpha)e^*$, where $e^*$ is the energy after the advection step. Even if $e^* > 0$, the updated energy $e^{n+1}$ will become negative if $\Delta t \alpha > 1$. This imposes a severe time step restriction $\Delta t \le 1/\alpha$ that is often far more restrictive than the advective CFL limit.

A powerful strategy to overcome this is to use an **Implicit-Explicit (IMEX)** time integration scheme . In this approach, the non-stiff flux terms are handled explicitly, while the stiff source term is handled implicitly. For the same cooling source, an implicit update solves $e^{n+1} = e^* - \Delta t \alpha e^{n+1}$. The solution is $e^{n+1} = e^* / (1 + \Delta t \alpha)$. Since the denominator is always positive for $\Delta t, \alpha > 0$, this update unconditionally preserves the positivity of energy, regardless of the stiffness of the source. This demonstrates that a careful, and often implicit, treatment of source terms is a critical component of a fully [positivity-preserving scheme](@entry_id:1129980) for realistic physical models.