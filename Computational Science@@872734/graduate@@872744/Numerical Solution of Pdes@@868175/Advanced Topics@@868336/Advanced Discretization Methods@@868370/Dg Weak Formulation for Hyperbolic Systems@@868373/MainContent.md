## Introduction
Hyperbolic [systems of conservation laws](@entry_id:755768) are fundamental to modeling a vast array of physical phenomena, from [gas dynamics](@entry_id:147692) to [traffic flow](@entry_id:165354), often characterized by the formation of shocks and discontinuities. Numerically approximating these systems presents a significant challenge, requiring methods that can handle complex geometries, capture sharp features without [spurious oscillations](@entry_id:152404), and deliver [high-order accuracy](@entry_id:163460). The Discontinuous Galerkin (DG) method has emerged as a uniquely powerful solution, elegantly combining the geometric flexibility of [finite element methods](@entry_id:749389) with the shock-capturing prowess of [finite volume](@entry_id:749401) schemes. This article provides a comprehensive exploration of the DG weak formulation, from its theoretical underpinnings to its application at the frontiers of computational science.

The journey begins in **Principles and Mechanisms**, where we derive the weak formulation step-by-step. This chapter illuminates the core concepts of element-wise [polynomial approximation](@entry_id:137391), the crucial introduction of the [numerical flux](@entry_id:145174) to handle discontinuities, and the resulting semi-discrete system. It further delves into the stability and accuracy properties that make the DG method robust and reliable. Next, **Applications and Interdisciplinary Connections** demonstrates the method's remarkable versatility. We will see how the foundational principles are adapted to tackle real-world problems in geophysical flows, compressible turbulence, and network systems, and how the framework extends to advanced topics like adjoint-based error analysis and [data-driven modeling](@entry_id:184110). Finally, **Hands-On Practices** provides a set of targeted problems designed to solidify understanding by applying the concepts to derive key results in stability, [well-balancing](@entry_id:756695), and sensitivity analysis. Through this structured exploration, readers will gain a deep appreciation for the theory, practice, and power of the DG method.

## Principles and Mechanisms

The Discontinuous Galerkin (DG) method provides a powerful framework for the numerical approximation of hyperbolic [systems of conservation laws](@entry_id:755768). Its strength lies in its ability to combine the geometric flexibility of [finite element methods](@entry_id:749389) with the [high-order accuracy](@entry_id:163460) and shock-capturing capabilities often associated with finite volume schemes. This chapter elucidates the fundamental principles and mechanisms that underpin the DG [weak formulation](@entry_id:142897), starting from its derivation and moving through its analytical properties and practical implementation details.

### The Foundational Weak Formulation

We begin with a general system of [hyperbolic conservation laws](@entry_id:147752) in $d$ spatial dimensions, expressed as:
$$
\boldsymbol{u}_t + \nabla\cdot \boldsymbol{f}(\boldsymbol{u}) = \boldsymbol{0}
$$
Here, $\boldsymbol{u}(\boldsymbol{x}, t)$ is a vector of $m$ [conserved quantities](@entry_id:148503) in the spatial domain $\Omega \subset \mathbb{R}^d$, and $\boldsymbol{f}: \mathbb{R}^m \to \mathbb{R}^{m \times d}$ is the flux tensor. The core idea of the DG method is to partition the domain $\Omega$ into a mesh $\mathcal{T}_h$ of non-overlapping elements $K$. Within each element, the solution is approximated by a function from a finite-dimensional [polynomial space](@entry_id:269905), typically the space of polynomials of degree at most $p$, denoted $\mathcal{P}^p(K)$. Crucially, the approximate solution, $\boldsymbol{u}_h$, is allowed to be discontinuous across the boundaries of these elements.

To derive the weak formulation, we follow the standard Galerkin procedure. We multiply the PDE by an arbitrary vector-valued test function $\boldsymbol{v}_h$, which belongs to the same [polynomial space](@entry_id:269905) as $\boldsymbol{u}_h$, and integrate over a single element $K$:
$$
\int_K \boldsymbol{v}_h^\top (\boldsymbol{u}_{h,t} + \nabla\cdot \boldsymbol{f}(\boldsymbol{u}_h)) \, \mathrm{d}\boldsymbol{x} = 0
$$

A key step in the DG formulation is to apply the divergence theorem ([integration by parts](@entry_id:136350)) to the flux divergence term. This serves to weaken the derivative requirement on the solution and naturally introduces boundary terms. Applying this to the second term gives:
$$
\int_K \boldsymbol{v}_h^\top (\nabla\cdot \boldsymbol{f}(\boldsymbol{u}_h)) \, \mathrm{d}\boldsymbol{x} = \int_{\partial K} \boldsymbol{v}_h^\top (\boldsymbol{f}(\boldsymbol{u}_h) \cdot \boldsymbol{n}) \, \mathrm{d}s - \int_K \nabla\boldsymbol{v}_h : \boldsymbol{f}(\boldsymbol{u}_h) \, \mathrm{d}\boldsymbol{x}
$$
where $\boldsymbol{n}$ is the outward unit normal to the boundary $\partial K$, and the colon notation $\nabla\boldsymbol{v}_h : \boldsymbol{f}(\boldsymbol{u}_h)$ represents the [tensor contraction](@entry_id:193373) $\sum_{i,j} (\partial_{x_j} v_{h,i}) f_{i,j}$.

Substituting this back into our integrated equation, we arrive at:
$$
\int_K \boldsymbol{v}_h^\top \boldsymbol{u}_{h,t} \, \mathrm{d}\boldsymbol{x} - \int_K \nabla\boldsymbol{v}_h : \boldsymbol{f}(\boldsymbol{u}_h) \, \mathrm{d}\boldsymbol{x} + \int_{\partial K} \boldsymbol{v}_h^\top (\boldsymbol{f}(\boldsymbol{u}_h) \cdot \boldsymbol{n}) \, \mathrm{d}s = 0
$$

At this point, we confront the central challenge posed by the discontinuous nature of $\boldsymbol{u}_h$. On any face $F$ of the element boundary $\partial K$, the trace of the solution $\boldsymbol{u}_h$ is ambiguous. A face $F$ shared between elements $K^-$ and $K^+$ has two distinct solution values, the interior trace $\boldsymbol{u}_h^-$ (from within $K^-$) and the exterior trace $\boldsymbol{u}_h^+$ (from within $K^+$). Consequently, the physical flux $\boldsymbol{f}(\boldsymbol{u}_h) \cdot \boldsymbol{n}$ is not uniquely defined on the interface.

The DG method resolves this ambiguity by replacing the physical flux in the boundary integral with a **numerical flux**, denoted $\hat{\boldsymbol{f}}(\boldsymbol{u}_h^-, \boldsymbol{u}_h^+; \boldsymbol{n})$. This numerical flux is a single-valued function that depends on the state on both sides of the interface and the normal vector. By convention, we use the interior trace of the [test function](@entry_id:178872), $\boldsymbol{v}_h^-$. This leads to the canonical semi-discrete DG weak formulation [@problem_id:3377294]: For every element $K \in \mathcal{T}_h$, we seek $\boldsymbol{u}_h(\cdot,t) \in [\mathcal{P}^p(K)]^m$ such that for all test functions $\boldsymbol{v}_h \in [\mathcal{P}^p(K)]^m$:
$$
\int_K \boldsymbol{v}_h^\top \boldsymbol{u}_{h,t} \, \mathrm{d}\boldsymbol{x} - \int_K \nabla\boldsymbol{v}_h : \boldsymbol{f}(\boldsymbol{u}_h) \, \mathrm{d}\boldsymbol{x} + \int_{\partial K} \boldsymbol{v}_h^-{}^\top \hat{\boldsymbol{f}}(\boldsymbol{u}_h^-, \boldsymbol{u}_h^+; \boldsymbol{n}) \, \mathrm{d}s = 0
$$
This equation holds for each element in the mesh, forming a coupled system of ordinary differential equations (ODEs) for the time-dependent coefficients of the polynomial approximation.

### Essential Properties of the Numerical Flux

The choice of [numerical flux](@entry_id:145174) $\hat{\boldsymbol{f}}$ is critical to the stability and accuracy of the DG method. A valid [numerical flux](@entry_id:145174) must satisfy several key properties.

First is **consistency**: if the solution is continuous across an interface (i.e., $\boldsymbol{u}^- = \boldsymbol{u}^+ = \boldsymbol{u}$), the numerical flux must revert to the physical flux. This ensures that in regions where the discrete solution is smooth, the scheme is a consistent approximation of the original PDE. Mathematically:
$$
\hat{\boldsymbol{f}}(\boldsymbol{u}, \boldsymbol{u}; \boldsymbol{n}) = \boldsymbol{f}(\boldsymbol{u}) \cdot \boldsymbol{n}
$$

Second is **conservation**. The DG method should preserve the total amount of the conserved quantity $\boldsymbol{u}$ over the entire domain $\Omega$, assuming no flux through the domain boundary (e.g., with [periodic boundary conditions](@entry_id:147809)). To see how this is achieved, we choose a constant [test function](@entry_id:178872), $\boldsymbol{v}_h = \boldsymbol{c}$, on a given element $K$. In this case, $\nabla\boldsymbol{v}_h = \boldsymbol{0}$, and the [weak formulation](@entry_id:142897) simplifies to:
$$
\boldsymbol{c}^\top \frac{d}{dt} \int_K \boldsymbol{u}_h \, \mathrm{d}\boldsymbol{x} = -\boldsymbol{c}^\top \int_{\partial K} \hat{\boldsymbol{f}}(\boldsymbol{u}_h^-, \boldsymbol{u}_h^+; \boldsymbol{n}) \, \mathrm{d}s
$$
Summing over all elements $K$ in the mesh, the total rate of change of the quantity is:
$$
\frac{d}{dt} \int_\Omega \boldsymbol{u}_h \, \mathrm{d}\boldsymbol{x} = -\sum_{K \in \mathcal{T}_h} \int_{\partial K} \hat{\boldsymbol{f}}(\boldsymbol{u}_h^-, \boldsymbol{u}_h^+; \boldsymbol{n}_K) \, \mathrm{d}s
$$
The sum on the right-hand side covers every face of every element. For any interior face $F$ shared by elements $K^-$ and $K^+$, the face appears twice in the sum, once with normal $\boldsymbol{n}^-$ and once with normal $\boldsymbol{n}^+ = -\boldsymbol{n}^-$. The total contribution from this face is the integral of $\hat{\boldsymbol{f}}(\boldsymbol{u}^-, \boldsymbol{u}^+; \boldsymbol{n}^-) + \hat{\boldsymbol{f}}(\boldsymbol{u}^+, \boldsymbol{u}^-; \boldsymbol{n}^+)$. For the total sum to be zero (ensuring global conservation), the integrand must vanish on every interior face. This gives the conservation condition [@problem_id:3377294]:
$$
\hat{\boldsymbol{f}}(\boldsymbol{u}^-, \boldsymbol{u}^+; \boldsymbol{n}) + \hat{\boldsymbol{f}}(\boldsymbol{u}^+, \boldsymbol{u}^-; -\boldsymbol{n}) = \boldsymbol{0}
$$
This condition simply states that the flux leaving one element across a face must be equal to the flux entering the adjacent element through the same face.

A widely used class of numerical fluxes that satisfy these properties is **upwind fluxes**. For a simple [linear advection equation](@entry_id:146245) $u_t + a u_x = 0$, the [upwind flux](@entry_id:143931) is $a u^-$ if the advection speed $a$ is positive (information flows from left to right) and $a u^+$ if $a$ is negative. For systems, the direction of information flow is determined by the signs of the eigenvalues of the matrix $\boldsymbol{A}_n = \frac{\partial(\boldsymbol{f}\cdot\boldsymbol{n})}{\partial\boldsymbol{u}}$. Other common choices include the Lax-Friedrichs flux, which adds numerical dissipation, and central fluxes, which are simpler but can be less stable.

### The Discrete System: A System of ODEs

The DG weak formulation defines a system of ODEs for the time-dependent coefficients of the polynomial approximation. This is often termed the **Method of Lines (MoL)**. Let's make this concrete. On a [reference element](@entry_id:168425), we choose a set of basis functions $\{\phi_j(\boldsymbol{\xi})\}_{j=1}^{N_p}$, where $N_p$ is the number of degrees of freedom per component. The solution on element $K$ is expanded as:
$$
\boldsymbol{u}_h(\boldsymbol{x}, t) = \sum_{j=1}^{N_p} \boldsymbol{c}_j(t) \phi_j(\boldsymbol{\xi}(\boldsymbol{x}))
$$
where $\boldsymbol{c}_j(t) \in \mathbb{R}^m$ are the vector-valued degrees of freedom. By substituting this expansion into the [weak formulation](@entry_id:142897) and testing against each [basis function](@entry_id:170178) $\boldsymbol{v}_h = \phi_i(\boldsymbol{\xi}) \boldsymbol{e}_k$ (where $\boldsymbol{e}_k$ is a standard basis vector in $\mathbb{R}^m$), we obtain a matrix system.

This system takes the general form:
$$
\boldsymbol{M} \frac{d\boldsymbol{C}}{dt} = \boldsymbol{L}(\boldsymbol{C})
$$
where $\boldsymbol{C}$ is the global vector of all coefficients $\boldsymbol{c}_j$. The **mass matrix** $\boldsymbol{M}$ arises from the time-derivative term. For a single element, its entries are given by $M_{ij} = \int_K \phi_i \phi_j \, \mathrm{d}\boldsymbol{x}$. If the basis functions are orthogonal, this matrix is diagonal; otherwise, it is symmetric and positive definite. The right-hand side, $\boldsymbol{L}(\boldsymbol{C})$, represents the spatial operator, encompassing both the volume and face integral terms.

For example, consider the P2 (quadratic) approximation for a scalar problem on the reference element $K = [-1, 1]$ using the monomial basis $\{1, \xi, \xi^2\}$. The local [mass matrix](@entry_id:177093) entries are $M_{ij} = \int_{-1}^1 \xi^i \xi^j \, d\xi$ for $i,j \in \{0, 1, 2\}$. Direct computation yields [@problem_id:3377336]:
$$
\boldsymbol{M} = \begin{pmatrix} 2  & 0 & \frac{2}{3} \\ 0 & \frac{2}{3} & 0 \\ \frac{2}{3} & 0 & \frac{2}{5} \end{pmatrix}
$$
The properties of this matrix, such as its condition number $\kappa(\boldsymbol{M}) = \lambda_{\max}/\lambda_{\min}$, are crucial for practical computations. For this specific matrix, $\kappa(\boldsymbol{M}) = (71 + 9\sqrt{61})/10$. A large condition number can negatively impact the stability and efficiency of [explicit time-stepping](@entry_id:168157) schemes [@problem_id:3377336].

### Stability and Accuracy Analysis

A central concern for any numerical method is its stability and accuracy. For DG methods, these properties are analyzed using two primary approaches: the [energy method](@entry_id:175874) and Fourier analysis.

#### $L^2$-Energy Stability

The [energy method](@entry_id:175874) provides insight into the stability of the scheme in the $L^2$ norm. Consider the total discrete energy $E(t) = \frac{1}{2} \int_\Omega |\boldsymbol{u}_h|^2 \, \mathrm{d}\boldsymbol{x}$. We can analyze its time evolution by setting the test function $\boldsymbol{v}_h = \boldsymbol{u}_h$ in the [weak formulation](@entry_id:142897) and summing over all elements. For the [linear advection equation](@entry_id:146245) with an [upwind flux](@entry_id:143931), this analysis reveals that the rate of change of energy is given by a sum of non-positive terms related to the jumps in the solution at interfaces, $\llbracket \boldsymbol{u}_h \rrbracket = \boldsymbol{u}_h^+ - \boldsymbol{u}_h^-$:
$$
\frac{dE}{dt} = -\sum_{\text{faces } F} \int_F \frac{|a_n|}{2} \llbracket u_h \rrbracket^2 \, \mathrm{d}s \le 0
$$
where $a_n$ is the normal advection speed. This demonstrates that the semi-discrete DG scheme is **$L^2$-stable**; the energy does not grow in time. This dissipation at the jumps is a key mechanism that allows DG methods to remain stable in the presence of sharp gradients or discontinuities. This property is fundamental to the design of **Strong Stability Preserving (SSP)** [time integrators](@entry_id:756005), which are constructed to maintain this energy-dissipating property at the fully-discrete level when a suitable time-step restriction is met [@problem_id:3377327].

In contrast, if a non-dissipative central flux were used, the energy rate would be zero, leading to an energy-conserving scheme. While this may seem desirable, the lack of dissipation can make the scheme susceptible to instabilities from aliasing errors, particularly for nonlinear problems.

#### Dispersion and Dissipation Analysis

For linear problems on uniform periodic meshes, Fourier analysis offers a more precise characterization of a scheme's accuracy. By analyzing how the scheme propagates plane-wave solutions of the form $u_j(t) = \hat{u} \exp(i j \theta - i \omega t)$, where $\theta = k h$ is the non-dimensional wavenumber, we can derive the scheme's **[dispersion relation](@entry_id:138513)**, which connects the numerical frequency $\omega$ to the [wavenumber](@entry_id:172452) $k$.

The real part of $\omega$ determines the **numerical phase speed**, $c_{\text{DG}} = \Re(\omega)/k$, while its imaginary part corresponds to numerical dissipation (or growth). For the exact PDE $u_t + a u_x = 0$, the phase speed is constant, $c_{\text{exact}} = a$. For [numerical schemes](@entry_id:752822), $c_{\text{DG}}$ typically depends on the wavenumber, meaning waves of different lengths travel at different speeds, an effect known as **[numerical dispersion](@entry_id:145368)**.

For a DG(0) scheme (piecewise constants, equivalent to a first-order upwind [finite volume method](@entry_id:141374)) applied to $u_t - a u_x = 0$ (with $a>0$, implying a left-propagating wave), the numerical phase speed is $c_{\text{DG}} = -a \frac{\sin(kh)}{kh}$. The signed relative phase speed error is therefore [@problem_id:3377312]:
$$
\varepsilon(\theta) = \frac{c_{\text{DG}}}{c_{\text{exact}}} - 1 = \frac{\sin(kh)}{kh} - 1
$$
This shows that for all $kh > 0$, the numerical phase speed is less than the exact speed (a lagging phase error), a hallmark of many dissipative schemes. The analysis can be extended to higher-order polynomials, such as the P1 case, where it reveals the existence of both a physical mode that approximates the true solution and non-physical, rapidly damped spurious modes [@problem_id:3377306].

### Practical Implementation Aspects

#### Mapped Elements and Quadrature

In practice, computations are almost always performed on a standard [reference element](@entry_id:168425) (e.g., the interval $[-1,1]$ or the reference triangle). A mapping function $\boldsymbol{x}(\boldsymbol{\xi})$ transforms the [reference element](@entry_id:168425) to the physical element $K$. This transformation introduces a Jacobian determinant into the [volume integrals](@entry_id:183482) and a corresponding scaling factor for face integrals.

For example, on a 2D curvilinear element, the bottom face might be parameterized by $\xi \in [-1,1]$. The physical [tangent vector](@entry_id:264836) along this face is $\boldsymbol{t}(\xi) = \frac{d\boldsymbol{x}}{d\xi}$, and the differential arclength is $ds = \|\boldsymbol{t}(\xi)\| d\xi$. The outward normal vector $\boldsymbol{n}$ must also be computed from the mapping's geometry. The evaluation of a face integral requires substituting the solution and test functions (expressed in reference coordinates), computing the numerical flux (which may depend on the physical normal $\boldsymbol{n}$), and integrating with respect to the reference coordinate $\xi$ using the correct [geometric scaling](@entry_id:272350) factor [@problem_id:3377335].

The integrals in the [weak form](@entry_id:137295) are rarely computed analytically. Instead, **numerical quadrature** is used. A [quadrature rule](@entry_id:175061) of degree $Q$ can exactly integrate any polynomial of degree up to $Q$. For nonlinear problems, where the flux $\boldsymbol{f}(\boldsymbol{u}_h)$ is a nonlinear function of the degree-$p$ polynomial $\boldsymbol{u}_h$, the integrand can be a very high-degree polynomial. If the [quadrature rule](@entry_id:175061) is not accurate enough, **aliasing errors** are introduced, which can corrupt the stability properties of the scheme. To avoid this, the [quadrature rule](@entry_id:175061) must be chosen with sufficient accuracy. If the flux $\boldsymbol{f}(\boldsymbol{u})$ is a polynomial of degree $r$ in its arguments, the integrand in the face integral, $\boldsymbol{v}_h^\top \hat{\boldsymbol{f}}$, will be a polynomial of degree $p + rp$. This dictates that the quadrature rule must be exact for polynomials of degree at least $Q = p(r+1)$ [@problem_id:3377334].

#### Time-Stepping and the CFL Condition

Solving the semi-discrete system $\boldsymbol{M} d\boldsymbol{C}/dt = \boldsymbol{L}(\boldsymbol{C})$ requires a [time integration](@entry_id:170891) scheme. For hyperbolic problems, explicit methods like SSP Runge-Kutta schemes are common. These methods are conditionally stable, meaning the time step $\Delta t$ must be restricted by a **Courant-Friedrichs-Lewy (CFL) condition**. For a DG scheme, this condition takes the form:
$$
\Delta t \le C_{\text{CFL}} \frac{h}{\alpha_{\max}(2p+1)}
$$
where $h$ is a measure of the element size, $\alpha_{\max}$ is the maximum wave speed in the system, $p$ is the polynomial degree, and $C_{\text{CFL}}$ is a constant of order one that depends on the specific time integrator and mesh geometry. The factor $(2p+1)$ arises from the ratio of the solution's norm on an element's boundary to its norm in the interior, which can be bounded using polynomial trace inequalities. This factor shows that for a fixed mesh size, higher-order methods require significantly smaller time steps for stability [@problem_id:3377303].

### Advanced Concepts and Extensions

#### Nonlinear Stability and Entropy Conservation

For nonlinear systems developing shocks, such as the Burgers' equation $u_t + \partial_x(u^2/2)=0$, L2-stability is not sufficient. A stronger condition related to [entropy stability](@entry_id:749023) is needed. Aliasing errors from inexact quadrature are a primary source of instability. One advanced technique to enhance robustness is to use a **split-form** or **skew-symmetric** formulation of the flux divergence. This involves rewriting the volume term $\nabla\cdot\boldsymbol{f}(\boldsymbol{u})$ as a combination of conservative and non-conservative forms.

In a discrete nodal DG setting with Summation-By-Parts (SBP) properties, one can construct a [flux splitting](@entry_id:637102) that makes the volume contribution to the energy rate a pure boundary term, thereby eliminating internal, aliasing-driven energy production. For Burgers' equation, this is achieved with a specific 50-50 split between the strong and weak forms of the derivative operator [@problem_id:3377315]. Such entropy-conservative formulations are a cornerstone of modern, robust DG schemes for shock-dominated flows.

#### Alternative DG Formulations

While the standard DG method is powerful, the large number of globally coupled degrees of freedom can be a drawback. This has motivated the development of related methods.

The **Hybridizable Discontinuous Galerkin (HDG)** method introduces an additional unknown, $\widehat{\boldsymbol{w}}$, representing the solution trace on the mesh skeleton. The interior solutions on each element are then solved for locally in terms of this trace unknown. This allows for **[static condensation](@entry_id:176722)**, where the element-interior unknowns are eliminated algebraically, resulting in a much smaller global system that only couples the trace unknowns on the element faces. For a 2D problem with polynomial degree $k$, the number of globally coupled unknowns in HDG is smaller than in DG by a factor of approximately $3/(k+2)$ [@problem_id:3377337].

Another important variant is the **space-time DG** method. Instead of applying the Method of Lines, this approach treats time as another dimension and discretizes space-time slabs. This provides a fully discrete formulation directly and can offer superior conservation and stability properties. For instance, space-time DG methods are inherently mass-conservative regardless of the polynomial degrees used in space and time, and the choice of a central flux in space-time can lead to exact [energy conservation](@entry_id:146975) for linear problems [@problem_id:3377327].

These principles and mechanisms form the theoretical and practical foundation of the DG method for [hyperbolic systems](@entry_id:260647), enabling its successful application to a wide array of problems in science and engineering.