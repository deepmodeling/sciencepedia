## Introduction
Accurately representing the complex, sloping bathymetry of the ocean floor is a fundamental challenge in computational oceanography. While geopotential coordinate systems, or [z-level grids](@entry_id:1134166), offer simplicity in the governing equations, their most basic implementation results in a crude "staircase" approximation of the seafloor. This simplification introduces significant [numerical errors](@entry_id:635587), most notably in the calculation of the horizontal pressure gradient force, which can generate spurious currents and corrupt model simulations. This article explores a sophisticated solution to this problem: the use of [z-level grids](@entry_id:1134166) with [partial bottom cells](@entry_id:1129363) (PBC). This technique provides a highly accurate representation of bathymetry while retaining the advantages of a fixed, horizontal grid structure.

This article will guide you through the theory and practice of this powerful method. The first chapter, **"Principles and Mechanisms,"** delves into the core concepts, explaining how [partial bottom cells](@entry_id:1129363) are defined, why they drastically reduce pressure gradient errors, and how they are implemented within a conservative finite-volume framework. We will also address the critical numerical stability challenges that arise from thin cells and the robust solutions developed to overcome them. Next, the chapter on **"Applications and Interdisciplinary Connections"** will demonstrate the method's impact on simulating real-world ocean dynamics, from boundary layer processes to large-scale circulation and its use in coastal and climate science. Finally, **"Hands-On Practices"** provides a set of targeted exercises to reinforce these concepts, moving from foundational geometric calculations to a full numerical experiment comparing different grid representations. We begin by examining the foundational principles that make [partial bottom cells](@entry_id:1129363) a cornerstone of modern ocean modeling.

## Principles and Mechanisms

### The Representation of Bathymetry in Z-Level Models

Ocean [general circulation models](@entry_id:1125562) commonly employ [vertical coordinate systems](@entry_id:1133787) to discretize the water column. One of the most conceptually straightforward is the **geopotential coordinate system**, often referred to as a **z-level grid**. In this system, coordinate surfaces are surfaces of constant geopotential height, which are, for practical purposes, horizontal and fixed in space. This choice offers significant advantages, particularly in the simplicity of the governing equations, as the coordinate surfaces do not tilt or move with the underlying bathymetry or the time-varying free surface.

However, this simplicity comes with a challenge: representing the complex, sloping bathymetry of the ocean floor. The most basic approach is the **staircase representation**, sometimes called a "full-cell" or "full-step" method. In this scheme, each grid cell is designated as either entirely "wet" (fluid) or entirely "dry" (land), based on whether the cell's geometric boundaries lie above or below the true bathymetry. This forces the model's representation of the seabed into a series of discrete steps, which can be a crude approximation of the actual, continuous seafloor.

A more sophisticated and accurate approach is the use of **[partial bottom cells](@entry_id:1129363) (PBC)**, also known as shaved cells. This method retains the fixed, horizontal nature of the z-level grid for all interior layers but allows the bottom-most wet cell in any given water column to be geometrically truncated by the true bathymetry. This creates a "partial" cell whose thickness is less than or equal to the nominal layer thickness. The principles governing this approach ensure an exact representation of the total water column depth . For a column with a true depth of $H(x,y)$ and a grid with nominal layer thickness $\Delta z_{\mathrm{full}}$, the number of full-thickness cells is $N_{\mathrm{full}} = \lfloor H(x,y) / \Delta z_{\mathrm{full}} \rfloor$. These full cells occupy the upper part of the water column. The thickness of the partial bottom cell, $\Delta z_b$, is then set to the residual depth required to match the true depth:

$$
\Delta z_b(x,y) = H(x,y) - N_{\mathrm{full}} \Delta z_{\mathrm{full}}
$$

By construction, this ensures that the sum of all layer thicknesses in the column precisely equals the true depth $H(x,y)$, and that the partial cell's thickness is bounded: $0 \le \Delta z_b(x,y)  \Delta z_{\mathrm{full}}$. This stands in stark contrast to the staircase method, where the modeled depth is quantized to integer multiples of $\Delta z_{\mathrm{full}}$, introducing a significant geometric error.

### The Principal Advantage: Mitigation of Pressure Gradient Force Errors

The primary motivation for employing [partial bottom cells](@entry_id:1129363) is the substantial reduction of numerical errors in the calculation of the **horizontal pressure [gradient force](@entry_id:166847) (PGF)**. In a hydrostatic fluid, the pressure $p$ at any depth is determined by the weight of the water column above it. The horizontal PGF, which drives ocean currents, is given by $-(1/\rho_0) \nabla_h p$, where $\rho_0$ is a reference density and $\nabla_h p$ is the pressure gradient on a horizontal surface.

In a discrete $z$-level model, the PGF term is typically calculated using a finite difference of pressure between adjacent water columns at the same fixed vertical level $k$ . The pressure itself is computed by summing the contributions of density from all layers above:

$$
p_i(z_k) \approx g \sum_{m=1}^{k-1} \rho_{i,m} \Delta z_{i,m} + \dots
$$

With a staircase representation of bathymetry, a significant problem arises. Consider a sloping bottom where isopycnals (surfaces of constant density) also slope, roughly following the topography. At a "step" in the staircase, a grid cell on the shallower side may be designated as dry "land," while the adjacent cell at the same vertical level is wet "ocean." When the model attempts to compute the pressure gradient across this interface, it must invent a pressure value for the dry cell, often by extrapolating from a nearby fluid cell. This artificial condition generates a large, non-physical pressure gradient, known as a **[spurious pressure gradient](@entry_id:1132231) error**. This numerical artifact can drive [spurious currents](@entry_id:755255) that flow along isobaths, contaminating the model solution.

Partial bottom cells dramatically mitigate this error. By representing the bathymetry with much greater fidelity, the large, artificial vertical walls of the staircase are replaced by much smaller steps or are eliminated altogether over gentle slopes. The calculation of hydrostatic pressure becomes more accurate, as the volume of fluid in the bottom-most cell is correctly accounted for. Consequently, the computed pressure difference between adjacent columns is a much better approximation of the true physical pressure gradient, and the spurious component of the PGF is significantly reduced .

The magnitude of this improvement can be quantified. The leading-order truncation error of the PGF in a staircase model is found to be proportional to the local topographic slope. Defining a non-dimensional slope parameter $r \equiv |\nabla H|/(2\Delta z)$, where $|\nabla H|$ is the change in bottom depth per horizontal grid cell and $\Delta z$ is the vertical grid spacing, the PGF error in a staircase model scales linearly with this parameter, i.e., as $O(r)$. The use of [partial bottom cells](@entry_id:1129363), under the assumption of a smoothly stratified fluid, cancels this first-order error term. The remaining residual error scales with the square of the slope, i.e., as $O(r^2)$ . For the typically small slopes encountered in many ocean regions, this reduction from a first-order to a second-order error is a profound improvement in accuracy.

This advantage is particularly noteworthy when compared to the primary alternative for handling bathymetry: **[terrain-following coordinates](@entry_id:1132950)** (often called **[sigma coordinates](@entry_id:1131617)**). In a sigma-coordinate system, the vertical coordinate surfaces are stretched to fit the bathymetry and the free surface. While this perfectly represents the bottom boundary, it introduces non-orthogonality into the coordinate system. The governing equations become more complex, containing metric terms that relate derivatives in the transformed coordinates to derivatives in physical space. Over steep topography, the discretization of these metric terms in the PGF calculation can lead to its own severe pressure gradient errors, often larger than those in a simple staircase z-level model  . Therefore, the z-level grid with [partial bottom cells](@entry_id:1129363) offers a compelling balance: it retains the simplicity and orthogonality of geopotential coordinates while achieving a highly accurate representation of bathymetry and a significant reduction in PGF errors.

### Numerical Implementation: A Finite-Volume Perspective

Implementing [partial bottom cells](@entry_id:1129363) correctly requires careful adherence to the principles of finite-volume discretization to ensure the conservation of mass, momentum, and tracers. This is typically done on a staggered grid, such as the **Arakawa C-grid**, where scalar variables like temperature and salinity (tracers, $T$) are located at the center of a grid cell, while velocity components are located on the cell faces ($u$ on east-west faces, $v$ on north-south faces). In the vertical, a **Lorenz staggering** is common, placing horizontal velocities at layer centers ($k$) and vertical velocity ($w$) at the interfaces between layers ($k \pm 1/2$) .

#### Conservation and Flux Formulation

The foundation of the numerical scheme is the [tracer conservation equation](@entry_id:1133277) in its integral, or flux, form. For a passive tracer $T$, the rate of change of the total tracer content within a control volume (a grid cell) is equal to the net flux across its boundaries. For a layer $k$ with thickness $h_k$, the layer-integrated tracer content is $h_k T_k$. The update equation takes the form :

$$
\frac{\partial (h_k T_k)}{\partial t} = -(\text{Horizontal Flux Divergence}) - (\text{Vertical Flux Divergence})
$$

When applying this to a partial bottom cell of thickness $h_b = f \Delta z$, the term on the left-hand side naturally uses the true, partial thickness $h_b$. The horizontal [flux divergence](@entry_id:1125154) terms also implicitly depend on $h_b$, as they involve layer-integrated transports. Crucially, the vertical fluxes at the interfaces (e.g., $F_{N-1/2}$ at the top of the cell) are *not* scaled by the partial fraction $f$. A flux leaving the cell above must equal the flux entering the cell below to ensure conservation. Any artificial scaling of the flux at the interface would create or destroy tracer. The resulting tendency of the tracer concentration, $\partial_t T_b$, is obtained by dividing the total flux divergence by the cell thickness $h_b$. This correctly captures the physical effect that a given flux into a smaller volume causes a larger change in concentration .

#### Masks and Geometric Factors

To translate the flux-form equation into a working algorithm on the staggered grid, we must define masks and geometric factors that respect the partial cell geometry.

A **wet/dry mask** is used to determine where computations should occur. A tracer cell $(i,j,k)$ is considered wet if its volume is non-zero, which corresponds to its partial wet fraction $f(k,i,j)$ being greater than zero. The mask for a tracer cell, $m_T$, is thus $1$ if $f > 0$ and $0$ otherwise. The volume of the cell is $V_T(k,i,j) = A_h(i,j) f(k,i,j) \Delta z_k$, where $A_h$ is the horizontal area .

The masks for velocity points on the cell faces follow a fundamental principle: a flux between two cells is only possible if both cells contain fluid. This translates to a logical `AND` operation. For instance, the mask for a $u$-velocity point at interface $(i+1/2, j, k)$ is the product of the masks of the adjacent tracer cells: $m_U(i+1/2,j,k) = m_T(i,j,k) \cdot m_T(i+1,j,k)$ . This rule elegantly handles all boundary conditions. At the solid seabed, the cell below the partial bottom cell is dry, so its mask is zero. The `AND` rule automatically sets the mask for the vertical velocity, $w$, at the seafloor to zero, naturally enforcing the no-normal-flow boundary condition ($w=0$) .

The areas of the faces through which fluxes pass must also account for the partial cell geometry. For a horizontal flux between two cells, the effective open area is limited by the shallower of the two. The wetted height of a $u$-face connecting cells $(i,j,k)$ and $(i+1,j,k)$ is therefore given by the minimum of their respective wetted thicknesses. The fractional open height of the face is $f_U(k,i+1/2,j) = \min(f(k,i,j), f(k,i+1,j))$, and the face area is $A_U = \Delta y \cdot f_U \cdot \Delta z_k$  . This `min` operator is geometrically intuitive and robustly prevents flux into or out of a dry region.

### Practical Challenges and Solutions

While [partial bottom cells](@entry_id:1129363) solve the problem of PGF errors, their implementation introduces a new numerical challenge related to stability.

#### The Thin Cell Problem and Numerical Stability

The very feature that makes PBCs accurate—their ability to conform to bathymetry—means that the thickness of the bottom cell, $h_b$, can become arbitrarily small. As seen in the [tracer conservation equation](@entry_id:1133277), the explicit time-update for a cell's concentration is scaled by the inverse of its thickness, $1/h_b$. For a very thin cell, this factor becomes very large, amplifying the effect of fluxes and potentially leading to numerical instability unless the time step, $\Delta t$, is made correspondingly small .

This is formalized by stability criteria like the Courant-Friedrichs-Lewy (CFL) condition. For explicit vertical advection with velocity $w$, stability and monotonicity for a [first-order upwind scheme](@entry_id:749417) require the Courant number to be bounded:

$$
C = \frac{w \Delta t}{h_b} \le 1
$$

For explicit vertical diffusion with diffusivity $K$, the constraint is even more severe, scaling with the square of the cell thickness:

$$
\Delta t \le \frac{h_b^2}{2K}
$$

As $h_b$ approaches zero, the maximum allowable time step for a stable integration also approaches zero, rendering the model computationally infeasible. For instance, a bottom cell of thickness $h_b=0.3$ m with a typical vertical diffusivity of $K=5 \times 10^{-5}$ m$^2$/s would limit the explicit time step to a maximum of 900 seconds, a constraint often driven by diffusion rather than advection due to the quadratic dependence on $h_b$ .

#### The Solution: Cell Merging with a Thickness Floor

To overcome this stability limitation, a pragmatic engineering solution is employed: a thin partial bottom cell is not allowed to exist. This is achieved by defining a **minimum thickness floor**, $h_{\min}$, and merging any cell thinner than this floor with the cell immediately above it .

The value for $h_{\min}$ is derived directly from the most restrictive stability criterion, which is typically diffusion. Rearranging the diffusion stability limit gives a minimum allowable thickness for a given time step $\Delta t$: $h_{\min} = \sqrt{2 K \Delta t}$. A safety factor $s \ge 1$ is often included for robustness:

$$
h_{\min} = s \sqrt{2 K \Delta t}
$$

If the computed bottom cell thickness $h_b$ is found to be less than $h_{\min}$, it is merged with the cell above, which has thickness $h_a$. The merging procedure must conserve the total mass, momentum, and tracer content of the two original cells. The new, merged cell has a thickness $h_a' = h_a + h_b$. To conserve the tracer inventory ($c \cdot h$) and layer-integrated momentum ($\rho_0 u \cdot h$), the properties of the new cell become a thickness-weighted average of the original properties:

$$
c_a' = \frac{c_a h_a + c_b h_b}{h_a + h_b}, \qquad u_a' = \frac{u_a h_a + u_b h_b}{h_a + h_b}
$$

This strategy of setting a thickness floor and applying a conservative merging scheme provides a robust and physically consistent method to prevent the numerical stability problems associated with very thin cells, allowing the model to benefit from the accuracy of the partial bottom cell approach without suffering from its potential computational cost.