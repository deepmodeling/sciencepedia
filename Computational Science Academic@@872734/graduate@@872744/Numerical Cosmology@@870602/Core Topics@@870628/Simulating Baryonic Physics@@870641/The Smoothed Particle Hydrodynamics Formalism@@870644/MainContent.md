## Introduction
Smoothed Particle Hydrodynamics (SPH) stands as one of the most versatile and powerful numerical techniques for simulating fluid dynamics and related physical phenomena. As a Lagrangian, [mesh-free method](@entry_id:636791), it is uniquely suited for problems involving complex geometries, free surfaces, and enormous dynamic ranges, conditions that often challenge traditional grid-based approaches. Its ability to naturally concentrate computational effort where matter is dense has made it an indispensable tool in [computational astrophysics](@entry_id:145768) and cosmology, enabling groundbreaking simulations of galaxy formation, star birth, and cosmic structure evolution.

Despite its widespread use, mastering SPH requires a cohesive understanding that bridges its foundational mathematical principles, the array of advanced [numerical schemes](@entry_id:752822) developed to overcome its inherent challenges, and its broad applicability across scientific disciplines. This article addresses this need by providing a structured journey through the SPH formalism. It aims to connect the elegant theory of [kernel interpolation](@entry_id:751003) with the practical necessities of numerical stability and physical accuracy, revealing how a few core ideas blossom into a framework capable of tackling a vast spectrum of complex problems.

The reader will gain a multi-layered understanding of SPH across three distinct sections. The journey begins with **Principles and Mechanisms**, which deconstructs the formalism from first principles, building from the core concept of [kernel interpolation](@entry_id:751003) to the derivation of the [equations of motion](@entry_id:170720) and the advanced techniques required for modern simulations. Next, **Applications and Interdisciplinary Connections** explores the remarkable versatility of SPH, showcasing its power in its native domain of astrophysics before venturing into [magnetohydrodynamics](@entry_id:264274), multi-fluid systems, and surprising applications in geomechanics, [image processing](@entry_id:276975), and machine learning. Finally, **Hands-On Practices** provides a series of problems designed to solidify the theoretical concepts, challenging the reader to apply their knowledge to fundamental numerical tasks and validation tests.

## Principles and Mechanisms

Smoothed Particle Hydrodynamics (SPH) is a Lagrangian, mesh-free numerical method that models a continuous fluid as a set of discrete particles. In contrast to grid-based methods that solve equations at fixed spatial locations, SPH solves the fluid equations for each particle as it moves with the local flow. This chapter elucidates the fundamental principles of the SPH formalism, from the core concept of [kernel interpolation](@entry_id:751003) to the derivation of the equations of motion and the advanced mechanisms developed to address its inherent challenges.

### The Foundation: Kernel Interpolation and Particle Approximation

The conceptual cornerstone of SPH is the representation of any continuous field quantity, $A(\mathbf{r})$, through an integral interpolation procedure. This is achieved by convolving the field with a localized, symmetric smoothing function, or **kernel**, $W$, which has a characteristic width defined by the **smoothing length**, $h$. The integral representation of the field $A$ at a position $\mathbf{r}$ is given by:

$$
\langle A(\mathbf{r}) \rangle = \int_{\Omega} A(\mathbf{r'}) W(\mathbf{r} - \mathbf{r'}, h) \, dV'
$$

This expression represents a weighted average of the field $A$ in the neighborhood of $\mathbf{r}$, where the kernel function determines the weight. The kernel is typically designed to have **[compact support](@entry_id:276214)**, meaning it vanishes for distances greater than a multiple of the smoothing length, $h$. This localizes the interaction and makes the method computationally efficient.

To transition from the continuous integral to a discrete particle-based approximation, we discretize the fluid domain into a finite number of particles, each carrying a specific mass, $m_j$, and occupying a [volume element](@entry_id:267802) $dV_j$. The mass density of particle $j$, $\rho_j$, is related to its mass and volume by $\rho_j = m_j / dV_j$. Substituting $dV_j = m_j / \rho_j$ into the integral representation and replacing the integral with a summation over all particles $j$, we arrive at the general SPH summation formula for a quantity $A$ at the position of particle $i$, $\mathbf{r}_i$:

$$
A_i = \sum_j m_j \frac{A_j}{\rho_j} W(|\mathbf{r}_i - \mathbf{r}_j|, h_i)
$$

Here, $A_i$ and $A_j$ are the values of the quantity at particles $i$ and $j$, and $W_{ij}(h_i) \equiv W(|\mathbf{r}_i - \mathbf{r}_j|, h_i)$ is the kernel evaluated for the distance between the two particles, using the smoothing length of the target particle $i$.

The most fundamental application of this formula is the estimation of the mass density itself. By setting $A = \rho$, the SPH density estimator for particle $i$ becomes:

$$
\rho_i = \sum_j m_j \frac{\rho_j}{\rho_j} W_{ij}(h_i) = \sum_j m_j W_{ij}(h_i)
$$

This equation lies at the heart of the SPH method. It states that the density at a particle's location is a weighted sum of the masses of its neighboring particles, with the weights provided by the [smoothing kernel](@entry_id:195877).

### The Smoothing Kernel: Properties and Consistency

The accuracy and stability of the SPH method depend critically on the properties of the [smoothing kernel](@entry_id:195877) $W$. Several conditions are imposed on the kernel to ensure a reasonable and convergent approximation of the underlying continuum equations.

The most fundamental properties are:
- **Positivity**: $W(\mathbf{r}, h) \ge 0$. This ensures that densities are positive and aligns with the interpretation of the kernel as a probability density.
- **Compact Support**: There exists a constant $\kappa$ such that $W(\mathbf{r}, h) = 0$ for $|\mathbf{r}| > \kappa h$. This ensures that summations are performed over a finite number of neighbors, which is essential for [computational efficiency](@entry_id:270255).
- **Normalization (Zeroth Moment Condition)**: The kernel must integrate to unity.
  $$ \int_{\mathbb{R}^d} W(\mathbf{r}, h) \, d\mathbf{r} = 1 $$
- **Symmetry and Vanishing First Moment**: The kernel should be an [even function](@entry_id:164802), $W(-\mathbf{r}, h) = W(\mathbf{r}, h)$, which implies that its first moment vanishes.
  $$ \int_{\mathbb{R}^d} \mathbf{r} \, W(\mathbf{r}, h) \, d\mathbf{r} = \mathbf{0} $$

These [moment conditions](@entry_id:136365) are not arbitrary; they are directly linked to the **consistency** of the SPH approximation, which refers to its ability to exactly reproduce polynomial functions. By requiring the SPH interpolation of a general linear function $f(\mathbf{r}) = a + \mathbf{b} \cdot \mathbf{r}$ to be exact, one can derive these conditions from first principles. The exactness condition $\langle f(\mathbf{r}) \rangle = f(\mathbf{r})$ directly yields the normalization and vanishing first [moment conditions](@entry_id:136365) [@problem_id:526208].

The consistency order determines the approximation error. To see this, we can perform a Taylor [series expansion](@entry_id:142878) of a [smooth function](@entry_id:158037) $f(\mathbf{y})$ around a point $\mathbf{x}$ inside the continuous SPH integral. Let $\mathbf{s} = \mathbf{y} - \mathbf{x}$:
$$
f(\mathbf{y}) = f(\mathbf{x}) + (\nabla f)_{\mathbf{x}} \cdot \mathbf{s} + \frac{1}{2} \mathbf{s}^{\top} (\mathbf{H}f)_{\mathbf{x}} \mathbf{s} + \dots
$$
where $\mathbf{H}f$ is the Hessian matrix of second derivatives. Substituting this into the integral form and integrating term by term using the [moment conditions](@entry_id:136365) shows that the error in the approximation is:
$$
\langle f(\mathbf{x}) \rangle - f(\mathbf{x}) = \frac{1}{2} \sum_{i,j} \frac{\partial^2 f}{\partial x_i \partial x_j} \int s_i s_j W(\mathbf{s}, h) \, d\mathbf{s} + \mathcal{O}(h^3)
$$
If the second moment integral scales as $\mathcal{O}(h^2)$, which is standard for typical kernels, the [approximation error](@entry_id:138265) is $\mathcal{O}(h^2)$. This is known as **[second-order accuracy](@entry_id:137876)**. Exact reproduction of quadratic polynomials would require the second moment integral to be zero. However, for a positive kernel ($W \ge 0$), the integrand $s_i^2 W$ is non-negative, and its integral can only be zero if $W$ is a Dirac [delta function](@entry_id:273429), which is not a suitable [smoothing kernel](@entry_id:195877). Thus, a non-trivial, positive SPH kernel cannot reproduce quadratic polynomials exactly [@problem_id:3419997].

A crucial distinction exists between the continuous integral and the discrete particle sum. The elegant consistency properties of the continuous formulation are only guaranteed for the discrete particle approximation if the particle distribution itself satisfies the discrete [moment conditions](@entry_id:136365), such as the **discrete partition of unity**:
$$
\sum_j V_j W(\mathbf{x} - \mathbf{x}_j, h) \approx 1
$$
For irregular [particle distributions](@entry_id:158657), particularly near boundaries or in highly non-uniform regions, these discrete conditions are often violated. This violation leads to a degradation of accuracy and is a key source of error in basic SPH implementations [@problem_id:3419997].

### The SPH Equations of Motion

To simulate fluid dynamics, the SPH formalism is used to discretize the continuum conservation laws. In a Lagrangian frame, the time derivative follows the fluid particles.

#### The Continuity Equation

The SPH representation of the [continuity equation](@entry_id:145242), which describes how density changes in time, can be derived by taking the [total time derivative](@entry_id:172646) of the summation density estimator $\rho_i = \sum_j m_j W_{ij}$. Assuming constant particle masses and a fixed smoothing length for now, and applying the [chain rule](@entry_id:147422), we obtain:
$$
\frac{d\rho_i}{dt} = \sum_j m_j \frac{dW_{ij}}{dt} = \sum_j m_j \left( (\mathbf{v}_i - \mathbf{v}_j) \cdot \nabla_i W_{ij} \right)
$$
where $\mathbf{v}_{ij} = \mathbf{v}_i - \mathbf{v}_j$ is the [relative velocity](@entry_id:178060) between particles $i$ and $j$, and we have used the [antisymmetry](@entry_id:261893) of the kernel gradient ($\nabla_i W_{ij} = -\nabla_j W_{ij}$). This widely used form expresses the rate of density change at particle $i$ as a sum of contributions from the [relative motion](@entry_id:169798) of all its neighbors [@problem_id:3335721].

#### The Momentum Equation

The SPH momentum equation discretizes the pressure gradient term $-\nabla P$ from the Euler equations. A common, symmetrized form derived from a [variational principle](@entry_id:145218) (a discrete Lagrangian) that ensures manifest [momentum conservation](@entry_id:149964) is:
$$
\frac{d\mathbf{v}_i}{dt} = - \sum_j m_j \left( \frac{P_i}{\rho_i^2} + \frac{P_j}{\rho_j^2} \right) \nabla_i W_{ij}
$$
Here, the force on particle $i$ due to particle $j$ is proportional to the sum of their pressure terms and the gradient of the kernel. The structure ensures that the force $\mathbf{F}_{ij}$ is equal and opposite to $\mathbf{F}_{ji}$, conserving linear and angular momentum.

### Advanced Mechanisms and Practical Challenges

The basic SPH formalism, while elegant, faces several practical challenges. Modern SPH has developed a suite of advanced mechanisms to address these issues.

#### Adaptive Smoothing Lengths and "Grad-h" Terms

In astrophysical simulations involving gravitational collapse, density can vary by many orders of magnitude. A fixed smoothing length $h$ would be unable to resolve high-density regions while also sampling low-density regions. The solution is to use an **adaptive smoothing length**, $h_i$, for each particle. A common approach is to adjust $h_i$ to keep the number of neighbors within the kernel support, $n_{\text{ngb}}$, approximately constant.

Under the assumption of a locally uniform particle distribution, this condition implies an implicit relationship between density and smoothing length. For a $\nu$-dimensional space, this relationship is approximately [@problem_id:3498253]:
$$
\frac{\rho_i}{m} h_i^{\nu} \approx \text{const}
$$
Differentiating this relation implicitly allows us to find the derivative of the smoothing length with respect to density, a term crucial for consistent equations of motion:
$$
\frac{\partial h_i}{\partial \rho_i} = - \frac{h_i}{\nu \rho_i}
$$
When the smoothing length $h_i$ varies in time because it depends on the evolving density $\rho_i$, taking the time derivative of the summation density $\rho_i = \sum_j m_j W_{ij}(h_i)$ produces an additional term, often called a **"grad-h" term** [@problem_id:3534836]:
$$
\frac{d\rho_i}{dt} = \sum_j m_j (\mathbf{v}_{ij} \cdot \nabla_i W_{ij}) + \left( \frac{dh_i}{dt} \right) \sum_j m_j \frac{\partial W_{ij}}{\partial h_i}
$$
Since $dh_i/dt = (\partial h_i/\partial \rho_i) (d\rho_i/dt)$, the rate of change of density $d\rho_i/dt$ appears on both sides of the equation. Solving for it leads to a corrected continuity equation of the form $d\rho_i/dt = \Omega_i^{-1} (\dots)$, where the correction factor $\Omega_i$ depends on $\partial h_i/\partial \rho_i$ and the sum of kernel derivatives with respect to $h$. A fully consistent derivation from a Lagrangian formulation shows that these $\Omega$ correction factors must also appear in the [momentum equation](@entry_id:197225) to ensure energy conservation. Omitting these "grad-h" corrections leads to systematic conservation errors in simulations with adaptive smoothing lengths [@problem_id:3363392].

#### Capturing Shocks: Artificial Viscosity

The SPH equations derived from the inviscid Euler equations cannot naturally handle shocks, which are physical discontinuities. In a simulation, this would lead to unphysical particle interpenetration and large post-shock oscillations. The solution is to introduce a controlled amount of dissipation through **[artificial viscosity](@entry_id:140376) (AV)**.

The physical behavior of a shock is governed by the **Rankine-Hugoniot jump conditions**, which are derived from integrating the conservation laws across the discontinuity. For a steady, planar shock, these conditions state that the flux of mass, momentum, and energy are conserved across the shock front. Furthermore, the second law of thermodynamics demands that the specific entropy must increase across a physical shock ($s_2 > s_1$).

Artificial viscosity is an additional pressure term, typically dependent on the convergence of the flow ($\nabla \cdot \mathbf{v}$), that is added to the momentum and energy equations. It serves two critical functions [@problem_id:3465332]:
1.  **Momentum Dissipation**: It acts as a strong repulsive force between rapidly approaching particles, preventing interpenetration and mimicking the sharp deceleration of fluid across a shock. This enforces the momentum [jump condition](@entry_id:176163).
2.  **Energy Dissipation and Entropy Production**: The work done by the [viscous force](@entry_id:264591) is converted into internal energy, heating the post-shock gas. This dissipation ensures that total energy is conserved across the shock and, crucially, produces the irreversible increase in entropy required by physics.

The mass conservation equation itself is not directly modified by AV; the SPH continuity equation inherently handles mass flux continuity.

#### Pathologies and Correction Schemes

SPH is known to suffer from several numerical pathologies that can affect the accuracy and physical realism of simulations.

- **Boundary Errors**: Near free surfaces or domain boundaries, a particle's kernel support is incomplete. This truncation of the neighbor sum leads to a systematic underestimation of density and errors in the calculation of gradients, compromising the conservation properties of the scheme [@problem_id:3335721]. Common remedies include using "ghost" particles reflected from the boundary to complete the kernel support, or applying a **[renormalization](@entry_id:143501)** factor to the SPH sums to correct for the missing kernel volume.

- **Tensile Instability**: In regions of low pressure or negative pressure (tension), standard SPH can suffer from an unphysical clumping instability where particles pair up and form artificial voids. This can be understood by analyzing the [net force](@entry_id:163825) on a particle when it is slightly displaced from an equilibrium position. If the effective "stiffness" of the inter-particle force is negative, the force is anti-restoring and amplifies the perturbation. This stiffness can be shown to be proportional to the second derivative of the kernel, $W''(r)$ [@problem_id:526170]. If $W''(r)  0$ at typical neighbor separations, the system is unstable.

A more rigorous analysis reveals that the instability is linked to the Fourier transform of the kernel, $\widehat{W}(k)$. If $\widehat{W}(k)$ becomes negative for a wavenumber $k$ that can be resolved by the particle lattice (i.e., for wavelengths comparable to the inter-particle spacing), an attractive force arises, triggering the instability. Certain kernels, like the popular [cubic spline](@entry_id:178370), are known to be susceptible to this instability, especially with a low number of neighbors. Kernels like the Wendland family have been specifically designed to have positive Fourier transforms over a wider range of wavenumbers, making them more resistant to this clumping [@problem_id:3498257].

- **Consistency Correction with Moving Least Squares (MLS)**: As noted earlier, particle disorder leads to a loss of consistency. To restore [high-order accuracy](@entry_id:163460), one can employ correction schemes. One powerful method is **Moving Least Squares (MLS)**. The idea is to construct a local polynomial approximation that best fits the neighboring particle data in a kernel-weighted, least-squares sense. This is achieved by solving a small linear system for the polynomial coefficients at each evaluation point. The moment matrix of this system, $\mathbf{M}$, is constructed from the kernel weights and the polynomial basis functions evaluated at the neighbor positions [@problem_id:3498252].
$$
\mathbf{M}(\mathbf{r}_0) = \sum_{i} W_{i0} \, \boldsymbol{\phi}(\mathbf{r}_i - \mathbf{r}_0)\, \boldsymbol{\phi}(\mathbf{r}_i - \mathbf{r}_0)^{\top}
$$
By solving for the coefficients, one obtains a corrected value of the field at $\mathbf{r}_0$ that, by construction, guarantees the exact reproduction of any polynomial within the chosen basis (e.g., up to second order). This restores high-order consistency even for disordered particles and near boundaries, although it comes at an increased computational cost and requires careful handling of potentially ill-conditioned matrices [@problem_id:3498252].