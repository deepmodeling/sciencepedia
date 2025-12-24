## Introduction
The governing equations of fluid dynamics—the Euler and Navier-Stokes equations—are the mathematical embodiment of fundamental physical conservation principles. While these principles are universal, their mathematical expression can take different forms, most notably the **[conservation form](@entry_id:1122899)** and the **nonconservation form**. For smooth, continuous flows, these formulations are entirely equivalent. However, in the realm of high-speed aerospace engineering and other fields involving [compressible flow](@entry_id:156141), this equivalence shatters in the presence of discontinuities such as shock waves. This distinction is not merely a theoretical nuance; it is a critical fork in the road that determines whether a mathematical model and its numerical implementation can capture the correct physics.

This article addresses the fundamental knowledge gap that arises from the deceptive simplicity of the nonconservation form. It clarifies why its direct application fails catastrophically when flow variables change abruptly, leading to unphysical predictions. By understanding the rigorous foundation of the [conservation form](@entry_id:1122899), we can build robust models and [numerical schemes](@entry_id:752822) capable of accurately simulating the complex, shock-laden environments encountered in real-world applications.

To guide you through this essential topic, the article is structured into three chapters. First, in **Principles and Mechanisms**, we will delve into the mathematical foundations, deriving the two forms from integral [balance laws](@entry_id:171298) and exploring why only the [conservation form](@entry_id:1122899) correctly produces the Rankine-Hugoniot jump conditions at discontinuities. Then, **Applications and Interdisciplinary Connections** will broaden our perspective, demonstrating how these concepts are applied to model complex systems like viscous and [reacting flows](@entry_id:1130631), magnetohydrodynamics, and multiphase phenomena, and how non-conservative terms arise from averaging or geometric complexities. Finally, **Hands-On Practices** will provide an opportunity to solidify these concepts through practical exercises focused on deriving shock properties, implementing the Geometric Conservation Law, and diagnosing numerical instabilities.

## Principles and Mechanisms

The governing equations of fluid dynamics—the Navier-Stokes and Euler equations—are mathematical expressions of fundamental physical conservation laws: the conservation of mass, momentum, and energy. While the underlying physical principles are unique, their mathematical representation is not. The equations can be formulated in different ways, most notably in **[conservation form](@entry_id:1122899)** (also called [divergence form](@entry_id:748608)) and **nonconservation form**. For smooth, continuous flows, these forms are mathematically equivalent. However, in the study of high-speed aerospace flows, which are often characterized by discontinuities such as shock waves, the distinction between these forms becomes critically important. This chapter elucidates the principles distinguishing these formulations, explains the mechanisms by which they behave differently in the presence of discontinuities, and explores the profound implications for the theory and numerical simulation of compressible flows.

### Integral and Differential Forms of Conservation Laws

A conservation law states that the rate of change of the total amount of a physical quantity within a fixed control volume $V$ is equal to the net rate at which the quantity flows across the volume's boundary $S$, plus the rate at which the quantity is created or destroyed by sources or sinks within the volume.

Let $\mathbf{U}$ represent the vector of conserved quantities per unit volume (e.g., mass density, [momentum density](@entry_id:271360), total energy density). Let $\mathbf{F}$ be the corresponding flux tensor, where the column $\mathbf{F}_i$ represents the flux of $\mathbf{U}$ in the $i$-th coordinate direction. If $\mathbf{S}$ is a source term per unit volume, the integral form of the conservation law is:

$$
\frac{d}{dt} \int_V \mathbf{U} \, dV + \oint_S \mathbf{F} \cdot \mathbf{n} \, dS = \int_V \mathbf{S} \, dV
$$

where $\mathbf{n}$ is the outward-pointing [unit normal vector](@entry_id:178851) on the surface $S$. The [surface integral](@entry_id:275394) represents the net efflux of the conserved quantity from the control volume.

By applying the Gauss divergence theorem to the [surface integral](@entry_id:275394), $\oint_S \mathbf{F} \cdot \mathbf{n} \, dS = \int_V (\nabla \cdot \mathbf{F}) \, dV$, we can convert the integral form into a single [volume integral](@entry_id:265381). For a fixed control volume, the time derivative can be moved inside the integral:

$$
\int_V \left( \frac{\partial \mathbf{U}}{\partial t} + \nabla \cdot \mathbf{F} - \mathbf{S} \right) dV = 0
$$

Since this equation must hold for any arbitrary control volume $V$, the integrand itself must be zero. This yields the **[differential conservation law](@entry_id:166470)**, also known as the **[conservation form](@entry_id:1122899)** or **[divergence form](@entry_id:748608)** of the governing equations:

$$
\frac{\partial \mathbf{U}}{\partial t} + \nabla \cdot \mathbf{F}(\mathbf{U}) = \mathbf{S}(\mathbf{U})
$$

This form is fundamental because it derives directly from the integral balance law, which is the most basic statement of the physical principle. As we will see, its structure is essential for the correct mathematical and numerical treatment of discontinuities.

A prime example is the system of **compressible Euler equations** for an inviscid, non-heat-conducting gas. For a 3D flow, the state vector $\mathbf{U}$ and the Cartesian flux vectors $\mathbf{F}_i$ are given by :

$$
\mathbf{U} = \begin{pmatrix} \rho \\ \rho u_1 \\ \rho u_2 \\ \rho u_3 \\ \rho E \end{pmatrix}, \quad
\mathbf{F}_i = \begin{pmatrix} \rho u_i \\ \rho u_1 u_i + p\delta_{1i} \\ \rho u_2 u_i + p\delta_{2i} \\ \rho u_3 u_i + p\delta_{3i} \\ (\rho E + p) u_i \end{pmatrix}
$$

Here, $\rho$ is the density, $\mathbf{u}=(u_1, u_2, u_3)$ is the velocity vector, $p$ is the pressure, and $E$ is the specific total energy. The quantity $\rho E$ is the total energy per unit volume, and $\delta_{ji}$ is the Kronecker delta.

### The Nonconservation Form and its Relation to the Conservation Form

The conservation-form equations can be transformed into an alternative formulation using the [chain rule](@entry_id:147422), provided the solution $\mathbf{U}$ is continuously differentiable. The divergence of the flux can be expanded as:

$$
\nabla \cdot \mathbf{F}(\mathbf{U}) = \frac{\partial \mathbf{F}}{\partial \mathbf{U}} \nabla \mathbf{U}
$$

where $\frac{\partial \mathbf{F}}{\partial \mathbf{U}}$ is the Jacobian matrix of the flux vector with respect to the state vector. Let us denote this matrix by $A(\mathbf{U})$. The conservation law then becomes:

$$
\frac{\partial \mathbf{U}}{\partial t} + A(\mathbf{U}) \frac{\partial \mathbf{U}}{\partial x} = \mathbf{S}(\mathbf{U})
$$

This is a **quasi-linear nonconservation form** of the equations. Often, it is more convenient to work with **primitive variables** (e.g., $\mathbf{q} = (\rho, \mathbf{u}, p)^T$) rather than the [conserved variables](@entry_id:747720) $\mathbf{U}$. A similar transformation yields a system in nonconservation form for the primitive variables . For the Euler equations, this process yields the familiar nonconservative primitive-variable form:

$$
\frac{\partial \rho}{\partial t} + \mathbf{u}\cdot\nabla \rho + \rho\nabla\cdot\mathbf{u} = 0
$$

$$
\frac{\partial \mathbf{u}}{\partial t} + (\mathbf{u}\cdot\nabla)\mathbf{u} + \frac{1}{\rho}\nabla p = \mathbf{0}
$$

$$
\frac{\partial p}{\partial t} + \mathbf{u}\cdot\nabla p + \gamma p\nabla\cdot\mathbf{u} = 0
$$

This form is appealing because it clearly separates the [local time](@entry_id:194383) rate of change (e.g., $\frac{\partial \mathbf{u}}{\partial t}$), advective transport (e.g., $(\mathbf{u}\cdot\nabla)\mathbf{u}$), and source-like terms (e.g., pressure gradients). For any smooth, continuously differentiable flow, the conservation and nonconservation forms are pointwise equivalent . However, this equivalence is deceptive and catastrophically fails when discontinuities are present.

### The Breakdown at Discontinuities: Shock Waves

The critical flaw of the nonconservation form reveals itself in the presence of shock waves or [contact discontinuities](@entry_id:747781). At a discontinuity, the solution is not differentiable, and the [chain rule](@entry_id:147422) used to transform from the [conservation form](@entry_id:1122899) is invalid. The mathematical product of a [discontinuous function](@entry_id:143848) and its [distributional derivative](@entry_id:271061) (a Dirac [delta function](@entry_id:273429)), which appears in the nonconservation form, is not uniquely defined.

The consequences of this ambiguity are profound. The correct physical behavior of a discontinuity is dictated by the [integral conservation law](@entry_id:175062). By applying the integral law to an infinitesimal control volume moving with a shock wave, we derive the **Rankine-Hugoniot jump conditions**. For a one-dimensional system, these conditions relate the shock speed, $s$, to the change in the state vector, $[\mathbf{U}] = \mathbf{U}_R - \mathbf{U}_L$, and the change in the [flux vector](@entry_id:273577), $[\mathbf{F}] = \mathbf{F}(\mathbf{U}_R) - \mathbf{F}(\mathbf{U}_L)$, across the shock:

$$
s[\mathbf{U}] = [\mathbf{F}(\mathbf{U})]
$$

These jump conditions are unique and path-independent; they depend only on the states on either side of the shock, not on the internal structure of the shock itself.

In stark contrast, any attempt to derive [jump conditions](@entry_id:750965) from a nonconservation form leads to non-unique, path-dependent results . The result depends on the specific mathematical interpretation of the ill-defined nonconservative product.

A classic illustration of this failure is the inviscid Burgers' equation, a simplified model for [compressible flow](@entry_id:156141) given by $\partial_t u + \partial_x (u^2/2) = 0$. This is a conservation law with $U=u$ and $F(u)=u^2/2$. The corresponding nonconservation form is $\partial_t u + u \partial_x u = 0$. Consider a shock wave separating a left state $u_L=2$ from a right state $u_R=-1$.

-   From the **[conservation form](@entry_id:1122899)**, the Rankine-Hugoniot condition gives the unique shock speed:
    $s_{\text{cons}} = \frac{[F(u)]}{[u]} = \frac{F(u_R) - F(u_L)}{u_R - u_L} = \frac{0.5(-1)^2 - 0.5(2)^2}{-1 - 2} = \frac{0.5 - 2}{-3} = 0.5$.

-   From the **nonconservation form**, the [jump condition](@entry_id:176163) is ambiguous. If we adopt a specific rule to define the product $u \partial_x u$ at the shock (e.g., by interpreting it as multiplication by the state on the right, $u_R$), we derive a different shock speed: $s_{\text{adv}} = u_R = -1$.

At time $t=2$, the physically correct shock predicted by the [conservation form](@entry_id:1122899) is at position $x = s_{\text{cons}} \times t = 1$. The non-physical shock predicted by one interpretation of the nonconservation form is at $x = s_{\text{adv}} \times t = -2$. The discrepancy is not a minor error; it is a fundamental failure of the nonconservative model to capture the correct physics .

### Weak Solutions and Entropy Conditions

To build a rigorous mathematical theory that accommodates discontinuities, the concept of a **[weak solution](@entry_id:146017)** is introduced. A function $u$ is a [weak solution](@entry_id:146017) of a conservation law if, instead of satisfying the PDE in the classical sense, it satisfies an equivalent integral identity for all smooth "[test functions](@entry_id:166589)" $\varphi$ with [compact support](@entry_id:276214). For a [scalar conservation law](@entry_id:754531) $\partial_t u + \partial_x f(u) = 0$, the [weak form](@entry_id:137295) is:

$$
\int_{0}^{\infty} \int_{\mathbb{R}} \left( u \frac{\partial \varphi}{\partial t} + f(u) \frac{\partial \varphi}{\partial x} \right) dx dt + \int_{\mathbb{R}} u(x,0) \varphi(x,0) dx = 0
$$

This formulation is derived by integrating the PDE against $\varphi$ and using [integration by parts](@entry_id:136350) to transfer all derivatives from the potentially discontinuous solution $u$ to the infinitely smooth [test function](@entry_id:178872) $\varphi$ . A function satisfying the Rankine-Hugoniot conditions is a [weak solution](@entry_id:146017), but the converse is also true: any piecewise smooth [weak solution](@entry_id:146017) must satisfy the Rankine-Hugoniot conditions at its jumps.

However, the framework of weak solutions is not a complete remedy, as it often admits multiple solutions for a single initial condition. For instance, the Rankine-Hugoniot conditions for the Burgers' equation admit both physically correct compression shocks and physically impossible expansion shocks, which would violate the Second Law of Thermodynamics.

To restore uniqueness, an additional criterion, known as the **[entropy condition](@entry_id:166346)**, must be imposed. This condition serves to select the single, physically admissible [weak solution](@entry_id:146017). For [scalar conservation laws](@entry_id:754532), the most powerful and general form is the **Kruzhkov entropy condition**. It requires that for every real constant $k$, the following inequality holds in the distributional sense :

$$
\frac{\partial |u-k|}{\partial t} + \frac{\partial}{\partial x} \left[ \text{sgn}(u-k) (f(u) - f(k)) \right] \le 0
$$

The functions $\eta_k(u) = |u-k|$ are a family of convex entropy functions. The profound result of Kruzhkov's theory is that a [weak solution](@entry_id:146017) is the unique, physically correct solution if and only if it satisfies this family of inequalities for all $k$. A key consequence of this condition is the **$L^1$-contraction principle**: the $L^1$-distance between any two entropy solutions is a non-increasing function of time. This immediately implies the uniqueness of the solution for a given initial condition . For systems with a strictly convex flux (like the Euler equations), this general condition simplifies to the more intuitive **Lax [entropy condition](@entry_id:166346)**, which states that characteristic waves on both sides of a shock must propagate into the shock front .

### Hyperbolicity and Characteristic Waves

The distinction between the forms is also tied to the mathematical structure of the equations. The nonconservative form $\partial_t \mathbf{q} + B(\mathbf{q}) \partial_x \mathbf{q} = 0$ is classified by the properties of the matrix $B(\mathbf{q})$. For the 1D Euler equations, one can show that the eigenvalues of this matrix are real and distinct: $\lambda_1 = u-a$, $\lambda_2 = u$, and $\lambda_3 = u+a$, where $a$ is the local speed of sound . This identifies the system as **strictly hyperbolic**.

These eigenvalues are the **[characteristic speeds](@entry_id:165394)** at which information propagates through the fluid in smooth regions. The waves corresponding to $u \pm a$ are **acoustic waves**, while the wave corresponding to $u$ is the **contact (or entropy) wave**. This analysis provides invaluable insight into wave propagation phenomena but is strictly valid only for smooth solutions. Across shocks, the concept of characteristics breaks down, and one must return to the [integral conservation law](@entry_id:175062) and the Rankine-Hugoniot conditions for a correct description of the physics .

### Numerical Consequences of the Conservation Form

The superiority of the [conservation form](@entry_id:1122899) is not merely a theoretical curiosity; it is paramount for the development of robust numerical methods in CFD. Modern [shock-capturing schemes](@entry_id:754786), particularly **[finite volume methods](@entry_id:749402)**, are built directly upon the integral conservation law.

A finite volume scheme discretizes the domain into cells and updates the cell-averaged [state variables](@entry_id:138790) based on the fluxes across the cell faces. The semi-discrete equation for a cell $i$ is:

$$
V_i \frac{d\mathbf{U}_i}{dt} + \sum_{j} \mathbf{H}_{ij} = V_i \mathbf{S}_i
$$

where $\mathbf{H}_{ij}$ is the numerical flux vector across the face separating cell $i$ from its neighbor $j$. A key property of a properly constructed scheme is that the [numerical flux](@entry_id:145174) is conservative, meaning $\mathbf{H}_{ij} = -\mathbf{H}_{ji}$. That is, the flux leaving cell $i$ is exactly the flux entering cell $j$. When the equations for a block of cells are summed, all the interior fluxes cancel in pairs, leaving only the fluxes at the outer boundary of the block. This property of **[discrete conservation](@entry_id:1123819)** ensures that the scheme globally conserves mass, momentum, and energy, and it is a direct consequence of discretizing the [divergence form](@entry_id:748608) . Any converging [conservative scheme](@entry_id:747714) is guaranteed by the Lax-Wendroff theorem to converge to a [weak solution](@entry_id:146017) of the PDE, thus capturing shocks with the correct physical speed .

Schemes based on discretizing the nonconservative forms, such as by using finite differences for terms like $(\mathbf{u}\cdot\nabla)\mathbf{u}$, do not possess this flux-cancellation property and therefore do not enforce discrete conservation. They can produce spurious sources or sinks of conserved quantities, leading to incorrect shock speeds and strengths . Furthermore, nonconservative schemes often struggle with other fundamental requirements, such as preserving a uniform freestream flow on a distorted or [curvilinear grid](@entry_id:1123319), a problem that is naturally handled by schemes that correctly discretize the [conservation form](@entry_id:1122899) and satisfy the **Geometric Conservation Law (GCL)** .

### Distinguishing Conserved and Non-Conserved Quantities

Not all physical quantities of interest are conserved. A quantity is conserved only if its evolution equation can be written purely in [divergence form](@entry_id:748608) (plus external sources), without any terms representing conversion from other forms of energy or momentum. A clear example is **internal energy**. While total energy is conserved, internal energy is not. By starting with the total energy conservation law from the Navier-Stokes equations and subtracting the equation for kinetic energy (derived from the momentum equation), one can derive the evolution equation for specific internal energy $e$. The result is :

$$
\frac{\partial (\rho e)}{\partial t} + \nabla \cdot (\rho e \mathbf{u} + \mathbf{q}) = -p \nabla \cdot \mathbf{u} + \boldsymbol{\tau} : \nabla \mathbf{u} + \rho r
$$

The terms on the right-hand side, $-p \nabla \cdot \mathbf{u}$ (rate of work done by pressure forces in compression/expansion) and $\boldsymbol{\tau} : \nabla \mathbf{u}$ (rate of viscous dissipation), are source terms that represent the reversible and irreversible conversion of mechanical energy into internal energy. Because these terms cannot be written as the divergence of a flux, the quantity $\rho e$ is not conserved. Only the total energy $\rho E$, which accounts for both internal and kinetic forms, admits a true conservation law.

### Advanced Topic: Inherently Nonconservative Systems

While many fundamental systems in physics are conservative, some important models, particularly in multiphase flow, are **inherently nonconservative**—they cannot be derived from an underlying integral balance law. These systems take the form $\partial_t u + A(u)\partial_x u = 0$, where $A(u)$ is not the Jacobian of any flux function.

For these systems, the ambiguity of the nonconservative product is a central feature of the model itself. The **Dal Maso-LeFloch-Murat (DLM) theory** provides a rigorous framework by acknowledging that a specific **family of paths** $\Phi(u_L, u_R; \theta)$ in state space must be supplied as part of the problem definition. The [jump condition](@entry_id:176163) then becomes path-dependent, defined by an integral along this prescribed path .

The physical justification for a particular path often comes from a **viscous regularization**. The nonconservative system is viewed as the zero-viscosity limit of a more complex system containing diffusive terms. The smooth [traveling wave solutions](@entry_id:272909) of the viscous system trace out unique profiles in state space, and these profiles define the canonical path for the inviscid model. Numerical methods, known as **path-[conservative schemes](@entry_id:747715)**, must then be specifically designed to be consistent with this chosen path to converge to the correct physical solution . This advanced theory demonstrates that while the [conservation form](@entry_id:1122899) is paramount when it exists, a sophisticated mathematical structure is available to handle the challenging cases where it does not.