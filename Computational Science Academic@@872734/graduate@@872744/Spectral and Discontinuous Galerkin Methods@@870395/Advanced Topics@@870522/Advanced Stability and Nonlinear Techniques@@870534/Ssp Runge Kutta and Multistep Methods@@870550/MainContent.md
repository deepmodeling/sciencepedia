## Introduction
In the quest for highly accurate solutions to [hyperbolic partial differential equations](@entry_id:171951), the pairing of high-order spatial discretizations like Discontinuous Galerkin (DG) methods with a suitable time integrator is critical. While matching the order of accuracy in time is a primary goal, a more fundamental challenge arises: preserving essential nonlinear stability properties. Standard high-order [time-stepping schemes](@entry_id:755998) can fail to maintain physical constraints like positivity or [monotonicity](@entry_id:143760), leading to [spurious oscillations](@entry_id:152404) and non-physical results, especially in problems with shocks or sharp gradients. This knowledge gap highlights the need for a special class of [time integrators](@entry_id:756005) designed explicitly for stability.

This article introduces **Strong Stability Preserving (SSP) Runge-Kutta and [multistep methods](@entry_id:147097)**, a powerful framework for constructing high-order [time integrators](@entry_id:756005) that provably maintain these critical stability properties. By studying these methods, you will learn how to build robust, accurate, and physically meaningful numerical simulations for complex systems.

The following chapters offer a comprehensive exploration of the topic. The first chapter, **"Principles and Mechanisms,"** delves into the core theory behind SSP methods, explaining the principle of convex combinations and how it is used to construct both Runge-Kutta and linear multistep schemes. The second chapter, **"Applications and Interdisciplinary Connections,"** showcases the practical impact of SSP methods, from establishing stability for DG schemes in computational fluid dynamics to novel applications in [pharmacokinetics](@entry_id:136480) and [quantitative finance](@entry_id:139120). Finally, **"Hands-On Practices"** provides interactive problems to solidify your understanding and apply these concepts to practical coding and analysis scenarios. We begin by examining the fundamental principles that make these methods strongly stable.

## Principles and Mechanisms

In the numerical solution of [hyperbolic partial differential equations](@entry_id:171951), particularly when using high-order spatial discretizations such as discontinuous Galerkin (DG) or [spectral methods](@entry_id:141737), the choice of [time integration](@entry_id:170891) scheme is of paramount importance. While [high-order accuracy](@entry_id:163460) in time is desired to match the spatial accuracy, a more subtle and often critical requirement is the preservation of certain nonlinear stability properties. These properties, such as positivity of solutions (e.g., for density or concentration), monotonicity, or non-increase in [total variation](@entry_id:140383), are essential for producing physically meaningful and robust numerical results, especially for problems involving shocks or sharp gradients.

This chapter delves into the principles and mechanisms of **Strong Stability Preserving (SSP)** time [discretization methods](@entry_id:272547), a class of schemes specifically designed to guarantee these crucial stability properties, provided the simple first-order forward Euler method also satisfies them.

### The Need for Strong Stability

Consider a system of ordinary differential equations (ODEs) arising from a spatial [semi-discretization](@entry_id:163562) of a hyperbolic PDE:
$$
\frac{d\boldsymbol{u}}{dt} = \mathcal{L}(\boldsymbol{u})
$$
Here, $\boldsymbol{u}(t)$ is a vector of all degrees of freedom (e.g., cell averages and [higher-order moments](@entry_id:266936) in a DG method), and $\mathcal{L}$ is the spatial operator. For many such discretizations, it can be proven that the simple **forward Euler (FE)** method,
$$
\boldsymbol{u}^{n+1} = \boldsymbol{u}^n + \Delta t \, \mathcal{L}(\boldsymbol{u}^n)
$$
preserves a desired stability property under a Courant-Friedrichs-Lewy (CFL) type condition, $\Delta t \le \Delta t_{\mathrm{FE}}$. This stability is often expressed in terms of a **convex functional**, denoted $\Phi(\boldsymbol{u})$. For example, $\Phi$ could be the [total variation](@entry_id:140383) (TV) semi-norm, or a discrete [energy norm](@entry_id:274966) like the $L^2$-norm. The FE stability condition is then stated as:
$$
\Phi(\boldsymbol{u}^n + \Delta t \, \mathcal{L}(\boldsymbol{u}^n)) \le \Phi(\boldsymbol{u}^n) \quad \text{for all } \Delta t \le \Delta t_{\mathrm{FE}}
$$
This means that under the FE time step restriction, the "size" of the solution, as measured by $\Phi$, does not grow. [@problem_id:3420338] [@problem_id:3420299]

The forward Euler method, however, is only first-order accurate. Using it with a high-order spatial method would compromise the overall accuracy of the simulation. A natural impulse is to replace it with a classical high-order method, such as a standard Runge-Kutta or linear multistep scheme. This impulse, however, can lead to catastrophic failure of the stability property.

Consider, for example, the two-step Adams-Bashforth (AB2) method, a second-order scheme. Its formula involves weighted differences of the operator evaluations from previous steps. A simple numerical experiment reveals the danger [@problem_id:3420262]. Let's discretize the [linear advection equation](@entry_id:146245) $u_t + a u_x = 0$ with an upwind [finite volume method](@entry_id:141374) (equivalent to DG with polynomial degree $p=0$), for which the forward Euler method is positivity-preserving under the condition $\lambda = a \Delta t / \Delta x \le 1$. If we start with non-negative cell averages $\boldsymbol{U}^0 = \begin{pmatrix} 1 & 1 & 0 \end{pmatrix}^T$, a single FE step with $\lambda=1$ correctly yields the non-negative state $\boldsymbol{U}^1 = \begin{pmatrix} 0 & 1 & 1 \end{pmatrix}^T$. However, applying one step of the AB2 method,
$$
\boldsymbol{U}^{2} = \boldsymbol{U}^{1} + \Delta t \left( \frac{3}{2} \mathcal{L}(\boldsymbol{U}^1) - \frac{1}{2} \mathcal{L}(\boldsymbol{U}^0) \right)
$$
can produce a new state with a negative cell average, for instance, $U_1^2 = -1/2$. The method creates a new, non-physical minimum. The culprit is the negative coefficient, $-1/2$, in the formula. This demonstrates that a high-order method does not automatically inherit the stability properties of its underlying first-order building block. A special structure is required; this is the motivation for SSP methods.

### The Core Principle: Convex Combinations

Strong Stability Preserving methods are high-order [time integrators](@entry_id:756005) that guarantee the preservation of the monotonicity property of the forward Euler method. The formal definition of an SSP method is one for which
$$
\Phi(\boldsymbol{u}^{n+1}) \le \Phi(\boldsymbol{u}^n) \quad \text{whenever} \quad \Delta t \le C \cdot \Delta t_{\mathrm{FE}}
$$
The dimensionless constant $C > 0$ is called the **SSP coefficient**. The key insight, developed by Shu and Osher, is that this guarantee can be achieved if the high-order update $\boldsymbol{u}^{n+1}$ can be written as a **convex combination** of operators that are themselves monotonicity-preserving.

The simplest such operator is the forward Euler step itself. The core principle of all SSP methods is that their updates can be decomposed into a sequence of applications of the forward Euler operator and convex averaging. For a convex functional $\Phi$, if we have a set of states $\boldsymbol{v}_k$ that all satisfy $\Phi(\boldsymbol{v}_k) \le \Phi(\boldsymbol{u}^n)$, then any convex combination $\boldsymbol{w} = \sum_k \theta_k \boldsymbol{v}_k$ (where $\theta_k \ge 0$ and $\sum_k \theta_k = 1$) will also satisfy this property:
$$
\Phi(\boldsymbol{w}) = \Phi\left(\sum_k \theta_k \boldsymbol{v}_k\right) \le \sum_k \theta_k \Phi(\boldsymbol{v}_k) \le \sum_k \theta_k \Phi(\boldsymbol{u}^n) = \Phi(\boldsymbol{u}^n)
$$
SSP methods are ingeniously constructed so that each stage, and the final result, is precisely such a convex combination of results from stable forward Euler steps.

### Strong Stability Preserving Runge-Kutta (SSP-RK) Methods

Let's see how this principle is realized for explicit Runge-Kutta methods. An explicit $s$-stage SSP-RK method can be expressed in the so-called **Shu-Osher representation**. Each intermediate stage $\boldsymbol{u}^{(i)}$ and the final result $\boldsymbol{u}^{n+1}$ are formed as a convex combination of the results of forward Euler steps applied to previous stages:
$$
\boldsymbol{u}^{(i)} = \sum_{j=0}^{i-1} \left( \alpha_{ij} \boldsymbol{u}^{(j)} + \beta_{ij} \Delta t \, \mathcal{L}(\boldsymbol{u}^{(j)}) \right)
$$
where $\boldsymbol{u}^{(0)} = \boldsymbol{u}^n$, and the coefficients must satisfy $\alpha_{ij} \ge 0$, $\beta_{ij} \ge 0$, and $\sum_j \alpha_{ij} = 1$ for each stage $i$. This can be rewritten to make the structure even clearer:
$$
\boldsymbol{u}^{(i)} = \sum_{j=0}^{i-1} \alpha_{ij} \left( \boldsymbol{u}^{(j)} + \frac{\beta_{ij}}{\alpha_{ij}} \Delta t \, \mathcal{L}(\boldsymbol{u}^{(j)}) \right)
$$
(This holds for $\alpha_{ij} > 0$). Each term in the sum is now a forward Euler operator applied to a previous stage $\boldsymbol{u}^{(j)}$ with an effective time step $\tau = \frac{\beta_{ij}}{\alpha_{ij}} \Delta t$. To ensure that each of these building blocks is stable, we must require $\tau \le \Delta t_{\mathrm{FE}}$, which implies:
$$
\Delta t \le \frac{\alpha_{ij}}{\beta_{ij}} \Delta t_{\mathrm{FE}}
$$
This condition must hold for all terms in the convex combination across all stages. Therefore, the overall time step restriction for the SSP-RK method is
$$
\Delta t \le C \cdot \Delta t_{\mathrm{FE}}, \quad \text{where} \quad C = \min_{i,j \text{ with } \beta_{ij}>0} \left( \frac{\alpha_{ij}}{\beta_{ij}} \right)
$$

#### Illustrative Examples

Let's analyze a specific 2nd-order, 4-stage SSP-RK method to see this in practice [@problem_id:3420338]. The method is:
- $\boldsymbol{u}^{(1)} = \boldsymbol{u}^{n}$
- $\boldsymbol{u}^{(2)} = \boldsymbol{u}^{(1)} + \frac{\Delta t}{3} \mathcal{L}(\boldsymbol{u}^{(1)})$
- $\boldsymbol{u}^{(3)} = \boldsymbol{u}^{(2)} + \frac{\Delta t}{3} \mathcal{L}(\boldsymbol{u}^{(2)})$
- $\boldsymbol{u}^{(4)} = \boldsymbol{u}^{(3)} + \frac{\Delta t}{3} \mathcal{L}(\boldsymbol{u}^{(3)})$
- $\boldsymbol{u}^{n+1} = \frac{1}{4}\boldsymbol{u}^{n} + \frac{3}{4}\left(\boldsymbol{u}^{(4)} + \frac{\Delta t}{3}\mathcal{L}(\boldsymbol{u}^{(4)})\right)$

Each of the stages $\boldsymbol{u}^{(2)}, \boldsymbol{u}^{(3)}, \boldsymbol{u}^{(4)}$, and the final term in the parentheses, are forward Euler steps with a step size of $\tau = \Delta t/3$. For these steps to be individually stable, we need $\Delta t/3 \le \Delta t_{\mathrm{FE}}$. If this condition holds, then $\Phi(\boldsymbol{u}^{(k+1)}) \le \Phi(\boldsymbol{u}^{(k)})$, and by induction, $\Phi(\boldsymbol{u}^{(4)} + \frac{\Delta t}{3}\mathcal{L}(\boldsymbol{u}^{(4)})) \le \dots \le \Phi(\boldsymbol{u}^n)$. The final update is a convex combination of $\boldsymbol{u}^n$ and this final stable term. By the property of convex functionals, $\Phi(\boldsymbol{u}^{n+1}) \le \Phi(\boldsymbol{u}^n)$ is guaranteed. The time step restriction is $\Delta t \le 3 \Delta t_{\mathrm{FE}}$, so the SSP coefficient for this method is $C=3$.

As a second key example, consider the widely used 3-stage, 3rd-order SSP-RK method, often denoted SSPRK(3,3). Through algebraic manipulation, one can show that this method can also be decomposed into a sequence of convex combinations of FE steps [@problem_id:3420248]. The analysis reveals that stability for every component of the decomposition is maintained as long as $\Delta t \le 1 \cdot \Delta t_{\mathrm{FE}}$. Thus, for SSPRK(3,3), the SSP coefficient is $C=1$. The process of finding these decompositions and the optimal SSP coefficient can be formalized as a [linear programming](@entry_id:138188) problem [@problem_id:3420241].

Connecting this to a practical DG setting, the forward Euler time step limit $\Delta t_{\mathrm{FE}}$ is determined by the mesh size $h$, polynomial degree $p$, and maximum [wave speed](@entry_id:186208) $a$. A typical bound is $\Delta t_{\mathrm{FE}} \le \frac{\sigma h}{(2p+1)a}$ for some constant $\sigma$. An $s$-stage SSP-RK method with coefficient $C$ can then be used with a time step up to $\Delta t \le C \cdot \frac{\sigma h}{(2p+1)a}$ [@problem_id:3420295].

### Strong Stability Preserving Linear Multistep Methods (SSP-LMMs)

The principle of convex combinations also extends to [linear multistep methods](@entry_id:139528) (LMMs). An explicit $r$-step LMM has the general form:
$$
\boldsymbol{u}^{n+1} = \sum_{j=0}^{r-1} \alpha_{j} \boldsymbol{u}^{n-j} + \Delta t \sum_{j=0}^{r-1} \beta_{j} \mathcal{L}(\boldsymbol{u}^{n-j})
$$
To be SSP, this update formula must be representable as a convex combination of the stable forward Euler operator applied to the previous solutions $\boldsymbol{u}^{n-j}$. By rearranging the terms, we can show that the method is SSP if and only if it can be written as [@problem_id:3420255]:
$$
\boldsymbol{u}^{n+1} = \sum_{j=0}^{r-1} \left( A_j \boldsymbol{u}^{n-j} + B_j \left(\boldsymbol{u}^{n-j} + \frac{\Delta t}{C} \mathcal{L}(\boldsymbol{u}^{n-j}) \right) \right)
$$
where $A_j, B_j \ge 0$ and $\sum(A_j+B_j)=1$. Comparing this form with the standard LMM formula reveals the [necessary and sufficient conditions](@entry_id:635428) on the coefficients for the method to be SSP:
1. $\beta_j \ge 0$ for all $j=0, \dots, r-1$.
2. $\alpha_j \ge C \beta_j$ for all $j=0, \dots, r-1$.
3. $\sum \alpha_j = 1$. (A standard [consistency condition](@entry_id:198045)).

The second condition, $\alpha_j \ge C\beta_j$, is the most crucial. It implies that for every step $j$ where $\beta_j > 0$, the SSP coefficient $C$ is bounded by $C \le \alpha_j / \beta_j$. To satisfy this for all steps simultaneously, $C$ must be less than or equal to the minimum of these ratios. The maximal SSP coefficient is therefore:
$$
C_{\max} = \min_{j \text{ with } \beta_j > 0} \left( \frac{\alpha_j}{\beta_j} \right)
$$
This provides a clear recipe for constructing and analyzing SSP [linear multistep methods](@entry_id:139528), mirroring the framework for SSP-RK methods.

### Deeper Theoretical Aspects and Limitations

#### Linear Stability vs. Strong Stability

It is critical to distinguish the nonlinear stability guaranteed by the SSP property from standard **[linear stability analysis](@entry_id:154985)**. Linear stability is assessed by applying a method to the test equation $u' = \lambda u$, which yields an amplification factor $\psi(z)$ where $z = \Delta t \lambda$. The method is stable if $|\psi(z)| \le 1$. The set of all complex $z$ for which this holds is the **linear [stability region](@entry_id:178537)**, $\mathcal{S}$ [@problem_id:3420292]. This analysis is sufficient for linear problems where the operator's spectrum determines stability.

Strong stability is a much stronger condition. It applies to nonlinear operators satisfying a contractivity property in a specific norm. The SSP coefficient $C$ is technically defined by the method's **radius of absolute [monotonicity](@entry_id:143760)**, $R$. This is the largest value $r \ge 0$ such that the stability polynomial $\psi(z)$ and all its derivatives are non-negative on the interval $[-r, 0]$. It is a fundamental result that for an explicit RK method, its SSP coefficient is exactly this radius, $C = R$.

For virtually all SSP methods, the radius of absolute [monotonicity](@entry_id:143760) $R$ is strictly smaller than the length of the stability interval on the negative real axis, $S_{\mathbb{R}^-} = \sup\{ r \ge 0 : [-r, 0] \subset \mathcal{S} \}$. For example, the classical 2nd-order SSP-RK method has $R=1$ but is linearly stable for $z \in [-2, 0]$. This means that satisfying the linear stability condition is necessary, but not sufficient, to guarantee the SSP property for general nonlinear problems. The more restrictive condition governed by $R$ is required. [@problem_id:3420292]

#### Order Barriers and Stage Order

The requirement of non-negative coefficients in the Shu-Osher representation imposes significant constraints on the method. High-order accuracy in RK methods is typically achieved through delicate cancellation of truncation errors, which often requires negative coefficients. The SSP structure, based on convex combinations, forbids this at the stage level. This leads to a fundamental trade-off:

For an SSP-RK method, we must distinguish between its **overall order** (accuracy of the final step $\boldsymbol{u}^{n+1}$) and its **stage order** (accuracy of intermediate stages $\boldsymbol{u}^{(i)}$). To maintain the SSP property with a useful coefficient ($C>0$), the stage order of explicit SSP-RK methods is typically only one. High overall order is achieved by arranging the first-order stages in such a way that their errors cancel out in the final combination. Forcing a higher stage order (e.g., stage order 2) within the SSP framework would necessitate negative coefficients, destroying the convex combination structure and driving the SSP coefficient to zero [@problem_id:3420330].

Furthermore, there are theoretical barriers on the maximum achievable order. It has been proven that for linear problems, an explicit SSP-RK method cannot have an order greater than four. This is a significant limitation on the development of arbitrarily high-order SSP schemes. [@problem_id:3420330]

#### What Property Is Preserved?

Finally, it is essential to remember that SSP is a framework, not a single, universal stability property. An SSP time-stepping method **preserves** whatever contractivity property is held by the forward Euler method for a given [spatial discretization](@entry_id:172158) $\mathcal{L}$ and a given convex functional $\Phi$. The SSP method does not create stability where there is none.

This has important practical implications for DG methods [@problem_id:3420344] [@problem_id:3420299]:
- If a DG scheme with a [slope limiter](@entry_id:136902) is proven to be **Total Variation Diminishing (TVD)** with forward Euler (i.e., $\Phi$ is the TV semi-norm), then using an SSP time integrator will yield a fully discrete scheme that is also TVD under the appropriate SSP time step restriction.
- Conversely, if a DG scheme with an [upwind flux](@entry_id:143931) is proven to be **energy-stable** with forward Euler in a discrete $M$-norm (i.e., $\Phi(\boldsymbol{u}) = \sqrt{\boldsymbol{u}^T M \boldsymbol{u}}$), then an SSP integrator will preserve this [energy stability](@entry_id:748991). Standard high-order DG methods are generally not TVD (by Godunov's theorem) but can be energy-stable for linear problems.

The choice of which property is preserved is dictated entirely by the properties of the underlying spatial operator $\mathcal{L}$, not by the SSP time-stepper itself. The role of the SSP method is to extend that specific property to higher-order accuracy in time without violating it.