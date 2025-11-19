## Introduction
Systems of partial differential equations (PDEs) describing physical phenomena like fluid flow or heat transfer often involve processes on vastly different time scales. Discretizing these equations leads to [systems of ordinary differential equations](@entry_id:266774) (ODEs) plagued by **stiffness**, where stability, not accuracy, forces explicit [time integrators](@entry_id:756005) to take prohibitively small time steps. While fully explicit methods are computationally cheap per step but severely restricted, fully [implicit methods](@entry_id:137073) handle stiffness but require solving large, costly [nonlinear systems](@entry_id:168347). This creates a critical need for methods that can balance computational efficiency with stability for [stiff problems](@entry_id:142143).

Implicit-Explicit (IMEX) Runge-Kutta schemes provide an elegant solution by strategically splitting the system, treating the nonstiff components explicitly and the stiff ones implicitly. This article provides a comprehensive overview of these powerful methods. The first chapter, "Principles and Mechanisms," will detail the formulation, stability analysis, and key design considerations of IMEX schemes. The "Applications and Interdisciplinary Connections" chapter will then explore their use in diverse scientific fields, from [computational fluid dynamics](@entry_id:142614) to astrophysics. Finally, the "Hands-On Practices" section offers concrete problems to solidify understanding. By selectively applying implicit and explicit treatments within a single time step, IMEX methods offer a path to efficient and accurate simulations of multi-scale physical systems. We begin by examining the core principles that make this possible.

## Principles and Mechanisms

### The Rationale for Implicit-Explicit Methods

Many physical phenomena described by partial differential equations (PDEs), such as fluid dynamics, heat transfer, and wave propagation, involve processes that occur on vastly different time scales. When these PDEs are discretized in space using methods like the Finite Element Method (FEM) or the Discontinuous Galerkin (DG) method, they yield a large system of coupled [ordinary differential equations](@entry_id:147024) (ODEs). A common characteristic of these systems is **stiffness**, where the presence of rapidly decaying modes necessitates extremely small time steps for [explicit time integration](@entry_id:165797) schemes to remain stable, even if those modes contribute little to the overall dynamics of the solution.

A canonical example is the advection-diffusion equation, whose [semi-discretization](@entry_id:163562) often leads to an ODE system that can be additively split:
$$
\frac{\mathrm{d}\mathbf{u}}{\mathrm{d}t} = \mathbf{f}(\mathbf{u}) + \mathbf{g}(\mathbf{u})
$$
Here, $\mathbf{f}(\mathbf{u})$ represents the nonstiff advection (convection) operator, and $\mathbf{g}(\mathbf{u})$ represents the stiff [diffusion operator](@entry_id:136699). The stiffness arises from the different dependencies of the operators' eigenvalues on the mesh size, $h$. The advection operator's eigenvalues scale roughly as $\mathcal{O}(1/h)$, leading to a stability constraint for explicit methods of the form $\Delta t \le C h$, known as a Courant-Friedrichs-Lewy (CFL) condition. In contrast, the [diffusion operator](@entry_id:136699)'s eigenvalues scale as $\mathcal{O}(-1/h^2)$. To maintain stability with an explicit method, the time step must satisfy the much more restrictive constraint $\Delta t \le C h^2$. For fine meshes (small $h$), this quadratic dependency makes purely explicit methods prohibitively expensive.

One could resort to a fully implicit method, which can handle stiff terms with large time steps. However, this requires solving a large, coupled, and often [nonlinear system](@entry_id:162704) of equations at every time step, which can be computationally intensive. **Implicit-Explicit (IMEX) Runge-Kutta schemes** offer a powerful compromise by treating the nonstiff part of the system explicitly and the stiff part implicitly. This approach aims to circumvent the severe time step restriction imposed by the stiff term while avoiding the high computational cost of a fully implicit solve for the entire system [@problem_id:3391600].

### Formulation of IMEX Runge-Kutta Schemes

IMEX schemes are a class of **Additive Runge-Kutta (ARK)** methods designed for split ODE systems of the form $\mathbf{u}'(t) = \mathbf{f}_E(\mathbf{u}(t)) + \mathbf{f}_I(\mathbf{u}(t))$, where $\mathbf{f}_E$ is the explicit (nonstiff) component and $\mathbf{f}_I$ is the implicit (stiff) component. An $s$-stage IMEX-RK method is defined by two Butcher tableaux: one for the explicit part, $(\tilde{A}, \tilde{\mathbf{b}})$, and one for the implicit part, $(A, \mathbf{b})$.

The explicit tableau matrix $\tilde{A}$ is typically strictly lower triangular, meaning $\tilde{a}_{ij} = 0$ for $j \ge i$. The implicit tableau matrix $A$ is lower triangular, with at least some non-zero diagonal entries, i.e., $a_{ij} = 0$ for $j > i$. A common and computationally efficient choice is a **Diagonally Implicit Runge-Kutta (DIRK)** scheme, where $A$ is lower triangular.

The computation of the $s$ intermediate stage values, $\mathbf{Y}_i$, proceeds as follows:
$$
\mathbf{Y}_i = \mathbf{u}^n + \Delta t \sum_{j=1}^{i-1} \tilde{a}_{ij} \mathbf{f}_E(\mathbf{Y}_j) + \Delta t \sum_{j=1}^{i} a_{ij} \mathbf{f}_I(\mathbf{Y}_j), \quad \text{for } i=1, \dots, s.
$$
Note the limits of the summations. The explicit contribution to stage $i$ depends only on previous stages $j  i$. The implicit contribution includes the term $a_{ii} \mathbf{f}_I(\mathbf{Y}_i)$, which makes the equation for $\mathbf{Y}_i$ implicit. Because of the lower triangular structure, each stage $\mathbf{Y}_i$ can be solved for sequentially using the already computed values $\mathbf{Y}_1, \dots, \mathbf{Y}_{i-1}$. This is a significant saving over fully [implicit methods](@entry_id:137073) that require solving for all stages simultaneously.

After all stage values are computed, the solution at the next time level, $\mathbf{u}^{n+1}$, is formed by a final combination:
$$
\mathbf{u}^{n+1} = \mathbf{u}^n + \Delta t \sum_{i=1}^{s} \left( \tilde{b}_i \mathbf{f}_E(\mathbf{Y}_i) + b_i \mathbf{f}_I(\mathbf{Y}_i) \right).
$$

Many IMEX schemes are designed with **shared abscissae**, meaning the time points $t^n + c_i \Delta t$ at which the stages are centered are the same for both the explicit and implicit parts. The vector of abscissae, $\mathbf{c} = (c_1, \dots, c_s)^\top$, often satisfies the [consistency conditions](@entry_id:637057) $\mathbf{c} = \tilde{A}\mathbf{e}$ and $\mathbf{c} = A\mathbf{e}$, where $\mathbf{e}$ is the vector of ones. This property is not merely a theoretical convenience; it has significant practical advantages in parallel implementations, as we will see later [@problem_id:3391582].

### Stability Analysis

The primary goal of an IMEX scheme is to achieve stability for large time steps in the presence of stiffness. The stability of an IMEX scheme is analyzed by applying it to the [linear test equation](@entry_id:635061) $\mathbf{u}' = \lambda_E \mathbf{u} + \lambda_I \mathbf{u}$, where $\lambda_E$ represents the eigenvalues of the nonstiff operator and $\lambda_I$ represents those of the stiff operator. The numerical solution after one step is given by $\mathbf{u}^{n+1} = R(z_E, z_I) \mathbf{u}^n$, where $z_E = \Delta t \lambda_E$ and $z_I = \Delta t \lambda_I$. The function $R(z_E, z_I)$ is the **stability function** of the IMEX scheme. For the scheme to be stable, we require $|R(z_E, z_I)| \le 1$.

Let's consider the simplest one-stage IMEX scheme, which combines the Forward Euler method for the explicit part and the Backward Euler method for the implicit part. The update rule is:
$$
\frac{\mathbf{u}^{n+1} - \mathbf{u}^n}{\Delta t} = \lambda_E \mathbf{u}^n + \lambda_I \mathbf{u}^{n+1}
$$
Solving for $\mathbf{u}^{n+1}$ yields:
$$
\mathbf{u}^{n+1} = \frac{1 + \Delta t \lambda_E}{1 - \Delta t \lambda_I} \mathbf{u}^n
$$
The [stability function](@entry_id:178107) is therefore $R(z_E, z_I) = \frac{1 + z_E}{1 - z_I}$ [@problem_id:3391635]. The [stability region](@entry_id:178537) is the set of pairs $(z_E, z_I)$ such that $|1+z_E| \le |1-z_I|$. If we consider the stiff part alone by setting $z_E=0$, the [stability function](@entry_id:178107) becomes that of the Backward Euler method, $R(0, z_I) = 1/(1-z_I)$, which is stable for the entire left half-plane $\text{Re}(z_I) \le 0$. The overall time step $\Delta t$ is thus limited only by the explicit part, requiring $z_E$ to be within the stability region of the Forward Euler method.

For multi-stage methods, the derivation of $R(z_E, z_I)$ is more involved but follows the same principle: solve for the stage values sequentially and substitute them into the final update formula. For instance, for a 2-stage scheme defined by tableaux $(\tilde{A}, \tilde{\mathbf{b}})$ and $(A, \mathbf{b})$, the derivation proceeds by first solving for $Y_1$, then using $Y_1$ to solve for $Y_2$, and finally substituting both into the update for $\mathbf{u}^{n+1}$. This typically results in a [rational function](@entry_id:270841) in $z_E$ and $z_I$ [@problem_id:3391596].

A crucial property for the implicit part of the scheme is **L-stability**. An implicit scheme is **A-stable** if its stability region contains the entire left half-plane, i.e., $|R(0, z_I)| \le 1$ for all $\text{Re}(z_I) \le 0$. A-stability ensures that the method is stable for any stiff linear problem, but it might not damp the fastest-decaying components effectively. L-stability is a stronger condition requiring A-stability and, additionally, that the [stability function](@entry_id:178107) vanishes at infinity in the left half-plane:
$$
\lim_{|z_I| \to \infty, \text{Re}(z_I) \le 0} |R(0, z_I)| = 0
$$
In practice, for the rational stability functions typical of RK methods, this is checked by taking the limit $z_I \to -\infty$. L-stability is highly desirable because it ensures that contributions from the stiffest components (corresponding to very large negative $\lambda_I$) are strongly damped, mimicking the behavior of the true solution [@problem_id:3391647].

### Order Conditions and Method Design

Achieving a desired [order of accuracy](@entry_id:145189) $p$ requires the coefficients in the Butcher tableaux to satisfy a set of algebraic equations known as **order conditions**. For IMEX schemes, these conditions are more numerous and complex than for standard Runge-Kutta methods, as they involve coupling between the explicit and implicit parts. For example, some third-order conditions for an ARK scheme involve mixed products of the Butcher matrices, such as requiring $(\tilde{\mathbf{b}})^\top \tilde{A} A \mathbf{e}$ to equal a specific value like $1/6$ [@problem_id:3391582]. The derivation of these conditions is beyond the scope of this chapter, but their existence underscores the intricate design process required to construct high-order, stable IMEX schemes.

### Practical and Advanced Considerations

#### Implementation with Mass Matrices

When IMEX methods are applied to semi-discretizations from DG or FEM, the system often takes the form $M \mathbf{u}' = \mathbf{f}_E(\mathbf{u}) + \mathbf{f}_I(\mathbf{u})$, where $M$ is the **mass matrix**. It is computationally prohibitive to form and apply the inverse $M^{-1}$. Instead, a practical implementation works with the system in its original form. By multiplying the standard IMEX stage equation by $M$, we obtain:
$$
M \mathbf{Y}_i = M \mathbf{u}^n + \Delta t \sum_{j=1}^{i-1} \tilde{a}_{ij} \mathbf{f}_E(\mathbf{Y}_j) + \Delta t \sum_{j=1}^{i} a_{ij} \mathbf{f}_I(\mathbf{Y}_j)
$$
Isolating the terms involving the unknown stage $\mathbf{Y}_i$ leads to an implicit solve of the form:
$$
\left( M - \Delta t a_{ii} \mathcal{J}_I(\mathbf{Y}_i) \right) \mathbf{Y}_i = \text{known terms}
$$
where $\mathcal{J}_I$ is the Jacobian of $\mathbf{f}_I$. This formulation correctly incorporates the mass matrix into the implicit solve without requiring its inversion [@problem_id:3391586]. The conditioning of the matrix on the left-hand side is critical for the efficiency of [iterative solvers](@entry_id:136910). For example, in SIPDG methods for diffusion, the implicit operator depends on a [penalty parameter](@entry_id:753318) $\gamma$. Coercivity requires $\gamma$ to scale with the polynomial degree $p$ and mesh size $h$ as $\gamma \sim p^2/h$. Choosing a penalty significantly larger than necessary, while still ensuring stability, can severely degrade the condition number of the [system matrix](@entry_id:172230), slowing down solver performance [@problem_id:3391598].

#### Parallel Performance and Shared Abscissae

In large-scale DG simulations on parallel architectures, evaluating the spatial operators, which involves communicating data between neighboring mesh elements, is often the main bottleneck. Here, the choice of IMEX abscissae has a profound impact. If the scheme uses **shared abscissae** ($c^E_i = c^I_i$), then at each stage $i$, both operators $\mathbf{f}_E$ and $\mathbf{f}_I$ are evaluated on the same [state vector](@entry_id:154607) $\mathbf{Y}_i$. This allows for a single loop over mesh faces to compute all necessary [numerical fluxes](@entry_id:752791), and a single communication of neighbor data per stage. This minimizes data movement and simplifies [synchronization](@entry_id:263918), reducing the risk of [data hazards](@entry_id:748203) like race conditions.

Conversely, if the abscissae are not shared ($c^E_i \neq c^I_i$), the implementation becomes much more challenging. It would require either two separate face loops (one for $\mathbf{f}_E$, one for $\mathbf{f}_I$), doubling the work, or a single loop that communicates two different sets of neighbor data, increasing memory traffic. A third option, time-interpolation to a common evaluation point, adds significant complexity and can compromise accuracy. Therefore, the use of shared abscissae is a critical design choice for efficient high-performance implementations [@problem_id:3391591].

#### Stiff Accuracy and Order Reduction

For [stiff problems](@entry_id:142143) involving [time-dependent boundary conditions](@entry_id:164382), standard IMEX schemes can suffer from a phenomenon known as **temporal [order reduction](@entry_id:752998)**, where the observed order of accuracy is lower than the theoretically designed order. This occurs because the final update $\mathbf{u}^{n+1}$ is a [linear combination](@entry_id:155091) of stage values, each satisfying the boundary condition at a different intermediate time. The resulting combination $\mathbf{u}^{n+1}$ generally fails to satisfy the boundary condition at the final time $t^{n+1}$, introducing an error or "defect" at the boundary. For a scheme with stage order $q$ (often $q=1$ for standard methods), this defect is of size $\mathcal{O}(\Delta t^q)$. The stiff operator rapidly propagates this error into the domain, contaminating the solution and reducing the global accuracy to order $q$.

This problem can be overcome by using a **stiffly accurate** scheme. A scheme is stiffly accurate if the final solution is identical to the last stage value, $\mathbf{u}^{n+1} = \mathbf{Y}_s$. This is typically achieved if the last abscissa is $c_s=1$ and the weights match the last row of the implicit matrix, $b_i = a_{si}$. Since $\mathbf{Y}_s$ is computed via an implicit solve at time $t^{n+1}$, it correctly satisfies the boundary condition at that time. By setting $\mathbf{u}^{n+1} = \mathbf{Y}_s$, the boundary defect is eliminated, and the designed [order of accuracy](@entry_id:145189) can be restored [@problem_id:3391614].

#### Strong Stability Preservation (SSP)

For [hyperbolic conservation laws](@entry_id:147752), it is often desirable that the numerical scheme preserves certain nonlinear stability properties, such as [monotonicity](@entry_id:143760) of the solution (e.g., being [total variation diminishing](@entry_id:140255), TVD). **Strong Stability Preserving (SSP)** [time-stepping methods](@entry_id:167527) are designed to guarantee this property, provided the simple Forward Euler method is SSP under a given [time step constraint](@entry_id:756009) $\Delta t \le \Delta t_{FE}$. Higher-order SSP methods can be constructed if they can be written as a convex combination of Forward Euler steps. The largest factor $\mathcal{C}$ such that the method is SSP for $\Delta t \le \mathcal{C} \Delta t_{FE}$ is called the SSP coefficient.

This concept extends to IMEX schemes. An SSP-IMEX method requires the explicit part to be SSP. Additionally, the implicit part must also preserve the desired monotonicity property. This is typically achieved if the implicit stages can be viewed as convex combinations of Backward Euler-type steps, which are themselves assumed to be monotone for the stiff operator. This ensures that neither the explicit nor the implicit part of the integrator violates the stability property, making SSP-IMEX schemes a powerful tool for hyperbolic problems with stiff source terms or diffusion [@problem_id:3391597].