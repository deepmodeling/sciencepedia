## Introduction
In the field of nuclear reactor physics, simulating the behavior of neutrons is paramount for safety and design. The governing equation for this process, the linear Boltzmann transport equation, presents a significant numerical challenge: any viable solution method must simultaneously guarantee the physical law of particle conservation and the mathematical necessity of a non-negative, or positive, particle flux. While simpler schemes like the popular Diamond Difference method can enforce conservation, they often fail to maintain positivity, especially in optically thick materials, leading to unphysical results that can corrupt entire simulations.

This article introduces the Simple Corner Balance (SCB) method, a foundational [spatial discretization](@entry_id:172158) technique designed specifically to overcome this dual challenge. By providing a framework that is both conservative and unconditionally positive, SCB serves as a robust tool for transport calculations. Across the following chapters, this article will provide a comprehensive examination of the method. First, **"Principles and Mechanisms"** will deconstruct the theoretical underpinnings of SCB, deriving its equations from first principles and explaining how it achieves positivity where other methods fail. Next, **"Applications and Interdisciplinary Connections"** will explore its practical use in reactor analysis, its implementation on high-performance computers, and its conceptual links to other areas of computational science. Finally, **"Hands-On Practices"** will offer a series of guided exercises to translate theory into practical coding and analysis skills. We begin by delving into the core principles and mechanisms that define the Simple Corner Balance method.

## Principles and Mechanisms

This chapter delves into the principles and mechanisms of the Simple Corner Balance (SCB) method, a [spatial discretization](@entry_id:172158) scheme for the neutral [particle transport equation](@entry_id:1129402). As established in the introduction, numerical methods for transport must navigate the dual requirements of particle conservation and solution positivity to ensure physical fidelity. We will begin by formalizing the governing equations and the [finite volume](@entry_id:749401) framework, which provides the foundation for conservation. We then explore the challenge of positivity, demonstrating why simpler schemes may fail, before presenting the Simple Corner Balance method as a robust solution.

### The Governing Equation and the Finite Volume Framework

The foundation of our analysis is the steady-state, monoenergetic linear Boltzmann transport equation. After applying the [discrete ordinates](@entry_id:1123828) ($S_N$) approximation, the continuous angular dependence is replaced by a [discrete set](@entry_id:146023) of directions. For a specific direction, or ordinate, $\boldsymbol{\Omega}_m = (\mu_m, \eta_m)$ in two-dimensional Cartesian geometry, the equation for the angular flux $\psi_m(\mathbf{r})$ takes the form :

$$ \boldsymbol{\Omega}_m \cdot \nabla \psi_m(\mathbf{r}) + \Sigma_t(\mathbf{r})\psi_m(\mathbf{r}) = Q_m(\mathbf{r}) $$

Here, $\mathbf{r}=(x,y)$ is the spatial position, $\Sigma_t(\mathbf{r})$ is the total macroscopic cross section, and $Q_m(\mathbf{r})$ is the total source of particles into direction $\boldsymbol{\Omega}_m$. This source term aggregates contributions from external sources and, crucially, from particles scattering from all other directions $\boldsymbol{\Omega}_{m'}$ into direction $\boldsymbol{\Omega}_m$. For isotropic scattering, this in-scattering source is proportional to the scalar flux, $\phi(\mathbf{r}) \approx \sum_{m'} w_{m'} \psi_{m'}(\mathbf{r})$, where $w_{m'}$ are the [angular quadrature](@entry_id:1121013) weights.

To solve this equation numerically, we employ a **finite volume method**. This approach ensures that a fundamental physical law—the conservation of particles—is inherently satisfied by the numerical scheme. The process begins by integrating the transport equation over the volume of a single computational cell, $C_{i,j} = [x_{i-1/2}, x_{i+1/2}] \times [y_{j-1/2}, y_{j+1/2}]$. Applying the divergence theorem to the streaming term, $\boldsymbol{\Omega}_m \cdot \nabla \psi_m = \nabla \cdot (\psi_m \boldsymbol{\Omega}_m)$, transforms the [volume integral](@entry_id:265381) of this term into a [surface integral](@entry_id:275394) over the cell boundary $\partial C_{i,j}$ . This yields the exact [cell balance](@entry_id:747188) equation:

$$ \int_{\partial C_{i,j}} \psi_m (\boldsymbol{\Omega}_m \cdot \mathbf{n}) \,dS + \int_{C_{i,j}} \Sigma_t \psi_m \,dV = \int_{C_{i,j}} Q_m \,dV $$

Each term in this integral balance has a clear physical meaning:
*   **Leakage**: The [surface integral](@entry_id:275394), $\int_{\partial C_{i,j}} \psi_m (\boldsymbol{\Omega}_m \cdot \mathbf{n}) \,dS$, represents the net rate at which particles in direction $\boldsymbol{\Omega}_m$ stream out of the cell, also known as the net leakage. The term $\boldsymbol{\Omega}_m \cdot \mathbf{n}$, where $\mathbf{n}$ is the [outward-pointing normal](@entry_id:753030) vector, determines whether a face contributes to inflow ($\boldsymbol{\Omega}_m \cdot \mathbf{n} < 0$) or outflow ($\boldsymbol{\Omega}_m \cdot \mathbf{n} > 0$).
*   **Removal**: The [volume integral](@entry_id:265381), $\int_{C_{i,j}} \Sigma_t \psi_m \,dV$, represents the total rate of particle removal from direction $\boldsymbol{\Omega}_m$ due to collisions (absorption or scattering) within the cell.
*   **Source**: The [volume integral](@entry_id:265381), $\int_{C_{i,j}} Q_m \,dV$, represents the total rate of particle production into direction $\boldsymbol{\Omega}_m$ from all sources within the cell.

The balance equation states that, for a steady state, `Net Outflow + Removals = Sources`. A numerical method is called **conservative** if its discrete equations are a consistent approximation of this integral balance. This property is non-negotiable for physically meaningful simulations.

### The Imperatives of Positivity and Optical Thickness

While conservation is essential, it is not sufficient. The angular flux, $\psi_m(\mathbf{r})$, represents a particle density in phase space and, as such, must be non-negative. A numerical scheme should guarantee a non-negative (positive) discrete solution whenever the physical sources and boundary inflows are non-negative. This property is known as **positivity**. The failure to preserve positivity has severe consequences :
*   **Unphysical Reaction Rates**: A negative scalar flux can lead to calculated reaction rates (e.g., fission or absorption rates) being negative, which is physically nonsensical.
*   **Corruption of Eigenvalue Problems**: In reactor criticality calculations, the fission source for the next iteration is computed from the current flux distribution. A negative flux produces a negative fission source, which can destabilize or corrupt the [power iteration method](@entry_id:1130049) used to find the multiplication factor, $k_{\text{eff}}$.
*   **Inconsistency with a priori Knowledge**: For streaming-dominated problems (e.g., in near-void regions), the true solution is known to be non-negative. A scheme that produces negative values fails to converge to the correct physical behavior in this important limit.

Achieving both second-order accuracy and unconditional positivity is notoriously difficult for hyperbolic equations like the transport equation. The widely used **Diamond Difference (DD)** scheme, for instance, achieves [second-order accuracy](@entry_id:137876) by assuming the cell-average flux is the arithmetic mean of the face-average fluxes. However, this comes at the cost of positivity.

To understand this failure, we must introduce the concept of **[optical thickness](@entry_id:150612)**. The solution to the transport equation along a characteristic path involves an exponential [attenuation factor](@entry_id:1121239), $\exp(-\Sigma_t s)$, where $s$ is the path length. The exponent, $\Sigma_t s$, is a dimensionless quantity called the [optical thickness](@entry_id:150612). For a cell of width $\Delta x$, the path length a particle travels to cross it in the x-direction is $s_x = \Delta x / |\mu_m|$. The optical thickness along this coordinate direction is therefore :

$$ \tau_x = \Sigma_t s_x = \frac{\Sigma_t \Delta x}{|\mu_m|} $$

Similarly, the optical thickness in the y-direction is $\tau_y = \Sigma_t \Delta y / |\eta_m|$. These parameters measure how opaque the cell is to particles traveling in a specific direction. A high optical thickness implies strong attenuation.

In a simplified 1D slab-geometry problem, the DD scheme's update formula for the outgoing flux $\psi_{i+1/2}$ in terms of the incoming flux $\psi_{i-1/2}$ can be derived as :

$$ \psi_{i+1/2} = \left( \frac{1 - \tau/2}{1 + \tau/2} \right) \psi_{i-1/2} + \frac{\bar{Q} \Delta x / \mu}{1 + \tau/2} $$

where $\tau = \frac{\Sigma_t \Delta x}{\mu}$. For this update to be positive for any non-negative inflow $\psi_{i-1/2}$ and source $\bar{Q}$, the coefficient of $\psi_{i-1/2}$ must be non-negative. This is only true if $\tau \le 2$. When the cell is optically thick ($\tau > 2$), the DD scheme can produce unphysical negative fluxes. This issue is particularly acute for grazing angles of incidence ($\mu \to 0$), where $\tau$ can become very large even for physically thin cells.

### The Simple Corner Balance Method: A Positive Approach

The Simple Corner Balance (SCB) method is designed to be both conservative and unconditionally positive. Its core innovation is to abandon the single cell-average closure of the DD scheme and instead enforce [particle balance](@entry_id:753197) on smaller **subcells**.

In 2D, a rectangular cell is partitioned by its midlines into four rectangular subcells, or quadrants, associated with the four corners: Southwest (SW), Southeast (SE), Northwest (NW), and Northeast (NE). The SCB method solves for the angular flux values at these four corners. The solution proceeds via a **sweep** across the computational mesh, processing cells in an order consistent with the particle direction of travel, $\boldsymbol{\Omega}_m = (\mu_m, \eta_m)$.

The direction of the sweep is determined by the signs of the [direction cosines](@entry_id:170591). For a given cell, the faces through which particles enter are **incoming faces**, and the faces through which they exit are **outgoing faces**. The intersection of the two incoming faces is the **upwind corner**, and the intersection of the two outgoing faces is the **downwind corner**. This classification changes for each of the four angular quadrants :

*   **Quadrant I ($\mu_m > 0, \eta_m > 0$)**: Incoming faces are West and South. Outgoing are East and North. The sweep proceeds from the **Southwest (upwind)** corner to the **Northeast (downwind)** corner.
*   **Quadrant II ($\mu_m < 0, \eta_m > 0$)**: Incoming faces are East and South. Outgoing are West and North. The sweep proceeds from the **Southeast (upwind)** corner to the **Northwest (downwind)** corner.
*   **Quadrant III ($\mu_m < 0, \eta_m < 0$)**: Incoming faces are East and North. Outgoing are West and South. The sweep proceeds from the **Northeast (upwind)** corner to the **Southwest (downwind)** corner.
*   **Quadrant IV ($\mu_m > 0, \eta_m < 0$)**: Incoming faces are West and North. Outgoing are East and South. The sweep proceeds from the **Northwest (upwind)** corner to the **Southeast (downwind)** corner.

Within each cell, the corner fluxes are computed sequentially, following this upwind-to-downwind sweep logic.

### Derivation of the 2D SCB Equations

Let us derive the system of equations for the four corner fluxes ($\psi_m^{\mathrm{SW}}, \psi_m^{\mathrm{SE}}, \psi_m^{\mathrm{NW}}, \psi_m^{\mathrm{NE}}$) for a direction in Quadrant I ($\mu_m > 0, \eta_m > 0$). The SCB method approximates the angular flux as being piecewise-constant within each of the four subcells, with the value equal to the flux at the corresponding corner.

A [particle balance](@entry_id:753197) equation is written for each subcell. Consider the Northeast (NE) subcell, which has dimensions $\frac{\Delta x}{2} \times \frac{\Delta y}{2}$. Its inflow faces are its western boundary (from the NW subcell) and its southern boundary (from the SE subcell). Its outflow faces are the main cell's east and north boundaries. Integrating the transport equation over this subcell and applying the piecewise-constant flux approximation yields a balance equation :

$$ \left( \mu_m \psi_m^{\mathrm{NE}} \frac{\Delta y}{2} + \eta_m \psi_m^{\mathrm{NE}} \frac{\Delta x}{2} \right) + \Sigma_t \psi_m^{\mathrm{NE}} \frac{\Delta x \Delta y}{4} = \left( \mu_m \psi_m^{\mathrm{NW}} \frac{\Delta y}{2} + \eta_m \psi_m^{\mathrm{SE}} \frac{\Delta x}{2} \right) + Q_m \frac{\Delta x \Delta y}{4} $$

The terms on the left represent total outflow and removal from the NE subcell. The terms on the right represent total inflow from the adjacent upwind subcells and the internal source. By deriving analogous equations for the other three subcells, we obtain a system of four [linear equations](@entry_id:151487) for the four corner flux unknowns. Given the known incoming fluxes on the main cell's west and south faces (which provide the inflow for the SW subcell equations), this system can be solved sequentially: first SW, then SE and NW, and finally NE.

This system of subcell balances inherently ensures particle conservation for the entire cell. The positivity of the scheme stems from its connection to the [method of characteristics](@entry_id:177800). Indeed, the formula for the upwind corner flux (e.g., $\psi_{SW}$) can be shown to be a weighted average of the attenuated fluxes arriving from the inflow faces, with weights proportional to the inflow rates through the subcell faces . For the 1D case, this formulation reduces to the exact characteristic solution, which is unconditionally positive .

An alternative, but equivalent, view of SCB involves defining both the corner fluxes and the face-averaged fluxes as unknowns. The method then implicitly assumes a **bilinear flux distribution** within the cell that interpolates the four corner values. Under this assumption, a simple and elegant relationship emerges: the average flux on any face is the arithmetic average of the two corner fluxes adjacent to that face . For example, the average flux on the west face, $\psi_W$, is:

$$ \psi_W = \frac{\psi_{SW} + \psi_{NW}}{2} $$

These closure relations, combined with the overall [cell balance](@entry_id:747188) equation, provide the necessary equations to form a complete, solvable system. The subcell balance formulation is simply a direct and intuitive way to arrive at the same positive and conservative solution.

### Generalization to Three Dimensions

The principles of the Simple Corner Balance method extend directly to three-dimensional Cartesian geometry. For a hexahedral (brick-shaped) cell, the method is formulated as follows :

1.  **Unknowns**: There are $8$ corner flux unknowns and $6$ face-averaged flux unknowns for each discrete ordinate, for a total of $14$ unknowns per cell.

2.  **Subcell Balance**: The cell is partitioned into $8$ [octants](@entry_id:176379), each sharing a vertex at the cell center. The transport equation is integrated over each octant, yielding $8$ octant balance equations. These equations relate the flux at the octant's corner to the fluxes on its three inflow faces (determined by the signs of $\mu, \eta, \xi$).

3.  **Closure Relations**: To close the system, $6$ additional equations are required. These express each of the $6$ face-averaged fluxes as a convex, [bilinear interpolation](@entry_id:170280) of the $4$ corner fluxes lying on that face. The weighting factors in this interpolation depend on the transverse optical thicknesses to ensure positivity.

Summing the $8$ octant balances recovers the exact [particle balance](@entry_id:753197) for the entire cell, confirming that the 3D method is also conservative. The use of characteristic-based, upwinded subcell balances and convex closure relations ensures that the 3D SCB scheme remains unconditionally positive, providing a robust and physically reliable method for complex reactor simulations.