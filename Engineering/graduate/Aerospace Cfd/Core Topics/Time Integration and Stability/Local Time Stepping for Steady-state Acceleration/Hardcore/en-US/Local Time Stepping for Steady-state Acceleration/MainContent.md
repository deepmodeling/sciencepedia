## Introduction
In the realm of Computational Fluid Dynamics (CFD), achieving a converged [steady-state solution](@entry_id:276115) is often a computationally intensive process. Explicit [time-marching schemes](@entry_id:1133157), while straightforward to implement, are frequently hampered by stringent stability conditions that demand a single, global time step small enough to satisfy the most restrictive cell in the entire mesh. This bottleneck can lead to prohibitively long simulation times, particularly for complex problems with highly [non-uniform grids](@entry_id:752607). The Local Time Stepping (LTS) method offers a powerful solution to this challenge by decoupling the time step for each cell, allowing the simulation to evolve at a locally-optimized pace and dramatically accelerating convergence.

This article provides a comprehensive exploration of Local Time Stepping, designed for graduate-level students and practitioners in [aerospace engineering](@entry_id:268503) and related computational sciences. We will dissect the method from its theoretical foundations to its practical implementation. The first chapter, **Principles and Mechanisms**, will introduce the concept of [pseudo-transient continuation](@entry_id:753844) and explain how LTS leverages this to speed up calculations while maintaining a conservative solution. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate the synergy of LTS with other advanced numerical methods like multigrid and [preconditioning](@entry_id:141204), and showcase its broad applicability in aerospace, combustion, and even biophysics. Finally, the **Hands-On Practices** section will solidify these concepts through targeted problems that address the calculation of [local time](@entry_id:194383) steps and the enforcement of conservation.

## Principles and Mechanisms

In the pursuit of [steady-state solutions](@entry_id:200351) to the governing equations of fluid dynamics, the computational cost is often dominated by the number of iterations required for the numerical scheme to converge. When using [explicit time-marching](@entry_id:749180) methods, this cost is further exacerbated by stability constraints that limit the size of the time step. Local Time Stepping (LTS) is a powerful technique designed to accelerate convergence by overcoming the limitations of a single, global time step. This chapter elucidates the fundamental principles behind LTS, details its mechanisms, and explores the critical theoretical and practical considerations for its successful implementation.

### The Principle of Pseudo-Transient Continuation

The ultimate goal of a [steady-state simulation](@entry_id:755413) is to find the solution $\boldsymbol{U}^\ast$ to a system of nonlinear algebraic equations, which results from the spatial discretization of the governing partial differential equations (PDEs). For a finite-volume scheme, this system can be expressed as the vanishing of the [residual vector](@entry_id:165091) $\boldsymbol{R}(\boldsymbol{U})$ in every control volume $i$:
$$
\boldsymbol{R}_i(\boldsymbol{U}^\ast) = \boldsymbol{0} \quad \forall i
$$
where $\boldsymbol{R}_i$ represents the net flux imbalance for cell $i$.

Instead of employing a direct nonlinear solver, which can be complex and computationally expensive, **[pseudo-transient continuation](@entry_id:753844) (PTC)** reframes this [root-finding problem](@entry_id:174994) as a long-[time integration](@entry_id:170891) of a fictitious transient problem. An artificial time derivative is introduced, constructing an [ordinary differential equation](@entry_id:168621) (ODE) in a pseudo-time $\tau$:
$$
\frac{\partial \boldsymbol{U}}{\partial \tau} + \boldsymbol{R}(\boldsymbol{U}) = \boldsymbol{0}
$$
The steady state of this pseudo-transient ODE, where $\partial \boldsymbol{U} / \partial \tau = \boldsymbol{0}$, corresponds precisely to the desired [steady-state solution](@entry_id:276115) of the original problem, $\boldsymbol{R}(\boldsymbol{U}^\ast) = \boldsymbol{0}$.

This approach must be clearly distinguished from a physically time-accurate simulation. In a physical simulation, the objective is to accurately model the evolution of the flow field in real time, $t$. This requires a consistent discretization of the physical time derivative $\partial \boldsymbol{U} / \partial t$ and the use of a single, global time step $\Delta t$ that is small enough to resolve the fastest physical phenomena anywhere in the domain.

In contrast, [pseudo-transient continuation](@entry_id:753844) has no such objective. The path from the initial guess to the final solution in $\tau$-time is entirely artificial and devoid of physical meaning. Consequently, PTC discards the physical transient evolution and any requirement to match a physical initial condition. Its singular focus is on reaching the fixed point $\boldsymbol{R}(\boldsymbol{U}^\ast) = \boldsymbol{0}$ as efficiently as possible. Crucially, the method preserves the properties of the spatial operator $\boldsymbol{R}(\boldsymbol{U})$. If the [spatial discretization](@entry_id:172158) is conservative, the converged steady-state solution will also be conservative. The path to convergence, however, is not. This decoupling of the convergence path from physical reality is the conceptual key that unlocks the acceleration offered by Local Time Stepping .

### Local Time Stepping as an Acceleration Mechanism

Since the transient evolution in pseudo-time is non-physical, there is no reason to enforce that all parts of the computational domain evolve synchronously. This insight is the foundation of **Local Time Stepping (LTS)**. Instead of being constrained by a single global time step dictated by the most restrictive stability limit in the entire mesh (often in a region of very fine cells or high flow speeds), LTS allows each control volume to be advanced with its own, locally-determined pseudo-time step $\Delta \tau_i$.

For an explicit forward Euler update, the discretized pseudo-transient equation for cell $i$ with volume $V_i$ becomes:
$$
\boldsymbol{U}_i^{n+1} = \boldsymbol{U}_i^{n} - \frac{\Delta \tau_i}{V_i} \boldsymbol{R}_i(\boldsymbol{U}^n)
$$
The [local time](@entry_id:194383) step $\Delta \tau_i$ is chosen to be as large as possible while maintaining [numerical stability](@entry_id:146550) for that specific cell. This allows regions of the flow that are less restrictive (e.g., large cells in a far-field region) to take much larger steps, rapidly propagating information and accelerating the [global convergence](@entry_id:635436) to the steady state. The final converged solution, characterized by $\boldsymbol{R}_i(\boldsymbol{U}) = \boldsymbol{0}$, is independent of the distribution of [local time](@entry_id:194383) steps $\Delta \tau_i$ used to reach it, provided the iteration converges .

The [local time](@entry_id:194383) step for each cell is determined by its local **Courant-Friedrichs-Lewy (CFL) condition**. For an explicit finite-volume scheme applied to a hyperbolic system, the stability constraint for cell $i$ can be derived by considering the flux of information across its faces. The canonical formula for the [local time](@entry_id:194383) step is:
$$
\Delta \tau_i = \text{CFL} \cdot \frac{V_i}{\sum_{f \in \partial \Omega_i} |\lambda_f| A_f}
$$
Here, $\text{CFL}$ is the Courant number (a safety factor, typically $\le 1$), $V_i$ is the cell volume, $A_f$ is the area of face $f$, and the sum is over all faces of cell $i$. The term $|\lambda_f|$ represents the maximum characteristic [wave speed](@entry_id:186208) normal to the face $f$, which is the spectral radius of the normal flux Jacobian, $\rho(\partial (\boldsymbol{F} \cdot \boldsymbol{n}_f) / \partial \boldsymbol{U})$. This denominator represents the total volumetric rate of information exchange for cell $i$. In contrast, a [global time stepping](@entry_id:749933) scheme would be forced to use $\Delta \tau = \min_i (\Delta \tau_i)$, which can be orders of magnitude smaller than the average [local time](@entry_id:194383) step .

For the compressible Euler equations, the characteristic speeds of wave propagation normal to a face are $\{u_n - a, u_n, u_n + a\}$, where $u_n = \boldsymbol{u} \cdot \boldsymbol{n}_f$ is the [normal fluid](@entry_id:183299) velocity and $a$ is the local speed of sound. The maximum of the [absolute values](@entry_id:197463) of these speeds gives the spectral radius:
$$
|\lambda_f| = |u_n| + a
$$
Thus, the specific [local time](@entry_id:194383) step formula for inviscid [compressible flow](@entry_id:156141) is :
$$
\Delta \tau_i = \text{CFL} \cdot \frac{V_i}{\sum_{f \in \partial \Omega_i} (|u_n| + a)_f A_f}
$$

The ratio of the chosen time step to the maximum allowable stable time step is the local CFL number. From the formula above, the local CFL number for cell $i$ is defined as :
$$
\text{CFL}_i = \frac{\Delta \tau_i}{V_i} \sum_{f \in \partial \Omega_i} |\lambda_f| A_f
$$
In an LTS implementation, one typically sets a target $\text{CFL}_{target}$ for all cells and calculates each $\Delta \tau_i$ accordingly to maintain $\text{CFL}_i = \text{CFL}_{target}$.

### Linear Stability and Convergence

A deeper understanding of the stability of the LTS iteration can be gained by analyzing the propagation of errors. Consider the explicit update for the error $\boldsymbol{e}^n = \boldsymbol{U}^n - \boldsymbol{U}^\star$ around the steady-state solution $\boldsymbol{U}^\star$. By linearizing the residual operator, $\boldsymbol{R}(\boldsymbol{U}^n) \approx \boldsymbol{J} \boldsymbol{e}^n$, where $\boldsymbol{J}$ is the Jacobian of the residual, the [error propagation](@entry_id:136644) for a simplified local system can be described by:
$$
\boldsymbol{e}_i^{n+1} = (\boldsymbol{I} - \Delta \tau_i \boldsymbol{J}_i) \boldsymbol{e}_i^n
$$
where $\boldsymbol{J}_i$ represents the local Jacobian matrix $\partial \boldsymbol{R}_i / \partial \boldsymbol{U}_i$. For the error to decay, the mapping must be a **contraction**, which requires the spectral radius of the [amplification matrix](@entry_id:746417), $\boldsymbol{G}_i = \boldsymbol{I} - \Delta \tau_i \boldsymbol{J}_i$, to be less than one: $\rho(\boldsymbol{G}_i)  1$ .

The eigenvalues of $\boldsymbol{G}_i$ are $1 - \Delta \tau_i \mu_k$, where $\mu_k$ are the eigenvalues of $\boldsymbol{J}_i$. The stability condition therefore becomes $|1 - \Delta \tau_i \mu_k|  1$ for all eigenvalues $\mu_k$. This inequality states that the complex number $z_k = \Delta \tau_i \mu_k$ must lie strictly within a circular disk of radius 1 centered at $(1, 0)$ in the complex plane. A detailed analysis shows this leads to the stability constraint :
$$
\Delta \tau_i  \frac{2 \mathrm{Re}(\mu_k)}{|\mu_k|^2}
$$
This must hold for all eigenvalues $\mu_k$ of $\boldsymbol{J}_i$. For many common upwind discretizations of hyperbolic problems, the eigenvalues of the Jacobian are real and non-negative. In this important special case, the condition simplifies significantly. The spectral radius of the Jacobian is $\rho(\boldsymbol{J}_i) = \max_k \mu_k$, and the stability constraint becomes:
$$
\Delta \tau_i  \frac{2}{\rho(\boldsymbol{J}_i)}
$$
If we define a dimensionless local CFL number as $C_i = \rho(\boldsymbol{J}_i) \Delta \tau_i$, this stability limit is equivalent to $C_i  2$. This analysis provides a rigorous theoretical foundation for the CFL conditions used in practice .

### Practical Considerations and Implementation Constraints

While the principle of LTS is straightforward, its robust and correct implementation requires careful attention to several critical details. The introduction of heterogeneous time steps can interact with the physics and the discretization in subtle ways that, if ignored, can lead to instability, non-physical results, or convergence to incorrect solutions.

#### Time Step Constraints in Viscous Flows

For [viscous flows](@entry_id:136330) governed by the Navier-Stokes equations, the stability of an [explicit scheme](@entry_id:1124773) is limited by both convective (hyperbolic) and diffusive (parabolic) phenomena.
1.  **Convective Constraint:** As discussed, the CFL condition for convective terms leads to a time step limit that scales linearly with the characteristic cell size $h_i$: $\Delta \tau_{c,i} \propto h_i / (|\boldsymbol{u}| + a)$.
2.  **Diffusive Constraint:** The stability of explicit schemes for diffusion processes leads to a more restrictive constraint, where the time step scales with the square of the [cell size](@entry_id:139079): $\Delta \tau_{\nu,i} \propto h_i^2 / \nu_{\text{eff}}$, where $\nu_{\text{eff}}$ is the effective [kinematic viscosity](@entry_id:261275) (including molecular and turbulent contributions).

When both effects are present, the explicit update must be stable with respect to both. Therefore, the overall [local time](@entry_id:194383) step $\Delta \tau_i$ must be less than or equal to both individual limits. This is achieved by taking the minimum of the two:
$$
\Delta \tau_i = \min(\Delta \tau_{c,i}, \Delta \tau_{\nu,i}) = \min\left( C_c \frac{h_i}{|\boldsymbol{u}| + a}, C_\nu \frac{h_i^2}{\nu_{\text{eff}}} \right)
$$
The quadratic dependence on $h_i$ in the viscous constraint often makes it the dominant limitation in finely resolved regions, such as boundary layers, even when the flow velocity is low .

#### Preservation of Physical Admissibility

For compressible flows, the state vector must remain in the set of physically **admissible states**, meaning density $\rho$ and pressure $p$ must remain positive throughout the iteration. A state with negative density or pressure is non-physical, and attempting to evaluate thermodynamic properties like the speed of sound ($a = \sqrt{\gamma p / \rho}$) will cause the simulation to fail.

This is a critical concern for explicit methods, which can produce overshoots and undershoots. **Positivity preservation** is not automatic. However, for certain [numerical fluxes](@entry_id:752791) (e.g., first-order [monotone schemes](@entry_id:752159)), it can be proven that the updated state $\boldsymbol{U}_i^{n+1}$ is a convex combination of the previous state $\boldsymbol{U}_i^n$ and its neighbors' states, provided the time step is sufficiently small. Since the set of admissible states is convex, a convex combination of admissible states is itself admissible. This leads to a [sufficient condition](@entry_id:276242) on the [local time](@entry_id:194383) step, often expressed in terms of the local face-based Courant numbers $C_{if} = \frac{\Delta \tau_i}{V_i} s_{\max,f} A_{if}$:
$$
\sum_{f \in \partial \Omega_i} C_{if} \leq c
$$
where $c$ is a constant, typically $c=1$ for many common schemes. Enforcing this condition, often by rescaling the locally computed $\Delta \tau_i$, is a crucial mechanism for ensuring the robustness of an LTS scheme .

#### Ensuring Discrete Conservation

A cornerstone of the finite-volume method is discrete conservation. The change in a conserved quantity within the domain must equal the net flux through the domain boundary. A naive implementation of LTS can violate this principle.

Consider two adjacent cells, $i$ and $j$, sharing an interior face. The change in the conserved quantity in each cell is approximately $-\Delta \tau_i R_i$ and $-\Delta \tau_j R_j$. The residual for cell $i$ contains a flux contribution from the shared face, say $+F_f$, while the residual for cell $j$ contains the contribution $-F_f$. The net change for the pair of cells due to this face flux is proportional to $(-\Delta \tau_i F_f) + (-\Delta \tau_j (-F_f)) = (\Delta \tau_j - \Delta \tau_i) F_f$. If $\Delta \tau_i \neq \Delta \tau_j$, this term is non-zero, creating a spurious local source or sink of the conserved quantity.

To maintain [discrete conservation](@entry_id:1123819), a **flux accumulation** or face-based update approach is required. In this method, instead of updating cell states directly, one first computes and accumulates the time-integrated flux $\mathcal{J}_f$ for each face over a pseudo-time interval. The update to the cell states is then performed using these integrated fluxes. For an interior face between cells $i$ and $j$, the update to cell $i$ includes the term $-\mathcal{J}_f$, while the update to cell $j$ includes $+\mathcal{J}_f$. The cancellation is perfect, $(-\mathcal{J}_f) + (+\mathcal{J}_f) = 0$, and [discrete conservation](@entry_id:1123819) is maintained by construction, irrespective of the differing [local time](@entry_id:194383) steps used to compute the integrated flux values .

#### Avoiding Spurious Steady States

The final, and perhaps most subtle, pitfall is the risk of converging to a **spurious steady state**. A correct LTS implementation must ensure that the fixed point of the iteration corresponds to the true discrete steady state, $\boldsymbol{R}_i(\boldsymbol{U}) = \boldsymbol{0}$. The standard explicit LTS update, $u_i^{n+1} = u_i^n - (\Delta \tau_i/V_i) R_i(u^n)$, achieves this. At the fixed point, the update is zero, which, since $\Delta \tau_i > 0$, directly implies $R_i(u) = 0$.

However, incorrect implementations can modify the effective residual operator that the scheme is driving to zero. For example:
-   **Asynchronous updates:** If, within a single global iteration, the residual for cell $i$ is computed using neighbor states that have already been updated to the next pseudo-time level, the [flux balance](@entry_id:274729) is broken. The solver is iterating on a non-conservative, mixed-time operator $\tilde{\boldsymbol{R}}(\boldsymbol{U}^n, \boldsymbol{U}^{n+1})$.
-   **Weighted residual assembly:** If the residual contributions at a face are explicitly weighted by the differing [local time](@entry_id:194383) steps of the adjacent cells, the operator again becomes non-conservative.

In these cases, the scheme converges to a fixed point where the modified, non-physical residual is zero, $\tilde{\boldsymbol{R}}(\boldsymbol{U}^\star) = \boldsymbol{0}$. This state $\boldsymbol{U}^\star$ is not the true physical steady state, as the true conservative residual is non-zero, $\boldsymbol{R}(\boldsymbol{U}^\star) \neq \boldsymbol{0}$. Such spurious solutions are artifacts of the numerical scheme and lack physical validity. Ensuring that the assembled residual is always conservative and based on a consistent time level is paramount to guaranteeing a physically meaningful solution . Furthermore, it is important to recognize that even with locally stable time steps, strong off-diagonal coupling in the global Jacobian can, in principle, lead to global instability, highlighting the complex nature of such iterative systems .