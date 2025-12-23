## Introduction
Simulating multiphase [reacting flows](@entry_id:1130631), such as those in pulverized coal furnaces or liquid-fueled engines, is a critical challenge in modern engineering and science. The complexity arises from the intricate, bidirectional exchange of mass, momentum, and energy between the continuous fluid phase and dispersed particles. Accurately capturing this "[two-way coupling](@entry_id:178809)" is essential for predicting system performance, efficiency, and emissions. This article addresses the challenge by providing a detailed guide to the Particle-Source-in-Cell (PSI-CELL) method, a powerful and widely used Eulerian-Lagrangian approach for modeling these interactions.

Across three comprehensive chapters, this article will build your understanding from the ground up. In **Principles and Mechanisms**, you will learn the fundamental physics of interphase coupling, the conditions under which two-way coupling is dominant, and the core numerical machinery of the PSI-CELL method, including deposition kernels and conservation laws. Next, **Applications and Interdisciplinary Connections** will demonstrate how these principles are applied to model complex phenomena, such as droplet evaporation, soot transport, and [turbulence modulation](@entry_id:756227) in practical engineering systems. Finally, **Hands-On Practices** will offer guided problems to solidify your grasp of key computational procedures, from calculating source terms to implementing [conservative interpolation](@entry_id:747711) schemes.

## Principles and Mechanisms

The accurate simulation of multiphase [reacting flows](@entry_id:1130631), such as those encountered in [spray combustion](@entry_id:1132216) or pulverized coal furnaces, hinges on correctly modeling the intricate interplay between the continuous fluid phase and the dispersed particulate phase. This chapter delves into the fundamental principles and numerical mechanisms governing this interaction, with a focus on the widely adopted Particle-Source-in-Cell (PSI-CELL) methodology for two-way coupling. We will first establish a framework for classifying the intensity of [interphase](@entry_id:157879) coupling and then dissect the PSI-CELL method, from its foundational conservation laws to the specific models for mass, momentum, and energy exchange.

### Regimes of Particle-Fluid Interaction

The nature of the interaction between a carrier fluid and a [dispersed phase](@entry_id:748551) is not monolithic; it varies dramatically with the concentration and properties of the particles. A systematic classification of these interactions is essential for selecting an appropriate and efficient modeling strategy. The coupling regimes are typically categorized as one-way, two-way, or four-way, based on the dominant physical effects .

The key parameters governing these regimes are the **particle volume fraction**, $\epsilon_p$, defined as the volume occupied by particles per unit total volume, and the **[mass loading](@entry_id:751706) ratio**, $\phi_m$, which is the ratio of the total mass of the [dispersed phase](@entry_id:748551) to the mass of the carrier fluid within a representative control volume. While $\phi_m$ quantifies the potential for the particle ensemble to influence the bulk inertia and energy of the fluid, the effect on fluid momentum is more directly assessed by a nondimensional **momentum coupling parameter**, $\Pi$. This parameter is defined as the ratio of the magnitude of the dispersed-phase momentum source per unit volume to a characteristic convective momentum flux of the carrier fluid.

Using these parameters, we can define the coupling regimes as follows:

*   **One-Way Coupling**: This is the most dilute regime, characterized by very low [mass loading](@entry_id:751706) ($\phi_m \ll 1$) and negligible momentum feedback ($\Pi \ll 1$). In this scenario, the fluid significantly affects the motion of the particles (e.g., through drag), but the particles' presence has a negligible effect on the fluid flow. Particle-particle interactions are nonexistent. This regime is typical for simulations involving trace particles or very low concentrations of soot, where particle volume fractions can be on the order of $\epsilon_p \sim 10^{-6}$ .

*   **Two-Way Coupling**: As the particle concentration increases, the collective effect of the [dispersed phase](@entry_id:748551) on the continuous phase becomes significant. This regime is entered when either the [mass loading](@entry_id:751706) becomes substantial ($\phi_m = \mathcal{O}(1)$) or the momentum feedback is no longer negligible ($\Pi = \mathcal{O}(1)$). Here, there is a mutual exchange of mass, momentum, and energy: the fluid affects the particles, and the particles, in turn, affect the fluid. However, the particle volume fraction is still low enough ($\epsilon_p \lesssim 10^{-3}$) that direct particle-[particle collisions](@entry_id:160531) are rare and can be ignored. Spray combustion is a canonical example of two-way coupling, where droplet volume fractions are typically in the range $\epsilon_p \sim 10^{-4} \text{–} 10^{-3}$ but mass loadings can easily be of order unity . The PSI-CELL method is primarily designed to address this regime.

*   **Four-Way Coupling**: In dense flows, a third and fourth mode of interaction becomes important: particle-[particle collisions](@entry_id:160531). The onset of significant collisional effects is primarily determined by the [volume fraction](@entry_id:756566). When $\epsilon_p$ exceeds a threshold, typically around $10^{-3}$, the mean free path between particles becomes short enough that collisions are frequent and significantly influence the [particle dynamics](@entry_id:1129385). This regime, which includes the two-way fluid-particle coupling as well, is termed four-way coupling. Such conditions are often found in dense regions of pulverized coal combustors or fluidized beds, where volume fractions can reach $\epsilon_p \sim 10^{-3} \text{–} 10^{-2}$ or higher . Modeling this regime requires specialized techniques, such as Discrete Element Methods (DEM), to handle the collisional physics.

### The Point-Particle Model and Its Domain of Validity

The PSI-CELL method operates within the Eulerian-Lagrangian framework, where the fluid is described by continuum equations on a fixed (Eulerian) grid, and the individual particles are tracked as discrete entities in a Lagrangian frame. A central assumption in this approach is the **point-particle model**. This model treats each particle as a point in space that carries mass, momentum, and energy but has no spatial extent relative to the grid. All interactions between the particle and the fluid are modeled as localized point sources.

The validity of this approximation is contingent upon a clear [separation of scales](@entry_id:270204). For the PSI-CELL method to yield accurate results, several conditions related to particle size, flow physics, and concentration must be met :

1.  **Particle Size vs. Grid Resolution**: The particle diameter, $d_p$, must be significantly smaller than the smallest resolved fluid scale, which in a simulation is the grid cell size, $\Delta$. If a particle is comparable in size to a grid cell, the flow around it would be partially resolved, and a point-source representation becomes physically inaccurate. A common criterion is $d_p/\Delta \le 0.1$.

2.  **Continuum Assumption**: The standard models for drag and heat/mass transfer used in PSI-CELL are derived assuming the fluid behaves as a continuum. This is valid when the particle Knudsen number, $Kn = \lambda/d_p$ (where $\lambda$ is the gas mean free path), is very small ($Kn \ll 1$).

3.  **Subgrid Wake Effects**: The flow disturbance created by a particle, particularly its wake, must remain a subgrid-scale phenomenon. The particle Reynolds number, $Re_p$, governs the wake structure. For large $Re_p$ (e.g., $Re_p \gtrsim 200$), the wake can become unsteady and large, invalidating the local point-source approximation. Therefore, the application is typically limited to flows where $Re_p \lesssim 100$.

4.  **Dilute Flow Assumption**: As discussed previously, the standard PSI-CELL approach is for two-way coupling. This requires the particle [volume fraction](@entry_id:756566) to be low enough ($\epsilon_p \lesssim 10^{-3}$) to neglect four-way coupling effects.

5.  **Lumped-Capacitance Thermal Model**: When modeling particle heating or cooling, it is often assumed that the particle's internal temperature is uniform. This is valid only if internal thermal resistance is negligible compared to external convective resistance, a condition met when the Biot number is small ($Bi = h d_p / (2 k_s) \ll 0.1$, where $k_s$ is the particle thermal conductivity).

Adherence to these constraints ensures that the point-particle model provides a [faithful representation](@entry_id:144577) of the filtered or averaged effect of the particles on the resolved fluid dynamics.

### Fundamental Principle: Conservation of Momentum

The physical foundation of [two-way coupling](@entry_id:178809) is Newton's Third Law: for every action, there is an equal and opposite reaction. In the context of [particle-fluid interaction](@entry_id:1129376), the total [hydrodynamic force](@entry_id:750449) exerted by the fluid on a particle, $\mathbf{F}_{f \to p}$, is precisely equal in magnitude and opposite in direction to the force exerted by the particle on the fluid, $\mathbf{F}_{p \to f}$.

$$ \mathbf{F}_{p \to f} = -\mathbf{F}_{f \to p} $$

The PSI-CELL method must honor this principle in its discrete formulation to ensure that momentum is conserved for the total system. The source term, $S_{\mathbf{u}}(\mathbf{x},t)$, that appears in the fluid's momentum equation represents the force per unit volume exerted by the particle ensemble on the fluid. It is constructed by distributing the reaction forces from all particles.

A crucial consequence of this principle can be seen by integrating the source term over a control volume $V$. If the numerical scheme is constructed correctly, the total momentum sourced to the fluid within the volume must equal the sum of the reaction forces of all particles, $N_V$, contained within it. This leads to the fundamental conservation identity :

$$ \int_V S_{\mathbf{u}}(\mathbf{x},t) \, \mathrm{d}V = \sum_{p=1}^{N_V} \mathbf{F}_{p \to f}(\mathbf{x}_p, t) = -\sum_{p=1}^{N_V} \mathbf{F}_{f \to p}(\mathbf{x}_p, t) $$

This relationship is a direct result of Newton's Third Law and continuum averaging. Its fulfillment in the discrete numerical scheme is essential for physically consistent simulations. This conservation property holds universally, independent of the specific physical model used for the [hydrodynamic force](@entry_id:750449) $\mathbf{F}_{f \to p}$ (e.g., whether it is linear Stokes drag or a complex nonlinear drag law) .

### Mechanism I: The Deposition Kernel

The translation of discrete particle properties into continuous source fields for the Eulerian equations is the central mechanism of PSI-CELL. This process is known as **scattering** or **deposition**.

A point source from a particle $p$ at position $\mathbf{x}_p$, with a total source strength of $s_{\phi,p}$ for a quantity $\phi$, is mathematically represented by a Dirac [delta function](@entry_id:273429), $s_{\phi,p} \delta(\mathbf{x} - \mathbf{x}_p)$. In a numerical method, the delta function is replaced by a **kernel** or **shape function**, $w(\mathbf{r})$, which is a smooth, spatially-compact function. The source density field $S_{\phi}(\mathbf{x})$ is then constructed as a superposition of these kernel-weighted contributions from all particles :

$$ S_{\phi}(\mathbf{x}) = \sum_{p} w(\mathbf{x} - \mathbf{x}_{p}) \, s_{\phi,p} $$

The kernel $w$ must be normalized such that its integral over all space is unity: $\int_{\mathbb{R}^3} w(\mathbf{r}) \, \mathrm{d}\mathbf{r} = 1$. This normalization is precisely the property that guarantees global conservation of the quantity $\phi$, as shown in the derivation of the momentum [conservation principle](@entry_id:1122907) above  .

The choice of [kernel function](@entry_id:145324) involves a critical trade-off between computational simplicity and numerical accuracy :

*   **Delta-like Kernels**: The simplest approach is the **Nearest-Grid-Point (NGP)** method, which deposits the entire source from a particle into the single grid cell that contains it. This is equivalent to using a sharp, discontinuous kernel. While simple, NGP methods suffer from high **grid-dependence**; as a particle crosses a cell boundary, the source term jumps abruptly, creating significant numerical noise and spurious oscillations in the fluid solution. This is a form of **[aliasing error](@entry_id:637691)**, where high-frequency content from the particle motion is misrepresented on the coarse grid.

*   **Smooth Kernels**: To mitigate these issues, smoother, higher-order kernels are used. These functions (e.g., triangular-shaped clouds, or truncated Gaussians) distribute the source over several neighboring grid cells. By using a smooth function, the source deposition changes continuously as the particle moves, drastically reducing grid-dependence and numerical noise. In Fourier space, a smoother kernel acts as a more effective low-pass filter, attenuating the high-frequency content that leads to [aliasing error](@entry_id:637691). However, if a kernel like a Gaussian is truncated for [computational efficiency](@entry_id:270255), its discrete weights must be renormalized to sum to unity; otherwise, discrete global conservation will be violated .

A final, crucial aspect of the coupling mechanism is **discrete action-reaction symmetry**. For the numerical scheme to conserve energy as well as momentum, the "gathering" step (interpolating fluid properties from the grid to the particle location) must be consistent with the "scattering" step. This is typically achieved by using the exact same [kernel function](@entry_id:145324) (or shape function weights) for both operations. This property, known as adjointness, ensures that the work done by the fluid on the particles is equal and opposite to the work done by the particles on the fluid in the discrete sense  .

### Mechanism II: Modeling Interphase Exchange Sources

With the numerical machinery for deposition established, we now turn to the physics of the exchange processes themselves. The source strengths, $s_{\phi,p}$, must be derived from physical models of the interaction. In a reacting flow, we are concerned with the exchange of mass, momentum, and energy.

The gas-phase governing equations in their conservative form provide the sink for these source terms. For a compressible, multi-component gas, the equations including interphase source terms are :

Conservation of total mass:
$$ \frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{u}) = S_{\rho} $$

Conservation of species $k$ mass:
$$ \frac{\partial (\rho Y_k)}{\partial t} + \nabla \cdot (\rho Y_k \mathbf{u}) = -\nabla \cdot \mathbf{J}_k + \dot{\omega}_k + S_{\rho Y_k} $$

Conservation of momentum:
$$ \frac{\partial (\rho \mathbf{u})}{\partial t} + \nabla \cdot (\rho \mathbf{u} \otimes \mathbf{u} + p\mathbf{I}) = \nabla \cdot \boldsymbol{\tau} + S_{\rho\mathbf{u}} $$

Conservation of total energy:
$$ \frac{\partial (\rho E)}{\partial t} + \nabla \cdot ((\rho E + p) \mathbf{u}) = \nabla \cdot (\boldsymbol{\tau} \cdot \mathbf{u}) - \nabla \cdot \mathbf{q} - \nabla \cdot \left(\sum_{k=1}^{N_s} h_k \mathbf{J}_k\right) + S_{\rho E} $$

Here, $S_{\rho}$, $S_{\rho Y_k}$, $S_{\rho\mathbf{u}}$, and $S_{\rho E}$ are the volumetric source terms for mass, species mass, momentum, and total energy, respectively, which are computed via the PSI-CELL deposition of the corresponding particle source strengths.

#### Momentum Source

The force exerted by the fluid on a particle, $\mathbf{F}_{f \to p}$, is the sum of several contributions. The particle's equation of motion is given by $m_p \frac{d\mathbf{v}_p}{dt} = \sum_i \mathbf{F}_i$. In typical combustion applications, the most important forces are :

*   **Drag Force ($\mathbf{F}_D$)**: Arises from the [relative velocity](@entry_id:178060) between the particle and the fluid. A general form is $\mathbf{F}_D = \frac{1}{2} C_D(Re_p) \rho_g A_p |\mathbf{u} - \mathbf{v}_p| (\mathbf{u} - \mathbf{v}_p)$, where $C_D$ is a drag coefficient dependent on the particle Reynolds number $Re_p$.
*   **Net Gravitational Force ($\mathbf{F}_G$)**: This is the sum of the particle's weight and the buoyant force from the displaced fluid: $\mathbf{F}_G = (\rho_p - \rho_g) V_p \mathbf{g}$.
*   **Thermophoretic Force ($\mathbf{F}_{\text{th}}$)**: In flows with strong temperature gradients, particles are pushed from hotter to colder regions. This force is proportional to $-\nabla T_g / T_g$.

The momentum source deposited to the fluid grid is the reaction to these forces. A critical point is that [body forces](@entry_id:174230) like gravity are already accounted for in the fluid's own momentum equation (via the $\rho_g \mathbf{g}$ term that gives rise to [hydrostatic pressure](@entry_id:141627)). Including the reaction to buoyancy in the PSI-CELL source term would constitute double-counting. Therefore, the momentum source should only include the reaction to **surface interaction forces** like drag and [thermophoresis](@entry_id:152632) . The total momentum source from a particle $p$ is thus $s_{\mathbf{u},p} = -\left( \mathbf{F}_D + \mathbf{F}_{\text{th}} + \dots \right)$. If the particle is also emitting mass (evaporating), the momentum of this emitted mass, $\dot{m}_p \mathbf{u}_{in,p}$, must also be added to the fluid .

As a numerical illustration, consider a single cubic cell of edge length $L_c = 1.0 \times 10^{-2} \text{ m}$ containing three droplets experiencing Stokes drag, $\mathbf{F}_{\text{drag},p} = 3 \pi \mu d_p (\mathbf{u}_f - \mathbf{u}_p)$. The fluid has viscosity $\mu = 8.0 \times 10^{-5} \text{ Pa} \cdot \text{s}$ and velocity $\mathbf{u}_f = (2.0, 0.5, 0.0) \text{ m/s}$. Given the particle properties from the hypothetical scenario in , the reaction force on the fluid from each particle is $\mathbf{F}_{p \to f} = 3 \pi \mu d_p (\mathbf{u}_p - \mathbf{u}_f)$. Summing these forces for all three particles and dividing by the cell volume $V_c = L_c^3 = 1.0 \times 10^{-6} \text{ m}^3$ yields the cell-averaged momentum source term $\mathbf{S}_{\mathbf{u},c}$. Following the calculation, the resulting source vector is $\mathbf{S}_{\mathbf{u},c} = \begin{pmatrix} 7.540 \times 10^{-4} & -1.508 \times 10^{-3} & 1.546 \times 10^{-2} \end{pmatrix} \text{ N/m}^3$.

#### Mass and Species Source

When particles undergo [phase change](@entry_id:147324), such as the evaporation of liquid fuel droplets, they act as a source of mass for the gas phase. The rate of evaporation, $\dot{m}_p$, can be modeled using [film theory](@entry_id:155696). A common approach for quasi-steady, diffusion-limited evaporation relates the mass flux to the gradient of the vapor mass fraction between the droplet surface and the far field . This leads to expressions involving the **Sherwood number ($Sh$)**, which quantifies convective enhancement of mass transfer, and the **Spalding mass transfer number ($B_M$)**, which accounts for the effect of Stefan flow (blowing) at the surface. The [evaporation rate](@entry_id:148562) is given by:

$$ \dot{m}_{p} = \pi d_{p} \rho_{g} D_{g} Sh \ln(1 + B_{M}) $$

where $D_g$ is the vapor diffusivity. The total mass source for the fluid is $S_{\rho} = \sum_p \dot{m}_p$ distributed by the kernel. If the evaporating mass consists of species $k$ with a composition $z_{k,p}$, then the source for species $k$ is $S_{\rho Y_k} = \sum_p \dot{m}_p z_{k,p}$ .

#### Energy Source

The energy exchange is the most complex term, involving multiple pathways. The total energy source strength for the gas from a particle $p$, $s_{E,p}$, can be expressed as the sum of three main components :

1.  **Heat Transfer**: This includes convection and radiation. The convective part is $\dot{Q}_{\text{conv}} = h A_p (T_g - T_p)$, where $h$ is the heat transfer coefficient derived from a Nusselt number ($Nu$) correlation. The gas gains energy at a rate of $-\dot{Q}_{\text{conv}}$.
2.  **Work Done by Interphase Forces**: The force exerted by the particle on the fluid, $\mathbf{F}_{p \to g}$, does work at a rate of $\mathbf{F}_{p \to g} \cdot \mathbf{u}|_{\mathbf{x}_p}$, where $\mathbf{u}|_{\mathbf{x}_p}$ is the local gas velocity at the particle's position. This term represents the [mechanical power](@entry_id:163535) transferred to the fluid.
3.  **Energy of Injected Mass**: When a particle evaporates, the newly created vapor carries its own energy into the gas phase. This is given by $\dot{m}_p (h_{in,p} + \frac{1}{2}|\mathbf{u}_{in,p}|^2)$, where $h_{in,p}$ and $\mathbf{u}_{in,p}$ are the specific enthalpy and velocity of the injected matter. The enthalpy of the vapor, $h_{in,p}$, includes both the sensible enthalpy of the liquid at the surface temperature and the latent heat of vaporization, $L_v$.

Combining these, the total energy source strength from a particle is:

$$ s_{E,p} = h A_p (T_p - T_g) + \mathbf{F}_{p \to g} \cdot \mathbf{u}|_{\mathbf{x}_p} + \dot{m}_p \left( h_{in,p} + \frac{1}{2}|\mathbf{u}_{in,p}|^2 \right) $$

Note that the latent heat of vaporization, $L_v$, is implicitly included in $h_{in,p}$. An alternative and often clearer formulation for an evaporating droplet considers the energy balance explicitly. The gas provides energy to the droplet via convection, $\dot{Q}_{\text{conv}}$, and also provides the latent heat required for evaporation. The source term for the gas is then the sum of the reactions to these processes :

$$ s_{E,p} = - \dot{Q}_{\text{conv}} - \dot{m}_p L_v = h A_p(T_p - T_g) - \dot{m}_p L_v $$

As a concrete example from a hypothetical scenario in , consider a cell containing 150 identical evaporating droplets. By calculating the Reynolds and Nusselt numbers, we find the convective heat transfer rate from the hot gas to a cooler droplet. We also account for the energy sink due to the latent heat of vaporization. Summing these contributions for all particles and dividing by the cell volume gives the total volumetric energy source for the gas phase, calculated to be $S_{E,g} = -3.576 \times 10^5 \text{ W/m}^3$. The negative sign indicates that in this case, the gas is losing energy to heat up and evaporate the droplets, a common scenario in [spray combustion](@entry_id:1132216).

### Algorithmic Implementation

In a computational code, the PSI-CELL coupling procedure is executed at each time step. The overall algorithm can be summarized as follows:

1.  **Gather**: For each particle, interpolate the required fluid properties (e.g., velocity, temperature, density) from the surrounding Eulerian grid cells to the particle's location. This is typically done using the same kernel weights as in the deposition step.
2.  **Calculate Exchange**: Using the interpolated [fluid properties](@entry_id:200256) and the particle's own state, calculate the interphase exchange rates: the forces ($\mathbf{F}_{f \to p}$), the heat transfer rate ($\dot{Q}$), and the mass transfer rate ($\dot{m}_p$).
3.  **Update Particles**: Integrate the Lagrangian equations of motion for each particle over the time step to update its velocity, position, temperature, and mass.
4.  **Calculate Source Reactions**: Determine the reaction sources to be applied to the fluid. For example, the momentum source is $-\mathbf{F}_{f \to p}$ and the energy source follows the models described above.
5.  **Scatter**: Deposit these particle source strengths onto the Eulerian grid cells using the chosen deposition kernel, accumulating the contributions from all particles into the cell-based source term arrays ($S_{\rho}$, $S_{\rho\mathbf{u}}$, etc.).
6.  **Update Fluid**: Solve the discretized Eulerian [conservation equations](@entry_id:1122898) for the fluid, including the now-known source terms, to advance the fluid state over the time step.

For efficiency in large simulations with millions of particles, it is computationally prohibitive to search through all particles for each grid cell. Instead, a "particle list per cell" [data structure](@entry_id:634264) is employed. At the beginning of each time step, particles are binned into their host cells, allowing the gathering and scattering loops to operate on local data, which dramatically improves performance, especially in [parallel computing](@entry_id:139241) environments .