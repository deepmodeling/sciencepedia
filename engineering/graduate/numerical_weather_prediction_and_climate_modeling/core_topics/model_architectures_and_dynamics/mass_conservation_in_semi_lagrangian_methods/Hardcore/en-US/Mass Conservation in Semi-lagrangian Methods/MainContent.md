## Introduction
The semi-Lagrangian (SL) method is a powerful numerical technique for simulating the transport of scalars in a fluid flow, prized in atmospheric and climate modeling for its exceptional stability. By tracing fluid motion backward in time, it allows for large time steps that would be impossible with traditional Eulerian schemes, dramatically improving computational efficiency. However, this stability comes with a significant trade-off: standard SL schemes are inherently non-conservative, meaning they can spuriously create or destroy the total mass of the quantity being transported. This article addresses this critical knowledge gap, explaining the root causes of this non-conservation and exploring the advanced techniques developed to overcome it.

Over the next three chapters, you will gain a comprehensive understanding of this crucial topic. The "Principles and Mechanisms" chapter will deconstruct the SL method to reveal why interpolation leads to [mass loss](@entry_id:188886) and how [compressible flow](@entry_id:156141) complicates the issue, before introducing the fundamentally different approach of conservative remapping. Following this, the "Applications and Interdisciplinary Connections" chapter will demonstrate why [exact mass](@entry_id:199728) conservation is not just an academic concern but a practical necessity for robust climate projections, [carbon cycle modeling](@entry_id:202941), and simulations in fields beyond atmospheric science. Finally, the "Hands-On Practices" section will provide concrete exercises to solidify your understanding of both the problem and its solution, allowing you to calculate mass conservation errors and apply the principles of [conservative schemes](@entry_id:747715).

## Principles and Mechanisms

### The Semi-Lagrangian Method: Stability Through Characteristics

The numerical simulation of advection, the process by which scalars are transported by a flow, is a cornerstone of atmospheric and climate modeling. A powerful and widely used class of methods for this task is the **semi-Lagrangian (SL) method**. As detailed in the previous chapter, SL schemes offer a significant advantage in terms of computational stability, allowing for much larger time steps than are permissible with traditional Eulerian [advection schemes](@entry_id:1120842). To understand the principles of mass conservation in this context, we must first revisit the fundamental mechanism of the SL update.

Consider a passive [scalar field](@entry_id:154310), such as a pollutant [mixing ratio](@entry_id:1127970), denoted by $q(\mathbf{x}, t)$, which is transported by a velocity field $\mathbf{u}(\mathbf{x}, t)$. If the scalar is materially conserved, its evolution is governed by the advective form of the transport equation:
$$
\frac{\partial q}{\partial t} + \mathbf{u} \cdot \nabla q = 0
$$
This equation is equivalent to the statement that the material derivative, $Dq/Dt$, is zero. This means that the value of $q$ remains constant along the trajectory, or **characteristic curve**, of a fluid parcel. A characteristic curve $\mathbf{x}(t)$ is defined by the ordinary differential equation $d\mathbf{x}/dt = \mathbf{u}(\mathbf{x}(t), t)$.

The semi-Lagrangian method is a direct numerical discretization of this physical principle. To find the value of the scalar $q$ at a fixed Eulerian grid point $\mathbf{x}_i$ (the **arrival point**) at a future time $t^{n+1}$, the method traces the characteristic curve backward in time over one time step, $\Delta t = t^{n+1} - t^n$. This integration identifies the **departure point** $\mathbf{x}_d$, which is the location of the fluid parcel at the previous time $t^n$. The departure point is found by solving:
$$
\mathbf{x}_d = \mathbf{x}_i - \int_{t^n}^{t^{n+1}} \mathbf{u}(\mathbf{x}(\tau), \tau) d\tau
$$
where $\mathbf{x}(t^{n+1}) = \mathbf{x}_i$. Since $q$ is constant along this trajectory, the exact solution is $q(\mathbf{x}_i, t^{n+1}) = q(\mathbf{x}_d, t^n)$. The numerical scheme approximates this by interpolating the known [scalar field](@entry_id:154310) at time $t^n$, which is defined on the discrete grid, to the generally off-grid location of the departure point. If we denote the interpolation operator by $\mathcal{I}$, the update is:
$$
q^{n+1}(\mathbf{x}_i) \approx \mathcal{I}[q^n](\mathbf{x}_d)
$$
This procedure is pointwise consistent with the governing equation . The key to the method's stability lies in this alignment of the numerical algorithm with the physical transport path. Unlike explicit Eulerian schemes, whose [numerical domain of dependence](@entry_id:163312) is fixed by the grid stencil, the SL method actively seeks out the physical [domain of dependence](@entry_id:136381) (the departure point), regardless of how far it is from the arrival point. This allows the time step $\Delta t$ to be chosen based on accuracy considerations rather than the Courant–Friedrichs–Lewy (CFL) stability condition, which limits how far information can travel across the grid in a single time step .

### The Paradox of Pointwise Accuracy: Why Semi-Lagrangian Schemes are Not Conservative

While the semi-Lagrangian method is celebrated for its stability, the standard formulation described above suffers from a significant drawback: it does not, by itself, conserve the total mass of the advected scalar. This apparent paradox—a method that is highly accurate pointwise yet fails to conserve an integrated quantity—is central to understanding the need for more advanced formulations.

Mass conservation is fundamentally connected to the **[flux form](@entry_id:273811)** of the continuity equation. For a density-like scalar $p(\mathbf{x}, t)$, the conservation law is written as:
$$
\frac{\partial p}{\partial t} + \nabla \cdot (p \mathbf{u}) = 0
$$
Integrating this equation over a fixed domain $\Omega$ and applying the divergence theorem yields $\frac{d}{dt} \int_{\Omega} p \, dV = -\oint_{\partial \Omega} p \mathbf{u} \cdot d\mathbf{S}$. For a closed or periodic domain, the boundary flux is zero, and the total mass, $M = \int_{\Omega} p \, dV$, is conserved.

Numerical methods that are explicitly built to discretize this flux-form equation, such as **finite-volume (FV) methods**, are inherently conservative. An FV method updates the average value in a grid cell by calculating the net flux of the quantity across the cell's boundaries. When summed over the entire domain, the fluxes across all interior cell faces cancel out in a telescoping sum, guaranteeing that the discrete total mass is conserved to machine precision .

The standard semi-Lagrangian method, in contrast, is based on the advective form of the transport equation. It updates point values, not cell-integrated averages. The root cause of its non-conservation is the **interpolation step** . When we compute the new field at time $t^{n+1}$ by evaluating an interpolant at the set of departure points, the integral of the new field is not guaranteed to equal the integral of the old field. Mathematically, for a discrete total mass approximated by a sum over grid points, $\sum_i q(\mathbf{x}_i) \Delta V_i$, the following inequality generally holds:
$$
\sum_i \mathcal{I}[q^n](\mathbf{x}_{d,i}) \Delta V_i \neq \sum_i q^n(\mathbf{x}_i) \Delta V_i
$$
This is true regardless of the order or quality of the interpolation scheme (e.g., linear, cubic, [spline](@entry_id:636691)) and holds even for [divergence-free](@entry_id:190991) flows where the continuous integral is conserved . Conservation is only achieved in trivial cases, such as the advection of a spatially uniform field .

### The Added Complexity of Compressible Flow

In atmospheric modeling, flows are generally compressible, meaning the density $\rho$ can change. The physically conserved quantity is not the mixing ratio $q$ (a concentration per unit mass of air) but the tracer mass density, $\rho q$. Its evolution is governed by its own flux-form continuity equation:
$$
\frac{\partial (\rho q)}{\partial t} + \nabla \cdot (\rho q \mathbf{u}) = 0
$$
A naive application of the semi-Lagrangian method to this problem would involve transporting the [mixing ratio](@entry_id:1127970) $q$ and the air density $\rho$ separately. The mixing ratio $q$ is materially conserved ($Dq/Dt = 0$), so a standard SL update seems appropriate. The density $\rho$, however, evolves according to $D\rho/Dt = -\rho \nabla \cdot \mathbf{u}$ along a characteristic. A semi-Lagrangian update for density would take the form:
$$
\rho^{n+1}(\mathbf{x}_i) \approx \rho^n(\mathbf{x}_d) \exp\left(-\int_{t^n}^{t^{n+1}} \nabla \cdot \mathbf{u} \, d\tau\right)
$$
. Even if both $q$ and $\rho$ are updated with their correct characteristic-based formulas, the product of the updated fields, $\rho^{n+1} q^{n+1}$, will not conserve the total tracer mass $M_q = \int_{\Omega} \rho q \, dV$. The separate, uncoordinated interpolation of two different fields breaks the fundamental link between them that is necessary for conserving their product .

To understand this link more deeply, we must examine the deformation of fluid volumes. Let $\mathbf{x}^{n+1} = \Phi_n^{n+1}(\mathbf{x}^n)$ be the [flow map](@entry_id:276199) that takes a particle from its position $\mathbf{x}^n$ at time $t^n$ to its position $\mathbf{x}^{n+1}$ at time $t^{n+1}$. The local change in volume is described by the **Jacobian determinant** of this map, $J = \det(\nabla_{\mathbf{x}^n} \mathbf{x}^{n+1})$. The evolution of this determinant along a characteristic is given by Liouville's theorem:
$$
\frac{dJ}{dt} = J (\nabla \cdot \mathbf{u})
$$
Comparing this to the evolution of density, $d\rho/dt = -\rho (\nabla \cdot \mathbf{u})$, we find that the product $\rho J$ is constant along a characteristic. This is a profound statement of mass conservation for an infinitesimal fluid parcel: its mass $\delta m = \rho \delta V$ is constant. Since its volume evolves as $\delta V(t) = J(t) \delta V(t^n)$, it must be that $\rho(t) J(t) = \rho(t^n) J(t^n)$. Since $J(t^n) = 1$, we have $\rho(t) J(t) = \rho(t^n)$. At the end of the time step, this gives the exact pointwise relation:
$$
\rho^{n+1}(\mathbf{x}^{n+1}) = \frac{\rho^n(\mathbf{x}^n)}{J(\mathbf{x}^n)}
$$
. This mechanism, which explicitly links the change in density to the geometric deformation of the flow, is precisely what is missing in standard pointwise SL schemes. For a [divergence-free flow](@entry_id:748605), $\nabla \cdot \mathbf{u} = 0$, the Jacobian is unity, and density is constant along a characteristic, but even then, the interpolation step in the SL scheme for $q$ still prevents conservation of $\int q \, dV$.

### The Solution: Conservative Remapping

The remedy for the conservation problem is to reformulate the semi-Lagrangian method from a finite-volume perspective. These schemes, known as **conservative semi-Lagrangian (CSL)**, **cell-integrated semi-Lagrangian (CISL)**, or **flux-form semi-Lagrangian (FFSL)** methods, are designed to be conservative by construction.

The guiding principle is a direct application of the Reynolds [transport theorem](@entry_id:176504). The mass contained within a fixed Eulerian arrival cell $V_i$ at time $t^{n+1}$ must be identical to the mass that was contained in its corresponding Lagrangian departure volume $D_i$ at time $t^n$. The departure volume $D_i$ is the set of all points that the flow maps into $V_i$ over the time step. This gives the exact integral relation:
$$
\int_{V_i} (\rho q)^{n+1} dV = \int_{D_i} (\rho q)^n dV
$$
A [conservative remapping](@entry_id:1122917) scheme is a numerical algorithm that honors this equation. The procedure involves several steps  :

1.  **Reconstruction:** From the known cell-averaged mass values $\{(\overline{\rho q})_j^n\}$ at time $t^n$, a continuous or piecewise-continuous representation of the mass field, $\mathcal{R}[(\rho q)^n]$, is reconstructed over the entire domain. This reconstruction must be locally conservative, meaning the integral of the reconstructed profile over each cell $V_j$ must equal the original cell-averaged mass. Methods like the **Piecewise Parabolic Method (PPM)** are designed for this, and their [monotonicity-preserving limiters](@entry_id:1128141) are carefully constructed to maintain this integral property .

2.  **Departure Volume Calculation:** The geometric shape of the departure volume $D_i$ is determined by tracing the boundaries (faces, edges, vertices) of the arrival cell $V_i$ backward in time. Having uniquely defined trajectories for cell boundaries is crucial. Staggered grids, such as the Arakawa C-grid where velocities are stored on cell faces, are particularly well-suited for this, as they provide a non-ambiguous velocity to define the motion of the boundaries that separate mass cells .

3.  **Remapping (Overlap Integration):** The new mass in cell $V_i$ is computed by integrating the reconstructed field from step 1 over the departure volume from step 2:
    $$
    M_i^{n+1} = \int_{D_i} \mathcal{R}[(\rho q)^n](\mathbf{x}) dV
    $$
    In practice, this integral is computed by summing the mass contributions from all the old grid cells $V_j$ that overlap with the departure volume $D_i$. If the reconstructed field is piecewise constant, with value $(\overline{\rho q})_j^n$ in cell $V_j$, the update simplifies to:
    $$
    M_i^{n+1} = \sum_j \text{Vol}(D_i \cap V_j) \cdot (\overline{\rho q})_j^n
    $$
    This is a weighted sum where the weights are the intersection volumes of the departure region with the source grid cells.

Because the set of all departure volumes $\{D_i\}$ forms an exact, non-overlapping partition of the entire domain $\Omega$, the sum of the new cell masses is guaranteed to equal the total mass at the previous step:
$$
\sum_i M_i^{n+1} = \sum_i \int_{D_i} \mathcal{R}[(\rho q)^n] dV = \int_{\bigcup_i D_i} \mathcal{R}[(\rho q)^n] dV = \int_{\Omega} \mathcal{R}[(\rho q)^n] dV = \sum_j M_j^n
$$
This demonstrates that [conservative remapping](@entry_id:1122917) is mass-conservative by construction.

### Practical Considerations: Operator Splitting and Mass Fixers

In comprehensive numerical models, advection is just one of many processes. Physical parameterizations, such as those for radiation, [cloud microphysics](@entry_id:1122517), or chemical reactions, introduce source and sink terms, $S$. A common modeling strategy is **operator splitting**, where the dynamics (advection) and physics are handled in sequential steps. This practical choice, however, can break mass conservation.

Consider a scheme where a physics increment is first applied pointwise to the mixing ratio, $q^* = q^n + \Delta t S$, and then this intermediate field $q^*$ is advected using a semi-Lagrangian scheme . This approach is flawed for two reasons. First, if the subsequent advection step is a standard non-conservative SL scheme, mass is lost. Second, even if a conservative remapping scheme is used, applying the source term on the fixed Eulerian grid before advection is physically inconsistent. The source term should act on the fluid parcel as it moves along its trajectory. The split procedure effectively applies the source at one location and then advects a fluid parcel from a different location to take its place. A truly **split-conservative** remedy requires integrating the source term in a Lagrangian frame, accumulating the mass source within the departure volumes before the remapping step is performed .

Given the complexity of fully [conservative schemes](@entry_id:747715), some models employ a more pragmatic approach: they use an efficient, non-conservative SL [advection scheme](@entry_id:1120841) and then apply an *a posteriori* **mass fixer**. This procedure calculates the global mass imbalance $\Delta M$ at the end of a time step and then adds a correction $\delta_i$ to each grid column's mass $m_i$ such that $\sum_i \delta_i = -\Delta M$.

A desirable mass fixer should be minimally intrusive. A common approach is to find the set of corrections $\{\delta_i\}$ that minimizes a [quadratic penalty function](@entry_id:170825), such as one penalizing the relative mass change:
$$
J(\delta) = \sum_{i=1}^N \frac{\delta_i^2}{m_i}
$$
Using the method of Lagrange multipliers, one can show that minimizing this functional subject to the global conservation constraint yields corrections that are proportional to the local mass:
$$
\delta_i = -\Delta M \frac{m_i}{\sum_j m_j}
$$
This strategy, known as proportional rescaling, intuitively applies larger corrections to columns with more mass, thereby minimizing the relative perturbation to the mass field. For example, if a three-cell domain with masses $m_1 = 11000$, $m_2 = 9000$, and $m_3 = 10000 \, \text{kg} \, \text{m}^{-2}$ has a total mass surplus of $\Delta M = 30 \, \text{kg} \, \text{m}^{-2}$, this fixer would remove mass proportionally, yielding corrections of $\delta_1 = -11$, $\delta_2 = -9$, and $\delta_3 = -10 \, \text{kg} \, \text{m}^{-2}$ . While effective and simple, mass fixers are a correction for a known model deficiency, whereas conservative remapping schemes are an attempt to eliminate the deficiency from first principles.