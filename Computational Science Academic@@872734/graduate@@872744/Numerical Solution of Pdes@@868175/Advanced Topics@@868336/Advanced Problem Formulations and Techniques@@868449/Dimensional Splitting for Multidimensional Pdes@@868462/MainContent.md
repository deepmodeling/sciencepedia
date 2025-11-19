## Introduction
The numerical solution of partial differential equations (PDEs) in multiple spatial dimensions is a cornerstone of modern computational science, but it comes with a formidable challenge: the curse of dimensionality. As the number of dimensions increases, the size of the [discrete systems](@entry_id:167412) grows exponentially, making direct [implicit solution](@entry_id:172653) methods computationally intractable. A fully implicit scheme that is [unconditionally stable](@entry_id:146281) and efficient in one dimension becomes prohibitively expensive in two or three dimensions, requiring the solution of massive, complex linear systems. This creates a critical knowledge gap between the need for robust, stable solvers and the practical limitations of computation.

This article introduces [dimensional splitting](@entry_id:748441), an elegant and powerful family of methods designed to bridge this gap. The core idea is to replace a single, complex multidimensional problem with a sequence of simpler, one-dimensional problems that can be solved with high efficiency. By splitting the spatial operator along coordinate directions, we transform an otherwise unmanageable task into a series of straightforward steps.

Across the following chapters, you will gain a comprehensive understanding of this essential technique. In **Principles and Mechanisms**, we will delve into the mathematical foundation of [operator splitting](@entry_id:634210), deriving the first-order Lie-Trotter and second-order Strang splitting schemes and analyzing their accuracy through the lens of operator commutators. Next, **Applications and Interdisciplinary Connections** will showcase the method's versatility in fields like [computational fluid dynamics](@entry_id:142614) and heat transfer, exploring famous algorithms such as the Alternating Direction Implicit (ADI) method and [projection methods](@entry_id:147401) for incompressible flow. Finally, the **Hands-On Practices** section will guide you through implementing these methods to solve canonical problems, verifying their accuracy and exploring critical details like conservation properties.

## Principles and Mechanisms

The numerical solution of multidimensional [partial differential equations](@entry_id:143134) (PDEs) presents a significant challenge that scales poorly with the number of spatial dimensions. This is often referred to as the **[curse of dimensionality](@entry_id:143920)**. Consider a linear PDE in two dimensions, $u_t = \mathcal{L}_x u + \mathcal{L}_y u$, where $\mathcal{L}_x$ and $\mathcal{L}_y$ are spatial differential operators acting in the $x$ and $y$ directions, respectively. While an [implicit time-stepping](@entry_id:172036) scheme, such as the backward Euler method, is desirable for its [unconditional stability](@entry_id:145631) for many problems, its direct application to a multidimensional problem is computationally prohibitive. A discrete one-dimensional problem typically yields a linear system with a sparse, tridiagonal matrix, which can be solved efficiently in linear time. In contrast, a two-dimensional problem on an $N \times N$ grid results in a large, [block-tridiagonal matrix](@entry_id:177984) of size $N^2 \times N^2$, and direct inversion of this matrix is computationally expensive, scaling super-linearly with the number of grid points.

**Dimensional splitting** methods provide an elegant and effective strategy to circumvent this difficulty. The core principle is to replace the complex, multidimensional evolution problem with a sequence of simpler, one-dimensional problems. Instead of solving for all spatial directions simultaneously, we "split" the operator and advance the solution through a sequence of steps, each handling only one spatial direction at a time. This approach transforms an intractable multidimensional problem into a series of manageable one-dimensional tasks, each of which can be solved with high efficiency.

### Operator Splitting in the Semigroup Framework

To formalize the concept of [dimensional splitting](@entry_id:748441), it is instructive to adopt the language of operator semigroups. A linear evolution equation can be expressed as an abstract Cauchy problem on a suitable function space (e.g., $L^2(\Omega)$):
$$
\frac{du}{dt} = A u, \quad u(0) = u_0
$$
where $A$ is a [linear operator](@entry_id:136520) representing the spatial derivatives. For a multidimensional problem, $A$ is naturally decomposed as a sum of operators corresponding to each spatial direction, $A = A_x + A_y$. If $A$ is the generator of a [strongly continuous semigroup](@entry_id:274059), denoted $\exp(tA)$, the exact solution to the Cauchy problem is given by $u(t) = \exp(tA) u_0$.

The [operator exponential](@entry_id:198199) $\exp(\Delta t A) = \exp(\Delta t(A_x + A_y))$ is precisely the object that is difficult to compute. Splitting methods approximate this operator by a composition of the simpler, one-dimensional evolution operators $\exp(\Delta t A_x)$ and $\exp(\Delta t A_y)$ [@problem_id:3377951].

#### Lie-Trotter Splitting

The most straightforward splitting is the **Lie-Trotter splitting**, also known as Godunov splitting. It approximates the evolution over a time step $\Delta t$ by applying the evolution operators for each direction sequentially:
$$
u^{n+1} = \exp(\Delta t A_x) \exp(\Delta t A_y) u^n
$$
or with the operators in the reverse order. This corresponds to solving the PDE $u_t = A_y u$ for a duration $\Delta t$, and then using the result as the initial condition for solving $u_t = A_x u$ for a duration $\Delta t$. The accuracy of this approximation depends on the **commutator** of the operators, $[A_x, A_y] = A_x A_y - A_y A_x$. The Baker-Campbell-Hausdorff (BCH) formula reveals the structure of the error:
$$
\exp(\Delta t A_x) \exp(\Delta t A_y) = \exp\left(\Delta t(A_x+A_y) + \frac{1}{2}\Delta t^2 [A_x, A_y] + O(\Delta t^3)\right)
$$
The approximation differs from the exact [evolution operator](@entry_id:182628) $\exp(\Delta t(A_x+A_y))$ by a leading error term of order $\Delta t^2$. This results in a [local truncation error](@entry_id:147703) of $O(\Delta t^2)$ and, after accumulating over many time steps, a global error of $O(\Delta t)$. The Lie-Trotter splitting is therefore a **first-order accurate** method in time [@problem_id:3377986].

#### Strang Splitting

To achieve higher accuracy, one can use a symmetric composition, known as **Strang splitting**. This method involves half-steps and is constructed as follows:
$$
u^{n+1} = \exp\left(\frac{\Delta t}{2} A_x\right) \exp(\Delta t A_y) \exp\left(\frac{\Delta t}{2} A_x\right) u^n
$$
The symmetric structure of this composition leads to a cancellation of the $\Delta t^2$ error term in the BCH expansion. The leading error term is of order $\Delta t^3$ and involves nested commutators like $[A_x, [A_x, A_y]]$. This yields a [local truncation error](@entry_id:147703) of $O(\Delta t^3)$ and a [global error](@entry_id:147874) of $O(\Delta t^2)$, making Strang splitting a **second-order accurate** method [@problem_id:3377986]. This gain in accuracy comes at the cost of one additional one-dimensional solve per time step compared to the simplest Lie-Trotter scheme.

It is important to distinguish **[dimensional splitting](@entry_id:748441)** from generic [operator splitting](@entry_id:634210). The former specifically requires the decomposition of the operator to be aligned with spatial coordinate directions. Generic [operator splitting](@entry_id:634210), by contrast, allows for any convenient partition of the operator $A = B+C$, such as separating a [diffusion operator](@entry_id:136699) from a reaction operator in a reaction-diffusion equation [@problem_id:3377951].

### The Critical Role of Commutation

The accuracy of splitting methods hinges entirely on the commutator of the sub-operators. A remarkable simplification occurs when the operators commute, i.e., $[A_x, A_y] = 0$. In this case, all commutator terms in the BCH formula vanish, and the [operator exponential](@entry_id:198199) behaves like the scalar exponential:
$$
[A_x, A_y] = 0 \implies \exp(\Delta t A_x) \exp(\Delta t A_y) = \exp(\Delta t (A_x + A_y))
$$
This means that for [commuting operators](@entry_id:149529), both Lie-Trotter and Strang splitting are **exact**; they are not approximations but exact reformulations of the [evolution operator](@entry_id:182628) [@problem_id:3377986].

A vast and important class of PDEs benefits from this property. Consider the constant-coefficient linear [advection-diffusion equation](@entry_id:144002):
$$
u_{t} = a u_{x} + b u_{y} + \nu(u_{xx} + u_{yy})
$$
If we split this into operators $A_{x} = a\partial_{x} + \nu\partial_{xx}$ and $A_{y} = b\partial_{y} + \nu\partial_{yy}$, we can compute their commutator. Since the coefficients $a, b, \nu$ are constant and partial derivatives with respect to different variables commute (e.g., $\partial_x \partial_y u = \partial_y \partial_x u$ for [smooth functions](@entry_id:138942)), every term in the expansion of $[A_x, A_y]u = (A_x A_y - A_y A_x)u$ cancels out. For instance, $[a\partial_x, b\partial_y]u = ab(\partial_x\partial_y u - \partial_y\partial_x u) = 0$. Consequently, $[A_x, A_y] = 0$ [@problem_id:3377938]. For this entire class of equations, [dimensional splitting](@entry_id:748441) is an exact procedure at the continuous level, and any error in a numerical implementation arises solely from the [discretization](@entry_id:145012) of the one-dimensional subproblems.

### Applications and Implementation Techniques

The true power of [dimensional splitting](@entry_id:748441) is realized in its practical application, where it transforms complex implicit solves into simple sequential ones or allows for stable [explicit time-stepping](@entry_id:168157) with manageable constraints.

#### Fractional-Step and ADI Methods for Parabolic Equations

For [parabolic equations](@entry_id:144670) like the heat equation, $u_t = \kappa \Delta u$, implicit methods are favored for their stability. A [fractional-step method](@entry_id:166761) based on Lie-Trotter splitting and the backward Euler scheme proceeds in two stages:
1.  Solve for an intermediate solution $u^*$ from $u^n$: $(I - \Delta t \mathcal{L}_x) u^* = u^n$
2.  Solve for the final solution $u^{n+1}$ from $u^*$: $(I - \Delta t \mathcal{L}_y) u^{n+1} = u^*$

Each stage involves solving a set of one-dimensional problems. For example, the first stage requires solving a tridiagonal linear system for each grid line in the $x$-direction [@problem_id:3377939]. This is vastly more efficient than inverting the full two-dimensional operator $(I - \Delta t (\mathcal{L}_x + \mathcal{L}_y))$.

A particularly famous second-order scheme is the **Peaceman-Rachford Alternating Direction Implicit (ADI)** method [@problem_id:3377995]. It can be viewed as a splitting of the Crank-Nicolson method. The standard Crank-Nicolson scheme for $u_t = (L_x + L_y)u$ is:
$$
\left(I - \frac{\Delta t}{2} (L_x + L_y)\right) u^{n+1} = \left(I + \frac{\Delta t}{2} (L_x + L_y)\right) u^n
$$
The ADI method rearranges and splits this into two computationally efficient, tridiagonal solves:
1.  **x-implicit step**: $\left(I - \frac{\Delta t}{2} L_x\right) u^{n+1/2} = \left(I + \frac{\Delta t}{2} L_y\right) u^n$
2.  **y-implicit step**: $\left(I - \frac{\Delta t}{2} L_y\right) u^{n+1} = \left(I + \frac{\Delta t}{2} L_x\right) u^{n+1/2}$

For constant-coefficient problems, this scheme is algebraically equivalent to the original Crank-Nicolson method but replaces one large [matrix inversion](@entry_id:636005) with a sequence of simple 1D inversions.

#### Sequential Updates for Hyperbolic Equations

For hyperbolic equations like the [linear advection equation](@entry_id:146245) $u_t + a u_x + b u_y = 0$, explicit schemes are common. A sequential splitting using a [first-order upwind scheme](@entry_id:749417) in each direction can be analyzed for stability. A von Neumann stability analysis reveals a simple and intuitive result: the stability of the split scheme requires that the Courant-Friedrichs-Lewy (CFL) condition is met for each one-dimensional substep [@problem_id:338002]. For a Lie-Trotter splitting of two explicit 1D schemes, the overall scheme is stable if and only if each component scheme is stable. This leads to the combined stability condition:
$$
\Delta t \le \min\left( \frac{h_x}{|a|}, \frac{h_y}{|b|} \right)
$$
This is a significant practical advantage over unsplit explicit schemes, which often have more restrictive stability criteria involving both $h_x$ and $h_y$ in a single inequality.

### Caveats and Advanced Considerations

While powerful, [dimensional splitting](@entry_id:748441) is not a panacea. Its application requires careful consideration of several factors to ensure accuracy, stability, and physical fidelity.

#### Handling of Boundary Conditions

In a split scheme, boundary conditions must be applied correctly during each substep. When solving the 1D problem in the $x$-direction, the physical boundary conditions on the boundaries at the start and end of the $x$-domain must be enforced. Any other boundaries (e.g., those parallel to the $x$-direction) are not boundaries for the 1D subproblem and should not have artificial conditions imposed [@problem_id:3377939].

The treatment becomes more subtle for second-order methods with [time-dependent boundary conditions](@entry_id:164382). For Strang splitting to maintain its [second-order accuracy](@entry_id:137876), any boundary forcing must be evaluated at the temporal midpoint of its corresponding substep's integration interval [@problem_id:3377952]. For a scheme composed of an $x$-half-step, a $y$-full-step, and an $x$-half-step, the boundary data must be evaluated at times $t^n+\Delta t/4$, $t^n+\Delta t/2$, and $t^n+3\Delta t/4$, respectively. Using a single time for all substeps (e.g., $t^n$ or $t^n+\Delta t/2$) will degrade the overall temporal accuracy to first order. Similarly, the [spatial discretization](@entry_id:172158) of the boundary condition itself (e.g., a Neumann condition) must be at least second-order accurate to not pollute the [high-order accuracy](@entry_id:163460) of the interior scheme.

#### Conservation in Compressible Flows

For equations in conservation law form, $u_t + \nabla \cdot \mathbf{F}(u) = 0$, it is paramount that the splitting is applied to the conservative formulation. A naive splitting of the non-conservative or transport form, $u_t + \mathbf{F}'(u) \cdot \nabla u = 0$, can lead to the artificial creation or destruction of the conserved quantity (e.g., mass). This occurs because the splitting implicitly neglects the [source term](@entry_id:269111) $(\nabla \cdot \mathbf{b})u$ that arises from the product rule in [compressible flows](@entry_id:747589) where $\nabla \cdot \mathbf{b} \neq 0$ [@problem_id:3377962].

A correct implementation uses a [finite volume](@entry_id:749401) approach, where each 1D sweep solves a 1D conservation law, e.g., $u_t + (b_x u)_x = 0$. The update for each cell average is based on the difference of fluxes at the cell faces. The sum of updates over the entire domain then forms a [telescoping sum](@entry_id:262349), ensuring that the total discrete mass is conserved in each sweep up to machine precision.

#### Preservation of Qualitative Properties

Dimensional splitting can fail to preserve important qualitative properties of the solution, even if the underlying 1D schemes possess them.
- **Monotonicity and Maximum Principles**: A 1D monotone scheme (one that does not introduce new [extrema](@entry_id:271659)) does not guarantee that a 2D scheme constructed via splitting will be monotone. This issue can be particularly pronounced with highly anisotropic grids or with inconsistent handling of source terms, which can introduce unphysical overshoots or undershoots [@problem_id:3377996]. For instance, applying a [source term](@entry_id:269111) in every substep of a Lie splitting can effectively double its influence, breaking the delicate balance required for [monotonicity](@entry_id:143760). A simple fix is often to include the source term in only one of the substeps.
- **Total Variation Diminishing (TVD) Property**: Similarly, applying [dimensional splitting](@entry_id:748441) to a 1D TVD scheme does not guarantee that the resulting multidimensional scheme is TVD. A classic counterexample involves schemes like MUSCL, which are designed to be TVD in 1D. A naive splitting can still produce spurious oscillations and increase the total variation of the solution, particularly near sharp gradients or discontinuities [@problem_id:3377984]. This demonstrates that properties do not always extend from 1D to multiple dimensions through splitting, and more sophisticated multidimensional limiters may be necessary.

### Alternative Formulations: Additive Splitting

Finally, it is useful to contrast the sequential nature of [dimensional splitting](@entry_id:748441) with **additive splitting** methods. While [dimensional splitting](@entry_id:748441) computes updates sequentially, $u^* \leftarrow S_x u^n$, $u^{n+1} \leftarrow S_y u^*$, additive splitting aims to parallelize the subproblems [@problem_id:3377946].

An additive scheme can be interpreted as one step of a [fixed-point iteration](@entry_id:137769) (like a Jacobi or Richardson iteration) for the fully-coupled implicit equation $(I - \Delta t (A_x+A_y))u = u^n$. For example, one can define parallel subproblems for intermediate solutions $v_x$ and $v_y$ and then combine them:
$$
(I - \Delta t A_x) v_x = u^n + \Delta t A_y u^n \quad \text{(solve for } v_x\text{)}
$$
$$
(I - \Delta t A_y) v_y = u^n + \Delta t A_x u^n \quad \text{(solve for } v_y\text{)}
$$
These subproblems are uncoupled and can be solved in parallel. The final solution is then formed by an averaging process, e.g., $u^{n+1} = \frac{1}{2}(v_x+v_y)$. Such methods are often used in constructing [preconditioners](@entry_id:753679) for [iterative solvers](@entry_id:136910) for the full system rather than as standalone [time-stepping schemes](@entry_id:755998). They highlight a different philosophy of splitting, focused on [parallel computation](@entry_id:273857) rather than sequential decomposition.