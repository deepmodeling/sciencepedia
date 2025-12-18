## Introduction
How do we predict the path of a plastic bottle in the ocean, the dispersal of larvae between marine habitats, or the spread of an atmospheric pollutant? These questions, fundamental to countless problems in science and engineering, are all concerned with transport—the motion of matter through a fluid. While fluid flows are often described from a fixed (Eulerian) perspective, where we know the velocity at every point in space, understanding transport requires us to adopt the perspective of the moving object itself—the Lagrangian frame of reference. Bridging this gap between the [fixed field](@entry_id:155430) and the moving particle is the central challenge and purpose of Lagrangian [particle tracking](@entry_id:190741) and [trajectory analysis](@entry_id:756092).

This article provides a graduate-level guide to this powerful methodology, navigating from foundational theory to practical application. It addresses the knowledge gap between knowing a velocity field and extracting meaningful information about transport, dispersion, and flow structure. Across three comprehensive chapters, you will gain a robust understanding of this indispensable technique.

The first chapter, **Principles and Mechanisms**, lays the theoretical groundwork. We will explore the mathematical relationship between the Eulerian and Lagrangian frames, delve into the physics governing both ideal and inertial particle motion, and critically examine the numerical methods—from [time-stepping schemes](@entry_id:755998) to [spatial interpolation](@entry_id:1132043)—required for accurate and stable [trajectory integration](@entry_id:756093).

In the second chapter, **Applications and Interdisciplinary Connections**, we will see these principles in action. This section showcases the versatility of the Lagrangian viewpoint, with applications ranging from quantifying oceanic connectivity and Stokes drift to modeling multiphase flows in engineering, chemical transport in the atmosphere, and even large-deformation mechanics.

Finally, **Hands-On Practices** offers the opportunity to apply this knowledge through guided computational exercises. These problems are designed to build practical skills in implementing core algorithms and analytical techniques, solidifying your understanding of the concepts discussed. By the end of this journey, you will be equipped to use Lagrangian analysis to uncover the hidden dynamics of complex fluid systems.

## Principles and Mechanisms

Lagrangian [particle tracking](@entry_id:190741) is fundamentally concerned with solving the [initial value problem](@entry_id:142753) for a particle's [position vector](@entry_id:168381) $\mathbf{x}(t)$, which is governed by the [ordinary differential equation](@entry_id:168621) (ODE):

$$
\frac{d\mathbf{x}}{dt} = \mathbf{u}(\mathbf{x}(t), t)
$$

Here, $\mathbf{u}(\mathbf{x}, t)$ is a given Eulerian velocity field, representing the velocity of the fluid at a fixed point in space $\mathbf{x}$ and time $t$. The solution to this equation, $\mathbf{x}(t)$, is the Lagrangian trajectory—the path a massless, ideal tracer particle follows through the fluid. While this equation appears simple, its solution and interpretation in the context of complex oceanic flows involve a rich interplay of physical principles, computational methods, and advanced [mathematical analysis](@entry_id:139664). This chapter will systematically unpack these core principles and mechanisms.

### From Eulerian Fields to Lagrangian Trajectories

In fluid dynamics, we are often presented with data or model outputs in an **Eulerian frame of reference**, where properties like velocity, temperature, or salinity are described as fields at fixed locations in space. However, to understand transport and dispersion, we must adopt the **Lagrangian frame of reference**, which follows the motion of individual fluid parcels. The crucial link between these two perspectives is the **material derivative**, denoted $\frac{\mathrm{D}}{\mathrm{D}t}$.

The material derivative represents the total rate of change of a property experienced by a moving fluid parcel. For a [scalar field](@entry_id:154310), such as tracer concentration $C(\mathbf{x}, t)$, the [material derivative](@entry_id:266939) is the [total time derivative](@entry_id:172646) of $C$ evaluated along a Lagrangian trajectory $\mathbf{x}(t)$. By applying the [multivariable chain rule](@entry_id:146671), we can express this in terms of Eulerian quantities:

$$
\frac{\mathrm{D}C}{\mathrm{D}t} = \frac{\partial C}{\partial t} + \frac{\partial C}{\partial x_1}\frac{dx_1}{dt} + \frac{\partial C}{\partial x_2}\frac{dx_2}{dt} + \dots = \frac{\partial C}{\partial t} + \mathbf{u} \cdot \nabla C
$$

The first term, $\frac{\partial C}{\partial t}$, is the **local rate of change** at a fixed point. The second term, $\mathbf{u} \cdot \nabla C$, is the **advective rate of change**, representing the change in the property due to the parcel's movement into a region with a different background value.

This relationship becomes more complex when working in non-Cartesian [coordinate systems](@entry_id:149266), which are essential in oceanography. For instance, consider a tracer field $C(\lambda, \phi, t)$ on the surface of a spherical Earth of radius $a$, where $\lambda$ is longitude and $\phi$ is latitude. The physical velocity components are the eastward speed $u$ and northward speed $v$. To find the [material derivative](@entry_id:266939), we must relate these physical speeds to the rates of change of the angular coordinates, $\frac{d\lambda}{dt}$ and $\frac{d\phi}{dt}$. The infinitesimal arc length in the eastward direction is $a\cos\phi\,d\lambda$, and in the northward direction is $a\,d\phi$. Therefore, the velocities are given by $u = a\cos\phi \frac{d\lambda}{dt}$ and $v = a \frac{d\phi}{dt}$. Substituting the resulting expressions for $\frac{d\lambda}{dt}$ and $\frac{d\phi}{dt}$ into the [chain rule](@entry_id:147422) expansion gives the [material derivative](@entry_id:266939) in [spherical coordinates](@entry_id:146054) :

$$
\frac{\mathrm{D}C}{\mathrm{D}t} = \frac{\partial C}{\partial t} + \frac{u}{a\cos\phi}\frac{\partial C}{\partial \lambda} + \frac{v}{a}\frac{\partial C}{\partial \phi}
$$

The factors $\frac{1}{a\cos\phi}$ and $\frac{1}{a}$ are metric terms that correctly convert the angular gradients of $C$ into physical gradients, ensuring [dimensional consistency](@entry_id:271193). This example underscores the necessity of correctly handling coordinate system geometry when translating between Eulerian and Lagrangian frames.

### The Physics of Particle Motion

The fundamental kinematic equation $\frac{d\mathbf{x}}{dt} = \mathbf{u}(\mathbf{x}, t)$ describes the motion of an idealized tracer—a particle that is neutrally buoyant and has no inertia, effectively behaving as a fluid parcel itself.

#### The Ideal Tracer and the Role of Rotation

A common point of confusion in geophysical fluid dynamics is the role of the Coriolis force in Lagrangian particle motion. Since the fluid momentum equations solved in the Earth's [co-rotating frame](@entry_id:146008) explicitly include the Coriolis acceleration term, $-2\boldsymbol{\Omega} \times \mathbf{u}$ (where $\boldsymbol{\Omega}$ is the Earth's angular velocity vector), one might expect this term to appear in the particle's [equation of motion](@entry_id:264286). However, for an ideal tracer, this is not the case.

The key insight is that the Coriolis force is a dynamic [forcing term](@entry_id:165986) that shapes the fluid velocity field $\mathbf{u}(\mathbf{x}, t)$ itself. It is a primary driver of phenomena like [geostrophic currents](@entry_id:1125618) and inertial oscillations. When we solve the fluid momentum equations, we obtain a velocity field $\mathbf{u}$ in which the effects of rotation are already fully embedded. An ideal tracer, by definition, has the same density as the fluid and moves perfectly with it. Its motion is purely kinematic; it simply follows the pre-calculated velocity field. Therefore, the governing equation for an ideal tracer in the [co-rotating frame](@entry_id:146008) remains the simple kinematic statement :

$$
\frac{d\mathbf{x}}{dt} = \mathbf{u}(\mathbf{x}, t)
$$

There is no need to add an explicit Coriolis term to this equation, as doing so would be double-counting its effect. The particle's trajectory will naturally exhibit features of a rotating flow (such as inertial circles or movement along geostrophic contours) because those features are inherent to the structure of $\mathbf{u}$.

#### Inertial Particles and Slip Velocity

Many particles of interest in oceanography—such as sediment grains, [microplastics](@entry_id:202870), or certain types of plankton—are not ideal tracers. They may have a density $\rho_p$ different from the fluid density $\rho_f$ or have finite size, giving them inertia. Such particles do not perfectly follow fluid [pathlines](@entry_id:261720). Their deviation from the fluid flow is quantified by the **slip velocity**, $\mathbf{w} \equiv \mathbf{v}_p - \mathbf{u}$, where $\mathbf{v}_p$ is the particle's velocity.

The motion of a small, rigid, spherical inertial particle is described by the **Maxey-Riley-Gatignol equation**. A simplified version, which nonetheless captures the essential physics, can be derived by applying Newton's second law and accounting for the dominant forces :
1.  **Buoyancy-corrected Gravity**: The net [gravitational force](@entry_id:175476) on a submerged particle is $(m_p - m_f)\mathbf{g}$, where $m_p$ and $m_f$ are the masses of the particle and the displaced fluid, respectively.
2.  **Stokes Drag**: For low Reynolds number slip, the [viscous drag](@entry_id:271349) force is proportional to the slip velocity, $\mathbf{F}_D \propto -(\mathbf{v}_p - \mathbf{u})$.
3.  **Pressure Gradient Force**: An ambient pressure gradient in the fluid exerts a force on the particle, equal to $m_f \frac{\mathrm{D}\mathbf{u}}{\mathrm{D}t}$.
4.  **Added Mass**: As the particle accelerates relative to the fluid, it must also move some of the surrounding fluid. This effect is modeled as an "added mass" force, $\mathbf{F}_A = \frac{1}{2}m_f (\frac{\mathrm{D}\mathbf{u}}{\mathrm{D}t} - \frac{d\mathbf{v}_p}{dt})$.

Combining these forces leads to an equation for the particle's acceleration. In the important asymptotic limit where the particle's response time $\tau$ is very small compared to the timescales of the flow, the particle's velocity remains close to the fluid's velocity. In this regime, we can derive an explicit expression for the leading-order slip velocity. The particle velocity is approximated as :

$$
\mathbf{v}_p \approx \mathbf{u} + \tau (1 - \beta)\left(\mathbf{g} - \frac{\mathrm{D}\mathbf{u}}{\mathrm{D}t}\right)
$$

Here, $\tau$ is the particle response time (which depends on particle size, density, and fluid viscosity), and $\beta = \frac{3\rho_f}{2\rho_p + \rho_f}$ is a dimensionless coefficient. This equation elegantly reveals the primary mechanisms causing particle slip:
-   **Gravitational Settling/Rising**: The term proportional to $\mathbf{g}$ causes denser particles ($\rho_p > \rho_f \implies 1-\beta > 0$) to sink relative to the fluid and lighter particles ($\rho_p < \rho_f \implies 1-\beta < 0$) to rise.
-   **Inertial Ejection**: The term proportional to $-\frac{\mathrm{D}\mathbf{u}}{\mathrm{D}t}$ shows that particles are "ejected" from regions of high fluid acceleration. For instance, a dense particle in a fluid parcel that is accelerating upward will tend to lag behind, creating a downward slip velocity relative to the accelerating fluid.

### Computational Implementation of Trajectory Integration

Moving from theoretical equations to practical computation requires discretizing the governing ODEs in both time and space. The choice of numerical methods at this stage is critical, as it can introduce errors that may be misinterpreted as physical phenomena.

#### Temporal Discretization and Numerical Stability

To solve $\frac{d\mathbf{x}}{dt} = \mathbf{u}(\mathbf{x}, t)$, we use a [numerical time-stepping](@entry_id:1128999) scheme to advance the solution from $\mathbf{x}_n$ at time $t_n$ to $\mathbf{x}_{n+1}$ at time $t_{n+1} = t_n + \Delta t$. Common choices include the explicit Forward Euler method, the implicit Backward Euler method, and [higher-order schemes](@entry_id:150564) like the classical fourth-order Runge-Kutta (RK4).

The properties of these schemes can be examined using a simple, yet insightful, test case: two-dimensional [solid-body rotation](@entry_id:191086), where $\mathbf{u} = (-\Omega y, \Omega x)$. In this flow, ideal particles travel in perfect circles, preserving their distance from the origin. A good numerical scheme should replicate this behavior. Analyzing the performance of different schemes on this problem reveals their fundamental characteristics :
-   **Forward Euler**: This simple [explicit scheme](@entry_id:1124773) is always unstable for purely oscillatory systems. It causes the particle to spiral outwards, artificially amplifying its distance from the origin and violating the conservation of this key invariant.
-   **Backward Euler**: This implicit scheme is [unconditionally stable](@entry_id:146281) but is also dissipative. It causes the particle to spiral inwards, artificially damping its energy.
-   **Trapezoidal Rule (Crank-Nicolson)**: This second-order implicit scheme is unique among the common simple methods in that it exactly preserves the norm for this [rotational flow](@entry_id:276737). It belongs to a class of **symplectic integrators** that are designed to conserve geometric properties of Hamiltonian systems, making them excellent choices for long-term integrations of non-dissipative flows.
-   **Classical RK4**: This widely used [explicit scheme](@entry_id:1124773) is much more accurate than Forward Euler but still has a finite stability limit. For a given rotation rate $\Omega$, if the time step $\Delta t$ is too large (specifically, if $\Omega \Delta t > 2\sqrt{2}$), the scheme will become unstable and amplify the norm. Within its stability range, it is slightly dissipative.

This analysis demonstrates that numerical artifacts can easily be mistaken for physical dispersion or convergence. Careful selection of a time-stepping scheme, often favoring higher-order methods like RK4 or specialized conservative methods, is paramount for accurate Lagrangian simulations.

#### Spatial Discretization and Mass Conservation

In most ocean models, the velocity field $\mathbf{u}$ is not known analytically but is provided on a discrete grid. To integrate a particle's trajectory, one must interpolate the velocity from the grid points to the particle's arbitrary position $\mathbf{x}(t)$. The choice of interpolation scheme is just as critical as the time-stepping scheme.

A key physical property of oceanic flows over large scales is that they are approximately non-divergent, meaning $\nabla \cdot \mathbf{u} \approx 0$. This implies that the area of a patch of fluid is conserved as it is advected. If the interpolation scheme does not preserve this non-divergent property, it can create artificial sources and sinks in the velocity field, leading to spurious clustering or dispersion of particles.

Consider a velocity field given on a staggered Arakawa C-grid, where the zonal ($u$) and meridional ($v$) velocity components are located on the faces of grid cells. Suppose the discrete velocity data exactly satisfy a finite-volume non-divergence condition. We seek an interpolation method that creates a continuous velocity field that is also pointwise non-divergent within each cell. A comparison of methods reveals important differences :
-   **Component-wise Bilinear Interpolation**: A naive approach is to treat $u$ and $v$ as independent [scalar fields](@entry_id:151443) and interpolate each using a standard bilinear scheme. This method generally does not yield a non-divergent continuous field, even if the discrete data are non-divergent.
-   **Face-to-Face Linear Interpolation**: A simple and effective method is to interpolate $u$ linearly only in the x-direction between the two vertical faces of a cell, and interpolate $v$ linearly only in the y-direction between the horizontal faces. This construction results in a continuous velocity field that has a constant divergence within the cell, and this constant is exactly equal to the discrete divergence, which is zero by assumption. Thus, this method is locally non-divergent.
-   **Streamfunction-based Reconstruction**: For two-dimensional non-divergent flow, we can always define a [streamfunction](@entry_id:1132499) $\psi$ such that $u = \frac{\partial\psi}{\partial y}$ and $v = -\frac{\partial\psi}{\partial x}$. By construction, any velocity field derived from a streamfunction is automatically non-divergent ($\frac{\partial u}{\partial x} + \frac{\partial v}{\partial y} = \frac{\partial^2\psi}{\partial x \partial y} - \frac{\partial^2\psi}{\partial y \partial x} = 0$). One can construct values of $\psi$ at the corners of a grid cell consistent with the face-centered velocities, and then use [bilinear interpolation](@entry_id:170280) for $\psi$ within the cell. The resulting velocity field is guaranteed to be non-divergent everywhere.

This highlights the importance of choosing interpolation schemes that respect the physical conservation laws of the underlying flow.

### Stochastic Modeling of Subgrid-Scale Processes

Ocean velocity fields are turbulent across a vast range of scales. Any gridded velocity field inevitably represents a smoothed version of reality, omitting the effects of smaller, unresolved "subgrid-scale" eddies. To create more realistic simulations, these unresolved motions can be parameterized as a stochastic (random) component in the particle's [equation of motion](@entry_id:264286), which then becomes a Stochastic Differential Equation (SDE).

A common form for such an SDE is:
$$
d\mathbf{X}_t = \mathbf{a}(\mathbf{X}_t) dt + \mathbf{B}(\mathbf{X}_t) d\mathbf{W}_t
$$
where $\mathbf{a}$ is the resolved mean velocity, $\mathbf{B}$ is a matrix controlling the intensity of the noise, and $d\mathbf{W}_t$ represents the increments of a Wiener process (the formal representation of "white noise"). A crucial subtlety arises in how the [stochastic integral](@entry_id:195087) is interpreted. There are two main conventions:
-   The **Itô integral** is defined by evaluating the integrand $\mathbf{B}$ at the beginning of each time increment. It possesses convenient mathematical properties (e.g., the Itô integral of a non-anticipating function has [zero mean](@entry_id:271600)), but it does not obey the classical chain rule of calculus.
-   The **Stratonovich integral** is defined using the midpoint of the time increment. It obeys the ordinary chain rule, and importantly, it is often the correct interpretation when an SDE is derived as the white-noise limit of a more physical process with temporally correlated (colored) noise.

A Stratonovich SDE, written as $d\mathbf{X} = \mathbf{a}\,dt + \mathbf{B} \circ d\mathbf{W}_t$, can be converted to an equivalent Itô SDE. The Itô form will contain an additional deterministic term known as the **drift correction** or "spurious drift". This term arises because the correlation between the random forcing and the [state-dependent noise](@entry_id:204817) amplitude, which is implicitly handled in the Stratonovich midpoint evaluation, must be made explicit in the Itô left-point evaluation. By Taylor-expanding the midpoint evaluation, one can derive this correction term from first principles . The $i$-th component of the Itô SDE becomes:
$$
dX_i = \left( a_i + \frac{1}{2} \sum_{j,k} B_{kj} \frac{\partial B_{ij}}{\partial x_k} \right) dt + \sum_j B_{ij} dW_j
$$
The term $\frac{1}{2} \sum_{j,k} B_{kj} \frac{\partial B_{ij}}{\partial x_k}$ is the drift correction. It is non-zero only if the noise is **multiplicative** (i.e., $\mathbf{B}$ depends on $\mathbf{X}$) and spatially inhomogeneous. For example, if the noise intensity increases with distance from the origin, this correction term can manifest as a systematic drift away from the origin, a purely mathematical artifact of the Itô representation that corresponds to a real physical tendency in the underlying colored-noise process.

### Analysis of Trajectories and Dispersion

After computing an ensemble of Lagrangian trajectories, the next step is to analyze them to extract meaningful [physical information](@entry_id:152556) about transport and mixing.

#### Single-Particle and Absolute Dispersion

One of the most fundamental analyses is to study the statistics of an ensemble of particles released from the same location. This is known as **absolute dispersion**. The key quantities are the first and second moments of the particle displacements.

The **mean displacement**, $\langle \Delta \mathbf{x}(t) \rangle$, reveals the transport due to the mean flow. The **central second-moment tensor**, $M_{ij}(t) = \langle (\Delta x_i - \langle \Delta x_i \rangle)(\Delta x_j - \langle \Delta x_j \rangle) \rangle$, describes the spread of the particle cloud around its mean position, driven by the turbulent velocity fluctuations.

The growth of this second-moment tensor over time characterizes the dispersion regime:
-   **Ballistic Regime**: At very short times, particles have not yet "forgotten" their initial velocity fluctuations. They travel in nearly straight lines, and the variance grows quadratically with time: $M_{ij}(t) \propto t^2$.
-   **Diffusive Regime**: At long times, after particle velocities have decorrelated from their initial values, their motion resembles a random walk. The variance grows linearly with time: $M_{ij}(t) \propto t$.

In the [diffusive regime](@entry_id:149869), we can define the **eddy diffusivity tensor**, $\mathbf{K}$, as half the rate of growth of the second-moment tensor :

$$
K_{ij} = \frac{1}{2} \frac{dM_{ij}}{dt}
$$

This tensor provides a powerful, quantitative description of turbulent mixing. Since $\mathbf{K}$ is a [symmetric tensor](@entry_id:144567), it can be diagonalized. Its eigenvalues represent the diffusivities along its principal axes, and its eigenvectors give the orientation of these axes. This allows for a detailed characterization of **anisotropic diffusion**, where mixing is stronger in some directions than others. For example, one can compute the anisotropy ratio $R = K_{xx}/K_{yy}$ and the orientation angle $\theta$ of the principal axis of maximum diffusion, which are crucial metrics for understanding the structure of oceanic turbulence .

#### Two-Particle and Relative Dispersion

While absolute dispersion describes the spreading of a cloud, **relative dispersion** describes how the distance between a pair of particles evolves. This is directly related to the process of turbulent stirring, where nearby fluid parcels are separated by eddies.

The behavior of relative dispersion depends strongly on the separation distance $r$ relative to the scales of turbulence. Within the **[inertial subrange](@entry_id:273327)**—a range of scales where energy is transferred from large eddies to smaller ones without significant [viscous dissipation](@entry_id:143708)—relative dispersion follows a remarkable law discovered by Lewis Fry Richardson. He found that the mean square separation, $\langle r^2 \rangle$, grows at an accelerating rate. Based on Kolmogorov's theory of turbulence, this can be shown to follow the famous scaling law :

$$
\langle r^2(t) \rangle \sim C_R \varepsilon t^3
$$

Here, $\varepsilon$ is the rate of turbulent kinetic energy dissipation, and $C_R$ is a dimensionless constant. This **super-diffusive** ($t^3$) growth is a hallmark of turbulent transport. It arises because as two particles separate, they are acted upon by progressively larger and more energetic eddies, which increases their rate of separation. In this regime, the dispersion "forgets" the initial separation $r_0$ and depends only on the fundamental parameters of the turbulence itself.

### Characterizing Flow Structure: Coherent Structures and Stability

Beyond statistical analysis, Lagrangian trajectories can reveal the underlying geometric "skeleton" of a flow that organizes transport. This is the domain of **Lagrangian Coherent Structures (LCS)**.

The central tool for identifying LCS is the **Finite-Time Lyapunov Exponent (FTLE)**. The FTLE measures the maximum rate of separation of infinitesimally close particles over a finite time interval. To define it formally, we first introduce the **[flow map](@entry_id:276199)** $\Phi_{t_0}^{t_0+\tau}(\mathbf{x}_0)$, which maps a particle's initial position $\mathbf{x}_0$ at time $t_0$ to its final position at time $t_0+\tau$. The evolution of an infinitesimal [separation vector](@entry_id:268468) $\delta\mathbf{x}_0$ is given by the deformation gradient, $\delta\mathbf{x}_\tau \approx \nabla\Phi \cdot \delta\mathbf{x}_0$.

The amount of stretching depends on the initial orientation of $\delta\mathbf{x}_0$. The key object that quantifies this stretching is the **right Cauchy–Green strain tensor**, $\mathbf{C} = (\nabla\Phi)^\top (\nabla\Phi)$. This symmetric, [positive-definite tensor](@entry_id:204409) relates the final squared length of the [separation vector](@entry_id:268468) to its initial state via $\|\delta\mathbf{x}_\tau\|^2 \approx \delta\mathbf{x}_0^\top \mathbf{C} \delta\mathbf{x}_0$. The maximum possible stretch for any initial orientation is given by the square root of the largest eigenvalue of $\mathbf{C}$, $\lambda_{\max}(\mathbf{C})$. The FTLE, $\sigma$, is then defined as the normalized exponential rate of this maximal stretch :

$$
\sigma(\mathbf{x}_0, t_0; \tau) = \frac{1}{|\tau|} \ln\sqrt{\lambda_{\max}(\mathbf{C})}
$$

When computed over a grid of initial positions $\mathbf{x}_0$, the FTLE field reveals regions of intense stretching. Ridges of high FTLE values act as proxies for LCS. Repelling LCS (material lines from which particles move away) correspond to ridges in the forward–time FTLE field, while attracting LCS (lines toward which particles converge) correspond to ridges in the backward-time FTLE field. These structures act as the organizing boundaries for fluid transport.

The FTLE is the finite-time version of the asymptotic **Lyapunov exponent**. For a simple [linear flow](@entry_id:273786), $\dot{\mathbf{x}} = \mathbf{J}\mathbf{x}$, the Lyapunov exponents are simply the real parts of the eigenvalues of the constant [velocity gradient tensor](@entry_id:270928) $\mathbf{J}$. A positive Lyapunov exponent indicates exponential separation and [chaotic dynamics](@entry_id:142566). For incompressible flows ($\nabla \cdot \mathbf{u} = 0$), the trace of $\mathbf{J}$ is zero, which implies that the sum of the Lyapunov exponents must also be zero. This means that in a 2D incompressible flow, it is impossible for the flow to be asymptotically stable everywhere (i.e., having two negative exponents); if there is contraction in one direction, there must be expansion in another . The unstable manifolds of saddle points in the flow, which are tangent to the eigenvectors associated with positive eigenvalues of $\mathbf{J}$, are the infinite-time structures that the FTLE ridges approximate . This provides a deep connection between the [local stability analysis](@entry_id:178725) of the velocity field and the global [transport barriers](@entry_id:756132) revealed by Lagrangian methods.