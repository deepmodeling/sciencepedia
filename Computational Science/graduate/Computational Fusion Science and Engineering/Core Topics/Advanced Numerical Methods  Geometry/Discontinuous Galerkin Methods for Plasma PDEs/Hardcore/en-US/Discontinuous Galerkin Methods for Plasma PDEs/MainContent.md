## Introduction
The quest for fusion energy relies heavily on our ability to understand and predict the behavior of plasma, a state of matter governed by a complex and challenging set of partial differential equations (PDEs). Simulating these equations in the intricate geometries of fusion devices like tokamaks demands numerical methods that are not only accurate and robust but also geometrically flexible and highly scalable on modern supercomputers. The Discontinuous Galerkin (DG) method has emerged as a leading candidate that uniquely satisfies these demanding criteria, offering a powerful framework for advancing [computational fusion science](@entry_id:1122784).

This article bridges the gap between the abstract mathematical theory of DG methods and their concrete application to the PDEs of plasma physics. It provides a detailed guide for graduate students and researchers aiming to understand and implement these sophisticated schemes. Over three comprehensive chapters, you will gain a deep understanding of the method's inner workings. The journey begins in "Principles and Mechanisms," which deconstructs the DG formulation into its fundamental building blocks. It then moves to "Applications and Interdisciplinary Connections," showcasing the method's versatility across the spectrum of plasma models and its ability to handle complex fusion geometries. Finally, the "Hands-On Practices" chapter provides practical exercises to solidify your knowledge and guide you in building your own DG-based solvers.

## Principles and Mechanisms

Having established the motivation for employing Discontinuous Galerkin (DG) methods in [computational plasma physics](@entry_id:198820), we now turn to the principles and mechanisms that define this powerful class of [numerical schemes](@entry_id:752822). This chapter deconstructs the DG method into its fundamental components, beginning with the local approximation of solutions within a single element, proceeding to the coupling of these elements through interface fluxes, and culminating in an examination of the theoretical properties and advanced applications that make the method particularly suitable for the complex partial differential equations (PDEs) of fusion science.

### The Building Blocks: Local Approximation Spaces

The philosophical core of the DG method is to partition the computational domain $\Omega$ into a mesh of non-overlapping elements, or cells, $\mathcal{T}_h = \{K\}$, and to approximate the solution within each element independently. The "discontinuous" nature of the method arises from the fact that the polynomial approximations in adjacent cells are not required to be continuous at their shared interface. This local construction offers enormous flexibility in mesh generation ([h-adaptivity](@entry_id:637658)) and in the choice of approximation order ([p-adaptivity](@entry_id:138508)).

#### The Reference Element and Basis Functions

All geometric and functional operations are most conveniently defined on a canonical **reference element**, $\hat{K}$. For one-dimensional problems, this is typically the interval $\hat{K} = [-1, 1]$. On this interval, we define a local approximation space, usually the space of polynomials of degree at most $p$, denoted $\mathcal{P}_p(\hat{K})$. Any function $u_h$ in this space can be represented as a [linear combination](@entry_id:155091) of basis functions $\{\hat{\phi}_i(\xi)\}_{i=0}^p$:
$u_h(\xi) = \sum_{i=0}^p \hat{u}_i \hat{\phi}_i(\xi)$.

A particularly powerful choice for the basis is a set of **[modal basis](@entry_id:752055)** functions that are orthogonal with respect to the $L^2$ inner product on the reference element, $\langle f, g \rangle_{\hat{K}} = \int_{-1}^1 f(\xi)g(\xi)d\xi$. An ideal choice is the set of **orthonormal Legendre polynomials**, which we denote $\{\hat{\ell}_n(\xi)\}_{n=0}^p$. These are derived from the standard Legendre polynomials by scaling them to have a unit norm. They satisfy the crucial property:

$$
\int_{-1}^1 \hat{\ell}_n(\xi)\,\hat{\ell}_m(\xi)\,d\xi = \delta_{nm}
$$

where $\delta_{nm}$ is the Kronecker delta. The first basis function, $\hat{\ell}_0(\xi)$, is a constant and represents the cell average of the solution, while higher-order functions, $\hat{\ell}_n(\xi)$ for $n>0$, represent deviations from that average.

#### Mapping to Physical Elements and the Mass Matrix

To apply this basis to a physical element in the mesh, say $K_e = (x_{e-1}, x_e)$, we employ a mapping from the reference coordinate $\xi$ to the physical coordinate $x$. For a simple straight-sided element, an affine map suffices:

$$
x(\xi) = \frac{x_e - x_{e-1}}{2}\xi + \frac{x_e + x_{e-1}}{2}
$$

The derivative of this map, known as the **Jacobian** $J_e = \frac{dx}{d\xi} = \frac{x_e - x_{e-1}}{2}$, is a constant for each element. The physical basis functions $\phi_n^e(x)$ on element $K_e$ are then defined by pulling back the reference basis functions: $\phi_n^e(x) = \hat{\ell}_n(\xi(x))$.

This mapping has a profound consequence for the **local mass matrix**, a fundamental component in DG formulations, especially for time-dependent problems. Its entries are defined by the inner products of the physical basis functions over the element $K_e$:

$$
M_{nm}^e = \int_{K_e} \phi_n^e(x)\,\phi_m^e(x)\,dx
$$

By changing the variable of integration back to the reference coordinate $\xi$, the integral becomes:

$$
M_{nm}^e = \int_{-1}^1 \hat{\ell}_n(\xi)\,\hat{\ell}_m(\xi)\,J_e\,d\xi = J_e \int_{-1}^1 \hat{\ell}_n(\xi)\,\hat{\ell}_m(\xi)\,d\xi
$$

Leveraging the [orthonormality](@entry_id:267887) of the Legendre basis, this simplifies dramatically :

$$
M_{nm}^e = J_e\,\delta_{nm}
$$

This result reveals a key advantage of using an orthonormal [modal basis](@entry_id:752055): the local mass matrix is **diagonal**. For an explicit time-stepping scheme, the semi-discrete equation takes the form $M^e \frac{d\mathbf{u}_e}{dt} = \mathbf{R}_e$, where $\mathbf{R}_e$ represents the spatial operator. Inverting a diagonal matrix is trivial, which greatly enhances computational efficiency. The global mass matrix, assembled from all local matrices, becomes block-diagonal, with each block being a simple [diagonal matrix](@entry_id:637782) itself.

#### Extension to Multiple Dimensions and Degrees of Freedom

The framework extends naturally to higher dimensions, such as two-dimensional quadrilateral or three-dimensional [hexahedral elements](@entry_id:174602), which are common in fusion applications. These elements can be mapped from the reference [hypercube](@entry_id:273913) $\hat{K} = [-1,1]^d$, where $d$ is the spatial dimension.

The local approximation space on the [hypercube](@entry_id:273913), $Q_p(\hat{K})$, is constructed as the **[tensor product](@entry_id:140694)** of $d$ one-dimensional [polynomial spaces](@entry_id:753582): $Q_p(\hat{K}) = \mathcal{P}_p([-1,1]) \otimes \dots \otimes \mathcal{P}_p([-1,1])$. A basis for this space is formed by taking all possible products of the 1D basis functions. Using a multi-index $\boldsymbol{\alpha} = (\alpha_1, \dots, \alpha_d)$ where $0 \le \alpha_i \le p$, a multi-dimensional basis function is given by:

$$
\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) = \prod_{i=1}^{d} \hat{\ell}_{\alpha_i}(\xi_i)
$$

Due to the properties of the 1D [orthonormal basis](@entry_id:147779), this tensor-product basis is also orthonormal over the reference [hypercube](@entry_id:273913): $\int_{\hat{K}} \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) \Psi_{\boldsymbol{\beta}}(\boldsymbol{\xi}) d\boldsymbol{\xi} = \delta_{\boldsymbol{\alpha}\boldsymbol{\beta}}$.

The number of basis functions, and thus the number of **degrees of freedom (DoFs)** per element for a scalar field, can be determined by a simple counting argument. For each of the $d$ dimensions, the polynomial index $\alpha_i$ can take any of the $p+1$ values from $\{0, 1, \dots, p\}$. The total number of unique basis functions is therefore $(p+1)^d$.

For a system of PDEs involving $m$ independent component fields (e.g., $m=5$ for a five-moment fluid model, or $m=6$ for the electromagnetic fields in Maxwell's equations), each component is typically approximated in the same [polynomial space](@entry_id:269905). Because the DG basis is entirely element-local, the total number of DoFs per element is simply the product of the DoFs per component and the number of components :

$$
N_{\text{total}} = m(p+1)^d
$$

This formula is fundamental to estimating the computational cost and memory requirements of a DG simulation. The cost grows rapidly with both polynomial degree $p$ and spatial dimension $d$.

### Coupling Elements: The Role of Numerical Flux

The use of discontinuous basis functions begs a critical question: how do the elements communicate? If the solution in each cell is entirely independent, we have merely a collection of disconnected problems. The coupling mechanism is the "glue" of the DG method and is realized through fluxes at the element interfaces.

#### The Weak Formulation and Integration by Parts

Let us consider a generic hyperbolic conservation law, representative of many plasma transport models:

$$
\frac{\partial u}{\partial t} + \nabla \cdot \mathbf{F}(u) = 0
$$

To derive the DG formulation, we multiply by a test function $v_h$ from the same [polynomial space](@entry_id:269905) as our solution $u_h$, and integrate over a single element $K$:

$$
\int_K \frac{\partial u_h}{\partial t} v_h \,d\mathbf{x} + \int_K (\nabla \cdot \mathbf{F}(u_h)) v_h \,d\mathbf{x} = 0
$$

A key step is to apply integration by parts (the [divergence theorem](@entry_id:145271)) to the flux term:

$$
\int_K (\nabla \cdot \mathbf{F}(u_h)) v_h \,d\mathbf{x} = \oint_{\partial K} (\mathbf{F}(u_h) \cdot \mathbf{n}) v_h \,dS - \int_K \mathbf{F}(u_h) \cdot \nabla v_h \,d\mathbf{x}
$$

where $\partial K$ is the boundary of the element and $\mathbf{n}$ is the outward-pointing unit normal. Substituting this back, we arrive at the weak formulation on element $K$:

$$
\int_K \frac{\partial u_h}{\partial t} v_h \,d\mathbf{x} = \int_K \mathbf{F}(u_h) \cdot \nabla v_h \,d\mathbf{x} - \oint_{\partial K} (\mathbf{F}(u_h) \cdot \mathbf{n}) v_h \,dS
$$

This equation creates two contributions to the spatial operator: a **[volume integral](@entry_id:265381)** over $K$ and a **[surface integral](@entry_id:275394)** over its boundary $\partial K$. It is through the [surface integral](@entry_id:275394) that information is exchanged with neighboring elements.

#### The Riemann Problem and the Numerical Flux

At an interface between two elements, the solution $u_h$ is two-valued. We denote the trace of the solution from the interior of element $K$ as $u^-$ and the trace from the neighboring element as $u^+$. Consequently, the physical flux $\mathbf{F}(u_h) \cdot \mathbf{n}$ is not uniquely defined at the interface.

The DG method resolves this ambiguity by replacing the physical flux with a **numerical flux**, denoted $\widehat{\mathbf{F}}(u^-, u^+)$. This function must be consistent with the physical flux (i.e., $\widehat{\mathbf{F}}(u, u) = \mathbf{F}(u)$) and is typically designed by considering the solution to the local **Riemann problem** at the interface.

The simplest and most illustrative example is the linear advection equation in one dimension, $\partial_t u + a \partial_x u = 0$, where the physical flux is $f(u) = au$. The solution to this equation propagates along [characteristic lines](@entry_id:1122279) with speed $a$. The [numerical flux](@entry_id:145174) must respect this directionality of information flow. The **[upwind flux](@entry_id:143931)** does precisely this by selecting the value of $u$ from the "upwind" side of the interface :

$$
\widehat{f}(u^-, u^+) =
\begin{cases}
    a u^- & \text{if } a > 0 \\
    a u^+ & \text{if } a  0
\end{cases}
$$

If information flows from left to right ($a > 0$), the flux is determined by the state on the left, $u^-$. If it flows from right to left ($a  0$), the flux is determined by the state on the right, $u^+$. For [nonlinear systems](@entry_id:168347), the choice of numerical flux is more complex (e.g., Rusanov, HLL, HLLC fluxes), but the principle remains: the [numerical flux](@entry_id:145174) resolves the discontinuity at the interface in a physically and mathematically consistent way, providing the necessary coupling and stability for the scheme.

#### Locality and Parallel Communication

The structure of the DG spatial operator is inherently local. The semi-discrete update for the degrees of freedom on an element $K$ is determined by [volume integrals](@entry_id:183482) using data only from within $K$, and [surface integrals](@entry_id:144805) using data from within $K$ ($u^-$) and from its immediate face-neighbors ($u^+$). This "nearest-neighbor" computational stencil has profound implications for [high-performance computing](@entry_id:169980) .

When a mesh is partitioned and distributed across many processors in a parallel environment (e.g., using the Message Passing Interface, MPI), this locality translates directly into a highly scalable communication pattern. To compute the [numerical flux](@entry_id:145174) at a face on the boundary of a processor's domain, that processor only needs to receive the trace data ($u^+$) from the single neighboring processor that owns the adjacent element. There is no need for global communication.

The communication pattern for an explicit time-stepping scheme consists of sparse, point-to-point messages between geometric neighbors. The total volume of data exchanged per time step is proportional to the number of faces on the partition boundary, not the total number of elements within the partition. This favorable surface-to-volume ratio is a primary reason for the excellent [parallel scalability](@entry_id:753141) of DG methods, making them well-suited for [large-scale simulations](@entry_id:189129) on modern supercomputers  .

### Theoretical Properties: Stability and Convergence

Beyond its flexible structure, a numerical method is only useful if it is stable and converges to the true solution. For DG methods applied to hyperbolic PDEs, these properties are intimately tied to the choice of [numerical flux](@entry_id:145174).

#### $L^2$-Stability and the Role of the Flux

A scheme is considered **$L^2$-stable** if the "energy" of the numerical solution, measured by the square of its $L^2$ norm, does not grow without bound. For [hyperbolic conservation laws](@entry_id:147752), this stability is not automatic and must be built into the discretization.

The numerical flux is the primary mechanism for ensuring stability. Fluxes like the upwind or local Lax-Friedrichs schemes are **dissipative**: they contain terms that penalize the jump in the solution, $[u] = u^+ - u^-$, at interfaces. This numerical dissipation removes energy from unresolved scales and mimics the entropy-producing effects of physical viscosity, preventing the growth of spurious oscillations and ensuring stability.

In contrast, a simple **central flux**, $\widehat{f}(u^-, u^+) = \frac{1}{2}(f(u^-) + f(u^+))$, lacks this dissipative mechanism. While it is consistent, it is generally unstable for hyperbolic problems and can lead to catastrophic failure of the simulation. Therefore, the choice of a dissipative, monotone [numerical flux](@entry_id:145174) is not merely an implementation detail but a prerequisite for a stable DG scheme for [plasma transport](@entry_id:181619) equations .

#### A Priori Error Estimates

Provided a stable numerical flux is used, the DG method exhibits [high-order accuracy](@entry_id:163460). This is formalized by **[a priori error estimates](@entry_id:746620)**, which bound the error between the exact solution $u$ and the numerical solution $u_h$. For a smooth solution in a sufficiently regular Sobolev space ($H^s$), the $L^2$ error is typically bounded by:

$$
\|u - u_h\|_{L^2(\Omega)} \le C h^{p+1}
$$

where $C$ is a constant, $h$ is the characteristic mesh size, and $p$ is the polynomial degree. For sufficiently smooth solutions, the convergence rate is often stated as $h^{p+1/2}$ or, with more advanced analysis, $h^{p+1}$. This estimate powerfully demonstrates the two avenues for improving accuracy in a DG method: refining the mesh (decreasing $h$, known as **[h-refinement](@entry_id:170421)**) or increasing the polynomial degree (increasing $p$, known as **[p-refinement](@entry_id:173797)**). The ability to achieve very high accuracy on coarse meshes by simply increasing $p$ is a hallmark of DG and other [high-order methods](@entry_id:165413). It is crucial to remember that such theoretical guarantees of convergence hinge on the stability provided by a proper numerical flux .

### Practical Implementations: Nodal vs. Modal Bases and Nonlinearities

While the theory can be developed for an abstract [polynomial space](@entry_id:269905), practical implementations rely on a specific choice of basis. The two predominant choices, modal and nodal, lead to DG variants with distinct characteristics.

#### Nodal DG and Lagrange Bases

An alternative to the orthogonal [modal basis](@entry_id:752055) is a **nodal basis**, most commonly constructed from **Lagrange polynomials** $\{\ell_i(x)\}$ defined with respect to a set of interpolation nodes $\{x_j\}$ within the element. These basis functions have the simple property $\ell_i(x_j) = \delta_{ij}$. The degrees of freedom are now the physical point values of the solution at the nodes, $u_h(x_i)$, which can be more intuitive than the abstract coefficients of a modal expansion. A popular choice for nodes are the Legendre-Gauss-Lobatto (LGL) points, which include the element endpoints.

When [numerical quadrature](@entry_id:136578) is used to compute matrix entries, a nodal basis offers a particular synergy. If the quadrature points are chosen to be the same as the interpolation nodes (a so-called "collocation" approach), the mass matrix becomes diagonal, a phenomenon known as **[mass lumping](@entry_id:175432)**. For example, for the $p=2$ case with LGL nodes $\{-1, 0, 1\}$, the mass matrix entries computed with the corresponding [quadrature rule](@entry_id:175061) are $M_{ii} \approx w_i$, where $w_i$ are the [quadrature weights](@entry_id:753910), and $M_{ij} \approx 0$ for $i \ne j$ . This [diagonal mass matrix](@entry_id:173002) is computationally efficient. However, the exact [mass matrix](@entry_id:177093) (computed without [quadrature error](@entry_id:753905)) for a Lagrange basis is dense and becomes increasingly ill-conditioned as the polynomial degree $p$ increases .

The primary advantage of nodal DG lies in its efficiency for certain operations. Evaluating the solution at the boundaries to compute fluxes is trivial, as the boundary nodes are degrees of freedom. Implementing pointwise physical constraints, such as ensuring positivity of density or pressure, is also more direct, as one can check and modify the nodal values directly . For these reasons, nodal DG is often favored for complex, shock-dominated problems like resistive MHD .

#### Aliasing Instability in Nonlinear Problems

The convenience of nodal collocation comes at a price: **[aliasing instability](@entry_id:746361)**. Consider a nonlinear flux, such as the Burgers flux $F(u) = \frac{1}{2}u^2$. If the solution $u_h$ is a polynomial of degree $p$, the flux term $F(u_h)$ is a polynomial of degree $2p$. The integrand in the weak form, $\mathbf{F}(u_h) \cdot \nabla v_h$, can be a polynomial of degree up to $3p-1$. A [quadrature rule](@entry_id:175061) based on $p+1$ points, such as the LGL rule, is only exact for polynomials of degree up to $2p-1$.

Therefore, the [volume integrals](@entry_id:183482) are computed inexactly, or **underintegrated**. This [quadrature error](@entry_id:753905), known as aliasing, can act as a spurious source of energy. For the inviscid Burgers equation on a periodic domain, the continuous energy is exactly conserved. However, a standard nodal DG discretization with a central flux can be shown to generate a non-zero, positive contribution to the energy evolution equation, leading to an unstable scheme where the discrete energy grows without bound and the solution eventually blows up .

This instability is a critical challenge for nonlinear problems. Several remedies exist. One is **over-integration**, where a more expensive [quadrature rule](@entry_id:175061) with more points is used to compute the [volume integrals](@entry_id:183482) exactly, thereby eliminating the [aliasing error](@entry_id:637691). Another, more elegant solution is to use a **split-form** or **skew-symmetric** formulation of the nonlinear term. These reformulations are algebraically manipulated to enforce a discrete version of energy conservation, even when using an inexact [quadrature rule](@entry_id:175061), thus neutralizing the [aliasing instability](@entry_id:746361) without the cost of extra quadrature points .

#### A Comparative Summary

The choice between nodal and modal bases represents a fundamental design trade-off in developing a DG code .

*   **Modal Basis:**
    *   **Pros:** Diagonal or well-conditioned [mass matrix](@entry_id:177093) (on simple meshes), promoting stability and efficiency. Natural framework for hierarchical limiting and spectral filtering, which are ideal for controlling noise in smooth, wave-dominated problems (e.g., Vlasov-Poisson models).
    *   **Cons:** Evaluating solutions at arbitrary points (like face quadrature points) requires a full basis summation, which is computationally more expensive. Pointwise limiting is less direct.

*   **Nodal Basis:**
    *   **Pros:** Extremely efficient flux evaluation (if face quadrature points align with nodes). Direct access to point values makes it simple to implement [positivity-preserving limiters](@entry_id:753610) and to detect shocks. Often preferred for sharp, discontinuous solutions (e.g., MHD with shocks).
    *   **Cons:** The exact mass matrix is ill-conditioned. The common practice of [mass lumping](@entry_id:175432) via underintegration introduces aliasing errors that can cause catastrophic instability for nonlinear problems unless specific remedies are applied.

### Time Integration and Advanced Topics

The DG spatial discretization transforms a PDE into a large, coupled system of [ordinary differential equations](@entry_id:147024) (ODEs) of the form $\frac{d\mathbf{u}}{dt} = \mathbf{L}(\mathbf{u})$. Selecting an appropriate time integrator is the final piece of the puzzle.

#### Strong Stability Preserving (SSP) Time-Stepping

For hyperbolic problems, it is often desirable that the time integration scheme preserve certain stability properties (like positivity or [total variation diminishing](@entry_id:140255), TVD) that are known to hold for the simple first-order Forward Euler method under a suitable time step (CFL) condition. **Strong Stability Preserving (SSP)** methods are higher-order [time integrators](@entry_id:756005), typically of the Runge-Kutta family, designed for this purpose.

An SSP-RK scheme can be expressed as a convex combination of Forward Euler steps. This structure guarantees that if the Forward Euler step is stable with respect to some norm or semi-norm, the full high-order SSP scheme will also be stable under a related (and practical) [time step constraint](@entry_id:756009). A widely used example is the third-order SSP Runge-Kutta scheme, which can be written as a sequence of stages that are convex combinations of previous stage values and their Forward Euler updates . The use of SSP integrators is standard practice in high-order DG codes for plasma fluid and kinetic models.

#### Advanced Topic: Preserving the Divergence-Free Constraint in MHD

A critical challenge in [magnetohydrodynamics](@entry_id:264274) (MHD) is numerically preserving the [solenoidal constraint](@entry_id:755035), $\nabla \cdot \mathbf{B} = 0$. Failure to do so can lead to unphysical forces and simulation failure. Standard DG methods, like most [numerical schemes](@entry_id:752822), do not automatically enforce this constraint.

A powerful solution compatible with the DG framework is **Constrained Transport (CT)**. This approach introduces new degrees of freedom representing the magnetic flux through each face of the mesh, $\Phi_f = \int_f \mathbf{B} \cdot \mathbf{n} dS$. These face fluxes are evolved in time using a discrete version of Faraday's law of induction, applied to the loop bounding each face. A key property of this evolution is that, due to cancellations of the electric field [line integrals](@entry_id:141417) along shared edges, the sum of the time derivatives of fluxes around any closed cell is identically zero :

$$
\frac{d}{dt} \oint_{\partial K} \mathbf{B}_h \cdot \mathbf{n} \,dS = \sum_{f \in \partial K} \frac{d\Phi_f}{dt} = 0
$$

This guarantees that if the total magnetic flux out of a cell is zero initially, it remains zero for all time.

The final step is to reconstruct the magnetic field $\mathbf{B}_h$ *inside* the element in a way that is consistent with the face fluxes and is itself divergence-free. This is achieved by using special finite element spaces known as **$H(\text{div})$-conforming spaces** (e.g., Raviart-Thomas or Brezzi-Douglas-Marini elements). A local problem is solved on each element to find a vector field $\mathbf{B}_h$ in this space that both matches the CT-evolved face fluxes and satisfies $\nabla \cdot \mathbf{B}_h = 0$ exactly (in a polynomial sense) within the element. This DG-CT hybrid approach successfully combines the geometric flexibility and high-order accuracy of DG with the rigorous, physics-preserving structure of [constrained transport](@entry_id:747767), representing a state-of-the-art technique for ideal MHD simulations .