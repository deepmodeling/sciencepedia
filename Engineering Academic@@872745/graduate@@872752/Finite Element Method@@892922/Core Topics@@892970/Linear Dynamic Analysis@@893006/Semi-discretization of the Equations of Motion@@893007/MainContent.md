## Introduction
The analysis of dynamic systems in engineering and physics relies on solving the equations of motion, which are typically expressed as complex partial differential equations (PDEs). To make these problems computationally solvable, a critical transformation is required: discretization. **Semi-[discretization](@entry_id:145012)** is a powerful method within the finite element framework that achieves this by discretizing the spatial domain while leaving time as a continuous variable. This process systematically converts the governing PDE into a large but manageable system of coupled [ordinary differential equations](@entry_id:147024) (ODEs), forming the foundation for virtually all modern dynamic simulations. This article bridges the gap between the continuous physical problem and its discrete computational model.

Across the following chapters, you will embark on a comprehensive journey through the theory and application of [semi-discretization](@entry_id:163562). The first chapter, **"Principles and Mechanisms"**, delves into the derivation of the canonical system of motion from the weak form, meticulously examining the physical and mathematical properties of the resulting mass, stiffness, and damping matrices. The second chapter, **"Applications and Interdisciplinary Connections"**, demonstrates the versatility of this framework by applying it to [structural dynamics](@entry_id:172684), nonlinear stability analysis, and exploring its crucial links to [numerical time integration](@entry_id:752837) and [structural optimization](@entry_id:176910). Finally, **"Hands-On Practices"** provides a set of targeted problems designed to solidify your understanding of matrix formulation, physical properties, and the consequences of modeling choices.

## Principles and Mechanisms

The transition from the continuous [equations of motion](@entry_id:170720), expressed as [partial differential equations](@entry_id:143134) (PDEs), to a computationally tractable system is a cornerstone of modern engineering analysis. This process, known as [discretization](@entry_id:145012), can be approached in several ways. In the context of dynamic systems, a powerful and widely used strategy is **[semi-discretization](@entry_id:163562)**, where the spatial domain is discretized while the time variable is kept continuous. This procedure transforms the governing PDE into a large system of coupled ordinary differential equations (ODEs) in time. This chapter elucidates the principles and mechanisms of this transformation, deriving the canonical system of motion from first principles and exploring the physical and mathematical properties of its constituent parts.

### From the Weak Form to a System of Ordinary Differential Equations

The starting point for the [finite element analysis](@entry_id:138109) of a dynamic [solid mechanics](@entry_id:164042) problem is typically the [balance of linear momentum](@entry_id:193575), which represents Newton's second law for a continuum. For a body occupying a domain $\Omega$, this is expressed in its strong form as:

$$
\rho(\mathbf{x}) \ddot{\mathbf{u}}(\mathbf{x},t) - \nabla \cdot \boldsymbol{\sigma}(\mathbf{x},t) = \mathbf{b}(\mathbf{x},t)
$$

Here, $\rho$ is the mass density, $\mathbf{u}$ is the [displacement vector](@entry_id:262782), $\boldsymbol{\sigma}$ is the Cauchy stress tensor, $\mathbf{b}$ is the [body force](@entry_id:184443) vector per unit volume, and a double dot denotes the second derivative with respect to time $t$. This PDE is supplemented by boundary conditions: essential (or Dirichlet) conditions where displacements $\bar{\mathbf{u}}$ are prescribed on a part of the boundary $\Gamma_u$, and natural (or Neumann) conditions where tractions $\bar{\mathbf{t}}$ are prescribed on the remaining boundary $\Gamma_t$ [@problem_id:2594245].

While the strong form is a direct statement of physics, it requires a high degree of solution smoothness that is often not present in practical problems. The [finite element method](@entry_id:136884) is built upon the **weak form**, which is derived using the [principle of virtual work](@entry_id:138749). We multiply the [momentum equation](@entry_id:197225) by an arbitrary, kinematically admissible [virtual displacement](@entry_id:168781) (or test function) $\mathbf{w}$ and integrate over the domain $\Omega$. The test function space is chosen such that $\mathbf{w} = \mathbf{0}$ on the portion of the boundary $\Gamma_u$ where [essential boundary conditions](@entry_id:173524) are applied. Applying the divergence theorem to the stress term yields the weak form: Find $\mathbf{u}(t)$ in an appropriate [function space](@entry_id:136890) that satisfies the [essential boundary conditions](@entry_id:173524), such that for all test functions $\mathbf{w}$:

$$
\int_{\Omega} \rho \, \mathbf{w} \cdot \ddot{\mathbf{u}} \, dV + \int_{\Omega} \boldsymbol{\varepsilon}(\mathbf{w}) : \boldsymbol{\sigma} \, dV = \int_{\Omega} \mathbf{w} \cdot \mathbf{b} \, dV + \int_{\Gamma_t} \mathbf{w} \cdot \bar{\mathbf{t}} \, dS
$$

where we have used the symmetry of the stress tensor ($\boldsymbol{\sigma}=\boldsymbol{\sigma}^\mathsf{T}$), a consequence of the [balance of angular momentum](@entry_id:181848), to replace the gradient $\nabla \mathbf{w}$ with the symmetric strain tensor $\boldsymbol{\varepsilon}(\mathbf{w})$ [@problem_id:2594261].

The **[semi-discretization](@entry_id:163562)** step involves seeking an approximate solution $\mathbf{u}_h(\mathbf{x}, t)$ within a finite-dimensional subspace spanned by a set of basis functions, often called shape functions, $\mathbf{N}_i(\mathbf{x})$. The approximate solution is a [linear combination](@entry_id:155091) of these basis functions with time-dependent coefficients, which are the nodal degrees of freedom $\mathbf{d}(t)$:

$$
\mathbf{u}(\mathbf{x}, t) \approx \mathbf{u}_h(\mathbf{x}, t) = \sum_{i} \mathbf{N}_i(\mathbf{x}) d_i(t) = \mathbf{N}(\mathbf{x}) \mathbf{d}(t)
$$

The **Bubnov-Galerkin method** is a specific choice where the [test functions](@entry_id:166589) $\mathbf{w}$ are chosen from the same finite-dimensional subspace as the [trial functions](@entry_id:756165) $\mathbf{u}_h$. Substituting the approximation for $\mathbf{u}_h$ into the weak form and using the basis functions themselves as [test functions](@entry_id:166589) leads to a system of second-order ODEs. This system is the semi-discrete model, where space has been discretized but time remains continuous [@problem_id:2594279]:

$$
\mathbf{M} \ddot{\mathbf{d}}(t) + \mathbf{C} \dot{\mathbf{d}}(t) + \mathbf{K} \mathbf{d}(t) = \mathbf{f}(t)
$$

This equation is the central result of [semi-discretization](@entry_id:163562). The matrices $\mathbf{M}$, $\mathbf{C}$, and $\mathbf{K}$ are the global mass, damping, and stiffness matrices, respectively, and $\mathbf{f}(t)$ is the global vector of external forces. The subsequent sections will deconstruct each of these components.

### The Anatomy of the Semi-Discrete System

Each term in the semi-discrete [equation of motion](@entry_id:264286) originates from a corresponding term in the weak formulation and carries a distinct physical meaning.

#### The Stiffness Matrix $\mathbf{K}$

The stiffness matrix $\mathbf{K}$ arises from the [internal virtual work](@entry_id:172278) term, $\int_{\Omega} \boldsymbol{\varepsilon}(\mathbf{w}) : \boldsymbol{\sigma} \, dV$. For a linear elastic material, the stress is related to the strain via the [fourth-order elasticity tensor](@entry_id:188318) $\mathbb{C}$ (or its matrix form $\mathbf{D}$): $\boldsymbol{\sigma} = \mathbb{C} : \boldsymbol{\varepsilon}(\mathbf{u})$. The discrete strain field is expressed using the [strain-displacement matrix](@entry_id:163451) $\mathbf{B}$, which contains spatial derivatives of the [shape functions](@entry_id:141015): $\boldsymbol{\varepsilon}(\mathbf{u}_h) = \mathbf{B}(\mathbf{x})\mathbf{d}(t)$. The resulting global stiffness matrix is assembled from element-level contributions:

$$
\mathbf{K} = \sum_{e} \mathbf{K}^e \quad \text{with} \quad \mathbf{K}^e = \int_{\Omega_e} \mathbf{B}^\mathsf{T} \mathbf{D} \mathbf{B} \, dV
$$

Physically, the [stiffness matrix](@entry_id:178659) represents the structure's resistance to [elastic deformation](@entry_id:161971). The quadratic form $\frac{1}{2}\mathbf{d}^\mathsf{T} \mathbf{K} \mathbf{d}$ represents the total elastic strain energy stored in the discretized body [@problem_id:2563517].

A fundamental property of the stiffness matrix is its **symmetry**. This property is not automatic; it is a direct consequence of a corresponding symmetry in the material model. Specifically, the symmetry of $\mathbf{K}$ requires the **[major symmetry](@entry_id:198487)** of the [elasticity tensor](@entry_id:170728) ($C_{ijkl} = C_{klij}$). This [material symmetry](@entry_id:173835) is, in turn, equivalent to the existence of a quadratic [strain energy density function](@entry_id:199500), from which stress can be derived. Materials with this property are known as hyperelastic. The [balance of angular momentum](@entry_id:181848) ensures the Cauchy stress tensor is symmetric ($\boldsymbol{\sigma} = \boldsymbol{\sigma}^\mathsf{T}$), which allows the internal work to be expressed in terms of strain, but it is the [major symmetry](@entry_id:198487) of $\mathbb{C}$ that ensures the resulting [stiffness matrix](@entry_id:178659) is symmetric [@problem_id:2594261]. For a system with a symmetric [stiffness matrix](@entry_id:178659) and no external forces or damping, this property is essential for the [conservation of mechanical energy](@entry_id:175656).

#### The Mass Matrix $\mathbf{M}$

The mass matrix $\mathbf{M}$ originates from the inertial virtual work term, $\int_{\Omega} \rho \, \mathbf{w} \cdot \ddot{\mathbf{u}} \, dV$. Following the Galerkin procedure, this integral yields the **[consistent mass matrix](@entry_id:174630)**, so named because the same shape functions are used to interpolate both the [displacement field](@entry_id:141476) and the inertia distribution. Its element-level form is:

$$
\mathbf{M}^e = \int_{\Omega_e} \rho \, \mathbf{N}^\mathsf{T} \mathbf{N} \, dV
$$

The quadratic form $\frac{1}{2}\dot{\mathbf{d}}^\mathsf{T} \mathbf{M} \dot{\mathbf{d}}$ gives the total kinetic energy of the discretized system [@problem_id:2594310]. The off-diagonal terms in $\mathbf{M}$ represent inertial coupling between the degrees of freedom.

To make this concrete, consider a simple 1D elastic bar of length $L$, area $A$, and density $\rho$, discretized with a single two-node linear element. The shape functions are $N_1(x) = 1 - x/L$ and $N_2(x) = x/L$. Applying the integral definition, the [consistent mass matrix](@entry_id:174630) is calculated as [@problem_id:2676289]:

$$
\mathbf{M}_c = \int_{0}^{L} \rho A \begin{pmatrix} N_1^2 & N_1 N_2 \\ N_2 N_1 & N_2^2 \end{pmatrix} \,dx = \frac{\rho A L}{6} \begin{pmatrix} 2 & 1 \\ 1 & 2 \end{pmatrix}
$$

The [consistent mass matrix](@entry_id:174630), derived directly from the Galerkin principle, possesses crucial properties. Provided the mass density $\rho$ is strictly positive and the basis functions are linearly independent, the [consistent mass matrix](@entry_id:174630) $\mathbf{M}$ is always **symmetric and positive definite** [@problem_id:2594310]. Positive definiteness means that any non-zero nodal velocity vector $\dot{\mathbf{d}}$ will result in a positive kinetic energy, which is physically consistent. It is important not to confuse the properties of the [mass and stiffness matrices](@entry_id:751703): while the [stiffness matrix](@entry_id:178659) $\mathbf{K}$ becomes singular (positive semidefinite) if [rigid body motions](@entry_id:200666) are not suppressed by boundary conditions, the [mass matrix](@entry_id:177093) $\mathbf{M}$ remains [positive definite](@entry_id:149459), as [rigid body motions](@entry_id:200666) still possess kinetic energy.

#### Damping and External Forces

The damping matrix $\mathbf{C}$ is typically not derived from first principles in linear [elastodynamics](@entry_id:175818). It is added phenomenologically to model various [energy dissipation](@entry_id:147406) mechanisms. A common and convenient model is **Rayleigh damping** (or proportional damping), where the damping matrix is assumed to be a linear combination of the [mass and stiffness matrices](@entry_id:751703):

$$
\mathbf{C} = \alpha \mathbf{M} + \beta \mathbf{K}
$$

The coefficients $\alpha$ and $\beta$ are usually determined from experimental data for two different modes of vibration. This form is computationally advantageous because it preserves the eigenvectors of the undamped system.

The external force vector $\mathbf{f}(t)$ aggregates all external actions on the body. It arises from the virtual work of body forces and prescribed tractions:

$$
\mathbf{f}(t) = \sum_{e} \left( \int_{\Omega_e} \mathbf{N}^\mathsf{T} \mathbf{b}(t) \, dV + \int_{\Gamma_{t,e}} \mathbf{N}^\mathsf{T} \bar{\mathbf{t}}(t) \, dS \right)
$$

This expression shows how [distributed loads](@entry_id:162746) are converted into a set of work-equivalent nodal forces [@problem_id:2563517].

### The Role of Boundary Conditions in the Discrete System

A crucial aspect of the [finite element formulation](@entry_id:164720) is the fundamentally different treatment of [essential and natural boundary conditions](@entry_id:168198).

**Essential boundary conditions** (e.g., prescribed displacements, $u = \bar{u}$) are conditions imposed on the solution space itself. In the derivation of the [weak form](@entry_id:137295), they are satisfied by constructing the trial and test [function spaces](@entry_id:143478) accordingly. For [test functions](@entry_id:166589), this means they must vanish ($\mathbf{w}=\mathbf{0}$) on the part of the boundary $\Gamma_u$ where essential conditions are applied. This choice directly eliminates any boundary integral terms over $\Gamma_u$ from the [weak form](@entry_id:137295). In the final semi-discrete system $\mathbf{M}\ddot{\mathbf{d}} + \mathbf{K}\mathbf{d} = \mathbf{f}$, these conditions are enforced algebraically, for example, by partitioning the system of equations and directly substituting the known nodal displacement values [@problem_id:2594245].

**Natural boundary conditions** (e.g., prescribed tractions, $\boldsymbol{\sigma}\mathbf{n} = \bar{\mathbf{t}}$) are handled differently. They are termed "natural" because they arise naturally from the integration-by-parts step in the derivation of the [weak form](@entry_id:137295). The boundary integral over the traction boundary $\Gamma_t$ does not vanish (since [test functions](@entry_id:166589) are not required to be zero there) and becomes the mechanism for applying these loads. As shown in the expression for the external force vector $\mathbf{f}(t)$, prescribed tractions manifest as a boundary integral term that contributes directly to the system's [load vector](@entry_id:635284) [@problem_id:2594260].

Alternative methods for enforcing [essential boundary conditions](@entry_id:173524), such as the **[penalty method](@entry_id:143559)** or the use of **Lagrange multipliers**, transform the constraint into additional terms within the weak formulation itself, leading to modified stiffness matrices and force vectors or larger, augmented systems. However, even in these cases, the fundamental distinction remains: natural conditions are always incorporated via the external work terms [@problem_id:2594245].

### Properties and Consequences of Semi-Discretization

The semi-discrete system is an approximation of the original continuum. Its properties, while inheriting many features of the continuum, also exhibit unique characteristics that are artifacts of the discretization process.

#### Energy Conservation

A key property of the physical system is the [conservation of mechanical energy](@entry_id:175656) in the absence of [non-conservative forces](@entry_id:164833) (damping, external work). The semi-discrete system beautifully preserves this property. For an undamped, unforced system ($\mathbf{C=0}, \mathbf{f=0}$), the total discrete mechanical energy is $E(t) = T + U = \frac{1}{2} \dot{\mathbf{d}}^\mathsf{T} \mathbf{M} \dot{\mathbf{d}} + \frac{1}{2} \mathbf{d}^\mathsf{T} \mathbf{K} \mathbf{d}$. Taking the time derivative and using the symmetry of $\mathbf{M}$ and $\mathbf{K}$, we find:

$$
\frac{dE}{dt} = \dot{\mathbf{d}}^\mathsf{T} (\mathbf{M} \ddot{\mathbf{d}} + \mathbf{K} \mathbf{d})
$$

Since $\mathbf{M} \ddot{\mathbf{d}} + \mathbf{K} \mathbf{d} = \mathbf{0}$ from the [equation of motion](@entry_id:264286), it follows that $\frac{dE}{dt} = 0$. This demonstrates that the mechanical energy of the semi-discrete model is exactly conserved over continuous time. This analysis can be performed at the semi-discrete level, before any [time integration](@entry_id:170891) scheme is chosen, and hinges on the symmetry of the [mass and stiffness matrices](@entry_id:751703) [@problem_id:2594279] [@problem_id:2594261].

#### Mass Lumping: A Computational Trade-off

The [consistent mass matrix](@entry_id:174630) $\mathbf{M}_c$ is dense at the element level, leading to a global [mass matrix](@entry_id:177093) that is banded but not diagonal. This coupling increases computational cost, especially in [explicit time integration](@entry_id:165797) schemes which rely on inverting the [mass matrix](@entry_id:177093). To circumvent this, the **[lumped mass matrix](@entry_id:173011)**, $\mathbf{M}_l$, is often used. This is a [diagonal matrix](@entry_id:637782) that preserves the total mass of the element but discards the off-diagonal inertial coupling terms. A common technique is **[row-sum lumping](@entry_id:754439)**, where the diagonal entry $M_{ii}$ is the sum of all entries in the $i$-th row of the [consistent mass matrix](@entry_id:174630). For our 1D [bar element](@entry_id:746680) example, this yields [@problem_id:2594284]:

$$
\mathbf{M}_l = \frac{\rho A L}{2} \begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix}
$$

Lumping introduces a significant trade-off. While it simplifies computation, it alters the dynamic properties of the system.
-   Both $\mathbf{M}_c$ and $\mathbf{M}_l$ are [symmetric positive definite](@entry_id:139466) and preserve the total mass and [linear momentum](@entry_id:174467) of the element [@problem_id:2594284] [@problem_id:2578893].
-   The [consistent mass matrix](@entry_id:174630) $\mathbf{M}_c$ exactly represents the kinetic energy for any velocity field that can be represented by the element's [shape functions](@entry_id:141015). The [lumped mass matrix](@entry_id:173011) $\mathbf{M}_l$ is less accurate; for instance, it is only exact for a [constant velocity](@entry_id:170682) field (rigid-body translation) [@problem_id:2594284].
-   This difference in kinetic [energy representation](@entry_id:202173) affects the system's [natural frequencies](@entry_id:174472). For a given mesh, the frequencies obtained with $\mathbf{M}_l$ are generally different from those with $\mathbf{M}_c$. Specifically, [mass lumping](@entry_id:175432) tends to lower the computed natural frequencies, making the model dynamically "softer". The effect is more pronounced for higher-frequency modes, which involve more complex deformation patterns over the element [@problem_id:2578893].

#### Numerical Dispersion: The Discretized Wave

The final and most subtle consequence of [semi-discretization](@entry_id:163562) is its effect on [wave propagation](@entry_id:144063). In the original continuum, the [one-dimensional wave equation](@entry_id:164824) $u_{tt} = c^2 u_{xx}$ has a constant [wave speed](@entry_id:186208) $c$ for all frequencies. The semi-discretized system does not share this property.

By analyzing a [harmonic wave](@entry_id:170943) solution (a Bloch wave) propagating through a uniform mesh of linear elements, one can derive the **[numerical dispersion relation](@entry_id:752786)**, which connects the temporal frequency $\omega$ to the spatial [wavenumber](@entry_id:172452) $k$. For the 1D wave equation discretized with a [consistent mass matrix](@entry_id:174630), this relation is [@problem_id:2594248]:

$$
\omega^2(k) = \frac{6c^2}{h^2} \frac{1 - \cos(kh)}{2 + \cos(kh)}
$$

where $h$ is the element size. This equation reveals that the numerical phase velocity, $c_h(k) = \omega/k$, is no longer a constant $c$, but depends on the [wavenumber](@entry_id:172452) $k$ (i.e., on the wavelength). This phenomenon is called **[numerical dispersion](@entry_id:145368)**. Waves of different lengths travel at different speeds in the discrete model, causing a wave packet to spread out and distort, an effect not present in the original PDE.

The [group velocity](@entry_id:147686), $v_{g,h} = d\omega/dk$, which describes the propagation speed of the energy in a [wave packet](@entry_id:144436), is also frequency-dependent. For example, for a wave whose half-wavelength is twice the mesh size ($k = \pi/(2h)$), the group velocity can be computed as $v_{g,h} = \frac{3\sqrt{3}}{4}c \approx 1.3c$. For other wavelengths, the velocity may be less than $c$. This demonstrates that the semi-discrete system is not a perfect replica of the continuum; it is a model with its own distinct physical behavior that converges to the true behavior only as the mesh size $h$ approaches zero. Understanding these properties is critical for assessing the accuracy and fidelity of dynamic simulations.