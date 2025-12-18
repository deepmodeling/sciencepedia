## Introduction
Smoothed Particle Hydrodynamics (SPH) is a powerful and versatile Lagrangian numerical method used extensively in [computational astrophysics](@entry_id:145768) to simulate complex fluid flows. Its particle-based nature makes it exceptionally well-suited for problems involving free surfaces, large deformations, and complex geometries, from the collapse of [molecular clouds](@entry_id:160702) to the chaotic mergers of galaxies. However, the apparent simplicity of the SPH concept belies a sophisticated numerical framework where subtle choices in its implementation can have profound impacts on the accuracy, stability, and physical fidelity of a simulation. This article bridges the gap between the high-level concept and practical mastery, providing a deep dive into the foundational components of the SPH method.

The journey begins in the **Principles and Mechanisms** chapter, where we deconstruct the core of SPH. We will examine the mathematical properties of the [smoothing kernel](@entry_id:195877), the cornerstone of the method, and derive the discrete forms of the hydrodynamical [equations of motion](@entry_id:170720), paying close attention to the requirements for conserving fundamental quantities like mass and momentum. Following this, the **Applications and Interdisciplinary Connections** chapter demonstrates how the fundamental SPH algorithm is adapted to tackle the rich physics of the cosmos. We explore the implementation of [artificial viscosity](@entry_id:140376) for shock capturing, advanced techniques for modeling fluid instabilities, and the coupling of SPH with modules for self-gravity, [magnetohydrodynamics](@entry_id:264274), and [radiation transport](@entry_id:149254). Finally, the **Hands-On Practices** section provides a series of targeted problems, allowing you to apply these principles by deriving kernel normalization constants and analyzing the conditions for [numerical stability](@entry_id:146550), solidifying the theoretical concepts through practical application.

## Principles and Mechanisms

### The SPH Kernel: A Smoothed Representation of the Delta Function

The foundation of Smoothed Particle Hydrodynamics (SPH) rests on the concept of integral interpolation. Any continuous field $A(\mathbf{r})$ can be formally expressed as a convolution with the Dirac delta distribution, $\delta(\mathbf{r})$:

$$
A(\mathbf{r}) = \int A(\mathbf{r}') \delta(\mathbf{r} - \mathbf{r}') \, dV'
$$

In SPH, the singular Dirac delta is replaced by a smooth, spatially extended function $W(\mathbf{r}, h)$, known as the **[smoothing kernel](@entry_id:195877)**, where $h$ is a characteristic length scale called the **smoothing length**. This replacement, or mollification, transforms the exact identity into an approximation:

$$
\langle A(\mathbf{r}) \rangle = \int A(\mathbf{r}') W(\mathbf{r} - \mathbf{r}', h) \, dV'
$$

The kernel $W$ is not arbitrary; it must possess several key properties to ensure that this approximation is physically meaningful, computationally tractable, and consistent with the underlying [continuum mechanics](@entry_id:155125). These properties are chosen to make the kernel a well-behaved approximation of the [identity operator](@entry_id:204623) under convolution.

First and foremost is the **[normalization condition](@entry_id:156486)**. The kernel must integrate to unity over all space:

$$
\int W(\mathbf{r}, h) \, dV = 1
$$

This property is essential for zeroth-order consistency. For a constant field, $A(\mathbf{r}) = c$, the smoothing operation must reproduce the constant exactly: $\langle A(\mathbf{r}) \rangle = \int c W(\mathbf{r} - \mathbf{r}', h) \, dV' = c \int W(\mathbf{u}, h) \, dV = c$. The [normalization condition](@entry_id:156486) guarantees this. In the discrete particle representation, where density is computed as $\rho(\mathbf{r}) = \sum_j m_j W(\mathbf{r} - \mathbf{r}_j, h)$, this condition ensures that the total mass integrated over the domain equals the sum of the particle masses, $\int \rho(\mathbf{r}) dV = \sum_j m_j$. A failure to precisely normalize the kernel introduces a systematic error that directly compromises the conservation of global quantities. For instance, a kernel whose integral is $1 + \delta$ will result in a fractional error of $\delta$ in the total computed mass, momentum, and energy of a uniform system.

Second, the kernel must satisfy a **positivity condition**, $W(\mathbf{r}, h) \ge 0$. Since SPH is often used to model physical densities (mass, energy), which are inherently positive definite, this property ensures that the smoothing of a non-negative field results in a non-negative field. A kernel with negative regions could lead to unphysical results such as negative densities or energies.

Third, for most applications, the kernel is chosen to have **even symmetry**, $W(\mathbf{r}, h) = W(-\mathbf{r}, h)$, making it an isotropic function that depends only on the distance $r = |\mathbf{r}|$. This [isotropy](@entry_id:159159) ensures that the smoothing process has no preferred direction. Critically, this symmetry is fundamental to deriving manifestly momentum-conserving [equations of motion](@entry_id:170720). The gradient of an even function is an odd function: $\nabla W(-\mathbf{r}) = -\nabla W(\mathbf{r})$. When pairwise forces between particles $i$ and $j$ are constructed from the kernel gradient $\nabla_i W(\mathbf{r}_i - \mathbf{r}_j)$, this property ensures that the force on $i$ from $j$ is equal and opposite to the force on $j$ from $i$, fulfilling Newton's third law for the particle pair and guaranteeing conservation of [total linear momentum](@entry_id:173071).

Fourth, for computational reasons, kernels are typically designed with **[compact support](@entry_id:276214)**. This means the kernel is exactly zero outside a finite radius, commonly expressed as a multiple of the smoothing length, $W(r, h) = 0$ for $r > \kappa h$. This property is not a mathematical requirement for convergence—a Gaussian kernel, for example, is a valid [mollifier](@entry_id:272904) despite its infinite support—but it is a practical necessity. Compact support limits the number of interacting "neighbor" particles for any given particle, which reduces the [computational complexity](@entry_id:147058) of the pair-wise summations from an intractable $O(N^2)$ to a manageable $O(N \log N)$ or $O(N)$ with efficient neighbor-finding algorithms. The trade-off for truncating a kernel like the Gaussian at a radius $kh$ is the introduction of a **[truncation error](@entry_id:140949)**, as a fraction of the kernel's mass is neglected. For a 3D Gaussian, this fractional error is $\Gamma(3/2, k^2) / \Gamma(3/2)$, which decreases exponentially with the [cutoff radius](@entry_id:136708) factor $k$.

Finally, all these properties must be consistent with the **convergence condition**: in the limit that the smoothing length approaches zero, the kernel must behave as a delta distribution. Formally, for any smooth [test function](@entry_id:178872) $\phi(\mathbf{r})$:

$$
\lim_{h \to 0} \int \phi(\mathbf{r}) W(\mathbf{r}, h) \, dV = \phi(\mathbf{0})
$$

This ensures that as the resolution of the simulation increases ($h \to 0$), the SPH approximation converges to the true continuum equations.

### Practical Kernel Design and Properties

The properties outlined above guide the practical construction of kernel functions. A common functional form for a spherically symmetric kernel in $\nu$ dimensions is $W(r, h) = \sigma_{\nu} h^{-\nu} f(r/h)$, where $q = r/h$ is the dimensionless separation, $f(q)$ is a dimensionless shape function, and $\sigma_{\nu}$ is a [normalization constant](@entry_id:190182) that depends on the dimension $\nu$ and the shape function $f$.

To find $\sigma_{\nu}$, we enforce the [normalization condition](@entry_id:156486) $\int W dV = 1$. By converting to hyperspherical coordinates, we can solve for the constant. The [volume element](@entry_id:267802) is $dV = r^{\nu-1} dr d\Omega_{\nu-1}$, where $d\Omega_{\nu-1}$ is the solid angle element. The integral becomes:

$$
1 = \int_0^{\infty} \sigma_{\nu} h^{-\nu} f(r/h) S_{\nu-1} r^{\nu-1} dr
$$

where $S_{\nu-1} = \frac{2 \pi^{\nu/2}}{\Gamma(\nu/2)}$ is the surface area of a unit sphere in $\nu$ dimensions. Changing variables to $q=r/h$ and assuming [compact support](@entry_id:276214) up to $r=\kappa h$ (i.e., $q=\kappa$), the integral simplifies, and we find that the normalization constant is independent of $h$:

$$
\sigma_{\nu} = \frac{1}{S_{\nu-1} \int_0^{\kappa} f(q) q^{\nu-1} dq} = \frac{\Gamma(\nu/2)}{2 \pi^{\nu/2} \int_0^{\kappa} f(q) q^{\nu-1} dq}
$$

This general formula allows for the correct normalization of any spherically symmetric kernel given its shape function and support radius.

The gradient of the kernel, which appears in the SPH [equations of motion](@entry_id:170720), also takes a simple form for spherically symmetric kernels. Using the chain rule, the gradient with respect to a particle's position $\mathbf{r}_i$ is:

$$
\nabla_i W(|\mathbf{r}_i - \mathbf{r}_j|, h) = \frac{dW}{dr} \nabla_i r_{ij} = \frac{dW}{dr} \hat{\mathbf{r}}_{ij}
$$

where $r_{ij} = |\mathbf{r}_i - \mathbf{r}_j|$ and $\hat{\mathbf{r}}_{ij} = (\mathbf{r}_i - \mathbf{r}_j)/r_{ij}$ is the unit vector pointing from $j$ to $i$. The gradient of the kernel always points along the line connecting the two particles, with a magnitude determined by the radial derivative of the kernel function.

The behavior of this gradient near the origin is critical for numerical stability. For the force between two particles to be well-defined as $r \to 0$, its magnitude must vanish. This requires $\lim_{r\to 0} |\frac{dW}{dr}| = 0$, which for a smooth kernel implies $\frac{dW}{dr}|_{r=0} = 0$. Furthermore, to prevent **[tensile instability](@entry_id:163505)**—an unphysical clumping of particles—the force between nearly coincident particles must be repulsive. A repulsive pressure force requires $\frac{dW}{dr}  0$ for small $r>0$. For a function that is zero at the origin to become negative for positive $r$, its second derivative at the origin must be negative, $\frac{d^2W}{dr^2}|_{r=0}  0$. Together, these conditions mean that a stable SPH kernel must have a strict [local maximum](@entry_id:137813) at $r=0$, providing a repulsive restoring force that grows from zero as particles separate.

A widely used kernel that satisfies these properties is the **Monaghan cubic spline (M4) kernel**. In three dimensions, its shape function is a [piecewise polynomial](@entry_id:144637), and its radial derivative, with $q=r/h$, is given by:

$$
\frac{dW}{dr} =
\begin{cases}
\frac{3q(3q-4)}{4\pi h^{4}}  0 \le q  1 \\
-\frac{3(2-q)^{2}}{4\pi h^{4}}  1 \le q  2 \\
0  q \ge 2
\end{cases}
$$

While the M4 kernel has been a workhorse, it suffers from **[pairing instability](@entry_id:158107)**, especially when a large number of neighbors are used. This instability arises because the kernel's Fourier transform is not strictly positive. Modern kernels, such as the **Wendland kernels**, are constructed to have a [positive definite](@entry_id:149459) Fourier transform, guaranteeing stability against this pairing artifact. However, this stability comes at a small cost: for a fixed number of neighbors, Wendland kernels tend to produce slightly more [stochastic noise](@entry_id:204235) in the pressure [gradient estimates](@entry_id:189587). Both the M4 and Wendland kernels, when used in standard SPH formulations for smooth flows, achieve a [second-order convergence](@entry_id:174649) rate, with the error scaling as $\mathcal{O}(h^2)$.

### The SPH Equations of Motion

With a properly defined kernel, we can construct discrete equations of motion that approximate the fluid dynamics equations.

The first step is to estimate the density for each particle $i$ via a weighted sum over its neighbors $j$:

$$
\rho_i = \sum_j m_j W_{ij}(h_i)
$$

where $W_{ij}(h_i) = W(|\mathbf{r}_i - \mathbf{r}_j|, h_i)$. An alternative approach is to evolve the density by integrating the SPH discretization of the [continuity equation](@entry_id:145242), $\frac{d\rho_i}{dt} = \sum_j m_j \mathbf{v}_{ij} \cdot \nabla_i W_{ij}$, where $\mathbf{v}_{ij} = \mathbf{v}_i - \mathbf{v}_j$. These two methods are not necessarily equivalent, especially when the smoothing length $h_i$ is adaptive and varies with time. Taking the time derivative of the summation density reveals an extra term:

$$
\frac{d\rho_i}{dt} = \sum_j m_j \mathbf{v}_{ij} \cdot \nabla_i W_{ij} + \frac{dh_i}{dt} \sum_j m_j \frac{\partial W_{ij}}{\partial h_i}
$$

The second term, often called the "grad-h" term, is non-zero when $h_i$ adapts, for instance, to maintain a constant number of neighbors. Neglecting this term, which is common in older codes, leads to inconsistencies. For this reason, and to avoid the accumulation of secular errors from [time integration](@entry_id:170891), modern SPH codes often prefer to recompute the density via the direct summation at every timestep, solving for $\rho_i$ and $h_i$ self-consistently. It is important to note, however, that both methods suffer from inaccuracies near free surfaces or sharp density discontinuities, where the kernel support is incompletely sampled.

The SPH momentum equation is derived from the Euler equation, $\frac{d\mathbf{v}}{dt} = -\frac{\nabla P}{\rho}$. A robust discretization must conserve momentum. This is achieved by using a symmetrized form for the pressure gradient. A common form is:

$$
\frac{d\mathbf{v}_i}{dt} = - \sum_j m_j \left( \frac{P_i}{\rho_i^2} + \frac{P_j}{\rho_j^2} \right) \nabla_i W_{ij}
$$

The term in parentheses is symmetric upon swapping indices $i$ and $j$. As we've seen, the kernel gradient is antisymmetric, $\nabla_i W_{ij} = -\nabla_j W_{ji}$, due to the kernel's even symmetry. This ensures the force on $i$ from $j$ is equal and opposite to the force on $j$ from $i$, guaranteeing exact [conservation of linear momentum](@entry_id:165717) for the particle system.

Despite these conservative properties, this standard "density-entropy" formulation has a well-known failure at **[contact discontinuities](@entry_id:747781)**—interfaces where pressure is continuous but density and temperature (or entropy) jump. Because the SPH density $\rho_i$ is a smoothed average, it is erroneous near the discontinuity. This error in density translates, via the equation of state (e.g., $P = A\rho^\gamma$), into an unphysical "blip" or jump in the pressure field. This pressure error creates a spurious repulsive force, akin to a surface tension, that artificially separates the two fluid phases and suppresses physical mixing instabilities.

To address this, modern **pressure-entropy SPH** formulations have been developed. These methods are derived from the same variational principles but are re-formulated to treat pressure, rather than density, as the fundamental smoothed quantity. The particle pressures are determined implicitly to ensure a smooth, single-valued pressure field across the domain. The resulting momentum equation has a pairwise force that depends on the smoothed pressures of the interacting particles, eliminating the explicit dependence on the pathological density estimate. This approach correctly models the continuous pressure at the interface, thereby avoiding the spurious repulsive force and enabling a much more accurate representation of interfacial phenomena like Kelvin-Helmholtz instabilities.

### Numerical Integration and Timestepping

The SPH formalism converts the [partial differential equations](@entry_id:143134) of fluid dynamics into a large system of coupled [ordinary differential equations](@entry_id:147024) (ODEs) for the positions, velocities, and thermodynamic quantities of each particle. These ODEs must be integrated forward in time. For efficiency and accuracy, most SPH codes employ an adaptive timestep, where the global timestep for the system, $\Delta t$, is determined by the minimum of the stability-limited timesteps required by each individual particle. Several physical processes impose constraints on this timestep.

The most fundamental is the **Courant-Friedrichs-Lewy (CFL) condition**, which dictates that information must not propagate across a resolution element (of size $\sim h$) in a single step. This leads to a constraint of the form:

$$
\Delta t_{\text{CFL}} \le C \frac{h}{v_{\text{sig}}}
$$

Here, $C$ is a dimensionless constant (the Courant number) that depends on the stability of the time integrator, and $v_{\text{sig}}$ is the maximum [signal velocity](@entry_id:261601). For [hydrodynamics](@entry_id:158871), this is typically taken as $v_{\text{sig}} = c_s + |\mathbf{v}|$, or in a pairwise sense, it can be refined to include the local sound speed and the approach velocity between particles. The shape of the kernel can also influence the effective signal speed.

A second constraint arises from strong accelerations. To prevent particles from overshooting their neighbors in a single step, the timestep must be limited such that the displacement due to acceleration is a small fraction of the smoothing length. This leads to a **force condition** or **acceleration condition**:

$$
\Delta t_{\text{force}} \le C \sqrt{\frac{h}{|\mathbf{a}|}}
$$

where $|\mathbf{a}|$ is the magnitude of the particle's acceleration.

Finally, if the simulation includes explicit physical [diffusion processes](@entry_id:170696), such as viscosity or [thermal conduction](@entry_id:147831), these impose their own, often very strict, timestep limit. The stability of an explicit diffusion solver requires the timestep to scale with the square of the resolution length:

$$
\Delta t_{\text{diff}} \le C \frac{h^2}{D}
$$

where $D$ is the relevant diffusion coefficient. This quadratic dependence on $h$ means the diffusion timestep can become extremely small at high resolution.

The overall admissible timestep for a particle is the minimum of these individual constraints, $\Delta t_i = \min(\Delta t_{\text{CFL}}, \Delta t_{\text{force}}, \Delta t_{\text{diff}}, \ldots)$. The global system timestep is then $\Delta t = \min_i(\Delta t_i)$. The Courant constant $C$ is chosen to ensure stability; its value depends on the order and properties of the numerical integrator. For example, a second-order Leapfrog (Kick-Drift-Kick) integrator might require $C \approx 0.3$, whereas a more stable, higher-order scheme like a fourth-order Runge-Kutta (RK4) might allow for a larger value, such as $C \approx 0.5$, permitting a longer timestep at the cost of more function evaluations per step.