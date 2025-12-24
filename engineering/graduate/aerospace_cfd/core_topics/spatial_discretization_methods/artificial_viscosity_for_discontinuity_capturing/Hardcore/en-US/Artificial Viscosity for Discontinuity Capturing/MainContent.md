## Introduction
The simulation of fluid flows featuring sharp discontinuities like shock waves is a cornerstone of computational fluid dynamics (CFD), particularly in aerospace and [high-energy physics](@entry_id:181260) applications. The governing Euler equations, which model [inviscid flow](@entry_id:273124), are hyperbolic and naturally develop such non-differentiable fronts, causing standard numerical methods to fail with catastrophic oscillations. To achieve stable and physically meaningful results, simulations must incorporate a mechanism to manage these features. This article addresses this fundamental challenge by exploring **artificial viscosity**, a powerful technique designed to introduce controlled, localized dissipation that stabilizes computations and ensures the correct physical behavior is captured.

This guide provides a thorough examination of artificial viscosity, from its theoretical underpinnings to its modern applications. Across the following chapters, you will gain a deep understanding of this essential numerical tool.
*   The first chapter, **Principles and Mechanisms**, delves into the mathematical origins of discontinuities and the necessity of [weak solutions](@entry_id:161732) and entropy conditions. It then explains how artificial viscosity is formulated, from basic concepts to advanced "smart" sensors that distinguish shocks from other flow features.
*   The second chapter, **Applications and Interdisciplinary Connections**, demonstrates the versatility of [artificial viscosity](@entry_id:140376) by examining its use in stabilizing classic and high-order CFD methods, its role in astrophysical and fusion energy simulations, and its connection to turbulence modeling.
*   Finally, **Hands-On Practices** will provide you with the opportunity to solidify your understanding by tackling practical problems related to the analysis and calibration of [artificial viscosity](@entry_id:140376) in [numerical schemes](@entry_id:752822).

## Principles and Mechanisms

The accurate numerical simulation of flows containing discontinuities, such as shock waves and contact surfaces, represents a central challenge in computational fluid dynamics (CFD). The governing equations of inviscid fluid motion—the Euler equations—are [hyperbolic partial differential equations](@entry_id:171951). A defining feature of such systems is their tendency to develop sharp, non-differentiable fronts from initially smooth conditions. Standard numerical methods, which rely on Taylor series expansions and assumptions of solution smoothness, fail catastrophically in the presence of such features, producing unstable, oscillatory, and physically meaningless results. To overcome this, [numerical schemes](@entry_id:752822) must incorporate a mechanism that mimics the dissipative effects that are physically present at the microscale but absent from the idealized Euler model. This mechanism is known as **artificial viscosity** or **[artificial dissipation](@entry_id:746522)**. This chapter elucidates the fundamental principles underlying the necessity, formulation, and refinement of artificial viscosity for [discontinuity capturing](@entry_id:177926).

### The Origin of Discontinuities and the Need for Weak Solutions

To understand why discontinuities are an inevitable feature of inviscid compressible flow, it is instructive to begin with the simplest analogue: the one-dimensional [scalar conservation law](@entry_id:754531).
$$
\frac{\partial u}{\partial t} + \frac{\partial f(u)}{\partial x} = 0
$$
This equation models the conservation of a scalar quantity $u$ with a corresponding flux $f(u)$. Using the [chain rule](@entry_id:147422), for a smooth solution $u(x,t)$, we can write this equation in its quasilinear form:
$$
\frac{\partial u}{\partial t} + f'(u) \frac{\partial u}{\partial x} = 0
$$
The term $a(u) = f'(u)$ represents the local speed at which information about the value of $u$ propagates. For the equation to be hyperbolic, this **characteristic speed** must be real. Along curves in the $(x,t)$ plane defined by $\frac{dx}{dt} = a(u)$, the [total derivative](@entry_id:137587) of the solution is $\frac{du}{dt} = u_t + \frac{dx}{dt}u_x = u_t + a(u)u_x = 0$. This means the value of $u$ is constant along these **[characteristic curves](@entry_id:175176)**.

The non-linearity of the problem arises because the propagation speed $a(u)$ depends on the solution $u$ itself. If different parts of an initial profile have different values of $u$, they will propagate at different speeds. Consider a region where the [characteristic speed](@entry_id:173770) is a decreasing function of $x$. This means characteristics starting from upstream positions will travel faster than those starting downstream, leading to a collision of characteristics in finite time.

Mathematically, we can analyze the evolution of the spatial gradient $w = u_x$ along a characteristic. Differentiating the [quasilinear equation](@entry_id:173419) with respect to $x$ and performing a short derivation yields a Riccati equation for $w$:
$$
\frac{dw}{dt} = -f''(u) w^2
$$
If the flux function $f(u)$ is strictly convex, meaning $f''(u) > 0$, and there exists an initial compression where $u_x(x_0, 0)  0$, then $\frac{dw}{dt}$ is negative. The gradient $w$ becomes increasingly negative until it "blows up" to $-\infty$ at a finite time $t_{\star} = -1/(f''(u)u_x(0))$. This event, known as a **[gradient catastrophe](@entry_id:196738)**, marks the formation of a discontinuity, or a **shock wave**, where the solution ceases to be differentiable .

Once a shock forms, the classical (strong) solution concept breaks down. We must instead seek **[weak solutions](@entry_id:161732)**, which satisfy the integral form of the conservation law. For a discontinuity traveling with speed $s$, the integral form implies a [jump condition](@entry_id:176163) across the shock, known as the **Rankine-Hugoniot condition**:
$$
s [u] = [f(u)]
$$
where $[q] = q_R - q_L$ denotes the jump in a quantity $q$ from its state on the left ($u_L$) to its state on the right ($u_R$) of the discontinuity.

### The Entropy Condition and Vanishing Viscosity

A critical issue arises with weak solutions: they are generally not unique. For a given initial condition, multiple [weak solutions](@entry_id:161732) satisfying the Rankine-Hugoniot condition may exist, some of which are physically unrealistic (e.g., shocks that cause a decrease in entropy). An additional criterion is needed to select the single, physically relevant solution. This criterion is the **[entropy condition](@entry_id:166346)**.

The most physically intuitive and mathematically rigorous foundation for the entropy condition is the **[vanishing viscosity method](@entry_id:177856)**. We consider the original conservation law with a small amount of diffusion added, which regularizes the equation into a parabolic PDE:
$$
\frac{\partial u}{\partial t} + \frac{\partial f(u)}{\partial x} = \epsilon \frac{\partial^2 u}{\partial x^2}
$$
For any $\epsilon > 0$, this viscous equation possesses a unique, smooth solution. The physical entropy solution of the original inviscid equation is then defined as the limit of these smooth solutions as the viscosity parameter vanishes, i.e., as $\epsilon \to 0^+$. Within the smooth, viscous profile of the shock, the thickness of the transition layer is found to scale with the viscosity coefficient, i.e., as $\mathcal{O}(\epsilon)$ .

This limiting process provides a selection principle. For a strictly convex flux, the resulting condition is the **Lax [entropy condition](@entry_id:166346)**, which states that for a physically admissible shock, characteristics on both sides must propagate into the shock front:
$$
f'(u_L) > s > f'(u_R)
$$
This ensures the shock is compressive and that information flows into the discontinuity, not out of it .

For general, non-convex flux functions, a more powerful and comprehensive criterion is required. This is provided by the **Kruzkov [entropy condition](@entry_id:166346)**. It states that a bounded [weak solution](@entry_id:146017) $u$ is the entropy solution if, for every constant $k \in \mathbb{R}$, the following inequality holds in the sense of distributions:
$$
\frac{\partial |u-k|}{\partial t} + \frac{\partial}{\partial x} \left( \text{sgn}(u-k)(f(u)-f(k)) \right) \le 0
$$
Kruzkov's theory guarantees the [existence and uniqueness](@entry_id:263101) of a solution satisfying this condition for any bounded initial data, even for non-convex fluxes. The Kruzkov condition is the more fundamental one; for piecewise smooth solutions with convex flux, it implies the Lax condition. The solutions obtained from the [vanishing viscosity method](@entry_id:177856) are guaranteed to satisfy the Kruzkov entropy inequalities . In CFD, the goal of [artificial viscosity](@entry_id:140376) is to construct a numerical analogue of this vanishing viscosity mechanism, ensuring that any captured discontinuities implicitly satisfy the correct [entropy condition](@entry_id:166346).

### Artificial Viscosity for the Euler Equations

The principles developed for scalar equations extend to [systems of conservation laws](@entry_id:755768), such as the compressible Euler equations. Here, artificial viscosity is introduced by augmenting the momentum and energy fluxes with an **artificial viscous stress tensor** $\boldsymbol{\tau}_{\mathrm{av}}$ and an **artificial heat flux** $\boldsymbol{q}_{\mathrm{av}}$. For the resulting system to be physically and thermodynamically consistent, the modifications to the momentum and energy equations must be coupled.

The rate of change of specific internal energy $e$ is derived from the full system of conservation laws. This reveals that the work done by the artificial stress acts as an irreversible source of internal energy:
$$
\rho \frac{De}{Dt} = -p (\nabla \cdot \boldsymbol{u}) + \boldsymbol{\tau}_{\mathrm{av}} : \nabla \boldsymbol{u} + \nabla \cdot \boldsymbol{q}_{\mathrm{av}}
$$
Here, $\frac{D}{Dt}$ is the material derivative, and $\boldsymbol{\tau}_{\mathrm{av}} : \nabla \boldsymbol{u}$ represents the rate of viscous dissipation. The Second Law of Thermodynamics requires that the entropy production rate, $\sigma_s$, must be non-negative. This production rate is given by:
$$
\sigma_s = \frac{1}{T}(\boldsymbol{\tau}_{\mathrm{av}} : \nabla \boldsymbol{u}) - \frac{\boldsymbol{q}_{\mathrm{av}} \cdot \nabla T}{T^2} \ge 0
$$
To ensure entropy admissibility in captured shocks, it is sufficient to have a mechanism that guarantees $\sigma_s > 0$ within the [shock layer](@entry_id:197110). For a one-dimensional shock, the [velocity gradient tensor](@entry_id:270928) is dominated by the term $\frac{du}{dx}$. A [sufficient condition](@entry_id:276242) for entropy production is to introduce an **artificial bulk viscosity**, which takes the form of an isotropic stress proportional to the fluid's dilatation rate, $\nabla \cdot \boldsymbol{u}$:
$$
\boldsymbol{\tau}_{\mathrm{av}} = \zeta_{\mathrm{av}} (\nabla \cdot \boldsymbol{u}) \boldsymbol{I}
$$
With a positive coefficient $\zeta_{\mathrm{av}} > 0$, the dissipation term becomes $\zeta_{\mathrm{av}}(\nabla \cdot \boldsymbol{u})^2$, which is strictly positive in a compression or expansion. This simple model is sufficient to regularize shocks and enforce the entropy condition, without necessarily requiring artificial [shear viscosity](@entry_id:141046) or heat conduction . This realization forms the basis of many practical artificial viscosity schemes.

### The Design of Smart Dissipation: Sensors and Switches

The central dilemma in applying [artificial viscosity](@entry_id:140376) is that while it is essential for stability at shocks, it is detrimental in smooth regions of the flow. Excessive dissipation can smear out fine details, damp physical instabilities, and unphysically drain energy from phenomena like turbulence. The solution is to design a "smart" artificial viscosity coefficient that acts as a switch, turning on strongly in the presence of a discontinuity and turning off elsewhere.

A widely used form for the [artificial viscosity](@entry_id:140376) coefficient, $\mu_a$, in numerical schemes is derived from [scaling arguments](@entry_id:273307). To ensure a shock is smeared over a fixed number of grid cells ($\Delta x_s \sim \Delta x$), a balance between convective and diffusive fluxes suggests a scaling of the form $\mu_a \sim \rho u \Delta x_s$. Replacing the flow velocity $u$ with the more robust characteristic [wave speed](@entry_id:186208) $a$ (the sound speed) gives the fundamental scaling:
$$
\mu_a = C \rho a \Delta x \phi
$$
Here, $C$ is a dimensionless tuning constant, $\rho$ provides the correct scaling with fluid inertia, $a$ ties dissipation to the local wave propagation speed, and $\Delta x$ ensures the viscosity is a numerical artifact that vanishes as the grid is refined. The crucial element is $\phi$, a dimensionless, bounded **sensor function** designed to detect discontinuities .

The design of the sensor $\phi$ is an area of active research. Its goal is to distinguish different flow features based on local gradients.

#### Distinguishing Shocks from Smooth Flow
The most basic sensor activates based on large gradients. Since pressure changes sharply across a shock, a normalized pressure gradient is a common choice. For example:
$$
\phi = \frac{|\Delta p|}{|\Delta p| + p}
$$
In a smooth region, the pressure change across a cell $|\Delta p|$ is much smaller than the [absolute pressure](@entry_id:144445) $p$, so $\phi \to 0$. Near a shock, $|\Delta p| \sim p$, causing $\phi \to \mathcal{O}(1)$ and activating the viscosity .

#### Distinguishing Shocks from Contact Discontinuities
A [contact discontinuity](@entry_id:194702) is characterized by a jump in density and temperature, but pressure and velocity are continuous across it. A simple pressure-gradient sensor would correctly remain off. However, more advanced schemes may need to explicitly distinguish these features. A sensor can be designed to activate only in regions of both high pressure gradient *and* high Mach number, which is characteristic of shocks but not stationary contacts. An effective sensor might take the form:
$$
S(M, \phi) = \underbrace{\left(\frac{\phi}{1+\phi}\right)}_{\text{Pressure gradient switch}} \cdot \underbrace{\left(\frac{M^2}{1+M^2}\right)}_{\text{Mach number switch}} \quad \text{or} \quad S(M, \phi) = \left(\frac{\phi}{1+\phi}\right) \cdot e^{-1/M^2}
$$
These forms require both a significant normalized pressure gradient ($\phi \sim 1$) and a sufficiently high Mach number ($M \gtrsim 1$) to produce a strong signal, $S \sim 1$. They correctly remain quiescent at contact surfaces (where $\phi \approx 0$) and in smooth low-Mach regions (where $M \ll 1$) .

#### Distinguishing Shocks from Vorticity
Perhaps the most critical task for a sensor in turbulence-resolving simulations is to distinguish compressive shocks from incompressible vortical motion. A naive [artificial viscosity](@entry_id:140376), such as one modeled on the full velocity gradient tensor ($\boldsymbol{\tau}_{\mathrm{av}} \propto \nabla \boldsymbol{u}$), will dissipate kinetic energy in any region with velocity gradients, including shear layers and vortices. The kinetic energy dissipation rate from an artificial stress is $-\int_{\Omega} \boldsymbol{\tau}_{\mathrm{av}}:\nabla\boldsymbol{u} \, dV$. A naive model leads to a dissipation rate proportional to $\int_{\Omega} ||\nabla \boldsymbol{u}||_F^2 \, dV$, which is non-zero in a vortex and causes unphysical damping .

To avoid this, the [artificial viscosity](@entry_id:140376) must target only the compressive part of the flow. As established earlier, a pure [bulk viscosity](@entry_id:187773), $\boldsymbol{\tau}_{\mathrm{av}} = \lambda_a (\nabla \cdot \boldsymbol{u})\boldsymbol{I}$, has a [dissipation rate](@entry_id:748577) proportional to $\int_{\Omega} \lambda_a (\nabla \cdot \boldsymbol{u})^2 \, dV$. This term is zero in an incompressible region where $\nabla \cdot \boldsymbol{u}=0$, thus preserving the kinetic energy of vortical structures .

This principle can be embedded in a sensor that compares the magnitude of local compression (dilatation) to local rotation (vorticity). The **Ducros sensor** is a prominent example, defined as:
$$
\phi = \frac{(\nabla \cdot \boldsymbol{u})^2}{(\nabla \cdot \boldsymbol{u})^2 + ||\nabla \times \boldsymbol{u}||^2 + \epsilon}
$$
This sensor approaches 1 when dilatation dominates rotation (as in a shock) and approaches 0 when rotation dominates dilatation (as in a vortex), effectively switching off viscosity in turbulent eddies .

### Advanced Refinements of Artificial Viscosity

Beyond designing better sensors, the structure of the [artificial viscosity](@entry_id:140376) operator itself can be refined to improve accuracy.

#### Anisotropic Artificial Viscosity
Isotropic [artificial viscosity](@entry_id:140376), where the same amount of dissipation is applied in all directions, can cause excessive smearing of flow features that are oblique to the computational grid. For instance, an [oblique shock](@entry_id:261733) may be artificially thickened in the direction parallel to the shock front. To mitigate this, **anisotropic [artificial viscosity](@entry_id:140376)** can be employed. The scalar diffusion coefficient is replaced by a diffusion tensor $\mathbf{D}$. This tensor is constructed to align the strongest diffusion with the shock-normal direction, $\mathbf{n}$, while applying minimal diffusion in the tangential directions. The normal is typically detected using the normalized pressure gradient, $\mathbf{n} = \nabla p / ||\nabla p||$. A suitable diffusion tensor can be constructed using [projection operators](@entry_id:154142):
$$
\mathbf{D} = \kappa_n \mathbf{n}\mathbf{n}^{\top} + \kappa_t (\mathbf{I} - \mathbf{n}\mathbf{n}^{\top})
$$
where $\kappa_n$ is the normal diffusivity and $\kappa_t$ is the tangential diffusivity. By setting $\kappa_t = \varepsilon \kappa_n$ with a small parameter $\varepsilon \ll 1$, the dissipation is concentrated along the shock normal, significantly reducing transverse smearing. For this operator to be dissipative, the tensor $\mathbf{D}$ must be symmetric and positive semidefinite, which requires the eigenvalues $\kappa_n$ and $\kappa_t$ to be non-negative .

#### Low-Mach Number Correction
Standard artificial viscosity formulations, which scale the characteristic speed with the speed of sound ($a$), suffer from a severe deficiency in the low-Mach number limit ($M \to 0$). Asymptotic analysis reveals that the non-dimensional artificial pressure diffusion term scales as $M^{-1}$. As the Mach number approaches zero, this term becomes infinitely large, overwhelming the physical pressure evolution and destroying the accuracy of the solution. This is known as the **low-Mach number inconsistency** .

To create schemes that are accurate across all flow regimes ("all-speed" solvers), the characteristic speed used for dissipation must be modified. A common approach is to use a blended speed that correctly captures both acoustic and convective limits. A widely-used pressure-based switch modifies the dissipation speed $\lambda$ to scale with a pre-conditioned sound speed, for example, by replacing $a$ with a function $\tilde{a}(M) = \phi(M)a$. To correct the $M^{-1}$ divergence, the correction factor must scale linearly with Mach number in the low-Mach limit, i.e., $\phi(M) \sim M$. This effectively replaces the sound speed $a$ with the fluid velocity scale $U$ in the incompressible limit, ensuring that the artificial viscosity remains well-behaved and physically scaled across the entire range of Mach numbers . This correction is vital for simulating flows with both high-speed shocks and low-speed vortical regions, a common scenario in aerospace applications.