## Introduction
Simulating complex fluid flows governed by [nonlinear conservation laws](@entry_id:170694) demands numerical methods that are not only accurate but also robust. Standard [high-order schemes](@entry_id:750306) can suffer from instabilities, particularly when encountering shock waves or resolving turbulent structures, leading to unreliable or non-physical results. The core problem lies in ensuring that the discrete [numerical approximation](@entry_id:161970) respects the fundamental physical conservation principles and mathematical properties, such as energy conservation or entropy production, that guarantee the [well-posedness](@entry_id:148590) of the continuous equations. This article addresses this challenge by introducing a powerful framework for constructing provably stable, [high-order schemes](@entry_id:750306) based on the Summation-by-Parts (SBP) principle.

Over the next chapters, you will gain a comprehensive understanding of this structure-preserving methodology.
- **Principles and Mechanisms** will lay the theoretical groundwork, explaining the SBP property as a discrete analogue of integration-by-parts. It will demonstrate how this property leads to the construction of kinetic-energy-preserving and [entropy-stable schemes](@entry_id:749017) for [nonlinear systems](@entry_id:168347) like the compressible Euler equations.
- **Applications and Interdisciplinary Connections** will bridge theory and practice, showing how these principles are used to build complete, stable CFD solvers. This chapter explores handling complex geometries, implementing [stable boundary conditions](@entry_id:755316) via the SBP-SAT method, and extending the framework to [viscous flows](@entry_id:136330) and [shock capturing](@entry_id:141726).
- **Hands-On Practices** will provide opportunities to apply these concepts through targeted exercises, from analyzing aliasing errors to implementing a fully entropy-stable scheme for the Burgers' equation.

By mastering these concepts, you will be equipped to develop and analyze modern numerical methods that offer a new level of robustness and physical fidelity for challenging simulations in aerospace engineering, astrophysics, and beyond.

## Principles and Mechanisms

The construction of robust, high-order [numerical schemes](@entry_id:752822) for partial differential equations, particularly the conservation laws governing fluid dynamics, requires a framework that discretely mimics the fundamental physical and mathematical properties of the continuous equations. Proving the stability of a numerical method is paramount, and for hyperbolic PDEs, stability is intimately linked to the conservation or dissipation of integral quantities like energy or entropy. Summation-by-Parts (SBP) operators, in conjunction with penalty techniques, provide a rigorous and systematic methodology for designing schemes that possess provable stability, mimicking continuous energy arguments at the discrete level. This chapter elucidates the core principles of SBP operators and their application in constructing schemes that preserve kinetic energy or discretely satisfy the [second law of thermodynamics](@entry_id:142732).

### The Summation-by-Parts (SBP) Property: A Discrete Analogue to Integration by Parts

The foundation of energy-based stability analysis for [differential operators](@entry_id:275037) is the integration-by-parts (IBP) formula. For two sufficiently smooth functions $u(x)$ and $v(x)$ on an interval $[a, b]$, the IBP rule states:
$$
\int_a^b u \, (\partial_x v) \, dx = [uv]_a^b - \int_a^b v \, (\partial_x u) \, dx
$$
This identity relates the derivative of one function to the derivative of another, with the difference being accounted for by boundary terms. Summation-by-Parts operators are first-derivative [finite difference operators](@entry_id:749379) designed to satisfy a discrete analogue of this identity.

An SBP operator on a grid of $N$ nodes is not defined by a single matrix, but by a carefully constructed triple of matrices $(\boldsymbol{D}, \boldsymbol{H}, \boldsymbol{Q})$. For grid functions $\boldsymbol{u}, \boldsymbol{v} \in \mathbb{R}^N$, these matrices are defined by the following properties:

1.  $\boldsymbol{D} \in \mathbb{R}^{N \times N}$ is the **derivative operator** that approximates $\partial_x$.
2.  $\boldsymbol{H} \in \mathbb{R}^{N \times N}$ is a [symmetric positive-definite matrix](@entry_id:136714) ($\boldsymbol{H} = \boldsymbol{H}^T > 0$) that defines a discrete **norm** or inner product. The discrete inner product is given by $\langle \boldsymbol{u}, \boldsymbol{v} \rangle_{\boldsymbol{H}} = \boldsymbol{u}^T \boldsymbol{H} \boldsymbol{v}$, and the associated squared norm is $\|\boldsymbol{u}\|_{\boldsymbol{H}}^2 = \boldsymbol{u}^T \boldsymbol{H} \boldsymbol{u}$. $\boldsymbol{H}$ acts as a matrix of [quadrature weights](@entry_id:753910) for discretely integrating functions.
3.  The matrices are linked by the relation $\boldsymbol{D} = \boldsymbol{H}^{-1} \boldsymbol{Q}$.
4.  The matrix $\boldsymbol{Q}$ must satisfy the **SBP property**: $\boldsymbol{Q} + \boldsymbol{Q}^T = \boldsymbol{B}$, where $\boldsymbol{B}$ is a matrix that isolates the boundary points. For a one-dimensional domain, $\boldsymbol{B} = \mathrm{diag}(-1, 0, \dots, 0, 1)$.

From these algebraic conditions, a discrete integration-by-parts formula emerges. Consider the inner product of $\boldsymbol{u}$ with $\boldsymbol{Dv}$:
$$
\langle \boldsymbol{u}, \boldsymbol{Dv} \rangle_{\boldsymbol{H}} = \boldsymbol{u}^T \boldsymbol{H} (\boldsymbol{Dv}) = \boldsymbol{u}^T \boldsymbol{H} (\boldsymbol{H}^{-1}\boldsymbol{Q}\boldsymbol{v}) = \boldsymbol{u}^T \boldsymbol{Q} \boldsymbol{v}
$$
By adding this to its "swapped" counterpart, $\langle \boldsymbol{v}, \boldsymbol{Du} \rangle_{\boldsymbol{H}}$, we find:
$$
\langle \boldsymbol{u}, \boldsymbol{Dv} \rangle_{\boldsymbol{H}} + \langle \boldsymbol{v}, \boldsymbol{Du} \rangle_{\boldsymbol{H}} = \boldsymbol{u}^T \boldsymbol{Q} \boldsymbol{v} + \boldsymbol{v}^T \boldsymbol{Q} \boldsymbol{u} = \boldsymbol{u}^T \boldsymbol{Q} \boldsymbol{v} + (\boldsymbol{v}^T \boldsymbol{Q} \boldsymbol{u})^T = \boldsymbol{u}^T \boldsymbol{Q} \boldsymbol{v} + \boldsymbol{u}^T \boldsymbol{Q}^T \boldsymbol{v} = \boldsymbol{u}^T (\boldsymbol{Q} + \boldsymbol{Q}^T) \boldsymbol{v}
$$
Using the SBP property $\boldsymbol{Q} + \boldsymbol{Q}^T = \boldsymbol{B}$, we arrive at the discrete IBP formula :
$$
\langle \boldsymbol{u}, \boldsymbol{Dv} \rangle_{\boldsymbol{H}} + \langle \boldsymbol{v}, \boldsymbol{Du} \rangle_{\boldsymbol{H}} = \boldsymbol{u}^T \boldsymbol{B} \boldsymbol{v}
$$
This can be rearranged to more closely resemble the continuous identity:
$$
\boldsymbol{u}^T \boldsymbol{H} \boldsymbol{D} \boldsymbol{v} = - \boldsymbol{v}^T \boldsymbol{H} \boldsymbol{D} \boldsymbol{u} + \boldsymbol{u}^T \boldsymbol{B} \boldsymbol{v}
$$
Here, $\boldsymbol{u}^T \boldsymbol{H} \boldsymbol{D} \boldsymbol{v}$ is the discrete analogue of $\int u (\partial_x v) dx$, and $\boldsymbol{u}^T \boldsymbol{B} \boldsymbol{v} = u_N v_N - u_1 v_1$ is the discrete analogue of the boundary term $[uv]_a^b$. A crucial special case arises when we set $\boldsymbol{v} = \boldsymbol{u}$:
$$
\boldsymbol{u}^T \boldsymbol{H} \boldsymbol{D} \boldsymbol{u} = - \boldsymbol{u}^T \boldsymbol{H} \boldsymbol{D} \boldsymbol{u} + \boldsymbol{u}^T \boldsymbol{B} \boldsymbol{u} \quad \implies \quad 2\boldsymbol{u}^T \boldsymbol{H} \boldsymbol{D} \boldsymbol{u} = \boldsymbol{u}^T \boldsymbol{B} \boldsymbol{u} \quad \implies \quad \langle \boldsymbol{u}, \boldsymbol{Du} \rangle_{\boldsymbol{H}} = \frac{1}{2} \boldsymbol{u}^T \boldsymbol{B} \boldsymbol{u}
$$
This identity is the cornerstone of SBP-based stability proofs, as it precisely quantifies the energy change due to the derivative operator as a function of boundary values only.

### SBP Operators, Conservation, and Kinetic Energy Preservation

The power of the SBP framework becomes evident when applied to conservation laws.

#### Kinetic Energy Preservation in Linear Advection

Consider the simple [linear advection equation](@entry_id:146245) $\partial_t u + a \partial_x u = 0$. Discretizing in space using an SBP operator $\boldsymbol{D}$ yields the system of ordinary differential equations (ODEs):
$$
\frac{d\boldsymbol{u}}{dt} + a \boldsymbol{D} \boldsymbol{u} = \boldsymbol{0}
$$
The discrete kinetic energy, defined by the SBP norm, is $E_{kin} = \frac{1}{2}\|\boldsymbol{u}\|_{\boldsymbol{H}}^2 = \frac{1}{2}\boldsymbol{u}^T \boldsymbol{H} \boldsymbol{u}$. Its rate of change is:
$$
\frac{dE_{kin}}{dt} = \boldsymbol{u}^T \boldsymbol{H} \frac{d\boldsymbol{u}}{dt} = \boldsymbol{u}^T \boldsymbol{H} (-a \boldsymbol{D} \boldsymbol{u}) = -a \langle \boldsymbol{u}, \boldsymbol{Du} \rangle_{\boldsymbol{H}}
$$
Substituting our key identity, we find:
$$
\frac{dE_{kin}}{dt} = -a \left( \frac{1}{2} \boldsymbol{u}^T \boldsymbol{B} \boldsymbol{u} \right) = -\frac{a}{2} (u_N^2 - u_1^2)
$$
This remarkable result shows that the [semi-discretization](@entry_id:163562) is guaranteed to be stable, as the energy change is determined solely by the energy flux at the boundaries. If the domain is periodic, the [boundary operator](@entry_id:160216) $\boldsymbol{B}$ is the [zero matrix](@entry_id:155836). In this case, $\frac{dE_{kin}}{dt} = 0$, meaning the discrete kinetic energy is perfectly conserved . An operator $\boldsymbol{D}$ with $\boldsymbol{B}=\boldsymbol{0}$ is called **skew-symmetric** with respect to the $\boldsymbol{H}$-inner product, and it is purely non-dissipative. A von Neumann analysis of such schemes confirms this, showing zero numerical dissipation, though they are still dispersive .

#### Global Conservation and Consistency

Beyond energy, we can analyze the conservation of the quantity $\boldsymbol{u}$ itself. The total amount of the conserved quantity in the domain is given by the discrete integral $U_{total} = \sum_i H_{ii} u_i = \boldsymbol{1}^T \boldsymbol{H} \boldsymbol{u}$, where $\boldsymbol{1}$ is the vector of all ones. For a generic conservation law $\partial_t u + \partial_x f(u) = 0$, the [semi-discretization](@entry_id:163562) is $\frac{d\boldsymbol{u}}{dt} + \boldsymbol{D}\boldsymbol{f} = \boldsymbol{0}$, where $\boldsymbol{f}$ is the vector of [numerical flux](@entry_id:145174) values at the grid points. The rate of change of the total quantity is:
$$
\frac{dU_{total}}{dt} = \boldsymbol{1}^T \boldsymbol{H} \frac{d\boldsymbol{u}}{dt} = -\boldsymbol{1}^T \boldsymbol{H} \boldsymbol{D} \boldsymbol{f} = -\boldsymbol{1}^T \boldsymbol{Q} \boldsymbol{f}
$$
A fundamental requirement for a derivative operator is that it should be **consistent with constants**, meaning it must exactly differentiate a [constant function](@entry_id:152060) to zero. In discrete terms, this is the condition $\boldsymbol{D}\boldsymbol{1} = \boldsymbol{0}$, which is equivalent to $\boldsymbol{Q}\boldsymbol{1} = \boldsymbol{0}$. This [consistency condition](@entry_id:198045) has a profound consequence for conservation. Using the SBP property, we have $\boldsymbol{Q}^T \boldsymbol{1} = (\boldsymbol{B} - \boldsymbol{Q})\boldsymbol{1} = \boldsymbol{B}\boldsymbol{1} - \boldsymbol{Q}\boldsymbol{1}$. If $\boldsymbol{Q}\boldsymbol{1}=\boldsymbol{0}$, then $\boldsymbol{Q}^T\boldsymbol{1} = \boldsymbol{B}\boldsymbol{1} = \boldsymbol{e}_N - \boldsymbol{e}_1$. Taking the transpose, we get $\boldsymbol{1}^T \boldsymbol{Q} = \boldsymbol{e}_N^T - \boldsymbol{e}_1^T$.

Substituting this back into our expression for the rate of change of $U_{total}$:
$$
\frac{dU_{total}}{dt} = -(\boldsymbol{e}_N^T - \boldsymbol{e}_1^T)\boldsymbol{f} = -(f_N - f_1) = f_1 - f_N
$$
This is the discrete equivalent of the Fundamental Theorem of Calculus. It states that the total amount of a quantity in the domain changes only due to the flux entering at the left boundary ($f_1$) and leaving at the right ($f_N$). The SBP framework, when consistent, naturally recovers this perfect [flux balance](@entry_id:274729) .

#### Imposing Boundary Conditions with SBP-SAT

In non-periodic problems, boundary conditions must be enforced. The **Simultaneous Approximation Term (SAT)** method is a penalty technique that synergizes with SBP operators to enforce boundary conditions while maintaining stability. For the linear advection equation, the SBP-SAT scheme is:
$$
\frac{d\boldsymbol{u}}{dt} + a \boldsymbol{D} \boldsymbol{u} = \boldsymbol{H}^{-1} \left( \tau_{L} \boldsymbol{e}_{1} ( u_{1} - g_{L}(t) ) + \tau_{R} \boldsymbol{e}_{N} ( u_{N} - g_{R}(t) ) \right)
$$
Here, $g_L$ and $g_R$ are the prescribed boundary data, and $\tau_L, \tau_R$ are penalty parameters. The SAT terms on the right-hand side act as sources or sinks that drive the numerical solution at the boundary ($u_1, u_N$) towards the desired data. Stability analysis (in the $\boldsymbol{H}$-norm) guides the choice of penalty parameters.

When SATs are included, the global conservation property is modified. The rate of change of the total discrete mass $M_h = \boldsymbol{1}^T \boldsymbol{H} \boldsymbol{u}$ becomes :
$$
\frac{dM_h}{dt} = (a u_1 - a u_N) + \tau_{L} (u_1 - g_L) + \tau_{R} (u_N - g_R)
$$
The continuous system conserves mass up to the boundary fluxes, $\frac{dM}{dt} = ag_L - au_N$ (assuming inflow at left). The "conservation error" of the numerical scheme is the difference between the discrete and continuous mass balance. This error is found to be $E(t) = (a + \tau_L)(u_1 - g_L) + \tau_R(u_N - g_R)$. This demonstrates that the scheme is only perfectly conservative if the penalty terms are chosen to make this error zero (e.g., $\tau_L = -a$ for inflow and $\tau_R=0$ for outflow). This highlights a critical principle: SBP-SAT schemes are designed for *stability*, and exact conservation is a separate property that may require specific parameter choices.

### Entropy Stability for Nonlinear Conservation Laws

For [nonlinear systems](@entry_id:168347) like the compressible Euler equations, linear stability is insufficient. Shocks and other discontinuities can form, and a physically correct numerical solution must satisfy the [second law of thermodynamics](@entry_id:142732), which dictates that entropy must not decrease across these discontinuities. This requires a more sophisticated concept: **[entropy stability](@entry_id:749023)**.

#### Mathematical Entropy and the Second Law

A numerical scheme is entropy-stable if it satisfies a discrete version of the [entropy inequality](@entry_id:184404) $\partial_t U(\boldsymbol{u}) + \partial_x F(\boldsymbol{u}) \le 0$. Here, $(U, F)$ is a **mathematical entropy pair**, where $U$ is a convex scalar function of the [conserved variables](@entry_id:747720) $\boldsymbol{u}$, and $F$ is the corresponding entropy flux.

It is critical to distinguish mathematical entropy from [thermodynamic entropy](@entry_id:155885). For the Euler equations, the physical principle is that the [thermodynamic entropy](@entry_id:155885) density, $\rho s$, must not decrease: $\partial_t(\rho s) + \partial_x(\rho s u) \ge 0$. To align the mathematical inequality ($\le 0$) with the physical one ($\ge 0$), the mathematical entropy $U$ must be a decreasing function of the physical entropy. The canonical choice for the ideal gas Euler equations is $U(\boldsymbol{u}) = -\rho s$, where $s = \ln(p\rho^{-\gamma})$. Crucially, it can be proven that this specific function $U(\boldsymbol{u}) = -\rho s$ is a **strictly convex** function of the [conserved variables](@entry_id:747720) $\boldsymbol{u} = (\rho, \rho u, \rho E)^T$. This [convexity](@entry_id:138568) is the key property that enables the construction of provably stable schemes. Other choices, like total energy $\rho E$ or kinetic energy $\frac{1}{2}\rho u^2$, are also convex mathematical entropies, but they do not enforce the second law; they only guarantee conservation/dissipation of their respective quantities .

An important property is that if $(U,F)$ is an entropy pair, so is $(c U, c F)$ for any positive constant $c$. This scaling does not affect the physical principle or the stability of the resulting scheme .

#### Entropy-Conservative Fluxes and the Entropy Potential

The first step in building an entropy-stable scheme is to construct an **entropy-conservative** [numerical flux](@entry_id:145174), $\boldsymbol{f}^*$. This is a two-point [numerical flux](@entry_id:145174) function $\boldsymbol{f}^*(\boldsymbol{u}_L, \boldsymbol{u}_R)$ that, when used with a skew-symmetric SBP operator, exactly conserves the total entropy. The foundation for constructing such fluxes comes from the work of Tadmor.

The theory introduces **entropy variables** $\boldsymbol{v} = \nabla_{\boldsymbol{u}} U$ and an **entropy potential** $\psi$. The entropy flux $F$ can be written as $F(\boldsymbol{u}) = \boldsymbol{v}(\boldsymbol{u})^T \boldsymbol{f}(\boldsymbol{u}) - \psi(\boldsymbol{u})$. An entropy-conservative flux is one that satisfies the condition:
$$
(\boldsymbol{v}_R - \boldsymbol{v}_L)^T \boldsymbol{f}^*(\boldsymbol{u}_L, \boldsymbol{u}_R) = \psi(\boldsymbol{u}_R) - \psi(\boldsymbol{u}_L)
$$
where the subscripts $L$ and $R$ denote the states to the left and right of a cell interface. When this flux is used in an SBP scheme, the contribution from the interior fluxes to the total entropy change forms a [telescoping sum](@entry_id:262349), leading to exact [entropy conservation](@entry_id:749018).

For the one-dimensional Euler equations with the Harten entropy $U = -\frac{\rho s}{\gamma-1}$, a direct but lengthy derivation shows that the entropy potential is remarkably simple :
$$
\psi(\boldsymbol{u}) = m
$$
where $m = \rho u$ is the [momentum density](@entry_id:271360). This elegant result is a cornerstone of modern [entropy-stable schemes](@entry_id:749017). It provides a direct target for constructing [entropy-conservative fluxes](@entry_id:749013). Dissipation is then added to these conservative fluxes to achieve [entropy stability](@entry_id:749023) (non-decreasing entropy) in the presence of shocks.

### Kinetic Energy Preserving (KEP) Schemes for Compressible Flow

In certain [flow regimes](@entry_id:152820), such as decaying homogeneous [isotropic turbulence](@entry_id:199323), the primary mechanism of energy transfer is the inviscid convective motion, and numerical dissipation can contaminate the physically relevant dynamics. For such cases, it is desirable to design schemes where the convective terms, in the absence of pressure and viscous effects, exactly preserve kinetic energy. These are known as **Kinetic Energy Preserving (KEP)** schemes.

#### The General Condition for KEP

For a [semi-discretization](@entry_id:163562) based on a two-point flux-differencing SBP operator on a periodic domain, we can derive a general condition for the convective operator to be KEP. The discrete kinetic energy is $K_d = \sum_i H_{ii} \frac{1}{2}\rho_i u_i^2$. By analyzing its time derivative and setting the contribution from the convective terms to zero, we arrive at a necessary and [sufficient condition](@entry_id:276242) that relates the two-point numerical mass flux, $f^{\rho}_{ij}$, to the two-point numerical convective [momentum flux](@entry_id:199796), $f^{m, \text{conv}}_{ij}$ :
$$
f^{m, \text{conv}}_{ij} = \frac{u_i+u_j}{2} f^{\rho}_{ij}
$$
This condition states that for a scheme to be KEP, its convective [momentum flux](@entry_id:199796) between any two points must equal the [arithmetic mean](@entry_id:165355) of the velocities at those points multiplied by the mass flux between them. Any pair of consistent, symmetric [numerical fluxes](@entry_id:752791) satisfying this identity will produce a KEP scheme. For example, the simple choice of averaging the continuous fluxes, $f^{\rho}_{ij} = \frac{1}{2}(\rho_i u_i + \rho_j u_j)$ and $f^{m, \text{conv}}_{ij} = \frac{1}{2}(\rho_i u_i^2 + \rho_j u_j^2)$, does *not* satisfy this condition and is therefore not KEP. However, the choice $f^{\rho}_{ij} = \frac{1}{2}(\rho_i u_i + \rho_j u_j)$ and $f^{m, \text{conv}}_{ij} = \frac{1}{2}(u_i+u_j) f^{\rho}_{ij}$ does satisfy it by construction.

#### Split-Form Discretizations

An alternative and popular way to construct KEP schemes is to use a **split form** of the governing equations. The convective term in the momentum equation, $\partial_x(\rho u^2)$, can be written in various non-conservative forms. A KEP scheme can be constructed by discretizing a specific blend of these forms. A common skew-symmetric split form for the convective operator, $\mathcal{C}(\boldsymbol{m}, \boldsymbol{u})$, is:
$$
\mathcal{C}(\boldsymbol{m},\boldsymbol{u}) = \frac{1}{2} \boldsymbol{D}(\boldsymbol{m} \circ \boldsymbol{u}) + \frac{1}{2} \mathrm{diag}(\boldsymbol{u}) \boldsymbol{D} \boldsymbol{m} + \frac{1}{2} \mathrm{diag}(\boldsymbol{m}) \boldsymbol{D} \boldsymbol{u}
$$
where $\circ$ denotes the component-wise product. When this operator is used in the momentum equation $\boldsymbol{m}_t = -\mathcal{C}(\boldsymbol{m}, \boldsymbol{u}) - \boldsymbol{D}\boldsymbol{p}$, and combined with the continuity equation $\boldsymbol{\rho}_t = -\boldsymbol{D}\boldsymbol{m}$, a careful analysis of the kinetic energy evolution shows that the contribution from $\mathcal{C}$ is identically zero when using a skew-symmetric SBP operator ($\boldsymbol{Q}=-\boldsymbol{Q}^T$) . The change in kinetic energy is then solely due to the work done by the pressure gradient, $\frac{dK_d}{dt} = -\langle \boldsymbol{u}, \boldsymbol{Dp} \rangle_{\boldsymbol{H}}$. These split forms are algebraically equivalent to specific two-point fluxes that satisfy the general KEP condition . For instance, the KEP scheme for [isentropic flow](@entry_id:267193) can be seen as a split form with a specific blending parameter, and its stability can be analyzed using the [total mechanical energy](@entry_id:167353) as a convex entropy, for which the entropy potential is $\Psi = up$ .

### A Note on SBP Operator Construction

SBP operators are not unique. For a given order of accuracy in the interior of the domain, operators can be constructed with different norm matrices $\boldsymbol{H}$ and different boundary closures. A common distinction is between **diagonal-norm** and **full-norm** (or dense-norm) SBP operators .

-   **Diagonal-Norm SBP Operators:** The norm matrix $\boldsymbol{H}$ is diagonal. These operators are simpler to implement, particularly the inversion of $\boldsymbol{H}$ in SBP-SAT schemes. However, to maintain the SBP property, the [order of accuracy](@entry_id:145189) at the boundary stencils is typically lower than the interior accuracy. For example, a second-order interior scheme might have first-order boundary closures.

-   **Full-Norm SBP Operators:** The norm matrix $\boldsymbol{H}$ is dense (or block-diagonal near the boundaries). These operators are more complex but allow for the boundary closure to have the same order of accuracy as the interior stencil, which can be advantageous for overall solution accuracy.

Both types of operators satisfy the crucial SBP property $Q+Q^T=B$ and can be used to build stable schemes. The choice between them is a trade-off between implementation complexity and boundary accuracy. It is important to remember that stability proofs for SBP schemes are always formulated in the discrete $\boldsymbol{H}$-norm, $\|\cdot\|_{\boldsymbol{H}}$. Stability in the standard Euclidean norm is not guaranteed, and in fact, the derivative operator $\boldsymbol{D}$ is generally not a [normal matrix](@entry_id:185943).