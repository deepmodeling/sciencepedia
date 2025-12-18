## Introduction
The dynamic nature of intertidal zones, where shorelines advance and retreat with the tides, poses a significant challenge for numerical simulation. Accurately capturing these moving boundaries on a fixed computational grid requires specialized techniques that can handle the appearance and disappearance of water without violating fundamental physical laws. This article addresses this problem by providing a comprehensive exploration of [wetting](@entry_id:147044)–drying algorithms, the cornerstone of modern coastal and estuarine modeling. By mastering these methods, modelers can ensure their simulations are stable, accurate, and physically robust.

This article is structured to build a deep, practical understanding of the topic. The first chapter, **Principles and Mechanisms**, dissects the governing Shallow Water Equations and introduces the core numerical principles—mass conservation, the well-balanced property, and [positivity preservation](@entry_id:1129981)—that are essential for any reliable scheme. The second chapter, **Applications and Interdisciplinary Connections**, contextualizes these principles by examining their role in setting up realistic model domains, enhancing physical realism through friction modeling, and rigorously validating model performance. Finally, the **Hands-On Practices** section provides opportunities to engage directly with the key theoretical and computational challenges discussed, solidifying the concepts through practical problem-solving.

## Principles and Mechanisms

The numerical simulation of flows in intertidal zones presents a unique and formidable challenge: the computational domain itself, defined by the wetted area, evolves in time. The governing equations of fluid dynamics must be solved in a region whose boundaries—the shorelines—are in constant motion. Wetting–drying algorithms are the set of numerical principles and mechanisms designed to manage this [moving boundary problem](@entry_id:154637) on a fixed computational grid, ensuring that simulations are stable, accurate, and physically consistent. This chapter delineates these core principles, starting from the governing equations and progressing to the sophisticated numerical strategies required for robust implementation.

### The Governing Equations and Fundamental States

The physical foundation for modeling intertidal flows is the set of **Shallow Water Equations (SWEs)**. These equations are derived from the fundamental laws of mass and [momentum conservation](@entry_id:149964), depth-averaged under the assumption that the horizontal length scales of motion are much greater than the vertical scale (the water depth). For a two-dimensional horizontal domain, a particularly powerful and numerically advantageous formulation of the SWEs is the [conservative form](@entry_id:747710) with bathymetric source terms.

Let $h(x,y,t)$ be the water depth, $\boldsymbol{u}(x,y,t) = (u,v)$ the depth-averaged horizontal velocity vector, and $z_b(x,y)$ the bathymetric elevation relative to a reference datum. The free-surface elevation is given by $\eta(x,y,t) = h(x,y,t) + z_b(x,y)$. The [conservative form](@entry_id:747710) of the SWEs can be written as :

Mass Conservation:
$$ \partial_t h + \partial_x(h u) + \partial_y(h v) = 0 $$

Momentum Conservation ($x$-direction):
$$ \partial_t(h u) + \partial_x \! \left(h u^2 + \frac{1}{2}g h^2 \right) + \partial_y(h u v) = -g h \partial_x z_b - \frac{\tau_{bx}}{\rho} $$

Momentum Conservation ($y$-direction):
$$ \partial_t(h v) + \partial_x(h u v) + \partial_y \! \left(h v^2 + \frac{1}{2}g h^2 \right) = -g h \partial_y z_b - \frac{\tau_{by}}{\rho} $$

Here, $g$ is the acceleration due to gravity, $\rho$ is the constant fluid density, and $\tau_{bx}$ and $\tau_{by}$ are the components of the [bed shear stress](@entry_id:262541), which act as a momentum sink. The terms $\partial_t h$ and $\partial_t(h\boldsymbol{u})$ represent the local rates of change of mass and momentum per unit area. The divergence terms, such as $\partial_x(hu)$, represent the net flux of mass or momentum out of an infinitesimal area. The terms involving $\frac{1}{2} g h^2$ represent the flux of momentum due to the [hydrostatic pressure](@entry_id:141627) force integrated over the water column.

A crucial feature of this formulation is the separation of the pressure gradient into a flux term and a **bathymetric source term** (e.g., $-g h \partial_x z_b$). This specific structure is essential for developing "well-balanced" numerical schemes, a concept we will explore in detail.

The cornerstone of any wetting–drying algorithm is the seemingly simple definition of water depth: $h = \eta - z_b$. However, this relationship is only physically meaningful if $\eta$ and $z_b$ are referenced to the same vertical datum. In practice, free-surface data (from satellites or tide gauges) are often referenced to a [geodetic datum](@entry_id:1125591) like Mean Sea Level (MSL), while bathymetric charts are referenced to a hydrographic datum like Chart Datum (CD). A failure to unify these datums before computing the water depth introduces a systematic error that can render a simulation completely unphysical . For example, if the algorithm mistakenly computes depth using $\eta_{\mathrm{MSL}}$ and $z_{b,\mathrm{CD}}$, the resulting depth will be incorrect by the offset $\Delta$ between the datums. This can cause the model to perceive a deep layer of water where the ground is physically dry, leading to spurious inundation and a violation of mass conservation. The first step in any coastal simulation must therefore be the rigorous transformation of all vertical data to a single, consistent datum.

One of the most important equilibrium states for testing a numerical scheme is the **lake-at-rest** condition . This is a state of no motion ($\boldsymbol{u} = \boldsymbol{0}$) with a perfectly flat free surface ($\eta(x,y) = \text{constant}$). In this scenario, the water depth $h = \eta - z_b$ is non-uniform, mirroring the underlying topography. The governing momentum equations reduce to a perfect balance between the pressure gradient and the bed slope force: $\nabla(\frac{1}{2} g h^2) = -g h \nabla z_b$. A robust numerical scheme must be able to preserve this quiescent state indefinitely, without generating [spurious currents](@entry_id:755255). This "well-balanced" property is a central theme in the design of modern wetting–drying algorithms.

### Numerical Challenges at the Wet-Dry Interface

On a fixed computational grid, the continuous shoreline is replaced by a collection of discrete cells that can be either "wet" or "dry." The transition zone between these states is the source of numerous numerical pathologies.

A fundamental distinction exists between a **geometric criterion** and a **dynamic criterion** for classifying a cell's state . A purely geometric criterion defines a cell as wet if it contains any water, i.e., if the cell-averaged water depth $h > 0$. In contrast, dynamic criteria are implemented for numerical stability. A common dynamic criterion reclassifies cells as "dry" if their depth falls below a small positive threshold, $h  h_{\min}$. This is done to avoid the numerical problems associated with vanishingly thin layers of water. Cells can also be classified as "partially wet" or "numerically thin" to trigger special handling. For example, a cell might be considered partially wet if $0  h \le h_{\min}$ or if the flow becomes supercritical (Froude number $Fr = |\boldsymbol{u}|/\sqrt{gh} > 1$), a condition that can occur in very shallow, fast-moving water.

The need for such dynamic criteria arises from singularities that emerge in the governing equations as $h \to 0$.

First, the stability of [explicit time-stepping](@entry_id:168157) schemes is governed by the **Courant-Friedrichs-Lewy (CFL) condition**, which limits the time step $\Delta t$ based on the fastest signal speed in the domain. For the SWEs, the maximum local signal speed is $|\boldsymbol{u}| + \sqrt{gh}$ . While the gravity wave celerity $\sqrt{gh}$ vanishes as $h \to 0$, the velocity $\boldsymbol{u} = (h\boldsymbol{u})/h$ can become arbitrarily large if a cell has a small, non-zero momentum $h\boldsymbol{u}$ while its depth $h$ approaches zero. This forces the required time step $\Delta t$ to collapse, halting the simulation.

Second, the primitive (non-conservative) form of the momentum equation, which describes the fluid's acceleration $\partial_t \boldsymbol{u}$, contains terms that are divided by $h$. As $h \to 0$, these terms can produce unphysically large accelerations, leading to instability and erroneous velocities . A key goal of [wetting](@entry_id:147044)–drying algorithms is to tame these singularities.

### Core Principles of Robust Numerical Schemes

To overcome these challenges, a robust numerical algorithm for intertidal flows must adhere to a set of fundamental principles. These principles ensure that the discrete model remains a faithful and stable approximation of the underlying physics.

#### Mass Conservation

The continuity equation is a statement of mass conservation. A numerical scheme must preserve this property at the discrete level, especially during the activation and deactivation of cells. **Finite Volume (FV) methods** are exceptionally well-suited for this task . An FV scheme tracks the total mass (or volume) within fixed grid cells (control volumes). The change in mass in one cell is exactly accounted for by the [numerical fluxes](@entry_id:752791) across its faces. Because the flux leaving one cell is identical to the flux entering its neighbor, all internal fluxes cancel when summed over the domain, ensuring that the total mass changes only due to fluxes at the domain's external boundaries. In this framework, a cell wets or dries not because of an ad-hoc rule, but because mass has been physically transported into or out of it by the computed fluxes.

In contrast, more naive approaches, such as a simple Finite Difference (FD) scheme that enforces a dry state by "clipping" a computed negative depth to zero, or activates a cell by "seeding" it with a minimum depth $h_{\min}$, are non-conservative. These operations artificially create or destroy mass, leading to significant errors in the simulation of tidal [prisms](@entry_id:265758) and long-term sea-level change.

#### The Well-Balanced Property

As previously mentioned, the ability of a scheme to exactly preserve the lake-at-rest state is known as the **well-balanced property** (or C-property). This is not merely an academic exercise; it is critical for preventing unphysical flows from developing over complex bathymetry in near-still conditions, such as during slack tide. A scheme that is not well-balanced will generate [spurious oscillations](@entry_id:152404) and currents, polluting the solution.

Achieving a [well-balanced scheme](@entry_id:756693) requires a coupled, or balanced, discretization of the pressure gradient flux and the bathymetric source term . A simple approach where the flux is computed at cell faces and the source term is evaluated at cell centers using a standard finite difference will fail this test. The modern solution to this problem is a technique known as **[hydrostatic reconstruction](@entry_id:750464)** . The key insight is that while the water depth $h$ may be discontinuous across a sharp change in bathymetry, the free surface $\eta$ in a lake-at-rest is constant and therefore smooth. The algorithm first reconstructs the smooth variable $\eta$ to the cell interfaces. Then, it uses this reconstructed free surface and the known bathymetry of the adjacent cells to compute consistent water depth values on both sides of the interface. This method correctly captures the hydrostatic balance at the discrete level and is a cornerstone of robust SWE solvers.

#### Positivity Preservation

The water depth $h$ is a physical quantity that cannot be negative. A numerical scheme must guarantee that if the depth is non-negative at the beginning of a time step, it will remain non-negative at the end. This is the **positivity-preserving property**. Far from being an automatic feature, it requires careful design of the numerical flux and a sufficiently small time step.

For a first-order [finite volume](@entry_id:749401) scheme, it can be shown from first principles that a [sufficient condition](@entry_id:276242) for positivity is that the total volume of water fluxed out of a cell during a time step does not exceed the volume initially in the cell . This leads to a local [time-step constraint](@entry_id:174412) for each cell $i$:
$$ \Delta t \le \frac{\Delta x \, h_{i}^{n}}{\text{Total Outgoing Flux from cell } i} $$
This condition reveals that positivity is fundamentally a "draining time" constraint. Upwind-type [numerical fluxes](@entry_id:752791), which naturally link the outgoing flux from a cell to the state within that cell, are essential for satisfying this property. Furthermore, the [hydrostatic reconstruction](@entry_id:750464) technique contributes to positivity by ensuring that the depths used as input to the flux calculation are themselves non-negative.

### Algorithmic Mechanisms and Strategies

Building on these principles, we can assemble the key mechanisms of a modern [wetting](@entry_id:147044)–drying algorithm, typically implemented within a [finite volume](@entry_id:749401) framework.

#### The Finite Volume Update Cycle

A state-of-the-art FV scheme for the SWEs with [wetting](@entry_id:147044)-drying generally follows a three-step process for each time step :

1.  **Reconstruction:** Starting with cell-averaged values of the [conserved variables](@entry_id:747720) ($h$, $h\boldsymbol{u}$), the scheme reconstructs the state at the left and right sides of each cell interface. As discussed, a well-balanced, positivity-preserving approach involves performing a **[hydrostatic reconstruction](@entry_id:750464)**, where the free surface $\eta$ is reconstructed and used to define non-negative water depths at the interface.

2.  **Riemann Solution (Flux Calculation):** At each interface, the two reconstructed states (left and right) form a local **Riemann problem**. This problem is solved approximately (e.g., using an HLL or HLLC solver) to determine the numerical flux of mass and momentum across the interface. This step is critical as it encodes the wave propagation physics of the SWEs. The solver must incorporate **dry-state logic**: if both sides of an interface are dry, the flux is zero; if one side is wet and the other is dry, a special one-sided flux calculation is needed to model potential inundation correctly.

3.  **Evolution:** The cell-averaged state variables are updated using the computed fluxes in the conservative FV formula. The bathymetric source term is discretized in a way that is tightly coupled with the [hydrostatic reconstruction](@entry_id:750464) and pressure flux calculation to ensure the well-balanced property.

#### Handling Thin Films and Mitigating Instabilities

To address the singularities that arise as $h \to 0$, practical algorithms employ additional mechanisms.

The CFL time-step restriction caused by potentially infinite velocity $\boldsymbol{u}=(h\boldsymbol{u})/h$ is a severe problem. A common and effective mitigation is a **momentum reset policy**, also known as "stilling" . In this approach, a velocity threshold depth, $h_{\text{vel}}$, is defined. In any cell where the computed water depth $h$ falls below this threshold, the velocity is reset to zero ($\boldsymbol{u} = \boldsymbol{0}$, which implies $\boldsymbol{m} = \boldsymbol{0}$). This policy is justified by energy principles: setting the velocity to zero removes kinetic energy from the system ($\Delta E_{kin} \le 0$), acting as a physically plausible dissipation mechanism. It does not spontaneously create energy. By enforcing zero velocity in these numerically [thin films](@entry_id:145310), the problematic $|\boldsymbol{u}|$ term in the CFL condition is eliminated, stabilizing the time step.

An alternative and more complex approach is to use a **[semi-implicit scheme](@entry_id:1131429)** . These schemes treat the terms responsible for fast-moving gravity waves implicitly, removing the $\sqrt{gh}$ term from the CFL constraint. The time step is then limited only by the explicit advection, which is much less restrictive in many coastal applications. However, the challenge of managing momentum in [thin films](@entry_id:145310) still requires careful algorithmic treatment.

#### High-Resolution Shoreline Representation

While classifying entire cells as wet or dry is sufficient for many applications, some problems require a more precise representation of the shoreline's location. Advanced algorithms can achieve this by performing a **sub-cell [interface reconstruction](@entry_id:750733)** . This is often done using a level-set approach. A function $\phi(x,y) = \eta(x,y) - z_b(x,y) = h(x,y)$ is defined. The shoreline is precisely the zero-contour, $\phi = 0$. Within a partially wet cell, a [linear approximation](@entry_id:146101) of $\phi$ can be constructed using the cell-centered value and gradient. The line segment where this linear function equals zero provides a sub-grid approximation of the shoreline's location and orientation. This information can be used for more accurate flux calculations and for visualizing the wet-dry interface with much higher resolution than the grid itself.