## Introduction
Smoothed Particle Hydrodynamics (SPH) is a powerful mesh-free Lagrangian method for simulating fluid dynamics, with broad applications across science and engineering. However, the standard, ideal formulation of SPH confronts a critical limitation: its inability to naturally capture shock waves. This gap arises because ideal SPH conserves entropy, whereas physical shocks are inherently dissipative events that generate entropy. To resolve this, a numerical term known as **artificial viscosity** (AV) is deliberately introduced. This article provides a graduate-level exploration of this essential numerical method, explaining its foundational theory, modern implementations, and practical applications in fields such as [computational astrophysics](@entry_id:145768), where shocks are fundamental to phenomena like [structure formation](@entry_id:158241), supernova explosions, and accretion processes.

The journey begins in the **Principles and Mechanisms** section, where we will dissect why [artificial viscosity](@entry_id:140376) is necessary, how it bridges the gap between [ideal hydrodynamics](@entry_id:750508) and the physical reality of shocks defined by the Rankine-Hugoniot conditions, and the mechanics of the classic Monaghan-Gingold formulation. Next, the **Applications and Interdisciplinary Connections** section will explore the real-world impact of AV in simulations, discussing how it is adapted for cosmology, used as a diagnostic tool, and the challenges it poses in multiphysics contexts. Finally, the **Hands-On Practices** section provides concrete exercises to solidify your understanding, challenging you to derive key stability conditions and performance metrics related to artificial viscosity. Through this structured approach, you will gain a deep appreciation for the theory, implementation, and critical use of [artificial viscosity](@entry_id:140376) in modern SPH simulations.

## Principles and Mechanisms

The accurate modeling of astrophysical gas dynamics, particularly in the context of structure formation, requires robust numerical methods capable of handling the extreme physical conditions that arise, most notably [shock waves](@entry_id:142404). While Smoothed Particle Hydrodynamics (SPH) provides a powerful Lagrangian framework for evolving fluids, its standard formulation based on the inviscid Euler equations presents a fundamental challenge in capturing these essential dissipative phenomena. This chapter delves into the principles behind why [artificial viscosity](@entry_id:140376) is necessary in SPH and explores the mechanisms by which it is implemented, from classic formulations to modern refinements.

### The Fundamental Problem: Shocks in Ideal Lagrangian Hydrodynamics

The SPH method discretizes the fluid into a set of particles, whose properties evolve according to Lagrangian forms of the conservation laws. In its ideal, non-dissipative form, the SPH [discretization](@entry_id:145012) of the Euler equations is derived from a discrete Lagrangian. This elegant construction guarantees the [conservation of mass](@entry_id:268004), linear momentum, angular momentum, and, crucially, total energy to machine precision [@problem_id:3504476].

The evolution of a fluid's [thermodynamic state](@entry_id:200783) is governed by the first law of thermodynamics, which can be expressed for a fluid element in terms of the specific entropy $s$, specific internal energy $u$, temperature $T$, and density $\rho$: $T ds = du + P d(1/\rho)$. Taking the material derivative and substituting the standard fluid equations, we find that the rate of change of a particle's specific entropy is directly proportional to any non-[adiabatic heating](@entry_id:182901) or cooling, $Q$. In an ideal SPH framework without any explicit heating terms, $Q=0$, which leads to the conclusion that the specific entropy of each particle is conserved: $ds/dt = 0$ [@problem_id:3465269].

This inherent [entropy conservation](@entry_id:749018) poses a direct conflict with the physical reality of shocks. A shock wave is not merely a steep gradient but a true discontinuity where [irreversible processes](@entry_id:143308) occur. These processes are governed by the **Rankine-Hugoniot [jump conditions](@entry_id:750965)**, which are derived from the integral form of the Euler equations for mass, momentum, and energy conservation across the shock front. For a steady, planar shock, these conditions are [@problem_id:3465332]:

1.  **Mass Flux Conservation:** $[\rho u] = 0$
2.  **Momentum Flux Conservation:** $[\rho u^2 + p] = 0$
3.  **Energy Flux Conservation:** $[\rho u (e + \frac{1}{2}u^2 + p/\rho)] = 0$

Here, the bracket $[q] \equiv q_2 - q_1$ denotes the jump in a quantity $q$ from the upstream (pre-shock, state 1) to the downstream (post-shock, state 2) region, and $u$ is the [fluid velocity](@entry_id:267320) normal to the shock. While the Euler equations themselves are formally inviscid, a physically admissible solution to these jump conditions—one that respects the second law of thermodynamics—requires that entropy cannot decrease across the shock. For any compressive shock, entropy must strictly increase: $s_2 > s_1$ [@problem_id:3465332] [@problem_id:3465273].

An ideal SPH scheme, by conserving entropy for each particle, cannot satisfy this fundamental physical requirement. When particles representing a supersonic flow encounter a compression, their inability to generate entropy and dissipate kinetic energy leads to severe numerical pathologies. Particles may unphysically interpenetrate or form large, spurious oscillations (a Gibbs-like phenomenon), ultimately leading to an incorrect shock structure or a complete breakdown of the simulation. It is crucial to understand that the kernel smoothing inherent in SPH does not, by itself, provide the correctly structured dissipation needed to capture shocks [@problem_id:3504476]. A dedicated mechanism is required.

### Artificial Viscosity: A Numerical Solution

The solution to this problem is the introduction of an **artificial viscosity** (AV). This is a carefully constructed numerical term, added to the [equations of motion](@entry_id:170720), designed to mimic the dissipative effects of a true physical viscosity within the infinitesimally thin layer of a real shock. Its primary function is to provide a mechanism for the irreversible conversion of kinetic energy into thermal energy in regions of strong compression, thereby generating the required entropy increase.

The core thermodynamic requirement for any valid AV scheme is that it must produce non-negative heating in compressive flows. As derived from the first law, the rate of change of specific entropy is $T ds/dt = Q_{\mathrm{av}}$, where $Q_{\mathrm{av}}$ is the specific heating rate supplied by the artificial viscosity. To comply with the [second law of thermodynamics](@entry_id:142732) ($ds/dt \ge 0$), the heating term must be non-negative: $Q_{\mathrm{av}} \ge 0$ [@problem_id:3465269]. A formulation that violated this could lead to unphysical "cold shocks" or numerical instability.

This is achieved by introducing a [viscous force](@entry_id:264591) or pressure that acts between particles. The work done by this [viscous force](@entry_id:264591) is then added as a [source term](@entry_id:269111) to the internal [energy equation](@entry_id:156281). A correctly implemented, pairwise symmetric AV formulation ensures that [@problem_id:3465273] [@problem_id:3504476]:
*   Total linear and angular momentum are conserved, as the internal [viscous forces](@entry_id:263294) are equal and opposite and act along the line connecting particle pairs.
*   Total energy is conserved, as the kinetic energy dissipated by the [viscous force](@entry_id:264591) is exactly balanced by the increase in the total internal energy of the system.

This controlled dissipation allows the SPH simulation to satisfy the Rankine-Hugoniot conditions for momentum and energy and, most importantly, to produce the correct entropy jump across the shock front [@problem_id:3465332].

### The Monaghan-Gingold Formulation: A Classic Mechanism

The most widely used form of artificial viscosity in SPH is the formulation developed by Monaghan and Gingold. It introduces a symmetric, pairwise viscous pressure term, $\Pi_{ij}$, into the momentum and energy equations. The standard form is given by [@problem_id:3465317] [@problem_id:3504531]:

$$
\Pi_{ij} = 
\begin{cases}
\dfrac{-\alpha c_{ij} \mu_{ij} + \beta \mu_{ij}^2}{\rho_{ij}},  &\text{if } \mathbf{v}_{ij} \cdot \mathbf{r}_{ij}  0 \\
0,  \text{otherwise}
\end{cases}
$$

where $\mathbf{r}_{ij} = \mathbf{r}_i - \mathbf{r}_j$ and $\mathbf{v}_{ij} = \mathbf{v}_i - \mathbf{v}_j$ are the [relative position](@entry_id:274838) and velocity vectors. The terms $c_{ij}$, $\rho_{ij}$, and $h_{ij}$ are symmetric averages of the sound speed, density, and smoothing length of the particle pair $(i, j)$. The [dimensionless parameters](@entry_id:180651) $\alpha$ and $\beta$ control the strength of the viscous terms.

The term $\mu_{ij}$ is a dimensionless measure of the compression between the particles, defined as:
$$
\mu_{ij} = \frac{h_{ij} (\mathbf{v}_{ij} \cdot \mathbf{r}_{ij})}{r_{ij}^2 + \eta^2}
$$
Here, $r_{ij} = |\mathbf{r}_{ij}|$, and $\eta^2$ is a small [regularization parameter](@entry_id:162917) (e.g., $\eta^2 = 0.01 h_{ij}^2$) that prevents the denominator from becoming zero if two particles get very close [@problem_id:3465317].

Let's dissect the components of this formulation:
*   **The Switch:** The condition $\mathbf{v}_{ij} \cdot \mathbf{r}_{ij}  0$ is the crucial switch that activates the viscosity. It is only non-zero for pairs of particles that are approaching each other along their line of separation. This targets the dissipation to compressive regions, leaving expanding flows unaffected. Since $\mathbf{v}_{ij} \cdot \mathbf{r}_{ij}  0$ implies $\mu_{ij}  0$, the negative sign in the linear term ensures that $\Pi_{ij}$ acts as a repulsive pressure.

*   **The Linear Term ($\alpha$ term):** This term, proportional to $-\alpha c_{ij} \mu_{ij}$, can be thought of as a numerical [bulk viscosity](@entry_id:187773). It is effective at damping oscillations and capturing weak, low-Mach-number shocks. The inclusion of the sound speed $c_{ij}$ provides the correct [signal velocity](@entry_id:261601) scale for acoustic phenomena.

*   **The Quadratic Term ($\beta$ term):** This term, proportional to $\beta \mu_{ij}^2$, is essential for handling strong shocks. To understand why, consider the momentum balance across a high-Mach-number shock. The pressure jump required to slow the incoming fluid must be comparable to the fluid's [ram pressure](@entry_id:194932), which scales as $\rho v^2$. A viscous pressure that is only linear in velocity (like the $\alpha$ term) is insufficient to prevent particle interpenetration at high Mach numbers. The quadratic term, scaling with $v^2$ via $\mu_{ij}^2$, provides the necessary [stopping power](@entry_id:159202) [@problem_id:3465341] [@problem_id:3504476]. The transition between the dominance of the linear and quadratic terms occurs at a threshold Mach number, $\mathcal{M}_{\star} \equiv v_r / c_s$, where $v_r = -\mathbf{v}_{ij} \cdot \hat{\mathbf{r}}_{ij}$ is the approach speed. By equating the two terms, we find this threshold to be $\mathcal{M}_{\star} = (\alpha/\beta)(h/r_{ij})^{-1}$. For typical parameters in [cosmological simulations](@entry_id:747925), such as $\alpha=1$, $\beta=2$, and neighboring particles having $r_{ij} \approx h$, this gives $\mathcal{M}_{\star} = 0.5$. This indicates that for even mildly supersonic compressions, the quadratic term becomes the dominant source of dissipation [@problem_id:3465341].

With this definition, the SPH equations for momentum and specific internal energy for particle $i$ are modified to include the AV contributions [@problem_id:3504531]:
$$
\left.\frac{d\mathbf{v}_i}{dt}\right|_{\mathrm{AV}} = -\sum_j m_j \Pi_{ij} \nabla_i W_{ij}
$$
$$
\left.\frac{du_i}{dt}\right|_{\mathrm{AV}} = \frac{1}{2} \sum_j m_j \Pi_{ij} (\mathbf{v}_{ij} \cdot \nabla_i W_{ij})
$$
The factor of $1/2$ in the [energy equation](@entry_id:156281) ensures that the total energy dissipated from the kinetic energy of the pair $(i, j)$ is symmetrically distributed between them, preserving total energy conservation.

It is critical to distinguish this numerical construct from the physical viscosity found in the Navier-Stokes equations. Physical viscosity is a constitutive property of a fluid, and its effects (via the [viscous stress](@entry_id:261328) tensor) are present whenever there are velocity gradients. In contrast, SPH [artificial viscosity](@entry_id:140376) is a computational tool designed to be active only under the specific conditions of strong, convergent flows to stabilize the numerical scheme [@problem_id:3504531].

### Modern Refinements and Challenges

While the Monaghan-Gingold formulation is effective, it is not without its drawbacks. Decades of research have led to important refinements designed to make [artificial viscosity](@entry_id:140376) more physically accurate and less numerically intrusive.

#### The Signal Velocity Approach

A more physically intuitive way to motivate the viscosity term is through the concept of **[signal velocity](@entry_id:261601)**. In a pairwise interaction, the maximum speed at which information can propagate between particles $i$ and $j$ is bounded by the sum of their sound speeds plus their [relative velocity](@entry_id:178060) of approach. This leads to the definition of a [signal velocity](@entry_id:261601) for approaching particles [@problem_id:3465283]:
$$
v_{\text{sig}} = c_i + c_j - \beta (\mathbf{v}_{ij} \cdot \hat{\mathbf{r}}_{ij})
$$
where the term involving $\mathbf{v}_{ij}$ is only included for approaching pairs ($\mathbf{v}_{ij} \cdot \hat{\mathbf{r}}_{ij}  0$). This provides a robust upper bound on the [characteristic speed](@entry_id:173770) for compressive waves. The viscosity can then be constructed to be proportional to this [signal velocity](@entry_id:261601). A key advantage of this formulation, especially in cosmology, is that by using only peculiar (non-Hubble) velocities for $\mathbf{v}_{ij}$, it is automatically Galilean-invariant and insensitive to the uniform Hubble expansion, preventing spurious dissipation from the expansion of the universe itself [@problem_id:3465283].

#### The Problem of Shear Flows: The Balsara Switch

A significant flaw in the basic AV formulation is its inability to distinguish between pure compression and pure shear. A rotating disk or a shearing flow can trigger the $\mathbf{v}_{ij} \cdot \mathbf{r}_{ij}  0$ condition for some particle pairs, even when the net flow divergence is zero ($\nabla \cdot \mathbf{v} = 0$). This activates the viscosity, which then spuriously [damps](@entry_id:143944) the rotation or shear, leading to unphysical loss of angular momentum and the suppression of important fluid instabilities like the Kelvin-Helmholtz instability [@problem_id:3504476].

The most common solution is to introduce a **viscosity switch** that explicitly reduces the viscosity in regions dominated by shear or vorticity. The **Balsara switch** achieves this by multiplying the viscosity term $\Pi_{ij}$ by a factor $f_i$ that depends on the ratio of local flow divergence to [vorticity](@entry_id:142747) [@problem_id:3465350]:
$$
f_i = \frac{|\nabla \cdot \mathbf{v}|_i}{|\nabla \cdot \mathbf{v}|_i + |\nabla \times \mathbf{v}|_i + \epsilon c_i / h_i}
$$
In a pure 1D shock, vorticity $|\nabla \times \mathbf{v}|_i \approx 0$, so $f_i \to 1$ and the viscosity acts at full strength. Conversely, in a pure shear flow, divergence $|\nabla \cdot \mathbf{v}|_i \approx 0$, causing $f_i \to 0$ and effectively switching the viscosity off. The small regularization term in the denominator ensures [numerical stability](@entry_id:146550) in quiescent regions where both divergence and vorticity are near zero [@problem_id:3465350].

#### The Problem of Subsonic Turbulence: Time-Dependent Viscosity

Another major challenge is that the viscosity required to capture strong shocks is often excessively dissipative in subsonic regions. A constant, high value of $\alpha \sim 1$ can damp out physical turbulence in the interstellar medium or [intracluster medium](@entry_id:158282). The effective kinematic viscosity of the standard AV scales as $\nu_{\mathrm{eff}} \propto \alpha c_s h$. The Reynolds number, $\mathrm{Re} \equiv UL/\nu$, therefore scales as $\mathrm{Re} \propto (UL) / (\alpha c_s h)$. For a fixed resolution $h$ and constant $\alpha$, the effective Reynolds number of the simulation becomes proportional to the Mach number, $\mathcal{M} = U/c_s$. As the flow becomes more subsonic ($\mathcal{M} \to 0$), the Reynolds number plummets, and the flow becomes overly viscous, damping out turbulent eddies that should be physically present [@problem_id:3504527].

To overcome this, modern SPH codes often employ **time-dependent viscosity schemes**. In these methods, the parameter $\alpha$ is no longer a global constant but a variable, $\alpha_i(t)$, that evolves for each particle. The value of $\alpha_i$ is allowed to decay towards a small floor value over a characteristic timescale, but it is rapidly increased towards a maximum value whenever the particle encounters a shock trigger (typically a strong, negative velocity divergence). This allows the scheme to be highly dissipative only when and where it is needed—in shocks—while maintaining a low level of viscosity elsewhere, permitting a much higher effective Reynolds number and a more faithful representation of subsonic turbulence [@problem_id:3504527].

In summary, [artificial viscosity](@entry_id:140376) is an indispensable tool in SPH, bridging the gap between the ideal, entropy-conserving nature of the discretized Euler equations and the dissipative reality of [shock physics](@entry_id:196920). While classic formulations provide a robust foundation, modern refinements that account for signal speeds, shear flows, and subsonic dissipation are crucial for achieving high-fidelity simulations of complex astrophysical phenomena.