## Introduction
The accurate simulation of [wave propagation](@entry_id:144063) is fundamental to many fields, from geophysics to aerospace engineering. While numerous numerical methods exist, the Discontinuous Galerkin (DG) method has emerged as a particularly powerful and flexible framework, prized for its [high-order accuracy](@entry_id:163460), [robust stability](@entry_id:268091), and ability to handle complex geometries. However, harnessing its full potential requires a deep understanding of its formulation, from its physical underpinnings to its advanced algorithmic implementations. This article addresses the need for a comprehensive guide by systematically building the DG formulation for the [acoustic wave equation](@entry_id:746230).

The journey begins in the "Principles and Mechanisms" chapter, where we will derive the governing acoustic equations and establish the core DG weak formulation. You will learn about the critical role of [numerical fluxes](@entry_id:752791) in ensuring stability through discrete energy analysis. Next, the "Applications and Interdisciplinary Connections" chapter will demonstrate how this theoretical framework is applied to solve real-world problems, covering the modeling of physical boundaries, alternative DG discretizations, and crucial connections to high-performance and adaptive computing. Finally, the "Hands-On Practices" section provides targeted exercises to solidify your understanding of key concepts, translating theory into practical skill. By the end, you will have a thorough grasp of how to construct, analyze, and apply DG methods for acoustic wave simulation.

## Principles and Mechanisms

This chapter delves into the fundamental principles and underlying mechanisms of Discontinuous Galerkin (DG) formulations for the [acoustic wave equation](@entry_id:746230). We will begin by establishing the governing equations from first principles, explore their inherent mathematical structure related to energy conservation and [hyperbolicity](@entry_id:262766), and then construct the DG framework upon this foundation. A central focus will be placed on the role of numerical fluxes in ensuring stability and the methods for analyzing the discrete system's properties, including [energy dissipation](@entry_id:147406), accuracy, and behavior in complex scenarios.

### The Governing Equations of Linear Acoustics

The propagation of small-amplitude sound waves in a fluid can be described by linearizing the compressible Euler equations, which express the [conservation of mass](@entry_id:268004), momentum, and energy. We consider linearization around a quiescent base state of uniform density $\rho_0$ and pressure $p_0$. Assuming the perturbations are small and the process is isentropic (constant entropy), we can derive a [first-order system](@entry_id:274311) of partial differential equations governing the acoustic pressure perturbation, $p$, and the fluid velocity perturbation, $\boldsymbol{u}$.

This derivation [@problem_id:3375709] yields the first-order linear acoustic system:
$$
\begin{aligned}
\partial_t p + \rho_0 c^2 \nabla \cdot \boldsymbol{u} = 0 \\
\rho_0 \partial_t \boldsymbol{u} + \nabla p = 0
\end{aligned}
$$
Here, $c$ is the isentropic speed of sound, defined by the thermodynamic derivative $c^2 = (\partial p / \partial \rho)_s$ evaluated at the base state. For clarity and generality, we can express this system using the [bulk modulus](@entry_id:160069) $\kappa = \rho_0 c^2$ and density $\rho = \rho_0$. By dividing the momentum equation by $\rho$, we obtain the velocity-pressure [first-order system](@entry_id:274311):
$$
\begin{aligned}
\partial_t p + \kappa \nabla \cdot \boldsymbol{u} = 0 \\
\partial_t \boldsymbol{u} + \frac{1}{\rho} \nabla p = 0
\end{aligned}
$$
This set of equations forms a linear hyperbolic system, which is the mathematical starting point for our DG formulation. It can be written in a compact vector form $\partial_t \mathbf{w} + \sum_{j=1}^{d} A_j \partial_{x_j} \mathbf{w} = \mathbf{0}$, where $\mathbf{w} = (p, u_1, \dots, u_d)^T$ is the state vector and the $A_j$ are constant coefficient matrices.

### Energy Conservation and Hyperbolic Structure

A cornerstone property of the acoustic system is the conservation of energy. The total acoustic energy $E(t)$, comprising potential energy stored in compression and kinetic energy of fluid motion, is defined as:
$$
E(t) = \int_{\Omega} \left( \frac{p^2}{2\kappa} + \frac{\rho |\boldsymbol{u}|^2}{2} \right) \mathrm{d}\boldsymbol{x}
$$
By taking the time derivative of $E(t)$ and substituting the governing equations, one can show that the rate of change of energy within the domain $\Omega$ is entirely due to the flux of energy across its boundary $\partial\Omega$ [@problem_id:3375705]:
$$
\frac{\mathrm{d}E}{\mathrm{d}t} = - \int_{\partial\Omega} p (\boldsymbol{u} \cdot \boldsymbol{n}) \mathrm{d}S
$$
where $\boldsymbol{n}$ is the outward unit normal. For a [closed system](@entry_id:139565), or one with appropriate non-dissipative boundary conditions (e.g., a rigid wall where $\boldsymbol{u} \cdot \boldsymbol{n} = 0$, or a pressure-release surface where $p=0$), the boundary integral vanishes, and the total energy $E(t)$ is conserved. This conservation law is a fundamental physical principle that a robust numerical scheme should respect or mimic in a controlled manner.

The hyperbolic nature of the system is most clearly revealed through its characteristic properties. In one spatial dimension, the system decouples into two independent advection equations by introducing **[characteristic variables](@entry_id:747282)**. Defining the [acoustic impedance](@entry_id:267232) $Z = \rho c$, the [characteristic variables](@entry_id:747282) $w^{\pm} = p \pm Z u$ represent right-going and left-going waves, respectively. A direct substitution into the 1D acoustic equations shows that they satisfy simple advection equations [@problem_id:3375744]:
$$
\partial_t w^+ + c \partial_x w^+ = 0 \quad \text{and} \quad \partial_t w^- - c \partial_x w^- = 0
$$
This means that $w^+$ is constant along lines where $x - ct$ is constant, and $w^-$ is constant along lines where $x+ct$ is constant. This decomposition of the solution into propagating waves is central to understanding the physics and to constructing physically-motivated numerical methods.

In multiple dimensions, this structure is captured by the concept of **symmetrizability**. A crucial property for energy analysis is the existence of a [symmetric positive-definite matrix](@entry_id:136714) $H$, known as a **symmetrizer**, which relates the system to the conserved energy. For the acoustic system, the [quadratic form](@entry_id:153497) $\frac{1}{2}\mathbf{w}^T H \mathbf{w}$ must correspond to the physical energy density. This requirement uniquely determines the symmetrizer to be a diagonal matrix [@problem_id:3375709]:
$$
H = \text{diag}\left(\frac{1}{\rho c^2}, \rho, \dots, \rho\right) = \text{diag}\left(\frac{1}{\kappa}, \rho, \dots, \rho\right)
$$
The existence of such a symmetrizer confirms that the system is not just hyperbolic but symmetric hyperbolic, a stronger condition that provides a direct path to proving the stability of [numerical schemes](@entry_id:752822) via [energy methods](@entry_id:183021). The matrix $H$ defines the natural inner product, or energy norm, in which stability is analyzed.

### The Discontinuous Galerkin Weak Formulation

The Discontinuous Galerkin method begins by partitioning the spatial domain $\Omega$ into a mesh $\mathcal{T}_h$ of non-overlapping elements $K$. The core feature of DG is that the approximate solution is sought in a space of functions that are polynomials on each element but are allowed to be discontinuous across element boundaries [@problem_id:3375703].

To obtain the semi-discrete DG formulation, we multiply the governing equations by a [test function](@entry_id:178872) from the same [polynomial space](@entry_id:269905) and integrate over a single element $K$. For the pressure equation, this gives:
$$
\int_K (\partial_t p_h) v_h \, \mathrm{d}\boldsymbol{x} + \int_K (\kappa \nabla \cdot \boldsymbol{u}_h) v_h \, \mathrm{d}\boldsymbol{x} = 0
$$
Here, $p_h$, $\boldsymbol{u}_h$, and $v_h$ are polynomial approximations. Applying the divergence theorem (integration by parts) to the second term transfers the spatial derivative from the state variable $\boldsymbol{u}_h$ to the [test function](@entry_id:178872) $v_h$:
$$
\int_K (\partial_t p_h) v_h \, \mathrm{d}\boldsymbol{x} - \int_K \kappa \boldsymbol{u}_h \cdot \nabla v_h \, \mathrm{d}\boldsymbol{x} + \int_{\partial K} \kappa (\boldsymbol{u}_h \cdot \boldsymbol{n}) v_h \, \mathrm{d}S = 0
$$
The boundary integral term $\int_{\partial K} \kappa (\boldsymbol{u}_h \cdot \boldsymbol{n}) v_h \, \mathrm{d}S$ is the critical component. Because the solution is discontinuous, the trace of $\boldsymbol{u}_h$ on the boundary $\partial K$ is double-valued at interfaces between elements. To resolve this ambiguity and define a unique coupling mechanism, we replace the physical flux term $\kappa(\boldsymbol{u}_h \cdot \boldsymbol{n})$ with a **[numerical flux](@entry_id:145174)**, denoted by a star $(\cdot)^*$. The numerical flux is a single-valued function that depends on the states from both sides of the interface, which we denote by $(\cdot)^-$ and $(\cdot)^+$. The final weak form for the pressure equation is then:
$$
\int_K (\partial_t p_h) v_h \, \mathrm{d}\boldsymbol{x} - \int_K \kappa \boldsymbol{u}_h \cdot \nabla v_h \, \mathrm{d}\boldsymbol{x} + \int_{\partial K} (\kappa u_n)^* v_h \, \mathrm{d}S = 0
$$
A similar equation is derived for the [momentum equation](@entry_id:197225). This system of [ordinary differential equations](@entry_id:147024) for the polynomial coefficients on each element defines the DG [semi-discretization](@entry_id:163562).

### Numerical Fluxes for Stability and Accuracy

The choice of numerical flux is the most important decision in designing a DG scheme, as it dictates stability and accuracy. A [numerical flux](@entry_id:145174) must be **consistent**, meaning that if the states from both sides of an interface are identical, it reduces to the original physical flux.

A simple choice is the **central flux**, which takes the average of the states from both sides (e.g., $\boldsymbol{u}^* = \{\boldsymbol{u}\} \equiv (\boldsymbol{u}^- + \boldsymbol{u}^+)/2$). While consistent, this flux does not introduce any [numerical dissipation](@entry_id:141318) and typically leads to unstable schemes for hyperbolic problems.

To achieve stability, dissipative terms must be added. The **Local Lax-Friedrichs (LLF)** or **Rusanov flux** augments the central flux with a penalty term proportional to the jump in the solution variables:
$$
(\kappa u_n)^* = \kappa \{u_n\} - \frac{\alpha}{2} [p] \qquad \text{and} \qquad (p/\rho)^* = \{p/\rho\} - \frac{\alpha}{2} [u_n]
$$
Here, $[\cdot]$ denotes the [jump operator](@entry_id:155707), e.g., $[p] = p^+ - p^-$. The parameter $\alpha$ controls the amount of dissipation. For the scheme to be stable, this dissipation must be strong enough to damp any potential instabilities. An analysis based on the system's [characteristic speeds](@entry_id:165394) shows that the scheme is energy-stable provided $\alpha$ is greater than or equal to the maximum characteristic speed normal to the interface [@problem_id:3375743]. For the acoustic system, the normal [characteristic speeds](@entry_id:165394) are $\pm c$, so the stability condition is $\alpha \ge c$.

A more physically grounded choice is the **[upwind flux](@entry_id:143931)**, which is derived directly from the [characteristic decomposition](@entry_id:747276) of the system. It mimics the physical [wave propagation](@entry_id:144063) by constructing an interface state that selectively uses the information arriving at the interface from each side. For 1D [acoustics](@entry_id:265335), the interface state $(p^*, u^*)$ is determined by enforcing that the right-going characteristic ($p+Zu$) comes from the left state and the left-going characteristic ($p-Zu$) comes from the right state [@problem_id:3375744]. This leads to the unique upwind interface state:
$$
p^* = \{p\} - \frac{Z}{2}[u] \qquad \text{and} \qquad u^* = \{u\} - \frac{1}{2Z}[p]
$$
The [upwind flux](@entry_id:143931) is naturally dissipative and forms the basis for many robust and accurate DG schemes.

### Discrete Energy Analysis

The stability of a DG formulation can be rigorously proven by demonstrating that a discrete version of the acoustic energy is non-increasing in time. The discrete energy is defined by simply substituting the DG polynomial solution into the continuous [energy functional](@entry_id:170311):
$$
E_h(t) = \sum_{K \in \mathcal{T}_h} \int_K \left( \frac{p_h^2}{2\kappa} + \frac{\rho |\boldsymbol{u}_h|^2}{2} \right) \mathrm{d}\boldsymbol{x}
$$
By taking the time derivative of $E_h(t)$ and substituting the DG weak form, it can be shown that the rate of change of discrete energy is a sum of integrals over all the faces in the mesh. For a stable [numerical flux](@entry_id:145174), the contribution from each interface is non-positive. This guarantees that the total discrete energy does not grow, i.e., $\mathrm{d}E_h/\mathrm{d}t \le 0$, which implies stability.

The interface contribution to the [energy balance](@entry_id:150831) can be explicitly calculated. For the [upwind flux](@entry_id:143931), the [energy dissipation](@entry_id:147406) rate at an interface is a [positive definite](@entry_id:149459) [quadratic form](@entry_id:153497) in the jumps of the solution variables [@problem_id:3375715]:
$$
\frac{\mathrm{d}E_h}{\mathrm{d}t}\bigg|_{\text{interface}} = - \int_F \left( \frac{1}{2Z}[p]^2 + \frac{Z}{2}[u_n]^2 \right) \mathrm{d}S \le 0
$$
This term represents the rate at which energy is removed from the system by the numerical scheme at interfaces where the solution is discontinuous. This controlled dissipation is the mechanism that ensures the stability of the DG method.

### Implementation and Advanced Considerations

Several practical and advanced topics are crucial for the successful application of DG methods.

#### Polynomial Bases and Quadrature
The choice of basis functions for the [polynomial space](@entry_id:269905) within each element has significant computational implications [@problem_id:3375703].
- A **[modal basis](@entry_id:752055)**, typically built from [orthogonal polynomials](@entry_id:146918) like Legendre polynomials, is advantageous because the element mass matrix $M_{ij} = \int_K \phi_i \phi_j \, d\mathbf{x}$ becomes diagonal for affine elements, simplifying the inversion required in each time step.
- A **nodal basis**, built from Lagrange polynomials centered at a specific set of nodes (e.g., Legendre-Gauss-Lobatto (LGL) nodes), is often preferred. While the exact mass matrix is dense, a key advantage arises if the [volume integrals](@entry_id:183482) are evaluated approximately using a quadrature rule whose points coincide with the basis nodes. This practice, known as **[mass lumping](@entry_id:175432)**, results in a diagonal (or "lumped") mass matrix, which dramatically improves [computational efficiency](@entry_id:270255) for [explicit time-stepping](@entry_id:168157) schemes.

#### Variable Coefficients and Aliasing Error
When modeling wave propagation in [heterogeneous media](@entry_id:750241), the material properties $\kappa(\mathbf{x})$ and $\rho(\mathbf{x})$ are spatially variable. In a DG context, these coefficients are also approximated by polynomials. This increases the polynomial degree of the integrands in the [weak form](@entry_id:137295). For instance, a term like $\kappa_h (\nabla \cdot \boldsymbol{u}_h) v_h$ involves a product of three polynomials, leading to a high-degree result. If the [numerical quadrature](@entry_id:136578) used to evaluate this integral is not exact for this higher degree, an **[aliasing error](@entry_id:637691)** is introduced [@problem_id:3375716]. This under-integration can corrupt the solution and even lead to instability. Thus, for variable-coefficient problems, one must either use a [quadrature rule](@entry_id:175061) of sufficiently high order to evaluate integrals exactly or carefully analyze the stability of the under-integrated scheme.

#### Curvilinear Meshes and Free-Stream Preservation
To accurately model complex geometries, DG methods are often implemented on meshes with [curved elements](@entry_id:748117). A fundamental consistency requirement for any scheme on such a mesh is **free-stream preservation**: the scheme must be able to exactly maintain a constant flow state (e.g., $p=\text{const}, \boldsymbol{u}=\text{const}$). This property is not guaranteed and depends on how the geometric information of the curved element mapping (the Jacobian and metric terms) is treated discretely. Achieving free-stream preservation requires that the discrete geometric factors satisfy certain **[discrete metric](@entry_id:154658) identities**. For example, a common identity is $\mathbf{D}_{\xi} (\boldsymbol{J} \boldsymbol{a}_{\xi}) + \mathbf{D}_{\eta} (\boldsymbol{J} \boldsymbol{a}_{\eta}) = \boldsymbol{0}$, where $\mathbf{D}$ are discrete derivative operators and the other terms represent nodal values of the geometric factors. If these identities are violated, the scheme contains spurious source terms that can generate unphysical energy and errors, even from a perfectly uniform initial condition [@problem_id:335691].

#### Relationship to SBP-SAT Methods
The energy-stable properties of DG methods are deeply connected to another class of [high-order numerical methods](@entry_id:142601) known as **Summation-By-Parts (SBP)** operators combined with the **Simultaneous Approximation Term (SAT)** technique. SBP operators are discrete derivative approximations designed to mimic the integration-by-parts property at the discrete level, which makes them ideal for energy analysis. SATs are penalty terms added to the semi-discrete equations to weakly impose boundary or [interface conditions](@entry_id:750725) while preserving the [energy stability](@entry_id:748991) established by the SBP operators. It can be shown that the [interface coupling](@entry_id:750728) in DG via [numerical fluxes](@entry_id:752791) is mathematically equivalent to a particular SBP-SAT formulation, providing a unified perspective on the construction of provably stable [high-order schemes](@entry_id:750306) [@problem_id:3375708].

#### Dispersion and Dissipation Analysis
Beyond stability, a scheme's accuracy is paramount. **Discrete Fourier analysis** is a powerful tool for quantifying the accuracy of a scheme on a uniform mesh. By analyzing how the scheme propagates a [harmonic wave](@entry_id:170943) of a given [wavenumber](@entry_id:172452) $k$, we can derive the **[numerical dispersion relation](@entry_id:752786)**, $\omega(k)$. The real part of $\omega$ gives the **numerical phase speed**, while its imaginary part gives the **[numerical dissipation](@entry_id:141318)**. For an ideal scheme, the phase speed would be the constant sound speed $c$ for all wavenumbers. In practice, [numerical schemes](@entry_id:752822) exhibit **dispersive error**, meaning the phase speed depends on the wavenumber. For example, the DG method with P0 basis functions and an [upwind flux](@entry_id:143931) yields a phase speed of $v_p(k) = c \frac{\sin(k h)}{k h}$ [@problem_id:3375738]. This shows that short waves (large $k h$) travel slower than the true speed, causing [wave packets](@entry_id:154698) to spread out unnaturally. This analysis provides crucial insight into the practical performance and limitations of a given DG formulation.