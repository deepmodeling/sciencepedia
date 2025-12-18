## Introduction
Predicting the ground shaking from an earthquake is a fundamental challenge in [geophysics](@entry_id:147342) and [earthquake engineering](@entry_id:748777), with profound implications for public safety and infrastructure resilience. At the heart of this endeavor lies the ability to numerically simulate the propagation of [seismic waves](@entry_id:164985) through the Earth's complex geological structures. The [finite difference method](@entry_id:141078) offers a powerful and versatile framework for this task, but its successful application requires a deep understanding of the interplay between physical laws, [numerical algorithms](@entry_id:752770), and computational constraints. This article bridges the gap between the continuous physics of [elastodynamics](@entry_id:175818) and the discrete world of computational modeling, providing a comprehensive guide to building, running, and interpreting these simulations.

Our journey begins in **Principles and Mechanisms**, where we will lay the groundwork by dissecting the governing elastodynamic equations and their [numerical discretization](@entry_id:752782), focusing on core concepts like staggered grids, stability criteria, and boundary conditions. Next, in **Applications and Interdisciplinary Connections**, we will elevate this foundational knowledge by exploring how to incorporate realistic Earth physics, such as anisotropy and attenuation, and tackle advanced challenges like topography and fault representation, highlighting the method's role in large-scale, [high-performance computing](@entry_id:169980). Finally, the **Hands-On Practices** section will offer opportunities to apply these concepts through guided exercises in diagnosing numerical instabilities and analyzing the accuracy of different schemes. This structured approach will equip you with the essential knowledge to effectively model [earthquake ground motion](@entry_id:748778).

## Principles and Mechanisms

This chapter delves into the foundational principles and core mechanisms that underpin the [finite difference modeling](@entry_id:749378) of [earthquake ground motion](@entry_id:748778). We will transition from the continuous physical laws governing [seismic wave propagation](@entry_id:165726) to their discrete numerical counterparts, exploring the essential techniques required for building accurate and stable simulations. Our journey will cover the governing equations, spatial and [temporal discretization](@entry_id:755844), stability and accuracy criteria, and the implementation of realistic source and boundary conditions.

### The Governing Equations of Elastodynamics

The propagation of seismic waves through the Earth's crust is governed by the principles of continuum mechanics. For a linear, isotropic elastic medium, the behavior is described by a set of coupled partial differential equations (PDEs) that relate motion to internal forces.

The first fundamental principle is the **[conservation of linear momentum](@entry_id:165717)**. In its local form, known as Cauchy's first law of motion, it states that the acceleration of a particle is proportional to the [net force](@entry_id:163825) acting upon it. This force arises from the divergence of the [internal stress](@entry_id:190887) field and any external [body forces](@entry_id:174230). For a medium with spatially varying mass density $\rho(\mathbf{x})$, the equation is:

$$
\rho(\mathbf{x}) \frac{\partial v_i(\mathbf{x}, t)}{\partial t} = \frac{\partial \sigma_{ij}(\mathbf{x}, t)}{\partial x_j} + f_i(\mathbf{x}, t)
$$

Here, $v_i$ is the particle velocity vector, $\sigma_{ij}$ is the symmetric Cauchy stress tensor ($\sigma_{ij} = \sigma_{ji}$), and $f_i$ is the body force density vector (e.g., gravity or an earthquake source representation). The indices $i, j$ range from 1 to 3, representing the Cartesian coordinates, and we use the Einstein [summation convention](@entry_id:755635) over repeated indices.

The second core component is the **[constitutive relation](@entry_id:268485)**, which describes the material's response to deformation. For a linear, isotropic elastic material, this is **Hooke's Law**. It relates the stress tensor $\sigma_{ij}$ to the strain tensor $\varepsilon_{kl}$. To formulate a system of first-order equations in time, we consider the time derivative of Hooke's Law:

$$
\frac{\partial \sigma_{ij}}{\partial t} = \lambda(\mathbf{x}) \delta_{ij} \frac{\partial v_k}{\partial x_k} + \mu(\mathbf{x}) \left( \frac{\partial v_i}{\partial x_j} + \frac{\partial v_j}{\partial x_i} \right)
$$

In this equation, $\lambda(\mathbf{x})$ and $\mu(\mathbf{x})$ are the spatially varying **Lamé parameters**, which characterize the elastic properties of the medium, and $\delta_{ij}$ is the Kronecker delta. The term $\frac{\partial v_k}{\partial x_k}$ is the divergence of the velocity field, representing the rate of volume change (dilatation), and the term $\left( \frac{\partial v_i}{\partial x_j} + \frac{\partial v_j}{\partial x_i} \right)$ is twice the [strain-rate tensor](@entry_id:266108), representing the rate of shape change (shear).

Together, these two equations form the **first-order velocity-stress elastodynamic system**. This system comprises nine coupled, first-order PDEs: three for the components of velocity ($v_i$) and six for the independent components of the symmetric stress tensor ($\sigma_{ij}$). This formulation is particularly well-suited for [finite difference methods](@entry_id:147158) because it involves only first-order derivatives in both space and time, which are easier to discretize accurately than the [higher-order derivatives](@entry_id:140882) found in other formulations .

It is instructive to contrast this with the more classical **second-order displacement formulation**, often called the Navier-Cauchy equation. By substituting the [constitutive relation](@entry_id:268485) into the momentum balance and expressing everything in terms of the [displacement vector](@entry_id:262782) $\mathbf{u}$ (where $\mathbf{v} = \partial \mathbf{u} / \partial t$), one can arrive at a single vector equation for $\mathbf{u}$. For a homogeneous medium, this is:

$$
\rho \frac{\partial^2 \mathbf{u}}{\partial t^2} = (\lambda+2\mu) \nabla(\nabla \cdot \mathbf{u}) - \mu \nabla \times (\nabla \times \mathbf{u}) + \mathbf{f}
$$

While mathematically elegant, this second-order form involves second derivatives in space, which can be more complex to handle numerically, especially at boundaries and [material interfaces](@entry_id:751731). The [first-order system](@entry_id:274311), by advancing both velocity and stress as [independent variables](@entry_id:267118), provides direct access to the stress field and often simplifies the implementation of boundary conditions.

### Discretization in Space: The Finite Difference Method

To solve the elastodynamic equations on a computer, we must translate the continuous PDEs into a system of algebraic equations. The Finite Difference (FD) method achieves this by replacing the continuous domain with a discrete grid of points and approximating the derivatives at these points using the values of the function at neighboring points.

#### Approximating Derivatives

The foundation of the FD method is the approximation of derivatives using Taylor series expansions. Let us consider a smooth, one-dimensional function $u(x)$ on a uniform grid with spacing $h$. The Taylor series for $u(x+h)$ and $u(x-h)$ are:

$$
u(x+h) = u(x) + h u'(x) + \frac{h^2}{2!} u''(x) + \frac{h^3}{3!} u'''(x) + \dots
$$
$$
u(x-h) = u(x) - h u'(x) + \frac{h^2}{2!} u''(x) - \frac{h^3}{3!} u'''(x) + \dots
$$

By subtracting the second expansion from the first and rearranging, we obtain the simplest **[centered difference](@entry_id:635429)** approximation for the first derivative:

$$
u'(x) \approx \frac{u(x+h) - u(x-h)}{2h}
$$

The error in this approximation, known as the **[truncation error](@entry_id:140949)**, can be found from the Taylor series. It is of the order $\mathcal{O}(h^2)$, making this a second-order accurate scheme. More generally, we can construct higher-order approximations by using more points. A centered, antisymmetric approximation for the first derivative with an accuracy of order $2p$ can be written as :

$$
u'(x_i) \approx \frac{1}{h} \sum_{j=1}^{p} a_j [u(x_i+jh) - u(x_i-jh)]
$$

The coefficients $a_j$ are chosen to cancel out as many terms as possible in the Taylor expansion, leading to a [system of linear equations](@entry_id:140416). The leading term in the truncation error for such a scheme will be proportional to $h^{2p} u^{(2p+1)}(x_i)$, where $u^{(n)}$ is the $n$-th derivative of $u$. The key takeaway is that higher-order accuracy can be achieved at the cost of using a wider **stencil** (more grid points).

#### The Staggered Grid

When discretizing the first-order velocity-stress system, a simple approach would be to define all nine variables (three velocity components, six stress components) at the same grid points—a **[collocated grid](@entry_id:175200)**. However, using [centered difference](@entry_id:635429) operators on a [collocated grid](@entry_id:175200) for a [first-order system](@entry_id:274311) is known to be prone to numerical instabilities, manifesting as high-frequency oscillations that can corrupt the solution.

The solution is to use a **staggered grid**, where different components of the field variables are defined at different locations within a grid cell. The canonical [staggered grid](@entry_id:147661) for 3D [elastodynamics](@entry_id:175818), developed by Virieux, places variables in a way that all spatial derivatives required in the update equations can be computed with compact, second-order centered differences .

Specifically, consider a grid cell indexed by $(i,j,k)$. The standard arrangement is as follows:
- Normal stresses ($\sigma_{xx}, \sigma_{yy}, \sigma_{zz}$) are defined at the cell center $(i,j,k)$.
- Velocity components ($v_x, v_y, v_z$) are defined at the center of the faces normal to their respective directions. For example, $v_x$ is at $(i+\frac{1}{2}, j, k)$, $v_y$ at $(i, j+\frac{1}{2}, k)$, and $v_z$ at $(i, j, k+\frac{1}{2})$.
- Shear stresses ($\sigma_{xy}, \sigma_{xz}, \sigma_{yz}$) are defined at the center of the edges. For example, $\sigma_{xy}$ is at $(i+\frac{1}{2}, j+\frac{1}{2}, k)$.

To appreciate the elegance of this arrangement, consider the update for the velocity component $v_x$, located at $(i+\frac{1}{2}, j, k)$. The governing equation is $\rho \frac{\partial v_x}{\partial t} = \frac{\partial \sigma_{xx}}{\partial x} + \frac{\partial \sigma_{xy}}{\partial y} + \frac{\partial \sigma_{xz}}{\partial z}$.
- The term $\frac{\partial \sigma_{xx}}{\partial x}$ is naturally centered at $(i+\frac{1}{2}, j, k)$ and can be approximated as $\frac{\sigma_{xx}(i+1, j, k) - \sigma_{xx}(i, j, k)}{h_x}$. This uses the two adjacent cell-center locations where $\sigma_{xx}$ is defined.
- Similarly, $\frac{\partial \sigma_{xy}}{\partial y}$ is approximated as $\frac{\sigma_{xy}(i+\frac{1}{2}, j+\frac{1}{2}, k) - \sigma_{xy}(i+\frac{1}{2}, j-\frac{1}{2}, k)}{h_y}$, using the two adjacent edge locations where $\sigma_{xy}$ is defined.
This pattern holds for all derivative terms in all nine update equations. The [staggered grid](@entry_id:147661) ensures that all spatial derivatives are naturally centered and computed over the smallest possible distance, which enhances both stability and accuracy.

### Discretization in Time: Advancing the Solution

Once we discretize the governing equations in space, we are left with a very large system of coupled [first-order ordinary differential equations](@entry_id:264241) (ODEs) of the form:

$$
\frac{d\mathbf{q}(t)}{dt} = \mathbf{L}\mathbf{q}(t)
$$

Here, $\mathbf{q}(t)$ is a vector containing all the velocity and stress values at all grid points, and $\mathbf{L}$ is a large, sparse matrix representing the spatial [finite difference operators](@entry_id:749379). The next step is to discretize this system in time.

A common and efficient method is the second-order **[leapfrog scheme](@entry_id:163462)**. For the velocity-stress system, velocity and stress are defined at alternating half-time steps. A simplified representation for the generic system above is:

$$
\mathbf{q}^{n+1} = \mathbf{q}^{n-1} + 2 \Delta t \mathbf{L} \mathbf{q}^n
$$

where $\Delta t$ is the time step and the superscript $n$ denotes the time level $t_n = n \Delta t$. The leapfrog method is **explicit**, meaning the solution at the new time step can be computed directly from values at previous time steps. A key property of the [leapfrog scheme](@entry_id:163462), when applied to wave equations, is that it is **non-dissipative** . This means that within its stability range, it does not artificially damp the amplitude of waves, conserving the energy of the numerical solution. This is a desirable property for modeling the nearly perfect elastic propagation of seismic waves over long distances.

Other [time-stepping schemes](@entry_id:755998) can also be used, such as the family of **Runge-Kutta (RK)** methods. The classical fourth-order Runge-Kutta (RK4) scheme, for instance, achieves higher temporal accuracy by evaluating the spatial operator $\mathbf{L}$ at several intermediate stages within a single time step.

$$
\mathbf{q}^{n+1} = \mathbf{q}^n + \frac{\Delta t}{6} (\mathbf{k}_1 + 2\mathbf{k}_2 + 2\mathbf{k}_3 + \mathbf{k}_4)
$$

where the stages $\mathbf{k}_i$ are intermediate updates. Unlike the [leapfrog scheme](@entry_id:163462), RK4 is **dissipative**; it introduces a small amount of [numerical damping](@entry_id:166654). However, its higher order of accuracy and larger [stability region](@entry_id:178537) can be advantageous in some applications . The choice of [time integration](@entry_id:170891) scheme involves a trade-off between computational cost, accuracy, and dissipative properties.

### Numerical Stability and Accuracy

An FD simulation is only useful if it is both stable and accurate. Stability ensures that errors do not grow uncontrollably and destroy the solution, while accuracy ensures that the numerical solution is a faithful representation of the true physical behavior.

#### Stability and the CFL Condition

Explicit FD schemes are only **conditionally stable**. The stability is governed by the **Courant-Friedrichs-Lewy (CFL) condition**, which has a profound physical interpretation: in one time step, a wave must not be allowed to travel more than one grid cell. If it does, the numerical scheme cannot correctly propagate the information, leading to instability.

This condition can be derived formally using von Neumann stability analysis. For the 2D [acoustic wave equation](@entry_id:746230) discretized with second-order centered differences in space and time, the stability condition is :

$$
\sigma = \frac{c \Delta t}{h} \le \frac{1}{\sqrt{2}}
$$

where $\sigma$ is the dimensionless **Courant number**, $c$ is the [wave speed](@entry_id:186208), $\Delta t$ is the time step, and $h$ is the grid spacing (assuming $h_x=h_y=h$). In a heterogeneous 3D elastic medium, the condition becomes more complex, but the principle remains the same. Stability is governed by the *maximum* [wave speed](@entry_id:186208) ($c_{max}$, typically the P-wave velocity) and the *minimum* grid spacing in the model. The maximum permissible time step is therefore:

$$
\Delta t_{max} \le C \frac{h_{min}}{c_{max}}
$$

where $C$ is a constant that depends on the dimension and the order of the FD stencil (for the 3D velocity-stress system with a second-order stencil, $C \approx 1/\sqrt{3}$). In practice, simulations are run with a time step slightly smaller than this theoretical maximum (e.g., $0.9 \Delta t_{max}$) to provide a safety margin against instabilities that can arise from complex boundaries or [material interfaces](@entry_id:751731) .

#### Accuracy, Grid Resolution, and Dispersion

Even when a scheme is stable, its accuracy must be considered. A primary source of error in [wave propagation](@entry_id:144063) simulations is **numerical dispersion**. This is an unphysical artifact of the [discretization](@entry_id:145012) where the numerical phase velocity of a wave, $v_p^N$, depends on its frequency and direction of propagation relative to the grid, even if the underlying physical medium is non-dispersive . This causes [wave packets](@entry_id:154698) to change shape and spread out as they propagate. Numerical dispersion is most severe for short wavelengths, i.e., high-frequency waves that are poorly resolved by the grid.

This numerical artifact must be carefully distinguished from **physical dispersion**, which is a real property of the Earth. The Earth's materials are not perfectly elastic; they are viscoelastic, meaning they dissipate energy as waves pass through them. This attenuation is quantified by the [quality factor](@entry_id:201005), $Q$. Due to the principle of causality (as described by the Kramers-Kronig relations), any medium with physical attenuation must also be physically dispersive, meaning the true wave velocity depends on frequency . A successful simulation must minimize numerical dispersion so that it can accurately capture the true physical dispersion of the Earth model.

To control numerical dispersion, the grid must be fine enough to adequately resolve the shortest wavelengths of interest. A common practical rule is to require a minimum number of **points per wavelength**, $N_\lambda$. The minimum wavelength, $\lambda_{min}$, is determined by the maximum frequency of interest, $f_{max}$, and the *minimum* wave velocity in the model, $c_{min}$ (typically the shear-wave velocity, as S-waves have shorter wavelengths than P-waves at the same frequency). The relationship is:

$$
\lambda_{min} = \frac{c_{min}}{f_{max}}
$$

The required grid spacing $h$ is then chosen to satisfy the resolution criterion:

$$
h \le \frac{\lambda_{min}}{N_\lambda} = \frac{c_{min}}{f_{max} N_\lambda}
$$

A typical value for $N_\lambda$ in second-order schemes is between 5 and 10. This ensures that the numerical [phase velocity](@entry_id:154045) is close to the true velocity for all frequencies up to $f_{max}$ .

### Incorporating Physical Reality: Sources and Boundaries

A realistic simulation requires more than just a numerical engine for the wave equation; it must also include representations of the earthquake source and the physical boundaries of the domain, such as the Earth's free surface.

#### The Earthquake Source: Moment Tensors

An earthquake is a rapid slip on a fault, an internal failure process. Crucially, it generates no net force or [net torque](@entry_id:166772) on the surrounding medium. Modeling an earthquake with a simple [body force](@entry_id:184443) term, $f_i$, would violate this physical constraint, as a single point force (a force monopole) imparts net momentum .

The correct representation for an earthquake source in [elastodynamics](@entry_id:175818) is a **moment tensor**, $M_{ij}$. A moment tensor represents a system of force couples. The equivalent body force for a point moment tensor source located at $\mathbf{x}_0$ is not a simple force but a force dipole:

$$
f_i(\mathbf{x}, t) = - \frac{\partial}{\partial x_j} [M_{ij}(t) \delta(\mathbf{x} - \mathbf{x}_0)]
$$

This formulation automatically ensures zero net force. If the moment tensor is symmetric ($M_{ij} = M_{ji}$), it also guarantees zero net torque, consistent with the physics of faulting . In a finite difference code, this is implemented not by adding a force to a single grid point, but by adding stress contributions of opposite sign to adjacent grid cells, which discretely mimics the [divergence operator](@entry_id:265975) and preserves the zero-force property .

#### The Free Surface Boundary Condition

The Earth's surface is a boundary between solid rock/soil and the atmosphere. The vast difference in [acoustic impedance](@entry_id:267232) between the two media means that for [seismic waves](@entry_id:164985), the atmosphere exerts a negligible dynamic load on the ground. The principle of **[traction continuity](@entry_id:756091)** requires that the force per unit area (traction) be continuous across an interface. Since the air exerts negligible traction, the traction on the solid side of the boundary must be zero.

The traction vector $\mathbf{t}$ on a surface with [normal vector](@entry_id:264185) $\mathbf{n}$ is given by $t_i = \sigma_{ij}n_j$. For the Earth's surface at $z=0$, the [normal vector](@entry_id:264185) is $\mathbf{n} = (0, 0, 1)$. Setting the traction vector to zero ($t_x=t_y=t_z=0$) yields the three **stress-free boundary conditions** :

$$
\sigma_{xz}(z=0) = 0, \quad \sigma_{yz}(z=0) = 0, \quad \sigma_{zz}(z=0) = 0
$$

These conditions state that both the shear stresses and the [normal stress](@entry_id:184326) must vanish at the free surface. These are implemented in an FD code by modifying the difference stencils for grid points near the surface.

#### Artificial Absorbing Boundaries

While the free surface is a physical boundary, the other boundaries of our computational domain (bottom and sides) are artificial truncations of a much larger, effectively infinite Earth. Waves reaching these artificial boundaries must be absorbed without reflecting, to mimic the effect of an unbounded medium. Spurious reflections from these boundaries would contaminate the simulation and render it useless.

A simple approach is a **sponge layer**, where a damping term is added to the equations of motion in a zone near the boundary. This damps the [wave energy](@entry_id:164626). However, this damping also changes the [wave impedance](@entry_id:276571) of the medium, creating an impedance mismatch at the interface between the physical domain and the sponge layer, which itself causes reflections .

A more sophisticated and effective method is the **Perfectly Matched Layer (PML)**. A PML is an artificial absorbing layer designed to be reflectionless at its interface with the physical domain, at least in the continuous limit. This is achieved through a mathematical device known as [complex coordinate stretching](@entry_id:162960). The wave equation is modified within the PML region in such a way that the [wave impedance](@entry_id:276571) is perfectly matched at the interface, eliminating reflections. As a wave enters the PML, its amplitude is rapidly attenuated. In the time domain, implementing a PML requires introducing auxiliary memory variables or split fields to handle the frequency-dependent nature of the complex stretching . While [discretization](@entry_id:145012) introduces small, non-zero reflections, a well-designed PML can reduce boundary reflections to negligible levels, making it the state-of-the-art technique for [absorbing boundary conditions](@entry_id:164672) in FDTD modeling.