## Introduction
Hyperbolic conservation laws, such as the Euler equations governing fluid dynamics, are fundamental to modeling a vast array of physical phenomena. A central challenge in their numerical solution is the natural tendency for smooth initial conditions to evolve into discontinuous solutions like shock waves. Traditional numerical methods often struggle to capture these features with both accuracy and stability. The Discontinuous Galerkin (DG) method has emerged as a particularly powerful and flexible framework to address this challenge, uniquely blending the high-order accuracy of finite element methods with the shock-capturing robustness of finite volume schemes.

This article provides a thorough exploration of DG methods for conservation laws. It is designed to bridge the gap between abstract theory and practical application, guiding the reader from first principles to advanced implementation. To achieve this, the material is structured into three distinct chapters. First, in "Principles and Mechanisms," we will deconstruct the mathematical and algorithmic foundations of the DG method. Next, "Applications and Interdisciplinary Connections" will showcase the method's versatility by exploring its use in solving real-world problems across aerospace engineering, geophysics, and computational physics. Finally, "Hands-On Practices" will offer a set of guided problems to solidify understanding and build practical implementation skills.

## Principles and Mechanisms

Having established the context and significance of Discontinuous Galerkin (DG) methods for conservation laws in the preceding introduction, this chapter delves into the foundational principles and core mechanisms that define these powerful numerical techniques. We will deconstruct the method, beginning with its mathematical underpinnings in the theory of weak solutions, proceeding through the construction of the discrete system, and culminating in a discussion of the practical and advanced considerations essential for robust simulations of complex phenomena, such as those encountered in aerospace computational fluid dynamics.

### From Classical to Weak Solutions: The Foundation for Discontinuities

Hyperbolic conservation laws, such as the Euler equations governing inviscid fluid flow, are distinguished by their capacity to develop and sustain discontinuous solutions, even from smooth initial data. These discontinuities, which manifest physically as shock waves or contact surfaces, pose a fundamental challenge to classical mathematical analysis. A **classical solution** to a partial differential equation (PDE) is one that is continuously differentiable to the order of the highest derivative in the equation, allowing the PDE to be satisfied at every point in the domain. However, in the presence of a shock, the solution is not differentiable, and the notion of a classical solution breaks down.

To accommodate such solutions, the mathematical framework must be broadened. This is achieved through the concept of a **weak solution**. Instead of requiring the PDE to hold pointwise, we enforce it in an integral sense. Consider a scalar conservation law in one dimension, $\partial_t u + \partial_x f(u) = 0$. The weak formulation is derived by multiplying the PDE by a smooth **test function** $\varphi$, typically chosen from the space of infinitely differentiable functions with compact support, denoted $C_c^\infty$. Integrating over the entire space-time domain and applying integration by parts (an application of the divergence theorem) transfers the derivatives from the solution variable $u$ to the smooth test function $\varphi$.

Specifically, a locally integrable function $u \in L^1_{\mathrm{loc}}$ is a weak solution if it satisfies the following integral identity for all test functions $\varphi \in C_c^\infty(\mathbb{R} \times 0,T))$:
$$
\int_0^T \int_{-\infty}^{\infty} \left( u \frac{\partial \varphi}{\partial t} + f(u) \frac{\partial \varphi}{\partial x} \right) \, dx \, dt + \int_{-\infty}^{\infty} u_0(x) \varphi(x,0) \, dx = 0
$$
where $u_0(x)$ is the initial condition. Notice that this formulation requires no derivatives of $u$, only its [integrability. The initial condition is incorporated naturally through the temporal integration by parts. This framework is the bedrock upon which numerical methods for conservation laws are built, as it provides a rigorous basis for handling solutions with jumps. The Discontinuous Galerkin method is, at its core, a finite element-type discretization of this weak formulation [@problem_id:3955010].

### The Discontinuous Galerkin Method: A Local Weak Formulation

The central idea of the Discontinuous Galerkin method is to discretize the domain $\Omega$ into a collection of non-overlapping elements $K$ (e.g., intervals, triangles, hexahedra), forming a mesh $\mathcal{T}_h$. Instead of seeking a solution that is continuous across the entire domain, the DG method seeks an approximate solution $u_h$ that is a polynomial within each element but is permitted to be discontinuous across the boundaries between elements.

This choice of solution space necessitates a corresponding modification of the function spaces used in the analysis. The natural setting for DG methods is not the standard Sobolev space $H^s(\Omega)$, which imposes global smoothness constraints, but rather the **broken Sobolev space**. For a given mesh $\mathcal{T}_h$ of the domain $\Omega$, the broken Sobolev space $H^s(\mathcal{T}_h)$ is defined as the set of functions that are square-integrable on $\Omega$ and whose restriction to each element $K \in \mathcal{T}_h$ belongs to the standard local Sobolev space $H^s(K)$ [@problem_id:3954972]. Formally,
$$
H^s(\mathcal{T}_h) \equiv \left\{ v \in L^2(\Omega) \,:\, v|_K \in H^s(K)\ \text{for all}\ K \in \mathcal{T}_h \right\}
$$
The crucial difference is that no continuity is enforced at the interfaces between elements. This allows a function in $H^s(\mathcal{T}_h)$ to have different trace values when an interface is approached from either side, a feature forbidden in the global space $H^s(\Omega)$ for $s > 1/2$.

The DG approximation space, $V_h^p$, is a finite-dimensional subspace of this broken space, typically consisting of piecewise polynomials of degree at most $p$ on each element:
$$
V_h^p = \{ v \in L^2(\Omega) : v|_K \in P^p(K) \text{ for all } K \in \mathcal{T}_h \}
$$
Here, $P^p(K)$ represents the space of polynomials on element $K$. A global basis for $V_h^p$ is constructed by simply taking the union of local polynomial bases defined on each element. A key consequence of this construction is that each global basis function has a support limited to a single element [@problem_id:3955009]. This locality is a defining feature of the DG method and has profound implications for the structure of the resulting discrete system.

### Assembling the Semi-Discrete System: Volume and Surface Integrals

With the approximation space defined, we derive the semi-discrete DG formulation by applying the weak formulation on each element $K \in \mathcal{T}_h$. We seek an approximate solution $u_h \in V_h^p$ such that for every test function $v_h \in V_h^p$, the following holds for each element $K$:
$$
\int_K \frac{\partial u_h}{\partial t} v_h \, d\boldsymbol{x} + \int_K (\nabla \cdot \boldsymbol{f}(u_h)) v_h \, d\boldsymbol{x} = 0
$$
Applying integration by parts to the flux term, we obtain:
$$
\int_K \frac{\partial u_h}{\partial t} v_h \, d\boldsymbol{x} - \int_K \boldsymbol{f}(u_h) \cdot \nabla v_h \, d\boldsymbol{x} + \int_{\partial K} (\boldsymbol{f}(u_h) \cdot \boldsymbol{n}) v_h \, dS = 0
$$
where $\boldsymbol{n}$ is the outward unit normal to the boundary of the element, $\partial K$.

The surface integral term, $\int_{\partial K} (\boldsymbol{f}(u_h) \cdot \boldsymbol{n}) v_h \, dS$, is the conduit for communication between neighboring elements. However, since the solution $u_h$ is discontinuous across element boundaries, the flux $\boldsymbol{f}(u_h)$ is ambiguous at an interface. To resolve this, the physical flux $\boldsymbol{f}(u_h)$ on the boundary is replaced by a uniquely defined **numerical flux**, denoted $\hat{\boldsymbol{f}}(u_h^-, u_h^+)$. This function depends on the two values of the solution at the interface: the interior trace ($u_h^-$) and the exterior trace from the adjacent element ($u_h^+$) [@problem_id:3955010].

Summing the element-wise weak forms over all elements in the mesh, the complete semi-discrete formulation becomes:
$$
\frac{d}{dt} \int_{\Omega} u_h v_h \, d\boldsymbol{x} = \sum_{K \in \mathcal{T}_h} \left( \int_K \boldsymbol{f}(u_h) \cdot \nabla v_h \, d\boldsymbol{x} - \int_{\partial K} (\hat{\boldsymbol{f}}(u_h^-, u_h^+) \cdot \boldsymbol{n}) v_h^- \, dS \right)
$$
This is a method-of-lines formulation, resulting in a system of ordinary differential equations (ODEs) for the time-dependent coefficients of the polynomial basis functions. A careful rearrangement of the sum of surface integrals over all elements reveals that the total contribution from the interfaces provides the crucial coupling between elements. For a one-dimensional problem on a periodic domain, for instance, the sum of all interface contributions can be elegantly expressed as a sum over all interfaces of the jump in the test function multiplied by the numerical flux [@problem_id:3954965]:
$$
\sum_{i=1}^{N} [v_h]_{i+1/2} \hat{f}(u_h^-_{i+1/2}, u_h^+_{i+1/2})
$$
where $[v_h] = v_h^- - v_h^+$ is the jump operator. This term explicitly shows how information is exchanged across the discontinuities of the approximate solution.

### The Numerical Flux: Heart of the DG Method

The numerical flux $\hat{\boldsymbol{f}}$ is not arbitrary; it must satisfy certain properties to ensure that the resulting scheme is stable and converges to the correct weak solution. The most fundamental properties are [@problem_id:3955000]:

1.  **Consistency**: The numerical flux must be consistent with the physical flux, meaning that if the states on both sides of the interface are identical, the numerical flux must equal the physical flux: $\hat{\boldsymbol{f}}(u, u) = \boldsymbol{f}(u)$. This ensures that the scheme is accurate for smooth solutions.

2.  **Conservation**: Implicit in the single-valued nature of $\hat{\boldsymbol{f}}$ is conservation. The flux leaving one element is precisely the flux entering the adjacent element, ensuring that the scheme is globally conservative.

3.  **Monotonicity** (for scalar problems): A numerical flux $\hat{f}(u^-, u^+)$ is monotone if it is non-decreasing with respect to its first argument ($u^-$) and non-increasing with respect to its second ($u^+$). This property is sufficient to guarantee that the semi-discretization does not introduce new oscillations and is crucial for proving stability results like total variation diminishing (TVD) properties for first-order schemes.

Various numerical fluxes have been designed, broadly classified as central or upwind-type.
*   The **Central Flux**, $\hat{f}_C(u^-,u^+) = \frac{1}{2}(f(u^-) + f(u^+))$, is simple and consistent but not monotone. It lacks inherent dissipation and often relies on the scheme's other properties for stability, which may be insufficient for strong shocks.
*   **Upwind-type fluxes** incorporate information about the direction of wave propagation (characteristic speeds) to introduce numerical dissipation that stabilizes the scheme.
    *   The **Lax–Friedrichs (or Rusanov) Flux** adds a penalty term proportional to the jump in the solution: $\hat{f}_{LF}(u^-,u^+) = \frac{1}{2}(f(u^-) + f(u^+)) - \frac{\alpha}{2}(u^+ - u^-)$. If the penalty parameter $\alpha$ is chosen to be greater than or equal to the maximum local characteristic speed, the flux becomes monotone.
    *   The **Godunov Flux** is the archetypal upwind flux, derived from the exact solution of the local Riemann problem defined by the states $(u^-, u^+)$. It is known to be monotone for scalar convex conservation laws and provides the exact amount of dissipation needed.
    *   The **Roe Flux** is based on a linearized Riemann problem. While computationally efficient and popular, it is not always monotone and can fail to select the physically correct solution (i.e., it can admit entropy-violating shocks) unless an "entropy fix" is applied [@problem_id:3955000].

### From Theory to Practice: Implementation Details

Implementing a DG method requires handling several practical geometric and computational details.

#### Reference Element Mapping
To simplify computations, all integrations are performed on a fixed **reference element**, $\hat{K}$ (e.g., the interval $[-1, 1]$ in 1D, or the triangle with vertices $(0,0), (1,0), (0,1)$ in 2D). Each physical element $K$ in the mesh is related to $\hat{K}$ by an invertible mapping $\boldsymbol{x} = \boldsymbol{F}_K(\boldsymbol{\xi})$, where $\boldsymbol{\xi} \in \hat{K}$ and $\boldsymbol{x} \in K$. This mapping, often chosen to be affine for simplicity, induces transformations for integrals. The differential volume element transforms via the determinant of the Jacobian matrix $\boldsymbol{A} = D\boldsymbol{F}_K$: $d\boldsymbol{x} = \det(\boldsymbol{A}) \, d\boldsymbol{\xi}$. The outward normal vector $\boldsymbol{n}_x$ and surface element $dS_x$ on the physical boundary $\partial K$ are related to their reference counterparts via the cofactor matrix of the Jacobian [@problem_id:3954949]:
$$
\boldsymbol{n}_x dS_x = \operatorname{cof}(\boldsymbol{A}) \boldsymbol{n}_{\xi} dS_{\xi}
$$
These transformations allow all element-level computations, such as assembling mass and stiffness matrices, to be performed once on the reference element and then mapped to each physical element.

#### Numerical Quadrature
The volume and surface integrals that appear in the DG weak form are typically computed using **numerical quadrature** rules. A quadrature rule is said to have a **polynomial exactness** of degree $q$ if it can integrate any polynomial of degree up to $q$ exactly. To maintain the formal order of accuracy of the DG scheme and prevent aliasing errors, the quadrature rules must be sufficiently accurate. For a DG method using polynomials of degree $p$, the integrands in the mass matrix term ($\phi_i \phi_j$) and face integral terms ($\phi_i \hat{f}$) are generally polynomials of degree up to $2p$. Therefore, to compute these integrals exactly (for linear problems), the volume and face quadrature rules must be exact for polynomials of degree at least $2p$ [@problem_id:3954959]. For tensor-product elements, this corresponds to exactness for polynomials of degree $2p$ in each coordinate, typically achieved with a tensor-product Gaussian quadrature rule using at least $p+1$ points in each direction.

#### Matrix Structure
The choice of a discontinuous polynomial basis has a direct impact on the structure of the matrices in the semi-discrete ODE system $\boldsymbol{M} \frac{d\boldsymbol{U}}{dt} = \boldsymbol{R}(\boldsymbol{U})$.
*   **Mass Matrix ($\boldsymbol{M}$)**: The entries of the mass matrix are given by $M_{ij} = \int_K \phi_i \phi_j \, d\boldsymbol{x}$. Because the basis functions $\phi_i$ and $\phi_j$ have support on single elements, the global mass matrix is **block-diagonal**, with each block corresponding to an element in the mesh. This structure is highly advantageous, as the matrix is trivial to invert, often allowing for a fully explicit time-stepping scheme. If an orthonormal basis is used on the reference element and the element mapping is affine, the element mass matrix becomes diagonal, further simplifying the inversion [@problem_id:3955009].
*   **Spatial Operator ($\boldsymbol{R}$)**: The right-hand side, representing the spatial operator, contains the volume and surface integral terms. The volume integral only couples degrees of freedom within an element. The inter-element coupling arises exclusively from the numerical flux in the surface integral term, which links the degrees of freedom of an element with those of its immediate neighbors. Consequently, the Jacobian of this operator is a sparse matrix, reflecting the local connectivity of the mesh [@problem_id:3955009].

### Advanced Topics: Stability and Physical Admissibility

For a DG scheme to be truly robust, especially for complex systems like the Euler equations in high-speed flows, several advanced stability considerations are paramount.

#### Entropy Stability
For nonlinear systems of conservation laws, weak solutions are not unique. The second law of thermodynamics provides a physical selection criterion: the entropy of an isolated system must not decrease. This is mathematically formulated as an **entropy inequality**. An **entropy pair** consists of a convex scalar function of the conserved variables, $U(\boldsymbol{q})$, called the entropy, and an associated vector-valued entropy flux, $\boldsymbol{F}(\boldsymbol{q})$, which satisfy a compatibility condition. The physically relevant weak solution must then satisfy the entropy inequality in a distributional sense [@problem_id:3954958]:
$$
\partial_t U(\boldsymbol{q}) + \nabla \cdot \boldsymbol{F}(\boldsymbol{q}) \le 0
$$
For the Euler equations, a standard choice for the convex entropy is $U(\boldsymbol{q}) = -\frac{\rho s}{\gamma - 1}$, where $s$ is the specific physical entropy. Entropy-stable DG schemes are designed to satisfy a discrete version of this inequality, ensuring that the computed solution is physically realistic.

#### Positivity and Limiting
For the Euler equations, physical admissibility requires positive density and pressure ($\rho > 0, p > 0$). High-order polynomial approximations, due to the Gibbs phenomenon, can produce spurious oscillations near strong shocks. These oscillations can lead to local undershoots where the density or pressure becomes negative at certain points within an element (e.g., at quadrature points), causing the simulation to fail [@problem_id:3954988]. Standard DG schemes do not inherently preserve the positivity of these quantities. To overcome this, **limiters** are employed. These procedures detect and modify the polynomial solution in "troubled" cells (those near shocks) to enforce monotonicity or positivity constraints. This is often framed in terms of preserving the invariance of the convex set of admissible states. For instance, the set of states with positive density and pressure is a convex set in the space of conservative variables, and limiters are designed to ensure that the solution remains within this set [@problem_id:3954988].

#### Time Integration: Strong Stability Preservation (SSP)
The semi-discrete DG formulation results in a system of ODEs, $u_t = L(u)$, which must be integrated in time. When a limiter is used, the operator $L$ becomes highly nonlinear and non-smooth. A standard high-order time integrator (e.g., classical Runge-Kutta) can reintroduce oscillations that the limiter was designed to remove. To prevent this, **Strong Stability Preserving (SSP)** time-stepping methods are used. An explicit Runge-Kutta method is SSP if it can be written as a convex combination of forward Euler steps. If the forward Euler method is known to preserve a desired stability property (e.g., positivity, total variation diminishing) under a certain time-step restriction $\Delta t \le \Delta t_{\mathrm{FE}}$, then an SSP RK method will preserve that same property under a possibly modified time-step restriction $\Delta t \le C \cdot \Delta t_{\mathrm{FE}}$, where $C$ is the method's SSP coefficient [@problem_id:3954976]. This property is crucial for coupling high-order spatial discretizations with nonlinear limiters to achieve high-order accuracy in time while rigorously maintaining stability and non-oscillatory behavior near discontinuities [@problem_id:3954976].