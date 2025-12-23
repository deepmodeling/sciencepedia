## Introduction
Numerically solving time-dependent partial differential equations (PDEs), particularly the [hyperbolic systems](@entry_id:260647) found in fluid dynamics and [wave propagation](@entry_id:144063), requires [time integrators](@entry_id:756005) that do more than just advance the solution accurately. They must also preserve crucial physical and mathematical properties, such as the non-negativity of density or non-oscillatory behavior near shocks. Standard [high-order methods](@entry_id:165413) can fail to maintain these properties, introducing unphysical artifacts that corrupt the simulation. Strong Stability Preserving (SSP) [time integration methods](@entry_id:136323) are a class of schemes specifically designed to address this challenge, providing a rigorous framework for constructing higher-order accurate methods that inherit the [robust stability](@entry_id:268091) properties of the simple, first-order Forward Euler scheme.

This article provides a thorough exploration of SSP methods, bridging theory and application for the graduate-level reader.
- The first chapter, **Principles and Mechanisms**, will dissect the core theory, explaining how the concept of a stable Forward Euler step is generalized through convex combinations and the Shu-Osher form to build stable, [high-order schemes](@entry_id:750306).
- The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate the practical utility of these methods in core areas like [computational fluid dynamics](@entry_id:142614) and in surprising fields such as machine learning.
- Finally, **Hands-On Practices** will offer concrete exercises to solidify your understanding of these powerful numerical tools.

By navigating these sections, you will gain a deep appreciation for how SSP integrators form a cornerstone of modern, reliable [scientific computing](@entry_id:143987).

## Principles and Mechanisms

The numerical solution of time-dependent partial differential equations (PDEs) often proceeds via the [method of lines](@entry_id:142882), where a [spatial discretization](@entry_id:172158) method (such as a Discontinuous Galerkin, Spectral, or Finite Volume method) is first applied to the PDE. This process transforms the PDE into a large system of coupled [ordinary differential equations](@entry_id:147024) (ODEs):
$$
\frac{d\boldsymbol{u}}{dt} = \boldsymbol{F}(\boldsymbol{u}(t))
$$
Here, $\boldsymbol{u}(t)$ is a vector containing all the degrees of freedom of the numerical solution at time $t$ (e.g., [modal coefficients](@entry_id:752057) or nodal values in each element), and $\boldsymbol{F}$ is the [spatial discretization](@entry_id:172158) operator. A crucial challenge is to select a [time integration](@entry_id:170891) method for this ODE system that not only advances the solution accurately but also preserves certain stability properties inherent to the underlying physical problem, especially for nonlinear [hyperbolic systems](@entry_id:260647) where solutions can develop sharp gradients or discontinuities. Strong Stability Preserving (SSP) [time integration methods](@entry_id:136323) are designed precisely for this purpose.

### The Foundational Principle: Forward Euler Contractivity

The theory of SSP methods is built upon a fundamental assumption about the spatial operator $\boldsymbol{F}$. We assume that the simplest [explicit time-stepping](@entry_id:168157) scheme, the **Forward Euler (FE) method**, is stable when applied to the semi-discrete system, provided the time step $\Delta t$ is sufficiently small. This stability, however, is not measured in the conventional sense of linear stability but rather in terms of a problem-specific **convex functional**, often a norm or [seminorm](@entry_id:264573), denoted $\|\cdot\|$. This functional is chosen to measure a physical or mathematical property of the solution that should not increase over time, such as the total variation (for TVD schemes) or the $L^2$-norm.

The foundational hypothesis is that the semi-discrete system is **strongly stable** with respect to $\|\cdot\|$. This means there exists a positive time step, $\Delta t_{\mathrm{FE}}$, such that the Forward Euler update, $\boldsymbol{u}^{n+1} = \boldsymbol{u}^n + \Delta t \, \boldsymbol{F}(\boldsymbol{u}^n)$, is contractive (or non-expansive) in this functional for any time step $\Delta t$ in the interval $[0, \Delta t_{\mathrm{FE}}]$. Mathematically, this is expressed as:
$$
\|\boldsymbol{u}^n + \Delta t \, \boldsymbol{F}(\boldsymbol{u}^n)\| \le \|\boldsymbol{u}^n\| \quad \text{for all } 0 \le \Delta t \le \Delta t_{\mathrm{FE}}
$$
This inequality is the cornerstone upon which all SSP methods are built . The value of $\Delta t_{\mathrm{FE}}$ depends entirely on the [spatial discretization](@entry_id:172158) $\boldsymbol{F}$ and encapsulates properties like the mesh size and the local wave speeds (a CFL-like condition).

It is critical to recognize that this property is highly dependent on both the spatial operator $\boldsymbol{F}$ and the chosen functional $\|\cdot\|$. For example, a standard Fourier spectral semidiscretization of the [linear advection equation](@entry_id:146245) $u_t + a u_x = 0$ is not contractive in the [total variation](@entry_id:140383) [seminorm](@entry_id:264573), $\|\boldsymbol{v}\| = \int |v_x| dx$, for any $\Delta t > 0$. In fact, the FE method amplifies the magnitude of every Fourier mode, causing the [total variation](@entry_id:140383) to grow. However, the same semidiscretization exactly conserves the $L^2$-norm in the continuous-time case, a property that can be preserved by specific [time integrators](@entry_id:756005) (like Crank-Nicolson) but is violated by Forward Euler. This illustrates that a given [spatial discretization](@entry_id:172158) may be strongly stable with respect to one functional (e.g., the $L^2$-norm under certain conditions) but not another (e.g., the TV-norm) . SSP methods are primarily developed for spatial discretizations that are provably monotone with respect to functionals like [total variation](@entry_id:140383) or [local extrema](@entry_id:144991), which is a key design feature of modern DG and [finite volume methods](@entry_id:749402) for [hyperbolic conservation laws](@entry_id:147752).

### The Core Mechanism: SSP via Convex Combinations

Given a [spatial discretization](@entry_id:172158) that is strongly stable under Forward Euler, the central question becomes: how can we construct higher-order [time integrators](@entry_id:756005) that inherit this crucial non-expansive property? A [first-order method](@entry_id:174104) like Forward Euler is often too inaccurate for practical use. The key insight lies in the use of **convex combinations**.

A fundamental property of any convex functional $\|\cdot\|$ is that a convex combination of states satisfies Jensen's inequality:
$$
\left\| \sum_{i} \alpha_i \boldsymbol{v}_i \right\| \le \sum_{i} \alpha_i \|\boldsymbol{v}_i\|, \quad \text{for } \alpha_i \ge 0, \sum_i \alpha_i = 1
$$
If each state $\boldsymbol{v}_i$ satisfies $\|\boldsymbol{v}_i\| \le M$, then the convex combination also satisfies $\|\sum_i \alpha_i \boldsymbol{v}_i\| \le \sum_i \alpha_i M = M$.

A [time integration](@entry_id:170891) method is defined as **Strong Stability Preserving (SSP)** if its update from $\boldsymbol{u}^n$ to $\boldsymbol{u}^{n+1}$ can be written as a convex combination of Forward Euler steps, each of which is itself contractive. By doing so, the higher-order method guarantees the desired non-expansive property, $\|\boldsymbol{u}^{n+1}\| \le \|\boldsymbol{u}^n\|$.

This structure allows the method to take a larger time step than Forward Euler. If a method can be decomposed into FE steps with effective step sizes $\delta t_i$ that all satisfy $\delta t_i \le \Delta t_{\mathrm{FE}}$, while the overall method uses a step size $\Delta t$, the method is SSP for $\Delta t \le C \Delta t_{\mathrm{FE}}$. The dimensionless constant $C$ is the **SSP coefficient**. If $C>1$, the SSP method is more efficient than Forward Euler, achieving higher accuracy with a larger time step. The goal of SSP method design is to maximize this coefficient $C$ for a given order of accuracy and number of computations (stages) .

### SSP Runge-Kutta Methods and the Shu-Osher Form

For the widely used class of explicit Runge-Kutta (RK) methods, the principle of convex combinations is formalized through the **Shu-Osher representation**. An $s$-stage explicit RK method can be written as:
$$
\begin{aligned}
\boldsymbol{u}^{(0)} = \boldsymbol{u}^n \\
\boldsymbol{u}^{(i)} = \sum_{j=0}^{i-1} \left( \alpha_{ij} \boldsymbol{u}^{(j)} + \beta_{ij} \Delta t \boldsymbol{F}(\boldsymbol{u}^{(j)}) \right), \quad i=1, \dots, s \\
\boldsymbol{u}^{n+1} = \boldsymbol{u}^{(s)}
\end{aligned}
$$
where the coefficients $\alpha_{ij}$ and $\beta_{ij}$ depend on the method's Butcher tableau. A method is SSP if it admits at least one such representation where all coefficients $\alpha_{ij}$ and $\beta_{ij}$ are non-negative, and for each stage $i$, $\sum_{j=0}^{i-1} \alpha_{ij} = 1$.

Under these conditions, each stage update can be seen as a convex combination. By rewriting the stage update as
$$
\boldsymbol{u}^{(i)} = \sum_{j=0}^{i-1} \alpha_{ij} \left( \boldsymbol{u}^{(j)} + \frac{\beta_{ij}}{\alpha_{ij}} \Delta t \, \boldsymbol{F}(\boldsymbol{u}^{(j)}) \right),
$$
we see that $\boldsymbol{u}^{(i)}$ is a convex combination of terms, each of which is a Forward Euler step starting from a previous stage $\boldsymbol{u}^{(j)}$. For the overall method to be SSP with coefficient $C$, each of these internal FE steps must be contractive. This requires their effective time steps to be bounded by $\Delta t_{\mathrm{FE}}$ when the global step is $\Delta t = C \Delta t_{\mathrm{FE}}$:
$$
\frac{\beta_{ij}}{\alpha_{ij}} \Delta t \le \Delta t_{\mathrm{FE}} \implies \frac{\beta_{ij}}{\alpha_{ij}} (C \Delta t_{\mathrm{FE}}) \le \Delta t_{\mathrm{FE}} \implies C \le \frac{\alpha_{ij}}{\beta_{ij}}
$$
This must hold for all $i,j$ where $\beta_{ij} > 0$. The SSP coefficient of the method is therefore the largest $C$ for which such a representation is possible, given by $C = \min_{i,j | \beta_{ij}>0} (\alpha_{ij}/\beta_{ij})$.

#### A Concrete Example: Analysis of a Third-Order SSP Runge-Kutta Method

Let's illustrate this with the popular three-stage, third-order SSP-RK method, often denoted SSPRK(3,3) . Its Butcher tableau is:
$$
\begin{array}{c|ccc}
0 & 0 & 0 & 0 \\
1 & 1 & 0 & 0 \\
\frac{1}{2} & \frac{1}{4} & \frac{1}{4} & 0 \\
\hline
& \frac{1}{6} & \frac{1}{6} & \frac{2}{3}
\end{array}
$$
Following the logic of the Shu-Osher form, we can derive the stage representations:
1.  **Stage 1**: The first stage update is a simple Forward Euler step. Let $\boldsymbol{u}^{(0)} = \boldsymbol{u}^n$.
    $$ \boldsymbol{u}^{(1)} = \boldsymbol{u}^{(0)} + \Delta t \boldsymbol{F}(\boldsymbol{u}^{(0)}) $$
    In Shu-Osher form, this is $\alpha_{10}=1, \beta_{10}=1$. The ratio is $\alpha_{10}/\beta_{10} = 1$.

2.  **Stage 2**: The second stage update is formed using the result of the first.
    $$ \boldsymbol{u}^{(2)} = \boldsymbol{u}^{(0)} + \frac{1}{4}\Delta t \boldsymbol{F}(\boldsymbol{u}^{(0)}) + \frac{1}{4}\Delta t \boldsymbol{F}(\boldsymbol{u}^{(1)}) $$
    We can rewrite this by substituting $\Delta t \boldsymbol{F}(\boldsymbol{u}^{(0)}) = \boldsymbol{u}^{(1)} - \boldsymbol{u}^{(0)}$:
    $$ \boldsymbol{u}^{(2)} = \boldsymbol{u}^{(0)} + \frac{1}{4}(\boldsymbol{u}^{(1)} - \boldsymbol{u}^{(0)}) + \frac{1}{4}\Delta t \boldsymbol{F}(\boldsymbol{u}^{(1)}) = \frac{3}{4}\boldsymbol{u}^{(0)} + \frac{1}{4}\boldsymbol{u}^{(1)} + \frac{1}{4}\Delta t \boldsymbol{F}(\boldsymbol{u}^{(1)}) $$
    This is a convex combination of $\boldsymbol{u}^{(0)}$ and a Forward Euler step from $\boldsymbol{u}^{(1)}$. The coefficients are $\alpha_{20}=3/4, \alpha_{21}=1/4$ and $\beta_{21}=1/4$. The ratio is $\alpha_{21}/\beta_{21}=1$.

3.  **Final Stage**: The final update to $\boldsymbol{u}^{n+1}$ is:
    $$ \boldsymbol{u}^{n+1} = \frac{1}{3}\boldsymbol{u}^{(0)} + \frac{2}{3}\boldsymbol{u}^{(2)} + \frac{2}{3}\Delta t \boldsymbol{F}(\boldsymbol{u}^{(2)}) $$
    The coefficients are $\alpha_{30}=1/3, \alpha_{32}=2/3$ and $\beta_{32}=2/3$. The ratio is $\alpha_{32}/\beta_{32}=1$.

The SSP coefficient for the method is the minimum of all these ratios, which is $\min(1, 1, 1) = 1$. Therefore, this third-order method is SSP with $C=1$, meaning it preserves the monotonicity property of Forward Euler under the same [time step constraint](@entry_id:756009), $\Delta t \le \Delta t_{\mathrm{FE}}$. While it offers no advantage in step size over Forward Euler, it provides third-order accuracy for the same computational cost as a generic 3-stage RK method.

### A Theoretical Lens: Absolute Monotonicity

While the Shu-Osher representation provides a [constructive proof](@entry_id:157587) of the SSP property, it can be difficult to find such a representation for a given method. A powerful analytical tool for studying SSP methods is the method's **[stability function](@entry_id:178107)**, $\phi(z)$, which for an explicit RK method is a polynomial. When applied to the [linear test equation](@entry_id:635061) $u' = \lambda u$, the method gives $u^{n+1} = \phi(\Delta t \lambda) u^n$.

The SSP property is deeply connected to a property of $\phi(z)$ on the negative real axis. A function $\phi(z)$ is said to be **absolutely monotonic** on an interval $[-r, 0]$ if it is infinitely differentiable and all its derivatives are non-negative on that interval:
$$
\phi^{(k)}(z) \ge 0 \quad \text{for all integers } k \ge 0 \text{ and all } z \in [-r, 0].
$$
The largest such $r$ is called the **radius of absolute [monotonicity](@entry_id:143760)**, denoted by $R$ .

A fundamental theorem of SSP theory states that for any explicit RK method, the SSP coefficient $C$ is bounded by the radius of absolute [monotonicity](@entry_id:143760) $R$.
$$
C \le R
$$
This inequality is always true. It provides a necessary condition: a method cannot be SSP with a coefficient larger than its radius of absolute monotonicity. Equality, $C=R$, is achieved if and only if the method admits a Shu-Osher representation with non-negative coefficients. Such methods are known as **optimal SSP RK methods** . This theorem provides a powerful link between the algebraic structure required for the convex combination (the Shu-Osher form) and an analytical property of the method's stability polynomial.

### Optimizing and Extending SSP Methods

The SSP framework is not limited to a single class of methods. Research in this area focuses on developing methods with larger SSP coefficients and extending the concepts to handle more complex physical problems.

#### Optimal SSP-RK Methods: The Quest for Larger Time Steps

A primary goal in designing SSP methods is to maximize the SSP coefficient $C$ for a given order of accuracy $p$ and number of stages $s$. Let $C_{\max}(s,p)$ be the maximum possible SSP coefficient. For a fixed order, increasing the number of stages (and thus the computational cost per step) can allow for a larger SSP coefficient and a more efficient method overall.

For second-order methods ($p=2$), a remarkable result is that the optimal SSP coefficient grows linearly with the number of stages, according to the formula $C_{\max}(s,2) = s-1$ for $s \ge 2$. For instance, the optimal coefficients are:
- $s=2, p=2: C_{\max} = 1$
- $s=3, p=2: C_{\max} = 2$
- $s=4, p=2: C_{\max} = 3$
This linear growth is achieved by a specific family of optimal SSPRK methods that can be constructed by composing $s-1$ Forward Euler steps followed by a final convex combination step to ensure [second-order accuracy](@entry_id:137876) . This demonstrates a direct trade-off: doubling the number of stages can nearly double the allowable time step, potentially halving the total number of steps needed for a simulation. For higher orders ($p \ge 3$), this linear growth is no longer possible, and the SSP coefficients are bounded by smaller constants.

#### SSP Linear Multistep Methods

The SSP concept also applies to Linear Multistep Methods (LMMs). A $k$-step explicit LMM is given by:
$$
\boldsymbol{u}^n = \sum_{j=1}^{k} \alpha_j \boldsymbol{u}^{n-j} + \Delta t \sum_{j=1}^{k} \beta_j \boldsymbol{F}(\boldsymbol{u}^{n-j})
$$
By rewriting this formula as a convex combination of previous states and Forward Euler-like steps, one can derive the [necessary and sufficient conditions](@entry_id:635428) for an LMM to be SSP with a coefficient $C > 0$. These conditions are elegantly simple:
1.  All coefficients must be non-negative: $\alpha_j \ge 0$ and $\beta_j \ge 0$ for all $j$.
2.  The $\alpha_j$ coefficients must sum to one: $\sum_{j=1}^{k} \alpha_j = 1$.
3.  The SSP coefficient is given by $C = \min_{j | \beta_j>0} \frac{\alpha_j}{\beta_j}$.
These conditions ensure that the method can be viewed as taking a convex average of contractive operations, thereby preserving the desired stability property .

#### SSP for Stiff and Non-Stiff Problems: IMEX Schemes

Many physical systems involve both non-stiff (e.g., advection) and stiff (e.g., diffusion, relaxation) phenomena. Such problems are described by a split ODE system:
$$
\frac{d\boldsymbol{u}}{dt} = \boldsymbol{F}(\boldsymbol{u}) + \boldsymbol{G}(\boldsymbol{u})
$$
where $\boldsymbol{F}$ is the non-stiff operator and $\boldsymbol{G}$ is the stiff operator. Implicit-Explicit (IMEX) methods are designed for these systems, treating $\boldsymbol{F}$ explicitly and $\boldsymbol{G}$ implicitly.

The SSP framework can be extended to IMEX methods by combining the building blocks of explicit SSP schemes with a new contractive operation: the **Backward Euler (BE) method**. If the BE update for the stiff part, $\boldsymbol{w} - \Delta t \boldsymbol{G}(\boldsymbol{w}) = \boldsymbol{v}$, is non-expansive in the same convex functional (i.e., $\|\boldsymbol{w}\| \le \|\boldsymbol{v}\|$), then it can be used as a building block.

An SSP IMEX scheme is constructed such that each stage is a convex combination of explicit FE steps on $\boldsymbol{F}$ and implicit BE steps on $\boldsymbol{G}$. This requires a Shu-Osher-like representation for the explicit part (with non-negative coefficients $\alpha_{ij}, \beta_{ij}$) and a corresponding monotone structure for the implicit part. To ensure strong damping of stiff components, the implicit part of the scheme is usually required to be **$L$-stable**, meaning its [stability function](@entry_id:178107) vanishes at infinity .

#### Beyond First Derivatives: Multiderivative SSP Methods

A further extension of the SSP concept involves **multiderivative methods**. These methods use not only the first time derivative $\boldsymbol{F}(\boldsymbol{u})$ but also higher time derivatives, such as $\ddot{\boldsymbol{u}} = \frac{d}{dt}\boldsymbol{F}(\boldsymbol{u}) = \boldsymbol{F}'(\boldsymbol{u})\boldsymbol{F}(\boldsymbol{u})$. For [hyperbolic conservation laws](@entry_id:147752), this higher derivative can often be computed efficiently via a Cauchy-Kowalewski procedure, expressing time derivatives as higher spatial derivatives.

The advantage of multiderivative methods is their potential for even larger SSP coefficients. This is achieved by introducing new, more stable building blocks into the convex combination. In addition to the standard FE step, one can use:
1.  A second-order Taylor-series (Lax-Wendroff type) step: $\boldsymbol{u} + \Delta t \boldsymbol{F}(\boldsymbol{u}) + \frac{1}{2} \Delta t^2 \ddot{\boldsymbol{u}}$.
2.  A pure second-derivative step: $\boldsymbol{u} + \gamma \Delta t^2 \ddot{\boldsymbol{u}}$.

If these new building blocks are themselves non-expansive under certain time step restrictions (e.g., $\|\boldsymbol{u} + \Delta t \boldsymbol{F}(\boldsymbol{u}) + \frac{1}{2} \Delta t^2 \ddot{\boldsymbol{u}}\| \le \|\boldsymbol{u}\|$ for $\Delta t \le \Delta t_{\mathrm{TS}}$), and if $\Delta t_{\mathrm{TS}} > \Delta t_{\mathrm{FE}}$, then a multiderivative method built as a convex combination of these steps can achieve an SSP coefficient larger than what is possible with single-derivative methods of the same order. This requires verifying additional forward-Euler-like [monotonicity](@entry_id:143760) conditions for these new derivative-involving steps .