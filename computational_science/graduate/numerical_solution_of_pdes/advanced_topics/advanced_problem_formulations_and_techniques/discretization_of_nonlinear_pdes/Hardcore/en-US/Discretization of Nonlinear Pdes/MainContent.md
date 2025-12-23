## Introduction
Nonlinear [partial differential equations](@entry_id:143134) (PDEs) are at the heart of modern science and engineering, modeling complex phenomena from [turbulent fluid flow](@entry_id:756235) to the large-scale deformation of materials. Unlike their linear counterparts, whose solutions can often be found through direct methods, nonlinear PDEs present a significant computational challenge. The process of discretization leads not to a simple matrix equation, but to a complex system of nonlinear algebraic equations that requires sophisticated iterative techniques to solve. This article provides a comprehensive guide to navigating this landscape, equipping readers with the theoretical understanding and practical knowledge to discretize and solve these critical equations.

The journey begins in the **Principles and Mechanisms** chapter, where we will lay the groundwork by classifying different types of nonlinearity and establishing the variational framework for [discretization](@entry_id:145012). We will explore how methods like the Finite Element and Finite Volume methods transform continuous problems into algebraic systems and detail the cornerstone of solving them: Newton's method and the [consistent linearization](@entry_id:747732) of the discrete operator. Building upon this foundation, the **Applications and Interdisciplinary Connections** chapter will demonstrate these techniques in action across diverse fields, from [structural mechanics](@entry_id:276699) to [computational fluid dynamics](@entry_id:142614) and numerical relativity. We will examine how real-world problems motivate advanced strategies for preserving physical structures, handling [non-local operators](@entry_id:752581), and tackling [multiphysics coupling](@entry_id:171389). Finally, the **Hands-On Practices** chapter offers an opportunity to translate theory into practice, with guided problems focused on implementing key algorithms like Jacobian derivation, spectral [de-aliasing](@entry_id:748234), and [parallel domain decomposition](@entry_id:753120) methods.

## Principles and Mechanisms

The [discretization](@entry_id:145012) of [nonlinear partial differential equations](@entry_id:168847) (PDEs) represents a significant conceptual and practical step beyond the analysis of linear systems. Whereas [linear operators](@entry_id:149003) can be discretized once into a matrix system that is then solved, nonlinear operators give rise to systems of algebraic equations that are themselves nonlinear. The core challenge, therefore, lies in managing and linearizing this nonlinearity in a manner that is both computationally tractable and faithful to the underlying physics of the continuous problem. This chapter details the foundational principles for classifying, discretizing, and solving nonlinear PDEs, exploring the primary mechanisms employed in modern numerical methods.

### The Nature of Nonlinearity in PDEs

Before devising [numerical schemes](@entry_id:752822), it is crucial to classify the nature of the nonlinearity within a given PDE. This classification dictates the mathematical structure of the problem and profoundly influences the selection of appropriate analytical and numerical tools. For a general differential operator $\mathcal{N}$ acting on a function $u$, the problem is cast as $\mathcal{N}(u) = f$. The nonlinearity is categorized based on how the operator $\mathcal{N}$ depends on the unknown solution $u$ and its derivatives. 

A partial differential equation is classified as **semilinear** if it is linear in its highest-order derivatives, but contains nonlinear terms involving lower-order derivatives or the function $u$ itself. The coefficients of the highest-order terms must be independent of $u$ and its derivatives. A canonical example is a [reaction-diffusion equation](@entry_id:275361):
$$
-\Delta u + u^3 = f
$$
Here, the highest-order operator is the Laplacian, $\Delta u$, which is linear in the second derivatives of $u$. The coefficient ($-1$) is constant. The nonlinearity arises from the cubic reaction term, $u^3$, which depends only on the zeroth-order term, $u$.

A PDE is **quasilinear** if it remains linear with respect to its highest-order derivatives, but the coefficients of these terms may depend on the solution $u$ or its lower-order derivatives. This class of equations is prevalent in physics and engineering. For instance, consider a diffusion problem where the conductivity depends on the solution itself:
$$
-\nabla \cdot (a(u)\nabla u) = f
$$
Expanding the [divergence operator](@entry_id:265975) reveals the structure: $-a(u)\Delta u - a'(u)|\nabla u|^2 = f$. The equation is linear in the second derivatives of $u$ (which appear in $\Delta u$), but the coefficient of this highest-order term, $a(u)$, depends on the solution $u$. Another classic example of a quasilinear PDE is the **p-Laplacian** equation, which appears in non-Newtonian fluid mechanics and [nonlinear elasticity](@entry_id:185743): 
$$
-\nabla \cdot (|\nabla u|^{p-2}\nabla u) = f, \quad \text{for } p>1
$$
Here, the coefficients of the second-order derivatives, which arise from differentiating the term $|\nabla u|^{p-2}\nabla u$, explicitly depend on the gradient of the solution, $\nabla u$.

Finally, a PDE is **fully nonlinear** if it is nonlinear with respect to its highest-order derivatives. These equations pose the most significant analytical and numerical challenges. The archetypal example is the Monge-Ampère equation:
$$
\det(D^2 u) = g
$$
where $D^2 u$ is the Hessian matrix of [second partial derivatives](@entry_id:635213) of $u$. In two dimensions, this equation is $u_{xx}u_{yy} - u_{xy}^2 = g$, which is a quadratic polynomial in the second derivatives of $u$. The structure of such equations often precludes the use of standard variational techniques.

### The Variational Framework and Weak Formulations

The finite element method (FEM) and related variational approaches are built upon the weak formulation of a PDE. This is typically derived by multiplying the PDE by a suitable test function $v$ and integrating over the domain $\Omega$, transferring derivatives from the unknown solution $u$ to the test function $v$ via [integration by parts](@entry_id:136350) (Green's identities). The nature of the resulting [weak form](@entry_id:137295) depends directly on the class of nonlinearity.

For a **semilinear** problem like $-\Delta u + u^3 = f$ with homogeneous Dirichlet boundary conditions ($u=0$ on $\partial\Omega$), we choose a [test function](@entry_id:178872) $v$ from a suitable space, typically the Sobolev space $H_0^1(\Omega)$, which consists of functions with square-integrable first derivatives that vanish on the boundary. The procedure yields:
$$
\int_{\Omega} (-\Delta u) v \,dx + \int_{\Omega} u^3 v \,dx = \int_{\Omega} fv \,dx
$$
Integration by parts on the first term gives the [weak formulation](@entry_id:142897): find $u \in H_0^1(\Omega)$ such that for all $v \in H_0^1(\Omega)$,
$$
\int_{\Omega} \nabla u \cdot \nabla v \,dx + \int_{\Omega} u^3 v \,dx = \int_{\Omega} fv \,dx
$$
This form is additively separable into a bilinear part, representing the [linear operator](@entry_id:136520), and a nonlinear part. 

For a **quasilinear** problem like the p-Laplacian, the nonlinearity is embedded within the principal part of the operator. Starting from $-\nabla \cdot (|\nabla u|^{p-2}\nabla u) = f$ and integrating against a [test function](@entry_id:178872) $v$ from the appropriate space $W_0^{1,p}(\Omega)$, integration by parts gives: find $u \in W_0^{1,p}(\Omega)$ such that for all $v \in W_0^{1,p}(\Omega)$,
$$
\int_{\Omega} |\nabla u|^{p-2} \nabla u \cdot \nabla v \,dx = \int_{\Omega} fv \,dx
$$
Here, the entire left-hand side is a nonlinear operator, often denoted $A(u; v)$, which is no longer a simple bilinear form in $u$ and $v$.

For **fully nonlinear** equations such as the Monge-Ampère equation, this standard procedure is often intractable. There is no general integration-by-parts formula that simplifies the term $\det(D^2 u)$ into a usable [weak form](@entry_id:137295) in spaces like $H^1(\Omega)$. Consequently, alternative theoretical frameworks, such as the theory of **[viscosity solutions](@entry_id:177596)**, are required to even define a notion of a weak solution, and standard conforming Galerkin methods are not directly applicable. 

A different class of nonlinearity arises from constraints on the [solution space](@entry_id:200470). The **obstacle problem** seeks to find the [equilibrium state](@entry_id:270364) of an elastic membrane stretched over an obstacle. This is not formulated as an equality but as a **[variational inequality](@entry_id:172788)**. The solution $u$ minimizes an energy functional over a [convex set](@entry_id:268368) of admissible functions $K = \{v \in H_0^1(\Omega) : v \ge \psi\}$, where $\psi$ is the obstacle. The resulting optimality condition is: find $u \in K$ such that for all $v \in K$,
$$
\int_{\Omega} \nabla u \cdot \nabla (v-u) \,dx \ge \int_{\Omega} f (v-u) \,dx
$$
This inequality structure, rather than a direct nonlinearity in the differential operator, is the source of the problem's nonlinear character. 

### Discretization: From Continuous to Algebraic Nonlinearity

The process of discretization translates the continuous nonlinear problem, typically expressed in its weak form, into a finite-dimensional system of nonlinear algebraic equations.

#### Finite Element Method (FEM)

The Galerkin principle is the foundation of the [finite element method](@entry_id:136884). The infinite-dimensional solution and test spaces ($\mathcal{U}$ and $\mathcal{V}$) are replaced by finite-dimensional subspaces ($\mathcal{U}_h \subset \mathcal{U}$ and $\mathcal{V}_h \subset \mathcal{V}$). The solution is approximated as a linear combination of basis functions, $u_h(x) = \sum_{j=1}^N U_j \phi_j(x)$, where $U_j$ are the unknown nodal coefficients and $\phi_j(x)$ are the basis functions (e.g., piecewise linear "hat" functions).

Substituting this expansion into the weak form and testing against each [basis function](@entry_id:170178) $\phi_i(x)$ transforms the [variational equation](@entry_id:635018) into a system of equations for the coefficient vector $\mathbf{U} = (U_1, \dots, U_N)^\top$. For the quasilinear p-Laplacian in one dimension, for example, the discrete equation for a single degree of freedom $a$ in the expansion $u_h = a\phi_1$ takes the form: 
$$
\left( \int_0^1 |\phi'_1(x)|^p \, dx \right) |a|^{p-2}a = \int_0^1 f(x)\phi_1(x) \, dx
$$
This illustrates how the nonlinearity of the PDE (the term $|\nabla u|^{p-2}\nabla u$) directly translates into a nonlinear algebraic equation for the unknown coefficients (the term $|a|^{p-2}a$). The integrals involved are computed element-wise, typically using numerical quadrature rules chosen to be sufficiently accurate for the integrands, which involve products of basis functions and nonlinear material coefficients.

#### Finite Volume Method (FVM) for Conservation Laws

For [hyperbolic conservation laws](@entry_id:147752), such as the scalar law $u_t + \partial_x f(u) = 0$, the [finite volume method](@entry_id:141374) is often preferred. This method is based on integrating the PDE over control volumes (or cells) and applying the divergence theorem. The semi-discrete form for the cell-average $u_i$ is:
$$
\frac{d u_i}{dt} = -\frac{1}{\Delta x} \left( F_{i+1/2} - F_{i-1/2} \right)
$$
The core of the method lies in the definition of the **numerical flux** $F_{i+1/2}$ at the interface between cells $i$ and $i+1$. This flux must approximate the physical flux $f(u)$ and ensure stability.

The **Godunov method** provides a canonical way to define this flux. It posits that the flux at the interface should be determined by the exact solution to the **Riemann problem**, which is the conservation law with piecewise constant initial data $u_L$ and $u_R$ corresponding to the states in the adjacent cells. The Godunov flux is $g(u_L, u_R) = f(u^\ast)$, where $u^\ast$ is the state that appears at the interface ($x/t = 0$) in the [self-similar solution](@entry_id:173717) of this Riemann problem. 

For a strictly convex flux function (e.g., $f(u) = u^2/2$ for Burgers' equation), the solution to the Riemann problem is either a continuous **[rarefaction wave](@entry_id:172838)** (if $u_L  u_R$) or a discontinuous **shock wave** (if $u_L > u_R$). The state $u^\ast$ at the interface is determined by the propagation speeds of these waves. For a rarefaction, $u^\ast$ depends on whether the [characteristic speeds](@entry_id:165394) $f'(u_L)$ and $f'(u_R)$ are positive or negative relative to the interface. For a shock, $u^\ast$ depends on the sign of the shock speed, which is given by the Rankine-Hugoniot condition. This physical reasoning is directly embedded into the discrete operator, making it a fundamentally nonlinear and physically-motivated [discretization](@entry_id:145012).

### Solving the Nonlinear System: Linearization and Iteration

Regardless of the [discretization](@entry_id:145012) method, the end result is a system of nonlinear algebraic equations of the form $\mathbf{N}(\mathbf{U}) = \mathbf{F}$. Except in the simplest cases, this system cannot be solved directly. Instead, [iterative methods](@entry_id:139472) are required, with the most common being Newton's method (also known as the Newton-Raphson method).

#### Newton's Method and the Consistent Jacobian

Newton's method linearizes the system at the current iterate $\mathbf{U}^k$ and solves for an update $\delta\mathbf{U}$:
$$
\mathbf{J}(\mathbf{U}^k) \delta\mathbf{U} = -\mathbf{N}(\mathbf{U}^k)
$$
where $\mathbf{N}(\mathbf{U}^k)$ is the [residual vector](@entry_id:165091) and $\mathbf{J}(\mathbf{U}^k) = \frac{\partial \mathbf{N}}{\partial \mathbf{U}}|_{\mathbf{U}^k}$ is the **Jacobian matrix**, also known as the **[tangent stiffness matrix](@entry_id:170852)** in [solid mechanics](@entry_id:164042). The next iterate is then $\mathbf{U}^{k+1} = \mathbf{U}^k + \delta\mathbf{U}$. The quadratic convergence of Newton's method hinges on the accurate computation of this Jacobian.

The derivation of the "consistent" Jacobian is a crucial step. It involves differentiating the discrete [residual vector](@entry_id:165091), which is assembled from element-level integrals, with respect to each nodal degree of freedom. Let the element residual for a general nonlinear problem be $R_i^e(\mathbf{U}^e) = \int_{\Omega^e} [\alpha(u_h)\nabla u_h \cdot \nabla N_i + \beta(u_h)N_i] \, d\Omega$. The Jacobian entry $J_{ij}^e = \partial R_i^e / \partial U_j$ is found by applying the chain and product rules. The differentiation is moved inside the integral, and since $u_h = \sum_k U_k N_k$, we have $\partial u_h/\partial U_j = N_j$ and $\partial \nabla u_h/\partial U_j = \nabla N_j$.

The complete expression for the Jacobian entry, expressed as a sum over quadrature points $q$ on a reference element, is: 
$$
J_{ij}^{e} = \sum_{q=1}^{n_q} \left[ \alpha(u_h) (\nabla N_i \cdot \nabla N_j) + \alpha'(u_h) N_j (\nabla u_h \cdot \nabla N_i) + \beta'(u_h) N_i N_j \right]_{q} \det(\mathbf{J}_e) w_q
$$
This expression reveals the structure of the Jacobian. The first term, $\alpha(u_h) (\nabla N_i \cdot \nabla N_j)$, is analogous to the standard stiffness matrix but evaluated with the solution-dependent coefficient. The second and third terms arise from the differentiation of the nonlinear coefficients $\alpha(u_h)$ and $\beta(u_h)$ and are essential for achieving [quadratic convergence](@entry_id:142552).

#### The Commutation of Discretization and Linearization

The Jacobian derived for Newton's method is the result of first discretizing the PDE to get $\mathbf{N}(\mathbf{U})$ and then linearizing (differentiating) to get $\mathbf{J}(\mathbf{U})$. This is the **discretize-then-linearize (D-then-L)** approach. An alternative is the **linearize-then-discretize (L-then-D)** approach, where one first computes the Gateaux derivative ([directional derivative](@entry_id:143430)) of the [continuous operator](@entry_id:143297) $\mathcal{N}$ and then discretizes the resulting linear operator.

For a standard conforming Galerkin FEM with smooth coefficients and solution-independent [quadrature rules](@entry_id:753909), these two approaches **commute**; they yield the same discrete linear operator. This is because the discretization operator itself is linear and does not depend on the solution. However, commutation breaks down when the [discretization](@entry_id:145012) scheme itself is solution-dependent.  This occurs in several important scenarios:
*   **Nonlinear Stabilization:** Methods like Streamline Upwind/Petrov-Galerkin (SUPG) often use stabilization parameters that depend on the local solution or its residual, making the discrete operator nonlinear in a way not present in the original PDE.
*   **Flux/Slope Limiters:** In FVM or discontinuous Galerkin (DG) methods, limiters used to enforce [monotonicity](@entry_id:143760) are inherently nonlinear and solution-dependent functions.
*   **Partitioned Schemes:** In multiphysics problems solved with staggered or partitioned algorithms, one field is often "lagged" or held constant while solving for another. This algorithmic choice omits physical coupling terms from the tangent system, which would be present in a monolithic L-then-D formulation.

When commutation fails, the D-then-L Jacobian correctly represents the sensitivity of the discrete residual, ensuring the convergence of the algebraic solver. The L-then-D operator may be easier to derive but can lead to suboptimal or stalled convergence if it does not accurately reflect the behavior of the chosen numerical scheme.

#### Specialized Solvers

For certain nonlinear structures, Newton's method is not suitable. For the [variational inequality](@entry_id:172788) arising from the **obstacle problem**, the nonsmooth [complementarity condition](@entry_id:747558) $\lambda_i (u_i - \psi_i) = 0$ must be addressed. The **Primal-Dual Active Set (PDAS)** method is a highly effective iterative solver for this class of problems.  At each iteration, the algorithm partitions the nodes into a predicted "active set" $A^k$ (where the constraint is active, $u_i = \psi_i$) and an "inactive set" $I^k$ (where the constraint is inactive, $\lambda_i = 0$). It then solves a reduced linear system on the inactive set and updates the partitioning based on the new solution and multiplier values. This method can be interpreted as a semismooth Newton method and often converges in a finite number of steps.

Furthermore, the linear systems generated at each Newton step can be very large. **Nonlinear [multigrid methods](@entry_id:146386)**, such as the **Full Approximation Scheme (FAS)**, are designed to solve the nonlinear system efficiently without ever forming the global Jacobian. FAS works by recursively correcting the solution on a hierarchy of grids. A key component is the **tau correction**, which modifies the right-hand-side of the coarse-grid problem to ensure consistency between the fine-grid and coarse-grid operators. The FAS coarse-grid equation is: 
$$
\mathcal{N}_{H}(u_{H}) = R_{h}^{H}(f_{h} - \mathcal{N}_{h}(u_{h})) + \mathcal{N}_{H}(I_{h}^{H} u_{h})
$$
The term $\mathcal{N}_{H}(I_{h}^{H} u_{h}) - R_{h}^{H} \mathcal{N}_{h}(u_{h})$ (part of the full right-hand side) is the tau correction, which accounts for the fact that the coarse-grid operator acting on the restricted solution is not the same as the restricted fine-grid operator acting on the solution.

### Advanced Topics and Structure-Preserving Discretizations

Modern numerical analysis of nonlinear PDEs increasingly focuses on developing "structure-preserving" discretizations, which are schemes that inherit fundamental physical or mathematical properties of the continuous model at the discrete level.

#### Temporal Discretization and Stability

For time-dependent nonlinear PDEs, such as the [nonlinear diffusion](@entry_id:177801) equation $u_t = \nabla \cdot (\phi(u)\nabla u)$, the choice of time integrator is critical. **Explicit methods**, like forward Euler, are simple to implement but are only conditionally stable. A von Neumann analysis of the linearized equation shows that the time step $\Delta t$ is typically restricted by the mesh size $h$ and the maximum diffusivity $\phi_{\max}$. For a standard central difference [spatial discretization](@entry_id:172158), this leads to a severe restriction of the form:
$$
\Delta t \le \frac{h^2}{2d\phi_{\max}}
$$
where $d$ is the spatial dimension. This parabolic CFL condition can make explicit methods prohibitively expensive for fine meshes or problems with high diffusivity.

In contrast, **implicit methods**, like backward Euler, require solving a nonlinear system at each time step (using, for example, Newton's method) but are often [unconditionally stable](@entry_id:146281) for dissipative problems like diffusion. For the [nonlinear diffusion](@entry_id:177801) equation, the backward Euler method is contractive in the $\ell^2$-norm for any $\Delta t > 0$, because the discrete operator is negative semi-definite, a property inherited from the [continuous operator](@entry_id:143297). This allows for much larger time steps, limited by accuracy rather than stability.

#### Entropy Stability for Conservation Laws

For [hyperbolic conservation laws](@entry_id:147752), a critical property is the satisfaction of an **[entropy condition](@entry_id:166346)**, which ensures that the physically relevant [weak solution](@entry_id:146017) (containing shocks, not expansion shocks) is selected. While the Godunov method is entropy-stable by construction, many other schemes are not. An advanced design principle is to construct numerical fluxes that guarantee a [discrete entropy inequality](@entry_id:748505) is satisfied. 

This is achieved by splitting the numerical flux into an **entropy-conservative** part and a **dissipative** part. For a given entropy function $\eta(u)$, an entropy-conservative flux $f^{\text{ec}}$ is one that conserves the total discrete entropy $\sum_i \eta(u_i) \Delta x$. For Burgers' equation with the quadratic entropy $\eta(u) = u^2/2$, this flux is $f^{\text{ec}}(u_L, u_R) = (u_L^2 + u_L u_R + u_R^2)/6$. To ensure entropy decay at shocks, a carefully targeted [numerical dissipation](@entry_id:141318) term is added, often proportional to the square of the jump in the entropy variable across the interface. This gives a total rate of entropy change of the form:
$$
\frac{d S_h}{dt} = - \sum_i \frac{1}{2} \alpha_{i+1/2} (v_{i+1} - v_i)^2 \le 0
$$
where $v = \eta'(u)$ is the entropy variable and $\alpha_{i+1/2} \ge 0$ is a tunable dissipation coefficient. This approach provides a rigorous way to build stable, nonlinear schemes that respect a fundamental physical law of the system.

#### Adjoint Consistency in Optimization

The concept of consistency between continuous and discrete operators resurfaces in PDE-[constrained optimization](@entry_id:145264). Here, one wishes to compute the gradient of a [cost functional](@entry_id:268062) with respect to design parameters. The two main paradigms are **[optimize-then-discretize](@entry_id:752990) (O-D)** and **discretize-then-optimize (D-O)**. 

The D-O approach first discretizes the entire problem (state equation and [cost functional](@entry_id:268062)) and then derives the gradient of the discrete [cost functional](@entry_id:268062) using discrete adjoints. This approach, by construction, yields the exact gradient of the *discrete* model. The O-D approach first derives the [continuous adjoint](@entry_id:747804) equations in function space and then discretizes both the forward and adjoint equations.

For the two approaches to yield the same gradient, the numerical scheme must be **adjoint-consistent**, meaning the discretization of the [continuous adjoint](@entry_id:747804) operator must be equal to the transpose of the Jacobian of the discrete forward operator. Standard Galerkin FEM for self-adjoint problems is typically adjoint-consistent. However, many schemes, particularly those with [upwinding](@entry_id:756372) or other non-symmetric stabilizations, are not. In such cases, the D-O approach is generally preferred as it guarantees that any [gradient-based optimization](@entry_id:169228) algorithm will converge correctly for the chosen numerical model, even if that model's adjoint behavior does not perfectly mimic its continuous counterpart.