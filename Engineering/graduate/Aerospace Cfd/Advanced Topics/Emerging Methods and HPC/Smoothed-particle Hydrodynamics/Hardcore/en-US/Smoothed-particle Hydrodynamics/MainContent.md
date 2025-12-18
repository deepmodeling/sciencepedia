## Introduction
Smoothed-Particle Hydrodynamics (SPH) stands as a powerful and versatile computational method, offering a unique, mesh-free approach to simulating fluid dynamics and other continuum phenomena. As a fully Lagrangian technique, where the computational points (or "particles") move with the material, SPH naturally excels at tackling problems characterized by large deformations, [moving interfaces](@entry_id:141467), and complex free surfaces—scenarios that often pose significant challenges for traditional grid-based methods. Its intuitive particle-based framework has made it an indispensable tool in fields ranging from astrophysics to aerospace engineering. However, harnessing its full potential requires a deep understanding of its underlying mathematical principles, numerical subtleties, and practical implementation details. This article bridges the gap between theory and application, providing a structured journey into the world of SPH for graduate-level students and researchers.

We will begin by deconstructing the method in the **Principles and Mechanisms** chapter, where we build the SPH approximation from first principles, explore the discretization of the governing equations of fluid dynamics, and examine advanced formulations for specific physical regimes. Next, the **Applications and Interdisciplinary Connections** chapter will showcase the method's versatility by exploring its use in solving real-world problems in aerospace, geophysics, and multiphysics, highlighting how SPH is coupled with other methods to simulate complex systems. Finally, the **Hands-On Practices** section will provide targeted exercises that allow you to engage directly with the core concepts, from deriving kernel properties to verifying the accuracy of a complete simulation, solidifying your theoretical knowledge with practical computational skills.

## Principles and Mechanisms

This chapter delves into the foundational principles and numerical mechanisms that underpin the Smoothed-Particle Hydrodynamics (SPH) method. We will begin by constructing the SPH approximation from first principles, establishing the essential properties of the [smoothing kernel](@entry_id:195877). Subsequently, we will explore the process of discretizing continuum fields and [differential operators](@entry_id:275037), paying close attention to the concepts of [consistency and conservation](@entry_id:747722). Finally, we will examine advanced formulations designed to address specific physical challenges, such as incompressibility, shock waves, and boundary interactions, which are critical for the application of SPH in aerospace CFD and other demanding domains.

### The Kernel Approximation Framework

The central premise of SPH is to represent a continuous field by means of an integral interpolation, which smooths the field using a weighting function known as a **smoothing kernel**. For any scalar field $A(\mathbf{r})$, its SPH approximation at a point $\mathbf{r}$, denoted $\langle A(\mathbf{r}) \rangle$, is defined by the [convolution integral](@entry_id:155865):

$$
\langle A(\mathbf{r}) \rangle = \int_{\Omega} A(\mathbf{r}') W(\mathbf{r} - \mathbf{r}', h) \, dV'
$$

Here, $\Omega$ is the problem domain, $W$ is the smoothing kernel, and $h$ is a characteristic length scale called the **smoothing length**, which defines the spatial extent of the averaging. The [kernel function](@entry_id:145324) is not arbitrary; it must satisfy several fundamental properties to ensure the approximation is meaningful and convergent .

#### Fundamental Kernel Properties

To deduce these properties, we impose two basic requirements. First, the approximation must be able to reproduce a constant field exactly. If $A(\mathbf{r}) = C$, then:

$$
\langle C \rangle = C \int_{\Omega} W(\mathbf{r} - \mathbf{r}', h) \, dV'
$$

For $\langle C \rangle$ to equal $C$, the integral of the kernel over its entire support must be unity. This is the **[normalization condition](@entry_id:156486)** or **unity condition**:

$$
\int_{\Omega} W(\mathbf{s}, h) \, dV_s = 1
$$

Second, for the approximation to be a faithful representation, it must recover the exact pointwise value of the field in the limit that the smoothing scale vanishes. That is, $\lim_{h \to 0} \langle A(\mathbf{r}) \rangle = A(\mathbf{r})$. This requires the kernel to behave like the **Dirac delta distribution** in the limit $h \to 0$:

$$
\lim_{h \to 0} W(\mathbf{r}, h) = \delta(\mathbf{r})
$$

The [normalization condition](@entry_id:156486) is a prerequisite for this property. Furthermore, when interpolating physical quantities that are inherently non-negative, such as mass density, it is essential that the kernel itself be non-negative. This is the **positivity condition**, $W(\mathbf{r}, h) \ge 0$, which guarantees that a weighted sum of positive masses results in a positive density.

For computational efficiency, the kernel's influence is restricted to a finite region. This is achieved by selecting a kernel with **[compact support](@entry_id:276214)**, meaning it is zero beyond a certain radius, typically defined as a multiple of the smoothing length, $r_{\text{max}} = \kappa h$. A common choice is $\kappa=2$.

Finally, to ensure the normalization is independent of the smoothing length $h$, a specific scaling is adopted. Considering the dimensions, where $W$ has units of inverse volume ($[L]^{-d}$) in $d$ spatial dimensions, we define the kernel as $W(\mathbf{r}, h) = h^{-d} w(|\mathbf{r}|/h)$, where $w$ is a dimensionless profile function. This canonical form ensures that the normalization integral remains constant as $h$ is varied .

#### Common Kernel Functions

Numerous functions satisfy these criteria. A historically significant choice is the **[cubic spline kernel](@entry_id:748107)** (or Monaghan M4 spline), a [piecewise polynomial](@entry_id:144637) function that is $C^2$ continuous and has a [compact support](@entry_id:276214) of $2h$. While widely used, its Fourier transform is not strictly positive, which can be detrimental to the stability of certain [numerical schemes](@entry_id:752822).

More modern applications often favor **Wendland kernels**. These are a family of functions derived from the theory of radial basis functions that are specifically constructed to be positive definite, meaning their Fourier transform is positive. They are also compactly supported and can be designed to possess any desired degree of continuity (e.g., $C^2, C^4, C^6$), offering improved numerical stability and accuracy properties .

### Particle Discretization and Interpolation

To move from the continuum integral to a computable discrete form, SPH replaces the integral with a summation over a set of discrete points or "particles". Each particle $j$ carries a mass $m_j$ and occupies a volume element approximated by $\Delta V_j = m_j/\rho_j$, where $\rho_j$ is the density at its location $\mathbf{r}_j$. This particle [quadrature rule](@entry_id:175061) transforms the [convolution integral](@entry_id:155865) into a summation:

$$
\langle A(\mathbf{r}_i) \rangle \approx \sum_j A(\mathbf{r}_j) W(\mathbf{r}_i - \mathbf{r}_j, h) \Delta V_j
$$

Substituting the particle volume, we arrive at the standard SPH interpolation formula for a field $A$ at particle $i$:

$$
\langle A \rangle_i = \sum_j m_j \frac{A_j}{\rho_j} W_{ij}
$$

where $A_j = A(\mathbf{r}_j)$ and $W_{ij} = W(\mathbf{r}_i - \mathbf{r}_j, h)$. A special case of this is the **density summation**, which serves as the SPH definition of density itself. By setting $A = \rho$, the formula becomes:

$$
\rho_i = \sum_j m_j W_{ij}
$$

This is a weighted sum of the masses of neighboring particles, where the weights are given by the kernel function.

### Accuracy, Consistency, and Its Correction

The accuracy of the SPH approximation is formally assessed through **truncation [error analysis](@entry_id:142477)** and the concept of **consistency**. Consistency refers to the ability of the interpolation scheme to exactly reproduce polynomial fields of a certain degree.

#### Truncation Error and Continuum Consistency

For a sufficiently smooth field $f$, we can analyze the error of the *continuous* [kernel approximation](@entry_id:166372) by performing a Taylor series expansion of $f(\mathbf{r}_i + \mathbf{r})$ within the [convolution integral](@entry_id:155865) . This analysis reveals that for a symmetric, normalized kernel, the leading-order error term is:

$$
\langle f \rangle_i - f_i = \frac{C_2}{2d} h^2 \nabla^2 f_i + \mathcal{O}(h^4)
$$

where $d$ is the number of spatial dimensions and $C_2$ is a constant related to the second moment of the kernel profile. This result is profound: it demonstrates that the SPH interpolation method is formally **second-order accurate** in $h$ for smooth fields.

The conditions required for this level of accuracy can be stated in terms of kernel moments .
- **Zeroth-order consistency**, the ability to reproduce a [constant function](@entry_id:152060) ($f=C$), requires the zeroth moment of the kernel to be unity: $\int W(\mathbf{r},h) dV = 1$. This is the [normalization condition](@entry_id:156486).
- **First-order consistency**, the ability to reproduce a linear function ($f=\mathbf{a} \cdot \mathbf{r} + b$), additionally requires the first moment of the kernel to be zero: $\int \mathbf{r} W(\mathbf{r},h) dV = \mathbf{0}$. For any radially symmetric kernel, this condition is automatically satisfied.

#### Particle Inconsistency

A critical subtlety arises when we move from the continuum integral to the discrete particle sum. The discrete conditions for zeroth and first-order consistency become :

$$
\text{Zeroth-order: } \sum_j \frac{m_j}{\rho_j} W_{ij} = 1
$$

$$
\text{First-order: } \sum_j \frac{m_j}{\rho_j} (\mathbf{x}_i - \mathbf{x}_j) W_{ij} = \mathbf{0}
$$

Unlike in the continuum case, these conditions are **not** automatically satisfied for an arbitrary, disordered distribution of particles. The asymmetry in the neighbor distribution around particle $i$ leads to non-zero sums, resulting in a loss of consistency. This **particle inconsistency** is a fundamental source of error in the standard SPH formulation and is a primary motivation for the development of numerous correction methods.

### Discretization of Governing Equations

The SPH framework is used to discretize the partial differential equations of fluid dynamics by developing particle-based approximations for [differential operators](@entry_id:275037) like the gradient, divergence, and Laplacian. A guiding principle in this process is the formulation of operators that inherently conserve physical quantities.

#### Conservation through Symmetric Operators

The conservation of linear and angular momentum is fundamental to mechanics. In SPH, this is achieved by constructing force terms that are pairwise symmetric and satisfy Newton's third law. The standard SPH approximation for the acceleration due to a pressure gradient is a prime example :

$$
\frac{d\mathbf{v}_i}{dt} = - \sum_{j} m_j \left( \frac{P_i}{\rho_i^2} + \frac{P_j}{\rho_j^2} \right) \nabla_i W_{ij}
$$

Here, the term $\left( \frac{P_i}{\rho_i^2} + \frac{P_j}{\rho_j^2} \right)$ is symmetric upon swapping indices $i$ and $j$. The kernel gradient is antisymmetric, $\nabla_i W_{ij} = - \nabla_j W_{ij}$. The resulting force exerted on particle $i$ by particle $j$, $\mathbf{F}_{ij}$, is exactly equal and opposite to the force exerted on $j$ by $i$, $\mathbf{F}_{ji}$. This ensures that the total linear momentum of an [isolated system](@entry_id:142067) is perfectly conserved. Furthermore, because this force is central (acting along the line connecting the particles), total angular momentum is also exactly conserved. This robust conservation property is a major strength of the SPH method.

#### The Continuity Equation

The SPH form of the continuity equation can be derived by taking the [material derivative](@entry_id:266939) of the density summation formula, $\rho_i = \sum_j m_j W_{ij}$. Assuming constant particle masses and a constant smoothing length $h$, this yields :

$$
\frac{d\rho_i}{dt} = \sum_j m_j (\mathbf{v}_i - \mathbf{v}_j) \cdot \nabla_i W_{ij}
$$

This equation provides a means to evolve density in time. In practice, simulators may choose between two approaches:
1.  **Density Summation:** Recalculate $\rho_i = \sum_j m_j W_{ij}$ at every time step. This method is robust and ensures the density is always consistent with the current particle positions, but it can lead to noisy pressure fields as particles enter or leave a kernel's support.
2.  **Continuity Integration:** Integrate the discrete continuity equation in time. This typically produces smoother density and pressure fields but is susceptible to the accumulation of [numerical integration](@entry_id:142553) errors over long simulations, causing the density to "drift" from the value given by the summation.

This choice becomes more complex if the smoothing length $h$ is allowed to vary, as this introduces additional terms into the continuity equation. In such cases, density summation is often preferred for its inherent robustness .

#### Second Derivative Operators

Accurately modeling second-derivative terms, such as those in viscous diffusion ($\nabla \cdot (\nu \nabla \mathbf{v})$) or heat conduction ($\nabla \cdot (\kappa \nabla T)$), is a well-known challenge in SPH. A straightforward approach of applying the SPH formalism twice is highly sensitive to particle disorder. Several alternative formulations have been developed . One popular form, often attributed to Brookshaw and generalized by Morris for variable diffusivity $\kappa$, is:

$$
\langle \nabla \cdot (\kappa \nabla \phi) \rangle_i = \sum_j m_j \frac{\kappa_i + \kappa_j}{\rho_j} \frac{\phi_i - \phi_j}{|\mathbf{r}_{ij}|^2 + \eta^2} \mathbf{r}_{ij} \cdot \nabla_i W_{ij}
$$

(Note: The expression has been simplified for clarity and presented in a common variant). A formal truncation [error analysis](@entry_id:142477) shows that under quasi-uniform particle arrangements, this operator, along with several others, is second-order accurate ($O(h^2)$). These formulations transform the problematic second derivative into expressions involving differences between particle values and the kernel gradient, which are generally more stable .

### Advanced Formulations and Physical Regimes

Standard SPH must be adapted to handle specific [flow regimes](@entry_id:152820) common in aerospace applications, such as incompressible flows and flows with shock waves.

#### Incompressible vs. Weakly Compressible SPH

Modeling truly [incompressible flow](@entry_id:140301) (where $\nabla \cdot \mathbf{v} = 0$) is challenging in SPH. Two dominant approaches have emerged :

1.  **Weakly Compressible SPH (WCSPH):** This is the most common approach. Instead of enforcing incompressibility strictly, it allows for very small [density fluctuations](@entry_id:143540) (typically less than 1%). This is achieved by using a stiff "artificial" equation of state that relates pressure directly to density, such as $P = c_0^2 (\rho - \rho_0)$, where $c_0$ is an artificial speed of sound. The drawback is that this introduces artificial sound waves that propagate at speed $c_0$. For an [explicit time integration](@entry_id:165797) scheme, stability requires the time step $\Delta t$ to respect the Courant-Friedrichs-Lewy (CFL) condition, $\Delta t \lesssim h / c_0$. To keep density variations small, $c_0$ must be large (typically $c_0 \gtrsim 10 U_{\text{max}}$), which imposes a severe restriction on the time step.

2.  **Incompressible SPH (ISPH):** This approach enforces [incompressibility](@entry_id:274914) more directly. In a common variant, a two-step [projection method](@entry_id:144836) is used. First, velocities are advanced in time considering only viscous and [body forces](@entry_id:174230). This intermediate velocity field is not [divergence-free](@entry_id:190991). Second, a **Pressure Poisson Equation (PPE)** is formulated and solved to find a pressure field that, when applied as a correction, projects the velocity field onto a divergence-free space. While ISPH eliminates the stringent acoustic time-step restriction of WCSPH (the time step is limited by fluid convection and viscosity), it requires solving a large sparse linear system for the pressure at each step, which is computationally more demanding.

#### Shock Capturing and Artificial Viscosity

The Euler equations governing inviscid [compressible flow](@entry_id:156141) are non-dissipative, yet their solutions can develop discontinuities (shocks). A central-difference-like numerical scheme, such as standard SPH, will produce unphysical oscillations at these shocks. To obtain a stable and physically correct solution, a dissipative mechanism must be introduced, a role played by **artificial viscosity** .

The need for this dissipation is rooted in the mathematical theory of [hyperbolic conservation laws](@entry_id:147752), which requires that physical [weak solutions](@entry_id:161732) satisfy an **entropy condition**. The [artificial viscosity](@entry_id:140376) term in SPH acts as a numerical realization of the "vanishing viscosity" principle, adding dissipation precisely in regions of strong compression. A standard form, developed by Monaghan, adds a pressure-like term $\Pi_{ij}$ to the momentum equation that is non-zero only for approaching particles ($\mathbf{v}_{ij} \cdot \mathbf{r}_{ij}  0$). This term provides the necessary entropy production to capture shocks smoothly and without oscillation. Critically, this [artificial viscosity](@entry_id:140376) is constructed to be symmetric and pairwise, thus preserving the exact conservation of linear and angular momentum. Its function is analogous to the numerical diffusion found in upwind finite volume schemes like the Rusanov (or Lax-Friedrichs) flux .

#### Tensile Instability

A notorious pathology of standard SPH is the **[tensile instability](@entry_id:163505)**, an unphysical clumping of particles that occurs in regions of negative pressure . This can be analyzed via a [linear stability analysis](@entry_id:154985) of a 1D lattice of particles. When subjected to a tensile state ($P_0  0$), the analysis shows that small perturbations in particle positions lead to an imaginary wave frequency $\omega$, i.e., $\omega^2  0$. This corresponds to modes that grow exponentially in time, manifesting as particle clustering. The dispersion relation for these perturbations can be derived as :

$$
\omega^2(k) = C \cdot P_0 \cdot \sin^2\left(\frac{k \Delta x}{2}\right)
$$

where $C$ is a positive constant depending on kernel properties, $k$ is the wavenumber, and $\Delta x$ is the particle spacing. Since $P_0  0$, $\omega^2$ is negative for almost all wavenumbers, indicating widespread instability. This is a fundamental mechanism that requires special treatment, either through modified force laws or the addition of a small background pressure.

### Boundary Conditions

Properly modeling the interaction between the fluid and solid boundaries is crucial for any practical simulation but is particularly challenging in a meshfree method like SPH. The primary issue is **kernel truncation**: for a particle near a boundary, its kernel support is cut off by the boundary, leading to an incomplete sum over neighbors. This results in an erroneous underestimation of density and incorrect forces. Several strategies have been devised to counteract this .

1.  **Mirror (Ghost) Particles:** For each fluid particle near a boundary, one or more "ghost" particles are created virtually on the other side of the boundary. The properties of these ghost particles are set to enforce the desired physical boundary conditions. For example, to enforce a no-slip condition ($\mathbf{v}_{\text{fluid}} = \mathbf{v}_{\text{wall}}$) at a moving wall, the ghost particle velocity is set to $\mathbf{v}_{\text{ghost}} = 2\mathbf{v}_{\text{wall}} - \mathbf{v}_{\text{fluid}}$. This "anti-mirror" rule ensures that the interpolated velocity at the wall is exactly the wall velocity. To provide the necessary pressure support to prevent fluid penetration, the ghost particle's density and pressure are typically set equal to those of its corresponding fluid particle ($\rho_{\text{ghost}} = \rho_{\text{fluid}}$).

2.  **Dynamic Boundary Particles:** This strategy involves placing one or more layers of particles directly on the solid boundary. These particles have a prescribed velocity (e.g., the velocity of the wall) but participate in the SPH interactions with the fluid. The [no-penetration condition](@entry_id:191795) is enforced naturally: as fluid particles approach the boundary, the density of the boundary particles increases via the continuity equation, leading to a large repulsive pressure force. The no-slip condition is enforced through viscous [interaction terms](@entry_id:637283) between the fluid and boundary particles, which act to damp the relative velocity. This method provides a more dynamic and physically-based boundary interaction but is often more complex to implement than the ghost particle approach.