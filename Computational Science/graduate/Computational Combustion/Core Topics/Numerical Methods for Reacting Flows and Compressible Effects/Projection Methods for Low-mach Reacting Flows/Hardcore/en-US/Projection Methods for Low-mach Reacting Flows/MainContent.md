## Introduction
The simulation of [reacting flows](@entry_id:1130631), such as those found in combustion, presents a significant computational challenge due to the vast range of time and length scales involved. For many important applications, from industrial furnaces to atmospheric flames, the flow speed is much lower than the speed of sound. This "low-Mach number" regime is computationally stiff for standard [compressible flow solvers](@entry_id:1122759), as they must use prohibitively small time steps to resolve fast-moving but physically unimportant [acoustic waves](@entry_id:174227). This article addresses this challenge by focusing on a powerful and efficient class of numerical techniques: [projection methods](@entry_id:147401) tailored for low-Mach number reacting flows.

This article will guide you through the fundamental principles, practical applications, and advanced numerical implementations of this methodology. In the "Principles and Mechanisms" section, you will learn how the low-Mach number approximation filters acoustic phenomena and leads to a variable-density divergence constraint, and how the projection method enforces this constraint by solving an elliptic pressure equation. The "Applications and Interdisciplinary Connections" section will explore how these methods are used to study combustion phenomena, their coupling with advanced numerical algorithms like operator splitting and [adaptive mesh refinement](@entry_id:143852), and their relationship to [high-performance computing](@entry_id:169980). Finally, the "Hands-On Practices" section will provide opportunities to apply these concepts through targeted exercises, solidifying your understanding of this essential CFD technique.

## Principles and Mechanisms

The simulation of [reacting flows](@entry_id:1130631), particularly those involving combustion, presents a formidable computational challenge due to the wide range of temporal and spatial scales involved. In many practical applications, such as atmospheric flames, industrial furnaces, and gas turbines, the characteristic flow velocity $U$ is significantly smaller than the speed of sound $c$. The ratio of these scales is the Mach number, $M = U/c$. When $M \ll 1$, a profound simplification of the governing equations becomes possible through the **low-Mach number approximation**. This chapter elucidates the principles of this approximation and the mechanisms of the **[projection methods](@entry_id:147401)** used to solve the resulting system of equations.

### The Low-Mach Number Approximation: Filtering Acoustic Phenomena

The full compressible Navier-Stokes equations govern fluid motion across all speed regimes. However, they carry information about phenomena that are often irrelevant to the primary dynamics of low-speed [reacting flows](@entry_id:1130631). The most prominent of these are **[acoustic waves](@entry_id:174227)**, which propagate at the speed of sound. The characteristic time for an acoustic wave to traverse a domain of size $L$ is $t_a \sim L/c$, whereas the time for a fluid parcel to be convected across the same domain is $t_f \sim L/U$. The ratio of these timescales is precisely the Mach number: $t_a / t_f = M$.

In the low-Mach number regime, where $M \ll 1$, there is a stark separation of timescales: $t_a \ll t_f$. This implies that [acoustic waves](@entry_id:174227) propagate almost instantaneously relative to the fluid motion. This disparity creates a "stiffness" problem for numerical solvers; a time step small enough to resolve fast acoustic phenomena would be prohibitively restrictive for simulating the much slower convective and diffusive processes that typically govern [flame propagation](@entry_id:1125066) and pollutant formation.

The low-Mach number approximation systematically removes this stiffness by filtering out [acoustic waves](@entry_id:174227). This is achieved through a formal [asymptotic expansion](@entry_id:149302) of the governing equations in the small parameter $M$ . A central result of this analysis is the decomposition of the total pressure field $p(\mathbf{x}, t)$ into two distinct components:

$p(\mathbf{x}, t) = p_0(t) + \pi(\mathbf{x}, t)$

Here, $p_0(t)$ is the **thermodynamic pressure**. It is the leading-order term in the expansion and is found to be spatially uniform, varying only with time. This pressure component is responsible for thermodynamic state changes and appears in the equation of state. The second term, $\pi(\mathbf{x}, t)$, is the **hydrodynamic pressure**. It is a higher-order, spatially varying perturbation whose magnitude scales with the square of the Mach number, $\pi / p_0 = \mathcal{O}(M^2)$ . The physical role of the hydrodynamic pressure is not thermodynamic; rather, its gradient, $\nabla\pi$, acts within the momentum equation to ensure the velocity field remains consistent with the principles of mass conservation under this approximation. By decoupling the thermodynamic state from the small, local pressure fluctuations, the mechanism for acoustic wave propagation is eliminated from the model.

It is critical to understand the regime where this approximation is valid. Consider the contrast between a typical laboratory Bunsen flame and a detonation wave . For a Bunsen flame, characteristic flow speeds are a few meters per second, while the sound speed is hundreds of meters per second, yielding $M \ll 1$. The acoustic timescale is orders of magnitude smaller than the convective and chemical timescales. This clear separation makes the low-Mach approximation highly appropriate. Conversely, a detonation is a shock wave coupled to a reaction front, propagating at supersonic speeds, often with $M > 5$. Here, the fluid dynamic, acoustic, and chemical timescales are tightly coupled. An $\mathcal{O}(1)$ pressure jump across the shock is essential to the physics. Applying the low-Mach number approximation would filter out the shock wave itself, completely misrepresenting the phenomenon.

A common misconception is that the low-Mach number approximation is equivalent to an incompressible model or that it is invalidated by large density changes. This is incorrect. The primary purpose of low-Mach models in combustion is precisely to handle flows with large temperature variations and, consequently, large density variations (e.g., a factor of 7-8 density drop across a flame), while justifiably ignoring acoustic compressibility. The Bunsen flame is a prime example of a variable-density, low-Mach flow for which these methods are designed .

### The Variable-Density Divergence Constraint

The most significant consequence of the low-Mach number approximation in reacting flows is the emergence of a new kinematic constraint on the velocity field. In classical incompressible flow, the assumption of constant density, $\rho = \text{constant}$, reduces the continuity equation,
$$
\frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{u}) = 0
$$
to the familiar [divergence-free constraint](@entry_id:748603):
$$
\nabla \cdot \mathbf{u} = 0
$$

In a low-Mach [reacting flow](@entry_id:754105), density is far from constant. However, its variation is not driven by acoustic pressure fluctuations. Instead, it is dictated by the equation of state, which at leading order is governed by the thermodynamic pressure $p_0(t)$:
$$
p_0(t) = \rho(\mathbf{x}, t) \frac{R_{\mathrm{univ}}}{W(\mathbf{x}, t)} T(\mathbf{x}, t)
$$
where $R_{\mathrm{univ}}$ is the [universal gas constant](@entry_id:136843), $T$ is the temperature, and $W$ is the mixture molecular weight. This relation implies that density varies with changes in temperature and composition.

To find the new divergence constraint, we expand the continuity equation, $\frac{D\rho}{Dt} + \rho (\nabla \cdot \mathbf{u}) = 0$, which gives $\nabla \cdot \mathbf{u} = -\frac{1}{\rho}\frac{D\rho}{Dt}$. We then evaluate the material derivative of density by taking the [logarithmic derivative](@entry_id:169238) of the equation of state:
$$
\frac{1}{\rho}\frac{D\rho}{Dt} = \frac{1}{p_0}\frac{dp_0}{dt} - \frac{1}{T}\frac{DT}{Dt} - \frac{1}{W}\frac{DW}{Dt}
$$
Combining these results yields the **variable-density divergence constraint**:
$$
\nabla \cdot \mathbf{u} = S \equiv -\frac{1}{p_0}\frac{dp_0}{dt} + \frac{1}{T}\frac{DT}{Dt} + \frac{1}{W}\frac{DW}{Dt}
$$
This equation is a cornerstone of low-Mach [reacting flow simulation](@entry_id:1130632)  . It reveals that the velocity field is not divergence-free. Instead, its divergence, or dilatation, $S$, is determined by the rates of change of temperature (thermal expansion), composition (molecular weight changes), and background pressure. This is a form of "compressibility," but one driven by slow thermochemical processes, not fast acoustics.

The source terms on the right-hand side are themselves determined by the full transport equations for energy and species. For instance, the material derivative of temperature, $DT/Dt$, is governed by the energy equation, which includes terms for heat conduction, [chemical heat release](@entry_id:1122340), and [enthalpy diffusion](@entry_id:1124547). Similarly, the material derivatives of the species mass fractions, $DY_k/Dt$, which determine $DW/Dt$, are governed by the species conservation equations, including terms for species diffusion and [chemical reaction rates](@entry_id:147315)  .

A subtle but important point arises from [multi-component diffusion](@entry_id:1128256). The mass fluxes of individual species, $\mathbf{J}_i$, are typically defined relative to the [mass-averaged velocity](@entry_id:149575) such that their sum is zero, $\sum_i \mathbf{J}_i=0$, ensuring that diffusion is a purely redistributive process that conserves total mass. However, this does not mean diffusion has no effect on the velocity divergence. The contribution to $S$ from compositional changes depends on a weighted sum of species fluxes, for example, $\sum_i R_i (\nabla \cdot \mathbf{J}_i)$, where $R_i$ are the species gas constants. If species with different molecular weights (and thus different $R_i$) diffuse at different rates, the local mean molecular weight changes, causing the gas to expand or contract even if the net diffusive mass flux is zero .

### The Projection Method: Enforcing the Divergence Constraint

Numerically, the velocity and pressure fields are coupled. The momentum equation determines the evolution of velocity, while the [hydrodynamic pressure](@entry_id:1126255) $\pi$ acts as a Lagrange multiplier to enforce the divergence constraint. Projection methods provide a robust and efficient framework for solving this coupled system.

The conceptual basis for this method is a generalization of the **Hodge-Helmholtz decomposition** of a vector field. In its classical form, any sufficiently smooth vector field can be uniquely decomposed into the sum of a curl-free (irrotational) component and a divergence-free (solenoidal) component. For our variable-density system, the idea is adapted: we decompose a provisional velocity field, $\mathbf{u}^*$, into two parts: a field that satisfies our target divergence constraint, $\mathbf{u}^{n+1}$, and a correction term that adjusts the divergence without altering the vorticity .

The method proceeds in two steps at each time advancement from $t^n$ to $t^{n+1}$:

1.  **Prediction Step**: A provisional velocity field, $\mathbf{u}^*$, is computed by solving the momentum equation, typically including advection, diffusion (viscous), and [body force](@entry_id:184443) terms, but *omitting* the [hydrodynamic pressure](@entry_id:1126255) gradient term $\nabla \pi$.
    $$
    \frac{\mathbf{u}^* - \mathbf{u}^n}{\Delta t} = -(\mathbf{u}^n \cdot \nabla)\mathbf{u}^n + \frac{1}{\rho^n}\nabla \cdot \boldsymbol{\tau}^n + \mathbf{g}
    $$
    This provisional field $\mathbf{u}^*$ has the correct vorticity (to the order of the scheme) but does not, in general, satisfy the divergence constraint, i.e., $\nabla \cdot \mathbf{u}^* \neq S^{n+1}$.

2.  **Projection (Correction) Step**: The provisional velocity is corrected to produce the final, divergence-conforming velocity $\mathbf{u}^{n+1}$. The correction is performed by subtracting a pressure-gradient-like term:
    $$
    \mathbf{u}^{n+1} = \mathbf{u}^* - \Delta t \frac{1}{\rho^{n+1}} \nabla \pi^{n+1}
    $$
    To find the unknown pressure field $\pi^{n+1}$, we enforce the divergence constraint $\nabla \cdot \mathbf{u}^{n+1} = S^{n+1}$ by taking the divergence of the correction equation:
    $$
    \nabla \cdot \mathbf{u}^{n+1} = \nabla \cdot \mathbf{u}^* - \nabla \cdot \left( \Delta t \frac{1}{\rho^{n+1}} \nabla \pi^{n+1} \right)
    $$
    Substituting the constraint and rearranging yields an elliptic equation for the hydrodynamic pressure:
    $$
    \nabla \cdot \left( \frac{1}{\rho^{n+1}} \nabla \pi^{n+1} \right) = \frac{1}{\Delta t} \left( \nabla \cdot \mathbf{u}^* - S^{n+1} \right)
    $$
    This is a **variable-coefficient Poisson equation** for $\pi^{n+1}$ . The term $1/\rho^{n+1}$ varies spatially due to temperature and composition gradients, making the [elliptic operator](@entry_id:191407) $\nabla \cdot (\frac{1}{\rho}\nabla(\cdot))$ more complex to solve than the standard Laplacian operator, $\nabla^2(\cdot)$, which arises in the incompressible [projection method](@entry_id:144836) where $\rho$ is constant. Physical boundary conditions on velocity, such as impermeability at a wall ($\mathbf{n} \cdot \mathbf{u} = 0$), translate into Neumann boundary conditions for this pressure equation .

### Implementation and Physical Considerations

#### Operator Splitting for Stiff Chemistry

The governing equations for species and energy involve both [transport processes](@entry_id:177992) (advection and diffusion) and chemical reactions. Chemical kinetics are often "stiff," meaning they occur on timescales much faster than fluid transport. Solving these processes simultaneously with an explicit time-stepping scheme would require prohibitively small time steps dictated by the fastest chemical reaction.

To overcome this, **operator splitting** methods are employed. A particularly effective approach is **Strang splitting**, which achieves second-order accuracy. The evolution over a single time step $\Delta t$ is broken into three sequential sub-steps :
1.  **Reaction Half-Step**: Integrate the reaction ODEs for species and enthalpy for a half time step, $\Delta t/2$. This is done at each grid point independently, with no transport. Crucially, this step is modeled as an **isobaric** (constant pressure) process. As reactions release heat, the density and temperature evolve according to the equation of state to keep $p_0$ constant.
2.  **Transport Full-Step**: Integrate the [advection-diffusion equations](@entry_id:746317) for species, enthalpy, and momentum for a full time step, $\Delta t$. The chemical source terms are turned off during this step. The [projection method](@entry_id:144836) described above is performed as part of this step to compute the velocity field for the full time step.
3.  **Reaction Half-Step**: Integrate the reaction ODEs again for a final half time step, $\Delta t/2$, under the same isobaric assumption.

This symmetric splitting decouples the stiff chemistry from the non-stiff transport, allowing each part to be solved with an appropriate and efficient numerical method.

#### Open vs. Closed Systems: The Evolution of Thermodynamic Pressure

The behavior of the thermodynamic pressure $p_0(t)$ depends on the physical domain configuration.
*   **Open Systems**: For flows in unconfined domains, such as a flame burning in the open atmosphere, the system can freely expand and its pressure will equilibrate with the constant ambient pressure. In this common case, it is appropriate to assume $p_0$ is constant in time, so $dp_0/dt = 0$. The divergence source simplifies to $S = S_{\text{loc}}$, the local thermochemical expansion rate.

*   **Closed Systems**: For flows in a confined domain of fixed volume $V$, such as an [internal combustion engine](@entry_id:200042) cylinder, the situation is different. The total mass is conserved, and the boundaries are impermeable. By the divergence theorem, the integral of the velocity divergence over the entire volume must be zero: $\int_V (\nabla \cdot \mathbf{u}) dV = 0$.
If we were to set $dp_0/dt = 0$, this would imply $\int_V S_{\text{loc}} dV = 0$. However, a process like combustion typically releases heat throughout the volume, causing a net positive local expansion, so $\int_V S_{\text{loc}} dV > 0$. To satisfy the global constraint, the thermodynamic pressure $p_0(t)$ must be allowed to evolve. Its evolution provides a uniform compression effect that counteracts the average local expansion . The governing equation for $p_0(t)$ is found by enforcing the global constraint:
$$
\frac{dp_0}{dt} = p_0(t) \frac{\int_V S_{\text{loc}} dV}{\int_V \frac{1}{\gamma p_0} dV}
$$
where the denominator arises from relating density changes to pressure changes. A common simplification leads to $\frac{dp_0}{dt} \approx (\gamma - 1) \int_V \dot{q}''' dV / V$, relating pressure rise to total heat release. A more precise form, consistent with the divergence constraint, is:
$$
\frac{1}{p_0} \frac{dp_0}{dt} = \frac{\int_V ( \frac{1}{T}\frac{DT}{Dt} + \frac{1}{W}\frac{DW}{Dt} ) dV}{\int_V dV} = \langle S_{\text{loc}} \rangle
$$
where $\langle \cdot \rangle$ denotes a volume average. The divergence source term then becomes $S = S_{\text{loc}} - \langle S_{\text{loc}} \rangle$, ensuring that its [volume integral](@entry_id:265381) is always zero. This evolution of $p_0(t)$ correctly captures the overall pressure rise in a closed, reacting system.