## Introduction
Modeling the universe requires navigating an immense [dynamic range](@entry_id:270472), from the slow expansion of cosmic voids to the rapid collapse of matter into galaxies. A fixed time step small enough to capture the fastest dynamics would render such simulations computationally impossible. The solution is **[adaptive time-stepping](@entry_id:142338)**, a sophisticated control technique that dynamically adjusts the integration step size to match the evolving physical conditions throughout the simulation. This approach is not merely an optimization but a foundational enabling technology for modern [computational cosmology](@entry_id:747605).

This article provides a graduate-level exploration of [adaptive time-stepping](@entry_id:142338), from foundational theory to practical implementation. It aims to equip you with the knowledge to design, analyze, and implement robust and efficient [time integration schemes](@entry_id:165373) for complex physical systems. We will begin in **Principles and Mechanisms** by dissecting the core stability and accuracy constraints, exploring the "zoo" of physical timescales that govern cosmological dynamics, and grappling with advanced topics like stiffness and conservation laws. Next, in **Applications and Interdisciplinary Connections**, we will see these principles in action, examining their specific implementations in gravitational N-body problems, hydrodynamical shock-capturing, and multi-[physics simulations](@entry_id:144318), while also drawing connections to fields like [molecular dynamics](@entry_id:147283) and plasma physics. Finally, the **Hands-On Practices** section provides a curated set of coding problems designed to translate theory into practice, allowing you to build and test your own adaptive controllers for realistic cosmological scenarios.

## Principles and Mechanisms

The evolution of cosmological structures is a quintessential multiscale phenomenon. From the slow, stately expansion of the universe as a whole to the rapid, violent dynamics within a collapsing protostellar core, the relevant physical processes span an immense range of temporal and spatial scales. A central challenge in [numerical cosmology](@entry_id:752779) is to devise [integration algorithms](@entry_id:192581) that can navigate this complexity efficiently and accurately. While a fixed, globally small time step could, in principle, resolve the fastest dynamics, it would be computationally prohibitive, wasting immense resources on slowly evolving regions. The solution lies in **[adaptive time-stepping](@entry_id:142338)**, a control process that dynamically adjusts the integration step size, $\Delta t$, to match the local, instantaneous demands of the physics.

This chapter delves into the principles and mechanisms that govern [adaptive time-stepping](@entry_id:142338) in modern [cosmological simulations](@entry_id:747925). We will first establish the fundamental stability and accuracy criteria that any time step must satisfy. We will then explore how these criteria are derived from the physical timescales of gravity, hydrodynamics, and chemistry. Finally, we will examine advanced topics, including [numerical stiffness](@entry_id:752836), the choice of integration variable, and the profound consequences of adaptive stepping for the conservation of [physical quantities](@entry_id:177395) like energy and momentum.

### The Rationale for Adaptive Time-Stepping

In practice, numerical integrators for cosmological ordinary and [partial differential equations](@entry_id:143134) (ODEs and PDEs) employ one of three main time-stepping policies. Understanding their differences clarifies the unique role of adaptive stepping .

-   **Fixed Stepping**: A constant time step, $\Delta t$, is chosen at the beginning of the simulation and held fixed throughout. To ensure stability and accuracy, this $\Delta t$ must be smaller than the shortest timescale that occurs anywhere in the simulation domain at any point in its evolution. This "worst-case" approach is robust but catastrophically inefficient for problems with large [dynamic range](@entry_id:270472).

-   **Event-Driven Stepping**: The time step is chosen primarily to land the simulation at specific, pre-ordained moments in time. These "events" might be desired [redshift](@entry_id:159945) outputs for analysis, [synchronization](@entry_id:263918) points in a multi-physics coupling scheme, or the crossing of a particular physical threshold. While a robust implementation must still check against stability and accuracy limits, the primary driver for selecting $\Delta t$ is the event schedule, not the intrinsic dynamics of the system.

-   **Adaptive Stepping**: This policy treats the time step $\Delta t$ as a controlled variable that is re-evaluated at every step. The goal is to select the largest possible $\Delta t$ that still satisfies a set of pre-defined stability and accuracy criteria. It is a feedback loop: the state of the system at time $t$ is used to determine an [optimal step size](@entry_id:143372) $\Delta t_n$ to advance to $t_{n+1}$. This ensures that computational effort is precisely allocated where and when it is needed, making it the method of choice for complex [cosmological simulations](@entry_id:747925).

### Fundamental Constraints on the Time Step

An adaptive controller determines the optimal $\Delta t$ by evaluating a set of constraints and choosing the most restrictive one. These constraints fall into two broad categories: those ensuring [numerical stability](@entry_id:146550) and those ensuring accuracy.

#### Stability Constraints

Stability criteria prevent the unphysical, [exponential growth](@entry_id:141869) of errors in a numerical solution. For explicit integration schemes, which are common in cosmology, these constraints typically relate the time step to the spatial resolution and the speed of [signal propagation](@entry_id:165148).

The most famous of these is the **Courant-Friedrichs-Lewy (CFL) condition**, which applies to the numerical solution of hyperbolic PDEs, such as the Euler equations of fluid dynamics. It states that the [numerical domain of dependence](@entry_id:163312) must contain the physical domain of dependence. In practical terms, this means that information, traveling at the maximum characteristic speed of the fluid, must not propagate across more than one grid cell in a single time step.

For a simulation on a comoving grid with cell spacing $\Delta x$, the CFL condition for a time step in cosmic time $t$ is expressed as:
$$
\Delta t \le C_{\text{CFL}} \frac{\text{cell size}}{\text{signal speed}}
$$
where $C_{\text{CFL}}$ is the Courant number, a [safety factor](@entry_id:156168) typically in the range $0.1 - 1.0$. The key subtlety in a cosmological context is defining the "cell size" and "signal speed" consistently. Since the grid is comoving, the natural [cell size](@entry_id:139079) is the comoving spacing $\Delta x$. The signal speed must therefore also be expressed in comoving units. The maximum [characteristic speed](@entry_id:173770) of a fluid element is the sum of its bulk velocity and the sound speed relative to it. If the physical peculiar velocity is $\boldsymbol{v}$ and the physical sound speed is $c_{s,\text{phys}}$, the total physical signal speed is $|\boldsymbol{v}| + c_{s,\text{phys}}$. To convert this to a comoving speed, we divide by the [scale factor](@entry_id:157673) $a(t)$. The CFL condition is therefore :
$$
\Delta t_{\text{CFL}} \le C_{\text{CFL}} \frac{\Delta x}{|\boldsymbol{v}|/a + c_{s,\text{phys}}/a} = C_{\text{CFL}} \frac{a\,\Delta x}{|\boldsymbol{v}| + c_{s,\text{phys}}}
$$
This expression has a clear physical interpretation: the time step must be smaller than the time it takes for a signal traveling at the maximum physical [characteristic speed](@entry_id:173770) to cross one grid cell of physical size $a\Delta x$.

For other physical processes, different stability constraints arise. For instance, explicit schemes for [diffusion processes](@entry_id:170696), such as those modeling optically thick radiative transfer ($E_t = D \nabla^2 E$), are subject to a parabolic CFL condition of the form $\Delta t \le C (\Delta x)^2 / D$. The quadratic dependence on $\Delta x$ can make this constraint exceptionally restrictive on fine grids, a point we will return to when discussing stiffness .

#### Accuracy Constraints

While stability prevents the solution from diverging, accuracy ensures that it converges to the correct physical answer. Accuracy is maintained by controlling the **[local truncation error](@entry_id:147703) (LTE)**, which is the error introduced in a single integration step.

For systems of ODEs, such as those governing the background [cosmological expansion](@entry_id:161458) or [chemical reaction networks](@entry_id:151643), a powerful technique for controlling LTE is the use of **embedded Runge-Kutta (RK) methods** . An embedded RK pair, such as a Dormand-Prince 5(4) method, uses the same set of function evaluations to compute two solutions of different orders, say a 5th-order solution $\boldsymbol{y}^{[5]}$ and a 4th-order solution $\boldsymbol{y}^{[4]}$. The difference between these two solutions, $\boldsymbol{e} = \boldsymbol{y}^{[5]} - \boldsymbol{y}^{[4]}$, provides an estimate of the LTE of the lower-order method.

The challenge in cosmology is that the [state vector](@entry_id:154607) $\boldsymbol{y} = (a, \rho, H, \dots)$ contains components with vastly different magnitudes and dynamic ranges. A simple [absolute error](@entry_id:139354) tolerance, $|\boldsymbol{e}| \le \text{tol}$, is not robust. For example, a tolerance suitable for the scale factor $a$ (which is of order unity at late times) would be far too loose for the density $\rho$ (which can be many orders of magnitude larger). Conversely, a tolerance appropriate for early-time density would be far too strict for the scale factor when it is near zero.

The [standard solution](@entry_id:183092) is a mixed **[absolute and relative tolerance](@entry_id:163682)** criterion. For each component $y_i$, we define a tolerance weight $w_i$ and require that the scaled error is less than one:
$$
w_i = \text{atol}_i + \text{rtol}_i \cdot \max(|y_i^{\text{start}}|, |y_i^{\text{end}}|)
$$
$$
\left| \frac{e_i}{w_i} \right| \le 1
$$
Here, $\text{atol}_i$ is an **absolute tolerance** that sets a floor on the allowable error, which is crucial when $y_i$ is near zero. The **relative tolerance** $\text{rtol}_i$ controls the fractional error, ensuring accuracy when $|y_i|$ is large. The step is accepted only if this condition holds for all components. This scale-aware error control is indispensable for integrating cosmological ODEs .

For [particle-based methods](@entry_id:753189) like N-body and Smoothed Particle Hydrodynamics (SPH), accuracy is often controlled by a different type of criterion. Here, the goal is to ensure that the discrete time step is small enough to resolve the curvature of a particle's trajectory. A simple Taylor expansion shows that the displacement of a particle due to acceleration $|a|$ over a step $\Delta t$ is $\frac{1}{2}|a|(\Delta t)^2$. To accurately capture the trajectory, this displacement must be small compared to the relevant spatial resolution scale, $L_{\text{res}}$. This leads to an acceleration-based time-step criterion :
$$
\Delta t \le \eta \sqrt{\frac{L_{\text{res}}}{|a|}}
$$
where $\eta$ is a dimensionless accuracy parameter. The relevant resolution scale depends on the physics:
-   For collisionless dark matter or star particles, the force is regularized by a **[gravitational softening](@entry_id:146273) length**, $\epsilon$. Thus, $L_{\text{res}} = \epsilon$.
-   For SPH gas particles, the [hydrodynamic interactions](@entry_id:180292) are resolved over the **SPH smoothing length**, $h$. Thus, $L_{\text{res}} = h$.

### The Global Time-Step Criterion: Combining Constraints

In any realistic [cosmological simulation](@entry_id:747924), multiple physical processes operate simultaneously. A particle or fluid element is subject to constraints from [hydrodynamics](@entry_id:158871), gravity, [cosmic expansion](@entry_id:161002), and potentially [radiative cooling](@entry_id:754014) and chemistry. An [adaptive time-stepping](@entry_id:142338) algorithm must respect all of these constraints. The guiding principle is simple but strict: the actual time step used for any part of the system must be the minimum of all applicable constraints.
$$
\Delta t = \min(\Delta t_{\text{CFL}}, \Delta t_{\text{acc}}, \Delta t_{\text{grav}}, \Delta t_{\text{cool}}, \dots)
$$
Let us examine how this principle is applied in practice.

#### The Zoo of Cosmological Timescales

The physics of the cosmos can be characterized by a "zoo" of natural timescales. An adaptive integrator must be aware of them and ensure that the time step is shorter than the fastest active one . Key examples include:

-   **Hubble Time ($t_H$)**: Defined as $t_H = 1/H$, it is the characteristic timescale for the expansion of the universe. To accurately integrate equations with source terms proportional to $H$ (like the Hubble drag), we must have $\Delta t \ll t_H$.
-   **Dynamical Time ($\tau_{\text{dyn}}$)**: This is the [characteristic timescale](@entry_id:276738) for a self-gravitating system to respond to its own gravity, such as the [free-fall time](@entry_id:261377) for collapse. From [dimensional analysis](@entry_id:140259), it scales with local density $\rho$ as $\tau_{\text{dyn}} \propto (G\rho)^{-1/2}$. Explicit gravity solvers must use $\Delta t \lesssim \tau_{\text{dyn}}$ to prevent large errors in orbits and collapse dynamics.
-   **Cooling Time ($\tau_{\text{cool}}$)**: For a gas with thermal energy density $e$ and a net volumetric cooling rate of $\Lambda - \Gamma$, the cooling time is $\tau_{\text{cool}} = e/|\Lambda - \Gamma|$. An explicit update to the thermal energy, $e^{n+1} = e^n - (\Lambda - \Gamma)\Delta t$, will produce unphysical [negative energy](@entry_id:161542) if $\Delta t > \tau_{\text{cool}}$. Thus, stability and accuracy demand $\Delta t \lesssim \tau_{\text{cool}}$.
-   **Recombination Time ($\tau_{\text{rec}}$)**: In a chemical network, each reaction has a characteristic timescale. For hydrogen recombination, governed by the [rate equation](@entry_id:203049) $dn_e/dt \approx -\alpha_B n_e^2$, the timescale is $\tau_{\text{rec}} = n_e / |dn_e/dt| = 1/(\alpha_B n_e)$. Similar to cooling, explicit integration of the chemical network requires $\Delta t \lesssim \tau_{\text{rec}}$.

A robust adaptive time-step for a full [physics simulation](@entry_id:139862) would therefore be $\Delta t \le C \min(t_H, \tau_{\text{dyn}}, \Delta t_{\text{CFL}}, \tau_{\text{cool}}, \tau_{\text{rec}}, \dots)$, where the minimum is taken over the entire simulation domain.

#### Gravity vs. Hydrodynamics

A common scenario involves a competition between the gravitational dynamical time and the hydrodynamical CFL time. In regions of high [density contrast](@entry_id:157948), which constraint dominates? 
-   In **overdense regions** ($\delta \gg 0$), such as forming galaxies and filaments, the local density $\rho$ is extremely high. Since $\tau_{\text{dyn}} \propto \rho^{-1/2}$, the gravitational timescale becomes very short. This reflects the rapid gravitational collapse. In these regimes, the gravitational constraint, $\Delta t \lesssim \tau_{\text{dyn}}$, is almost always the most restrictive one, dictating the time step.
-   In **underdense voids** ($\delta \to -1$), the local density $\rho$ is very low. The gravitational timescale $\tau_{\text{dyn}}$ becomes extremely long, meaning gravity acts very slowly. However, the gas still has a non-zero temperature and peculiar velocity, resulting in a finite CFL time, $\Delta t_{\text{CFL}}$. In these regions, the CFL condition is typically the limiting factor.

#### Particle Hydrodynamics (SPH)

For SPH particles, which are subject to both gravitational and hydrodynamical forces, the time step must satisfy multiple criteria simultaneously. It must satisfy the CFL condition to ensure stability of advection and sound wave propagation, and it must also satisfy the acceleration-based criterion to ensure accurate [trajectory integration](@entry_id:756093). The advection part of the CFL condition, which states that a particle should not travel more than its smoothing length $h$ in one step, gives $\Delta t \le \eta h / |v|$. Combining this with the acceleration criterion gives the standard SPH time-step limiter :
$$
\Delta t_{\text{SPH}} \le \eta \min \left( \sqrt{\frac{h}{|a|}}, \frac{h}{|v| + c_s} \right)
$$
(Here we have included the sound speed $c_s$ for the full CFL condition, though the problem context  focused on the advective part.)

### Advanced Topics and Implementational Nuances

Beyond the basic combination of constraints, several advanced concepts profoundly impact the design and behavior of adaptive integrators.

#### Stiffness

A system of ODEs is called **stiff** when it contains multiple, widely separated timescales, and the fastest timescale corresponds to a rapidly decaying, stable mode. The problem with stiffness is that an explicit integrator's stability is governed by the fastest timescale (e.g., $\Delta t \lesssim \tau_{\text{fast}}$), even when the solution itself is evolving smoothly on a much longer timescale, $\tau_{\text{slow}}$. The explicit method is forced to take tiny, computationally expensive steps to maintain stability, not to gain accuracy. This is a crucial distinction from a generic **multiscale problem**, where fast modes are physically important and must be resolved for accuracy .

Cosmology is rife with stiff problems.
-   **Recombination Chemistry**: Near recombination equilibrium at $z \approx 1100$, the recombination time $t_{\text{rec}}$ can be hundreds of times shorter than the Hubble time $t_H$. The [electron fraction](@entry_id:159166) is in quasi-static equilibrium, evolving slowly on the Hubble timescale. However, any small perturbation from this equilibrium decays on the very fast recombination timescale. An explicit solver's stability is limited by $t_{\text{rec}}$, making the system stiff.
-   **Radiative Cooling**: In dense gas, the cooling time $t_{\text{cool}}$ can be millions of times shorter than the Hubble time or the local dynamical time. The gas quickly settles to a thermal equilibrium where heating balances cooling. An explicit method remains constrained by the very short $t_{\text{cool}}$, even though the gas temperature is changing slowly.

The primary solution to stiffness is to use **implicit or semi-[implicit integrators](@entry_id:750552)**, which are numerically stable even for time steps much larger than the fastest decay time, allowing $\Delta t$ to be chosen based on accuracy requirements for the slow evolution.

#### Choice of Integration Variable

For problems involving the cosmological background, the choice of the independent integration variable can have a significant impact on efficiency and accuracy . While cosmic time $t$ is the most intuitive choice, others can be advantageous.

-   **Conformal Time ($\eta$)**: Defined by $d\eta = dt/a(t)$, [conformal time](@entry_id:263727) is particularly useful for evolving relativistic perturbations (like photons or neutrinos). The equation of motion for a massless field mode with comoving wavenumber $k$ simplifies in [conformal time](@entry_id:263727). Its oscillation frequency becomes approximately constant, $\omega(\eta) \approx k$. This allows an adaptive integrator to use a nearly uniform step size $\Delta \eta$ to resolve the oscillations, which is far more efficient than using cosmic time $t$, where the physical frequency redshifts as $\omega_{\text{phys}}(t) \approx k/a(t)$.

-   **Scale Factor ($a$)**: Using the scale factor $a$ as the [independent variable](@entry_id:146806) can be powerful for dealing with stiffness in the background evolution itself. The relationship $dt = da/(aH)$ shows that a fixed step in $a$, $\Delta a$, corresponds to a time step $\Delta t$ that is automatically smaller when the Hubble parameter $H$ is large. If the background evolution is "stiff" in the sense that $H(a)$ varies rapidly over a small range of $a$ (e.g., during a phase transition), integrating with respect to $a$ causes the solver to naturally concentrate steps in that region, mitigating the stiffness.

#### Hierarchical and Individual Time-Stepping

To maximize efficiency, many modern codes employ hierarchical [time-stepping schemes](@entry_id:755998), where different parts of the simulation domain advance with different time steps.

-   **AMR Subcycling**: In Adaptive Mesh Refinement (AMR), finer grids require smaller time steps due to the CFL condition. **Subcycling** allows each refinement level $\ell$ to take multiple smaller steps for every single step taken by the coarser level $\ell-1$. Typically, the time steps are synchronized in integer ratios, $\Delta t_{\ell} = \Delta t_{\ell-1} / r_\ell$, where $r_\ell$ is the spatial refinement ratio (e.g., 2). This requires careful implementation to ensure [conservation of mass](@entry_id:268004), momentum, and energy across the coarse-fine interfaces. A process called **refluxing** is used to correct the fluxes at the interface, ensuring that the total flux out of a coarse region over its step $\Delta t_{\ell-1}$ exactly equals the sum of fluxes into the corresponding fine region over its $r_\ell$ substeps. This requires precise synchronization of the time intervals .

-   **Individual Particle Timesteps**: In N-body and SPH codes, it is common to assign an individual time step to each particle based on its local criteria. Particles are often organized into [discrete time](@entry_id:637509)-step "rungs," and only particles on the current rung are advanced. This allows particles in dense, rapidly evolving regions to be updated frequently, while particles in quiet voids are updated very rarely  .

#### Adaptive Stepping and Conservation Laws

A final, crucial consideration is the interaction between [adaptive time-stepping](@entry_id:142338) and fundamental conservation laws. Here, we must distinguish between two levels of conservation :

-   **Strong Invariance**: A property of the discrete algorithm itself. A quantity is a strong invariant if it is preserved exactly (to machine precision) for any valid finite time step $\Delta t$. This arises from the algebraic structure of the update, such as a [telescoping sum](@entry_id:262349).

-   **Weak Conservation**: A property of a convergent scheme. The quantity is not exactly conserved at finite $\Delta t$, but the error in its conservation approaches zero as $\Delta t \to 0$.

Adaptive time-stepping can degrade or destroy strong invariance.

-   **Momentum**: In an N-body system with individual, asynchronous time steps, Newton's third law ($\boldsymbol{F}_{ij} = -\boldsymbol{F}_{ji}$) is broken at the discrete level. When particle $i$ is updated due to the force from $j$, but $j$ is not updated simultaneously, the [action-reaction pair](@entry_id:167944) is not applied symmetrically. Total linear momentum is therefore not a strong invariant; it is only weakly conserved.

-   **Energy and Symplecticity**: The popular [leapfrog integrator](@entry_id:143802) is **symplectic** for a fixed time step, which means it exactly preserves a "shadow" Hamiltonian and phase-space volume. This leads to excellent long-term energy conservation (no secular drift). However, a [variable time step](@entry_id:756430) generally destroys the symplectic property. Consequently, energy is no longer a strong invariant of the modified map and is only weakly conserved, often exhibiting a random walk.

-   **Mass**: In contrast, the conservation of mass, momentum, and energy in conservative finite-volume Godunov schemes is a strong invariance that stems from the telescoping cancellation of fluxes at cell interfaces. This property can be maintained even under AMR [subcycling](@entry_id:755594), provided that a "flux correction" or refluxing procedure is implemented to enforce it  .

-   **Entropy**: Entropy is a special case. For physical reasons (the [second law of thermodynamics](@entry_id:142732)), it should not be conserved at shocks. Shock-capturing schemes like Godunov's method are designed not to conserve entropy but to satisfy a discrete **[entropy inequality](@entry_id:184404)**, ensuring entropy is properly generated. This property is preserved by adaptive stepping, but due to inherent [numerical dissipation](@entry_id:141318), these schemes do not keep entropy strictly constant even in smooth flow at finite $\Delta t$.

In summary, [adaptive time-stepping](@entry_id:142338) is a powerful and essential tool, but its implementation requires a deep understanding of its interplay with the stability, accuracy, and conservation properties of the underlying [numerical schemes](@entry_id:752822).