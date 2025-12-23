## Introduction
Simulating wave propagation is fundamental to many scientific and engineering fields, from probing the Earth's subsurface in geophysics to [medical ultrasound](@entry_id:270486) imaging. The [acoustic wave equation](@entry_id:746230) provides a powerful mathematical model for these phenomena, but solving it in complex, real-world scenarios requires sophisticated numerical techniques. The finite difference method (FDM) stands out as a robust and widely used approach for this task. However, translating continuous physical laws into a discrete, stable, and accurate computer algorithm presents significant challenges, from handling [material interfaces](@entry_id:751731) to preventing non-physical artifacts. This article provides a comprehensive exploration of [finite difference modeling](@entry_id:749378) for the [acoustic wave equation](@entry_id:746230), guiding you from foundational theory to advanced practical implementation.

To build a complete understanding, we will proceed through three distinct chapters. First, in **Principles and Mechanisms**, we will derive the governing equations and dissect the core finite difference algorithm, analyzing the critical concepts of [numerical stability](@entry_id:146550), accuracy, and dispersion. Next, the **Applications and Interdisciplinary Connections** chapter will bridge theory and practice, addressing how to model realistic sources, receivers, complex geology, and the all-important [absorbing boundary conditions](@entry_id:164672) needed for accurate simulations. Finally, you will have the opportunity to solidify your knowledge through a series of **Hands-On Practices**, applying the concepts to solve tangible computational problems.

## Principles and Mechanisms

This chapter delves into the fundamental principles that govern the propagation of acoustic waves and the core mechanisms underlying their numerical simulation using the [finite difference method](@entry_id:141078). We begin by deriving the governing [partial differential equations](@entry_id:143134) from the physical laws of continuum mechanics. Subsequently, we will explore how these continuous equations are translated into a discrete numerical algorithm, paying close attention to the challenges posed by material heterogeneities. Finally, we will undertake a rigorous analysis of the accuracy and stability of these [numerical schemes](@entry_id:752822), revealing the origins of common artifacts such as [numerical dispersion](@entry_id:145368) and anisotropy, and establishing best practices for obtaining reliable simulation results.

### The Governing Equations of Linear Acoustics

The [propagation of sound](@entry_id:194493) in a fluid is fundamentally a mechanical process described by the principles of mass and momentum conservation. For the purpose of acoustic modeling, we consider small perturbations around a stationary background state. Let $\rho_0(\mathbf{x})$ be the ambient mass density and $P_0$ be the constant ambient pressure. The acoustic wave is characterized by a small pressure perturbation, $p(\mathbf{x}, t)$, and a particle [velocity field](@entry_id:271461), $\mathbf{v}(\mathbf{x}, t)$, which represents the velocity of the fluid parcels oscillating about their equilibrium positions.

The first fundamental principle is the **[conservation of linear momentum](@entry_id:165717)**. In a non-viscous fluid, Newton's second law for a fluid element states that its acceleration is proportional to the net force exerted by the pressure gradient. In linearized form, this is Euler's equation:
$$
\rho_0(\mathbf{x}) \frac{\partial \mathbf{v}(\mathbf{x}, t)}{\partial t} = -\nabla p(\mathbf{x}, t)
$$
Here, we assume that the background density $\rho_0(\mathbf{x})$ can vary spatially, making the medium **heterogeneous**, but is constant in time.

The second principle combines the **[conservation of mass](@entry_id:268004)** with a **linear [equation of state](@entry_id:141675)**. The [equation of state](@entry_id:141675) relates changes in pressure to changes in density. In acoustics, this is captured by the **bulk modulus**, $\kappa(\mathbf{x})$, defined as the ratio of pressure increase to the fractional decrease in volume. A larger bulk modulus signifies a stiffer, less compressible medium. The rate of pressure change is related to the divergence of the velocity field by:
$$
\frac{1}{\kappa(\mathbf{x})} \frac{\partial p(\mathbf{x}, t)}{\partial t} = - \nabla \cdot \mathbf{v}(\mathbf{x}, t)
$$
This equation states that a net flow of particles out of a region ($\nabla \cdot \mathbf{v} > 0$) leads to a local pressure decrease.

These two first-order partial differential equations form a complete system for the pressure $p$ and velocity $\mathbf{v}$. However, it is often convenient to work with a single, second-order equation for the pressure field alone. To derive this, we first take the time derivative of the mass conservation equation and the divergence of the momentum equation:
$$
\frac{1}{\kappa(\mathbf{x})} \frac{\partial^2 p}{\partial t^2} = - \nabla \cdot \left(\frac{\partial \mathbf{v}}{\partial t}\right)
$$
$$
\nabla \cdot \left( \rho_0(\mathbf{x}) \frac{\partial \mathbf{v}}{\partial t} \right) = - \nabla \cdot (\nabla p)
$$
By rearranging the momentum equation to $\frac{\partial \mathbf{v}}{\partial t} = -\frac{1}{\rho_0(\mathbf{x})} \nabla p$ and substituting this into the time-differentiated [mass conservation](@entry_id:204015) equation, we eliminate the velocity variable. This yields the second-order [acoustic wave equation](@entry_id:746230) for a heterogeneous medium :
$$
\frac{1}{\kappa(\mathbf{x})} \frac{\partial^2 p(\mathbf{x}, t)}{\partial t^2} - \nabla \cdot \left( \frac{1}{\rho_0(\mathbf{x})} \nabla p(\mathbf{x}, t) \right) = s(\mathbf{x}, t)
$$
In this final form, we have included a **[source term](@entry_id:269111)**, $s(\mathbf{x}, t)$, which represents the injection of energy into the system, for example, from an earthquake or an ultrasonic transducer. For consistency, we will henceforth drop the subscript from the background density, denoting it simply as $\rho(\mathbf{x})$.

Let us briefly review the physical quantities and their units in the International System (SI):
- **Acoustic Pressure**, $p$: A scalar field representing the deviation from ambient pressure. Measured in Pascals ($\mathrm{Pa}$), where $1 \mathrm{Pa} = 1 \mathrm{N/m^2} = 1 \mathrm{kg \cdot m^{-1} \cdot s^{-2}}$.
- **Mass Density**, $\rho$: A scalar field representing the mass per unit volume of the background medium. Measured in kilograms per cubic meter ($\mathrm{kg \cdot m^{-3}}$).
- **Bulk Modulus**, $\kappa$: A [scalar field](@entry_id:154310) representing the medium's resistance to compression. Like pressure, it is measured in Pascals ($\mathrm{Pa}$).
- **Source Term**, $s$: Represents a rate of volume injection per unit volume, which, upon [dimensional analysis](@entry_id:140259) of the wave equation, has units of inverse seconds squared ($\mathrm{s^{-2}}$).

In a homogeneous medium where $\rho$ and $\kappa$ are constants, the equation simplifies to the classic wave equation:
$$
\frac{1}{c^2} \frac{\partial^2 p}{\partial t^2} - \nabla^2 p = \tilde{s}(\mathbf{x}, t)
$$
Here, $\nabla^2 \equiv \nabla \cdot \nabla$ is the Laplace operator, and $c = \sqrt{\kappa/\rho}$ is the constant **[phase velocity](@entry_id:154045)** of the wave. The form $\nabla \cdot (\frac{1}{\rho} \nabla p)$ is crucial; incorrectly writing this term as $\frac{1}{\rho} \nabla^2 p$ is only valid in a homogeneous medium and leads to significant errors at [material interfaces](@entry_id:751731) where density varies.

### Wave Interaction at Material Interfaces

In many real-world scenarios, such as geophysical exploration or [medical ultrasound](@entry_id:270486), the medium is composed of distinct layers or regions with different material properties. At the interfaces between these regions, where $\rho(\mathbf{x})$ and $\kappa(\mathbf{x})$ are discontinuous, waves are partially reflected and transmitted. The behavior at these interfaces is governed by boundary conditions derived directly from the fundamental conservation laws.

To derive these conditions, we consider an infinitesimally thin "pillbox" volume that straddles an interface $\Sigma$. By applying the integral form of the conservation laws to this volume and taking the limit as its thickness approaches zero, we can deduce the relationships between fields on either side of the interface .
1.  **From Momentum Conservation:** The integral of the momentum equation, $\int_V (\rho \partial_t \mathbf{v} + \nabla p) dV = \mathbf{0}$, balanced over the pillbox implies that in the absence of any singular [surface forces](@entry_id:188034), the pressure must be continuous across the interface. This is a dynamic boundary condition reflecting the balance of forces.
    $$
    [p] = 0 \quad \text{or} \quad p_+ = p_-
    $$
2.  **From Mass Conservation:** Similarly, the integral form of the mass conservation equation, $\int_V (\frac{1}{\kappa} \partial_t p + \nabla \cdot \mathbf{v}) dV = 0$, implies that if the fluid layers remain in contact without gaps or interpenetration, the component of the particle velocity normal to the interface must be continuous. This is a kinematic boundary condition.
    $$
    [v_n] = [\mathbf{v} \cdot \mathbf{n}] = 0 \quad \text{or} \quad v_{n,+} = v_{n,-}
    $$
Here, the bracket notation $[f] = f_+ - f_-$ denotes the jump in a quantity $f$ across the interface, and $\mathbf{n}$ is the [unit normal vector](@entry_id:178851) to the interface.

These two continuity conditions—of pressure and normal particle velocity—are the fundamental [interface conditions](@entry_id:750725) in linear acoustics. They determine the partitioning of [wave energy](@entry_id:164626) into reflected and transmitted components. The degree of [reflection and transmission](@entry_id:156002) is governed by the contrast in **[acoustic impedance](@entry_id:267232)**, $Z$, a material property defined as the product of density and wave speed:
$$
Z = \rho c = \rho \sqrt{\frac{\kappa}{\rho}} = \sqrt{\rho \kappa}
$$
For a [plane wave](@entry_id:263752) normally incident on an interface between two media with impedances $Z_1$ and $Z_2$, applying the continuity conditions for $p$ and $v_n$ yields the pressure reflection coefficient, $R_p$:
$$
R_p = \frac{Z_2 - Z_1}{Z_2 + Z_1}
$$
This simple but powerful result shows that reflections arise from an [impedance mismatch](@entry_id:261346). If the impedances are matched ($Z_1 = Z_2$), there is no reflection, even if the density and wave speed individually differ between the media . The behavior of waves at interfaces can also be elegantly described using **[characteristic variables](@entry_id:747282)** or Riemann invariants, $p \pm Zv$, which represent right- and left-propagating wave components in one dimension.

### Discretization Principles: From Continuous to Discrete

To solve the [acoustic wave equation](@entry_id:746230) on a computer, we must transform the continuous [partial differential equation](@entry_id:141332) into a system of algebraic equations. The finite difference method achieves this by replacing continuous derivatives with approximations computed on a discrete grid of points in space and time.

#### Discretizing the Wave Equation

We define a uniform Cartesian grid with spatial spacing $\Delta x, \Delta y, \Delta z$ and a time step $\Delta t$. A function value $p(i\Delta x, j\Delta y, k\Delta z, n\Delta t)$ is denoted by the discrete variable $p_{i,j,k}^n$.

The second derivatives in the wave equation are typically approximated using a **second-order centered finite difference** stencil. For the one-dimensional case, these are:
$$
\frac{\partial^2 p}{\partial t^2} \approx \frac{p_i^{n+1} - 2p_i^n + p_i^{n-1}}{(\Delta t)^2}
$$
$$
\frac{\partial^2 p}{\partial x^2} \approx \frac{p_{i+1}^n - 2p_i^n + p_{i-1}^n}{(\Delta x)^2}
$$
Substituting these into the homogeneous wave equation $p_{tt} = c^2 p_{xx}$ results in an [explicit time-stepping](@entry_id:168157) formula where the pressure at the next time level, $p_i^{n+1}$, can be calculated directly from values at the current and previous time levels, $p^n$ and $p^{n-1}$. This is a form of the **leapfrog method**.

#### Handling Heterogeneity: Effective Medium Parameters

Discretizing the heterogeneous wave equation, particularly the term $\nabla \cdot (\frac{1}{\rho} \nabla p)$, requires special care at interfaces where $\rho$ is discontinuous. A naive [discretization](@entry_id:145012) can lead to significant accuracy loss. A robust approach is to use a **staggered grid**, where pressure $p$ is defined at cell centers and the components of particle velocity $\mathbf{v}$ are defined at cell faces. This naturally aligns with the physics, as pressure gradients drive fluxes (velocities) across faces.

Consider the 1D term $\frac{\partial}{\partial x}(\frac{1}{\rho} \frac{\partial p}{\partial x})$. We can think of this as the divergence of a flux, $q = -\frac{1}{\rho} \frac{\partial p}{\partial x}$. The principle of flux continuity, derived from the physics, must be honored by the numerical scheme. Let pressure $p_i$ be at cell center $x_i$ and density $\rho_i$ be constant within cell $i$. The interface between cell $i$ and cell $i+1$ is at $x_{i+1/2}$. To compute the flux $q_{i+1/2}$ at this interface, we need an effective value for $1/\rho$. By demanding that the discrete flux correctly relates the [pressure drop](@entry_id:151380) $(p_{i+1} - p_i)$ across the interface, we find that the correct effective parameter is the **arithmetic mean** of the inverse densities, which corresponds to the **harmonic mean** of the densities themselves :
$$
\left(\frac{1}{\rho}\right)_{i+1/2}^{\text{effective}} = \frac{1}{2}\left(\frac{1}{\rho_i} + \frac{1}{\rho_{i+1}}\right) = \frac{\rho_i + \rho_{i+1}}{2\rho_i \rho_{i+1}}
$$
This is equivalent to:
$$
\rho_{i+1/2}^{\text{effective}} = \left( \frac{1}{2}\left(\frac{1}{\rho_i} + \frac{1}{\rho_{i+1}}\right) \right)^{-1} = \frac{2\rho_i \rho_{i+1}}{\rho_i + \rho_{i+1}}
$$
Using this harmonic average for density (or arithmetic average for bulk modulus $\kappa$ in the corresponding term) at interfaces is critical for accurate modeling in [heterogeneous media](@entry_id:750241).

#### Time Integration

The standard second-order [centered difference](@entry_id:635429) scheme for the wave equation is an example of the [leapfrog time integration](@entry_id:751211) method. It is favored for its efficiency and desirable stability properties when applied to wave problems. The semi-discretized acoustic system can be written abstractly as a system of [ordinary differential equations](@entry_id:147024), $\frac{d\mathbf{y}}{dt} = \mathbf{A}\mathbf{y}$, where $\mathbf{y}$ contains all grid values of pressure and velocity, and $\mathbf{A}$ is the [spatial discretization](@entry_id:172158) matrix. For non-dissipative wave systems, the eigenvalues of $\mathbf{A}$ are purely imaginary.

When analyzing [time integrators](@entry_id:756005) for such systems, their stability along the imaginary axis is paramount.
- The **leapfrog method** is conditionally stable. Its stability region includes a segment of the imaginary axis, $[-i, i]$. This means it is stable provided the time step $\Delta t$ is small enough, leading to the famous Courant–Friedrichs–Lewy (CFL) condition.
- In contrast, standard two-stage explicit **Runge-Kutta (RK)** methods (like the explicit midpoint or Heun's method) have [stability regions](@entry_id:166035) that do not include any non-zero portion of the [imaginary axis](@entry_id:262618). They are therefore unconditionally unstable for non-dissipative [wave propagation](@entry_id:144063) and cannot be used .

Furthermore, the leapfrog method is computationally efficient, requiring only one evaluation of the spatial operator per time step, whereas a two-stage RK method would require two. For these reasons of stability and cost, the [leapfrog integrator](@entry_id:143802) is the standard choice for explicit [finite difference modeling](@entry_id:749378) of the [acoustic wave equation](@entry_id:746230).

### The Fidelity of Numerical Solutions: Error and Convergence

A numerical solution is only an approximation. Understanding the nature and behavior of the error is essential for interpreting simulation results.

#### Local Truncation Error vs. Global Error

Two types of error are fundamental:
- **Local Truncation Error (LTE)**: This is the error made in a single time step, assuming the exact solution was known at previous steps. It is the residual that remains when the exact solution is plugged into the finite [difference equation](@entry_id:269892). For a scheme of order $p$ in time and $q$ in space, the LTE is of order $O((\Delta t)^p) + O((\Delta x)^q)$. For our standard centered scheme, $p=2$ and $q=2$.
- **Global Error**: This is the true difference between the numerical solution and the exact solution at a given time, after many steps have been taken and errors have accumulated.

The relationship between these errors is described by the **Lax Equivalence Theorem**: for a consistent linear scheme, stability is the necessary and sufficient condition for convergence. Convergence means the [global error](@entry_id:147874) goes to zero as $\Delta t$ and $\Delta x$ go to zero. More powerfully, for a stable and consistent scheme, the order of the [global error](@entry_id:147874) is the same as the order of the local truncation error, provided the [initial conditions](@entry_id:152863) and boundary conditions are handled with sufficient accuracy . That is, a second-order accurate scheme (LTE is $O((\Delta t)^2, (\Delta x)^2)$) will produce a solution with second-order global error ($O((\Delta t)^2, (\Delta x)^2)$).

#### Numerical Dispersion and Anisotropy

A key source of error in wave simulations is **numerical dispersion**. In the continuous world, the wave speed $c = \sqrt{\kappa/\rho}$ is constant for all frequencies (in a non-[dispersive medium](@entry_id:180771)). However, in the discrete world of the [finite difference](@entry_id:142363) grid, the effective speed of a numerical wave depends on its frequency and its direction of travel relative to the grid.

By substituting a [plane wave solution](@entry_id:181082) into the finite difference scheme, we can derive the **[numerical dispersion relation](@entry_id:752786)**, which relates the numerical frequency $\omega$ to the wavenumber $k$. From this, we find the **numerical phase velocity**, $c_{num}(k) = \omega/k$. For the standard second-order scheme, $c_{num}$ is always less than the true velocity $c$ and decreases as the wavenumber $k$ (and thus frequency) increases. This means shorter wavelengths (higher frequencies) travel slower than longer wavelengths on the grid, causing [wave packets](@entry_id:154698) to spread out and distort artificially.

This phenomenon dictates a practical rule of thumb for grid design: to limit dispersive errors to an acceptable level, one must ensure a sufficient number of grid points per wavelength. For instance, to keep the phase velocity error below 1%, a wave must be sampled by approximately 10 or more grid points per wavelength. This sets an upper limit on the frequencies that can be accurately propagated on a given grid and influences the choice of a source wavelet's peak frequency .

In multiple dimensions, the numerical phase velocity also depends on the angle of propagation relative to the grid axes. This effect is called **[numerical anisotropy](@entry_id:752775)**. For the standard 5-point Laplacian in 2D, waves travel slowest along the grid axes ($\theta=0^\circ, 90^\circ$) and fastest along the diagonals ($\theta=45^\circ$). This can cause an initially circular wavefront to become square-like as it propagates, a purely numerical artifact . Higher-order [finite difference stencils](@entry_id:749381) can be used to mitigate both [numerical dispersion](@entry_id:145368) and anisotropy.

#### The Modified Equation and Pre-asymptotic Behavior

A powerful tool for understanding numerical errors is the **modified equation**. Instead of viewing the finite difference scheme as an approximation to the original PDE, we can ask: what PDE does the scheme solve *exactly*? By performing a Taylor series expansion of the difference scheme, we find that it corresponds to the original PDE plus a series of higher-order derivative terms, which represent the error.

For the standard second-order scheme for $p_{tt}=c^2 p_{xx}$, the modified equation is approximately :
$$
p_{tt} = c^2 p_{xx} + \frac{c^2 (\Delta x)^2}{12}(1 - \lambda^2) p_{xxxx} + \dots
$$
where $\lambda = c\Delta t/\Delta x$ is the Courant number. The leading error term is a fourth-order spatial derivative, which is a dispersive term. This explains numerical dispersion from a differential equation perspective.

This analysis also explains **pre-asymptotic convergence**. While theory predicts [second-order convergence](@entry_id:174649) as $\Delta x \to 0$, on coarse grids where the wavelength is not much larger than $\Delta x$, the error contribution from the $p_{xxxx}$ term can be large and not scale cleanly with $(\Delta x)^2$. This leads to an observed convergence rate that may be lower than 2. Only when the grid becomes fine enough ("asymptotic regime") does the predicted second-order rate manifest clearly.

The modified equation also reveals a special case: if the Courant number $\lambda=1$, the leading dispersive error term vanishes. The scheme becomes much more accurate, a phenomenon known as a "sweet spot" in numerical modeling. This suggests that choosing the time step as large as stability allows can actually improve accuracy by reducing dispersion .

### Practical Considerations in Numerical Simulation

#### The Nyquist Criterion and Temporal Aliasing

When running a simulation, we must distinguish between the time step used for computation, $\Delta t_{sim}$, and the interval at which we save the output, $\Delta t_{out}$. Often, to save disk space, we might only store the wavefield every $M$ steps, so $\Delta t_{out} = M \cdot \Delta t_{sim}$.

This decimation process is a form of sampling, and it is subject to the **Nyquist-Shannon sampling theorem**. The theorem states that to avoid aliasing—the misrepresentation of high frequencies as lower frequencies—the sampling frequency $f_s = 1/\Delta t_{out}$ must be at least twice the maximum frequency present in the signal, $f_{max}$. The frequency $f_{Nyquist} = f_s/2 = 1/(2\Delta t_{out})$ is called the **Nyquist frequency**.

In a simulation, the maximum frequency, $f_{max}$, is determined by the spatial grid resolution and the source spectrum. The simulation itself must be run with a $\Delta t_{sim}$ small enough to satisfy both the stability (CFL) condition and its own Nyquist criterion ($1/(2\Delta t_{sim}) > f_{max}$). However, if we then decimate the output by a large factor $M$, the output Nyquist frequency, $1/(2M\Delta t_{sim})$, may fall below $f_{max}$. When this happens, frequencies in the signal between $f_{Nyquist}$ and $f_{max}$ will be "folded" back into the [frequency spectrum](@entry_id:276824) below $f_{Nyquist}$, corrupting the recorded data. Therefore, the choice of the output sampling interval is critical for avoiding [temporal aliasing](@entry_id:272888) and ensuring the integrity of the final simulation results .