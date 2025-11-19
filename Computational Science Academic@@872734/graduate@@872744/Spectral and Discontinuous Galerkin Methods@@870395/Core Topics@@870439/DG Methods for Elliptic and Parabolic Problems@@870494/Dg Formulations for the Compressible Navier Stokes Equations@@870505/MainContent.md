## Introduction
The Discontinuous Galerkin (DG) method has emerged as a powerful and versatile tool in [computational fluid dynamics](@entry_id:142614) (CFD), offering an elegant way to achieve [high-order accuracy](@entry_id:163460) on unstructured meshes. This makes it exceptionally well-suited for solving the compressible Navier-Stokes equations, which govern a vast range of fluid flow phenomena from [aerospace engineering](@entry_id:268503) to geophysical processes. However, the method's power comes with complexity; successfully applying DG requires a deep understanding of how to discretize both hyperbolic (convective) and parabolic (viscous) terms, ensure stability in the presence of nonlinearities and shocks, and implement the scheme efficiently. This article provides a comprehensive guide to the DG formulation for the compressible Navier-Stokes equations, bridging theoretical concepts with practical applications.

The journey begins in **Principles and Mechanisms**, where we will deconstruct the DG framework piece by piece. Starting with the [conservative form](@entry_id:747710) of the governing equations, we will explore the weak formulation, the crucial role of numerical fluxes for handling convective terms, and the distinct strategies—such as Interior Penalty and [mixed methods](@entry_id:163463)—for discretizing viscous effects. We will also address key implementation details and the theoretical underpinnings of the method's convergence.

Next, in **Applications and Interdisciplinary Connections**, we will showcase the framework's adaptability and power in solving real-world problems. This chapter demonstrates how the core formulation is extended to handle complex geometries, capture [shock waves](@entry_id:142404) robustly, and improve computational performance through advanced strategies like IMEX integration and hp-adaptation. We will explore its application in [turbulence modeling](@entry_id:151192), geophysical flows, reacting chemistry, and other frontier areas of scientific computing.

Finally, the article concludes with a series of **Hands-On Practices**. These guided problems are designed to solidify your understanding of critical concepts, from designing stable convective discretizations and [positivity-preserving limiters](@entry_id:753610) to developing [preconditioning techniques](@entry_id:753685) for all-speed flows. By working through these exercises, you will gain practical insight into the challenges and solutions at the heart of modern DG solvers.

## Principles and Mechanisms

The formulation of a Discontinuous Galerkin (DG) method for the compressible Navier-Stokes equations rests upon a clear understanding of the governing equations themselves, the principles of their discretization in a [discontinuous function](@entry_id:143848) space, and the specific mechanisms required to ensure stability and accuracy. This chapter elucidates these core principles, systematically building the DG framework from the continuous equations to the discrete algebraic system. We will explore the [conservative form](@entry_id:747710) of the equations, the choice of variables, the construction of numerical fluxes for both convective and diffusive terms, and key aspects of practical implementation and theoretical convergence.

### The Compressible Navier-Stokes Equations in Conservative Form

The foundation of any numerical method for fluid dynamics is the set of governing [partial differential equations](@entry_id:143134) (PDEs) that express the fundamental conservation laws. For a compressible, Newtonian fluid, these are the conservation of mass, momentum, and total energy. To facilitate numerical methods that can robustly handle discontinuities such as [shock waves](@entry_id:142404), it is essential to write these equations in **[conservative form](@entry_id:747710)**. This form ensures that the change in a conserved quantity within a [control volume](@entry_id:143882) is equal to the net flux of that quantity across the volume's boundary, plus any sources or sinks within the volume.

The compressible Navier-Stokes equations can be written compactly as:
$$
\partial_{t} U + \nabla \cdot F^{c}(U) = \nabla \cdot F^{v}(U, \nabla U) + S
$$
Here, $U$ is the vector of **[conserved variables](@entry_id:747720)**, $F^{c}(U)$ is the **convective (or inviscid) flux tensor**, $F^{v}(U, \nabla U)$ is the **viscous (or diffusive) flux tensor**, and $S$ is a vector of **source terms**. Let us define each of these components in a three-dimensional Cartesian coordinate system [@problem_id:3376463].

The vector of [conserved variables](@entry_id:747720) per unit volume is given by:
$$
U = \begin{pmatrix} \rho \\ \rho u_1 \\ \rho u_2 \\ \rho u_3 \\ \rho E \end{pmatrix}
$$
where $\rho$ is the fluid density, $\boldsymbol{u} = (u_1, u_2, u_3)^T$ is the velocity vector, and $E$ is the specific total energy. The total energy is the sum of the specific internal energy, $e$, and the specific kinetic energy: $E = e + \frac{1}{2}|\boldsymbol{u}|^2$.

The [convective flux](@entry_id:158187) tensor, $F^c$, represents the transport of [conserved quantities](@entry_id:148503) due to the bulk motion of the fluid. It can be written as a collection of three column vectors, where the $j$-th column is the flux vector in the $j$-th spatial direction:
$$
F^c_j(U) = \begin{pmatrix} \rho u_j \\ \rho u_1 u_j + p \delta_{1j} \\ \rho u_2 u_j + p \delta_{2j} \\ \rho u_3 u_j + p \delta_{3j} \\ (\rho E + p) u_j \end{pmatrix}
$$
Here, $p$ is the thermodynamic pressure and $\delta_{ij}$ is the Kronecker delta. The pressure term in the momentum flux arises from the isotropic forces exerted by the fluid, while the term $\rho E + p = \rho H$, where $H$ is the specific [total enthalpy](@entry_id:197863), appears in the [energy flux](@entry_id:266056).

The viscous flux tensor, $F^v$, accounts for momentum and [energy transport](@entry_id:183081) due to [molecular diffusion](@entry_id:154595), manifesting as viscous stresses and heat conduction. Its columns are the viscous flux vectors:
$$
F^v_j(U, \nabla U) = \begin{pmatrix} 0 \\ \tau_{1j} \\ \tau_{2j} \\ \tau_{3j} \\ \sum_{k=1}^3 \tau_{kj} u_k - q_j \end{pmatrix}
$$
The mass conservation equation has no [diffusive flux](@entry_id:748422). The [momentum flux](@entry_id:199796) components are the elements of the **[viscous stress](@entry_id:261328) tensor**, $\boldsymbol{\tau}$. The energy flux consists of two parts: the rate of work done by the viscous stresses, $\boldsymbol{\tau} \cdot \boldsymbol{u}$, and the **heat flux vector**, $\boldsymbol{q}$.

To close this system, we require [constitutive relations](@entry_id:186508) for $\boldsymbol{\tau}$ and $\boldsymbol{q}$. For a Newtonian fluid, the [viscous stress](@entry_id:261328) is assumed to be a linear, isotropic function of the [velocity gradient tensor](@entry_id:270928). The most general form involves two material coefficients, the dynamic (or shear) viscosity $\mu$ and the second coefficient of viscosity $\lambda$:
$$
\tau_{ij} = \mu \left( \frac{\partial u_i}{\partial x_j} + \frac{\partial u_j}{\partial x_i} \right) + \lambda (\nabla \cdot \boldsymbol{u}) \delta_{ij}
$$
This can be written more insightfully by decomposing the [rate-of-strain tensor](@entry_id:260652) into its deviatoric (trace-free) and isotropic (trace) parts. The **[bulk viscosity](@entry_id:187773)**, $\zeta$, is defined as $\zeta = \lambda + \frac{2}{3}\mu$. Taking the trace of the stress tensor reveals its physical meaning: $\mathrm{tr}(\boldsymbol{\tau}) = \tau_{kk} = (3\lambda + 2\mu)(\nabla \cdot \boldsymbol{u}) = 3\zeta(\nabla \cdot \boldsymbol{u})$. Thus, [bulk viscosity](@entry_id:187773) relates the mean viscous normal stress to the rate of fluid expansion or compression [@problem_id:3376443].

A common simplification is the **Stokes hypothesis**, which posits that the mechanical pressure (mean [normal stress](@entry_id:184326)) is equal to the thermodynamic pressure, implying that the trace of the viscous stress tensor is zero. This leads to $\zeta = 0$, which sets $\lambda = -\frac{2}{3}\mu$. Under this widely-used hypothesis, the [viscous stress](@entry_id:261328) tensor becomes:
$$
\tau_{ij} = \mu \left( \frac{\partial u_i}{\partial x_j} + \frac{\partial u_j}{\partial x_i} - \frac{2}{3} (\nabla \cdot \boldsymbol{u}) \delta_{ij} \right)
$$
This form is purely deviatoric and depends only on a single coefficient, the [shear viscosity](@entry_id:141046) $\mu$.

The heat flux vector, $\boldsymbol{q}$, is typically described by **Fourier's law of [heat conduction](@entry_id:143509)**, which states that heat flows from hotter to colder regions at a rate proportional to the temperature gradient:
$$
\boldsymbol{q} = -\kappa \nabla T
$$
where $\kappa$ is the thermal conductivity of the fluid and $T$ is the temperature.

Finally, the [source term](@entry_id:269111) vector $S$ accounts for external influences, such as a [body force](@entry_id:184443) per unit mass $\boldsymbol{f}$ (e.g., gravity) and a volumetric heat addition rate $s_Q$:
$$
S = \begin{pmatrix} 0 \\ \rho f_1 \\ \rho f_2 \\ \rho f_3 \\ \rho \boldsymbol{f} \cdot \boldsymbol{u} + s_Q \end{pmatrix}
$$

### Choice of Variables: Primitive vs. Conservative

While the DG scheme evolves the vector of [conserved variables](@entry_id:747720) $U$, many of the physical quantities and [constitutive relations](@entry_id:186508) are more naturally expressed in terms of **primitive variables**, such as the set $W = (\rho, \boldsymbol{u}, T)$ or $W' = (\rho, \boldsymbol{u}, p)$. For a system in [local thermodynamic equilibrium](@entry_id:139579), described by an [equation of state](@entry_id:141675) (e.g., the [ideal gas law](@entry_id:146757) $p = \rho R T$), these sets of variables are interchangeable. A crucial aspect of implementing a Navier-Stokes solver is understanding the mapping between these variable sets [@problem_id:3376445].

For a calorically perfect ideal gas, the specific internal energy is $e = c_v T$, where $c_v$ is the constant specific heat at constant volume. The conservative variable vector $U$ can be written in terms of the primitive variables $W = (\rho, \boldsymbol{u}, T)$ as:
$$
U(\boldsymbol{W}) = \begin{pmatrix} \rho \\ \rho \boldsymbol{u} \\ \rho (c_v T + \frac{1}{2}|\boldsymbol{u}|^2) \end{pmatrix}
$$
Conversely, given a physically realizable conservative state $U$ (i.e., with $\rho > 0$ and positive internal energy), we can uniquely recover the primitive variables $W$. This mapping, $U \leftrightarrow W$, is a smooth bijection, or a **[diffeomorphism](@entry_id:147249)**, on the space of physically admissible states. The existence of a smooth, invertible mapping is critical. A set like $(\rho, \boldsymbol{u}, p, T)$ is redundant for an ideal gas, as the variables are linked by the equation of state, and does not constitute a minimal set of independent variables. Conversely, a proposed "conservative" vector like $[\rho, \rho\boldsymbol{u}, p]^T$ is flawed because pressure does not obey a conservation law, and such a formulation would not be in [conservative form](@entry_id:747710) [@problem_id:3376445].

This transformation between variable sets is of great practical importance. For example, in [implicit time-stepping](@entry_id:172036) schemes, one must compute the Jacobian of the flux vector with respect to the conservative variables, $\partial F / \partial U$. Since the flux $F$ might be more easily expressed in terms of primitive variables $W$, the chain rule is indispensable:
$$
\frac{\partial F}{\partial U} = \frac{\partial F}{\partial W} \frac{\partial W}{\partial U} = \frac{\partial F}{\partial W} \left( \frac{\partial U}{\partial W} \right)^{-1}
$$
The existence and non-singularity of the transformation Jacobian $\partial U / \partial W$ guarantees that this procedure is well-defined. This applies to both the inviscid fluxes and the more complex viscous fluxes, whose Jacobians involve derivatives with respect to both the state and its gradient [@problem_id:3376445].

### The Discontinuous Galerkin Weak Formulation

The DG method begins by multiplying the governing PDE by a [test function](@entry_id:178872) $\phi_h$ from a specially designed [function space](@entry_id:136890) $V_h$ and integrating over a single computational element $K$. The space $V_h$ consists of functions that are polynomials of degree up to $p$ inside each element but are allowed to be discontinuous across element boundaries. For the convective term, this procedure yields:
$$
\int_K (\partial_t U) \phi_h \, d\boldsymbol{x} + \int_K (\nabla \cdot F^c(U)) \phi_h \, d\boldsymbol{x} = \dots
$$
Applying [integration by parts](@entry_id:136350) (the divergence theorem) to the flux term transforms it into a volume integral and a boundary integral:
$$
\int_K (\nabla \cdot F^c(U)) \phi_h \, d\boldsymbol{x} = -\int_K F^c(U) \cdot \nabla \phi_h \, d\boldsymbol{x} + \int_{\partial K} (F^c(U) \cdot \boldsymbol{n}) \phi_h \, dS
$$
where $\boldsymbol{n}$ is the outward-pointing unit normal to the element boundary $\partial K$. The crucial feature of DG arises in the boundary integral. Since the solution $U_h$ is discontinuous, it has two distinct values at any interior face: $U_h^-$ from the element on one side ("left") and $U_h^+$ from the other ("right"). This ambiguity means the physical flux $F^c(U) \cdot \boldsymbol{n}$ is not uniquely defined. The core idea of DG is to resolve this ambiguity by replacing the physical flux at the interface with a **numerical flux**, denoted $\widehat{F}(U_h^-, U_h^+, \boldsymbol{n})$.

### Discretization of the Inviscid Terms

The [numerical flux](@entry_id:145174) for the inviscid terms, $\widehat{F}^c(U_L, U_R, \boldsymbol{n})$, is the central component for discretizing the hyperbolic part of the Navier-Stokes equations. It acts as the communication mechanism between adjacent elements, enforcing the physics of wave propagation across interfaces. A well-designed [numerical flux](@entry_id:145174) must satisfy two fundamental properties [@problem_id:3376501]:
1.  **Consistency**: If the states on both sides of the interface are identical ($U_L = U_R = U$), the [numerical flux](@entry_id:145174) must reduce to the physical flux: $\widehat{F}^c(U, U, \boldsymbol{n}) = F^c(U) \cdot \boldsymbol{n}$. This ensures that the scheme is accurate for smooth solutions.
2.  **Conservation**: The flux from element A to element B must be the negative of the flux from B to A. This is typically expressed as an [anti-symmetry](@entry_id:184837) condition: $\widehat{F}^c(U_L, U_R, \boldsymbol{n}) = -\widehat{F}^c(U_R, U_L, -\boldsymbol{n})$. This property guarantees that when summing over all elements, fluxes across interior faces cancel out perfectly, leading to global [conservation of mass](@entry_id:268004), momentum, and energy.

Numerical fluxes are essentially approximate solutions to the local **Riemann problem** at each interface—a one-dimensional hyperbolic problem with the left and right states as initial data. Different approximations lead to different flux functions with varying properties of accuracy, robustness, and computational cost.

A simple yet robust example is the **local Lax-Friedrichs (or Rusanov) flux**. It is constructed by taking the average of the left and right physical fluxes and adding an [artificial dissipation](@entry_id:746522) term proportional to the jump in the [conserved variables](@entry_id:747720):
$$
\widehat{F}^c(U_L, U_R, \boldsymbol{n}) = \frac{1}{2} \left[ (F^c(U_L) \cdot \boldsymbol{n}) + (F^c(U_R) \cdot \boldsymbol{n}) \right] - \frac{1}{2} S_{\max} (U_R - U_L)
$$
The dissipation coefficient $S_{\max}$ must be large enough to stabilize the scheme. It is chosen as an upper bound on the local [signal propagation](@entry_id:165148) speed, typically the maximum of the spectral radii (largest absolute eigenvalues) of the flux Jacobians from the left and right states [@problem_id:3376449]. For the Euler equations, the normal wave speeds are $u_n$, $u_n+a$, and $u_n-a$, where $u_n = \boldsymbol{u} \cdot \boldsymbol{n}$ is the normal velocity and $a$ is the speed of sound. Thus, $S_{\max} = \max(|u_{n,L}|+a_L, |u_{n,R}|+a_R)$. While simple and robust, the Rusanov flux can be overly dissipative, smearing [contact discontinuities](@entry_id:747781).

More sophisticated fluxes offer better resolution. The **Roe flux** is based on a [local linearization](@entry_id:169489) of the Riemann problem, using a specially constructed "Roe average" state. It provides sharp resolution of discontinuities but requires an "[entropy fix](@entry_id:749021)" to handle sonic points correctly. The **HLLC (Harten-Lax-van Leer-Contact) flux** is a very popular choice; it extends the HLL flux by re-introducing the contact wave into its three-wave model. This allows HLLC to resolve contact and shear waves exactly, making it both robust and accurate for a wide range of flows [@problem_id:3376501]. In contrast, a simple central flux (the average part of the Rusanov flux without dissipation) is unconditionally unstable for hyperbolic problems.

### Discretization of the Viscous Terms

Discretizing the second-order viscous terms presents a different set of challenges. The viscous flux $F^v$ depends on the gradient of the state, $\nabla U$. In a DG framework, since $U_h$ is discontinuous, its gradient is ill-defined at element interfaces, containing Dirac delta functions. A naive formulation that only uses element-interior information would be non-conservative, as there would be no mechanism to enforce flux continuity between elements [@problem_id:3376502]. Two main strategies have emerged to overcome this.

#### Strategy 1: The Interior Penalty (IP) Method

The Interior Penalty method works directly with the second-order form of the equations. The most common variant is the **Symmetric Interior Penalty Galerkin (SIPG) method**. Starting from the weak form of the viscous operator, [integration by parts](@entry_id:136350) is applied once. This results in face integrals that involve both the solution values and their gradients. Using jump $[u] = u^- - u^+$ and average $\{u\} = \frac{1}{2}(u^- + u^+)$ operators, the SIPG formulation for a generic [diffusion operator](@entry_id:136699) $-\nabla \cdot (\kappa \nabla T)$ results in a [bilinear form](@entry_id:140194) $a(T, \phi)$:
$$
a(T, \phi) = \sum_{K} \int_K \kappa \nabla T \cdot \nabla \phi \, d\boldsymbol{x} - \sum_{F} \int_F \left( \{\kappa \nabla T \cdot \boldsymbol{n}\} [\phi] + \{\kappa \nabla \phi \cdot \boldsymbol{n}\} [T] \right) dS + \sum_{F} \int_F \sigma [T] [\phi] dS
$$
The first term is the standard Galerkin [volume integral](@entry_id:265381). The second term, containing the average of the flux and the jump of the [test function](@entry_id:178872) (and its symmetric counterpart), ensures consistency. The final term is the crucial **penalty term**. It penalizes jumps in the solution across faces, weighted by a [penalty parameter](@entry_id:753318) $\sigma$. This term provides the necessary inter-element coupling and ensures the [coercivity](@entry_id:159399) (and thus stability) of the discretization. For piecewise constant fields where gradients are zero inside the elements, this penalty term is the only non-zero contribution, demonstrating its central role in coupling the discontinuous solution [@problem_id:3376476].

#### Strategy 2: Mixed Formulations (LDG and BR2)

An alternative and very popular approach is to rewrite the single second-order PDE as a system of first-order PDEs. This is achieved by introducing an **auxiliary variable** for the gradient. For example, the viscous part of the system is reformulated as:
$$
\mathbf{Q} - \nabla U = \mathbf{0}
$$
$$
\partial_t U + \dots - \nabla \cdot F^v(U, \mathbf{Q}) = \mathbf{0}
$$
Now, both $U$ and the new variable $\mathbf{Q}$ are approximated as discontinuous polynomial fields. The DG method is then applied to this larger, first-order system. This elegant reformulation resolves the issue of defining gradients at interfaces. Both equations now involve only first derivatives, and a standard DG [discretization](@entry_id:145012) can be applied, leading to numerical fluxes for both $U$ and $\mathbf{Q}$ at the element interfaces. This provides the necessary coupling and, most importantly, maintains the conservative [divergence form](@entry_id:748608) of the physical equations, thereby ensuring discrete conservation of momentum and energy [@problem_id:3376502]. The **Local Discontinuous Galerkin (LDG)** method and the **Bassi-Rebay 2 (BR2)** scheme are prominent examples of this approach, differing in their specific choices of [numerical fluxes](@entry_id:752791) for the auxiliary system.

### Implementation in the Reference Element

For practical implementation, all computations are mapped to a standard **reference element**, $\hat{K}$, such as the square $[-1,1]^2$ in 2D. The solution within this element is represented using a [basis of polynomials](@entry_id:148579). In a **nodal DG** framework, the basis functions are Lagrange polynomials, $\ell_j(\boldsymbol{\xi})$, associated with a set of nodes (e.g., Gauss-Lobatto points). The solution is then stored simply as the vector of its values at these nodes.

Operations like differentiation are performed using pre-computed matrices. The gradient of a function in the 1D reference element is found by multiplying its vector of nodal values by a **[differentiation matrix](@entry_id:149870)**, $D$, whose entries are the derivatives of the basis functions evaluated at the nodes: $D_{ij} = \frac{d\ell_j}{d\xi}(\xi_i)$. In multiple dimensions, differentiation operators are built using tensor products of their 1D counterparts [@problem_id:3376458].

After computing a gradient in reference coordinates, $\nabla_{\boldsymbol{\xi}} U$, it must be transformed to physical coordinates using the chain rule and the Jacobian of the element mapping, $J = \partial \boldsymbol{x} / \partial \boldsymbol{\xi}$:
$$
\nabla_{\mathbf{x}} U = (J^{-1})^T \nabla_{\boldsymbol{\xi}} U
$$

A critical and subtle aspect of implementation is the evaluation of integrals, particularly the [volume integrals](@entry_id:183482) of nonlinear flux terms. If the solution is approximated by a polynomial of degree $p$, a quadratic flux term like $\rho \boldsymbol{u} \otimes \boldsymbol{u}$ results in a polynomial of degree $2p$. The volume integral in the weak form, $\int_K F^c(U_h) \cdot \nabla \phi_h \, d\boldsymbol{x}$, therefore involves an integrand of degree up to $p + (2p-1) = 3p-1$. An $N$-point Gaussian quadrature rule is exact only for polynomials up to degree $2N-1$. Thus, to compute the integral exactly, one must use a [quadrature rule](@entry_id:175061) with roughly $N \approx 3p/2$ points. Using fewer points (e.g., $N=p+1$, common in nodal DG) is called **under-integration**. This introduces **[aliasing](@entry_id:146322) errors**, where high-frequency content in the integrand is incorrectly represented as low-frequency modes. For nonlinear hyperbolic equations, this [aliasing error](@entry_id:637691) breaks discrete conservation properties and almost always leads to catastrophic **[nonlinear instability](@entry_id:752642)**, causing the simulation to fail. This instability is a volume effect and is not generally cured by dissipative fluxes on the element surfaces. To ensure robustness, one must either use a sufficiently accurate quadrature rule (**over-integration** or **[dealiasing](@entry_id:748248)**) or employ specially designed **split-form** or **entropy-stable** DG formulations that are stable even with under-integration [@problem_id:3376487].

### Theoretical Properties: A Brief Outlook on Convergence

A key motivation for using high-order DG methods is their ability to achieve high [rates of convergence](@entry_id:636873) for smooth solutions. A priori [error analysis](@entry_id:142477) provides a theoretical foundation for this expectation. For a sufficiently smooth solution to the compressible Navier-Stokes equations, a DG scheme using polynomials of degree $p$ on a mesh of characteristic size $h$ is expected to converge with an optimal rate in the $L^2$-norm [@problem_id:3376446]:
$$
\| U(T) - U_h(T) \|_{L^2(\Omega)} \le C h^{p+1}
$$
The constant $C$ depends on the smoothness of the exact solution, mesh regularity, and various parameters of the numerical scheme, but the rate of convergence, $p+1$, is determined by the polynomial approximation space. Crucially, the use of a consistent upwind-type inviscid flux (like Rusanov or HLLC) or a stable viscous [discretization](@entry_id:145012) (like SIPG) does not degrade this optimal [rate of convergence](@entry_id:146534) for smooth problems. While the amount of dissipation in the inviscid flux or the magnitude of the viscous penalty parameter will affect the size of the error constant $C$, they do not alter the asymptotic order of accuracy. This demonstrates that these schemes are not only stable but also highly accurate, making them a powerful tool for complex fluid dynamics simulations.