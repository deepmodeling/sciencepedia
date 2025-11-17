## Introduction
When solving time-dependent [partial differential equations](@entry_id:143134) with high-order methods like the Discontinuous Galerkin (DG) or spectral methods, the resulting system of [ordinary differential equations](@entry_id:147024) can involve millions or even billions of unknowns. For [explicit time-stepping](@entry_id:168157) schemes, the memory required to store the intermediate data for each step can become a more significant bottleneck than the computational cost itself. Standard implementations of high-order Runge-Kutta methods, which require storing numerous stage derivatives simultaneously, often exceed the memory capacity of a single compute node, limiting the scale of solvable problems.

This article addresses this critical memory-performance gap by providing a comprehensive overview of **low-storage Runge-Kutta (LSRK) schemes**. These are not new methods but rather clever algebraic reformulations of existing ones, designed to perform the time-step update using a minimal, fixed number of memory registers. Throughout this article, you will learn how these schemes achieve significant memory savings without compromising the accuracy or stability of the underlying method.

The following chapters will guide you through the theory and practice of LSRK schemes. The first chapter, **"Principles and Mechanisms,"** delves into the algorithmic reformulations that reduce memory usage and establishes their mathematical equivalence to classical methods. The second chapter, **"Applications and Interdisciplinary Connections,"** explores the practical impact of LSRK in [large-scale scientific computing](@entry_id:155172), its synergy with DG methods, and its advantages on modern hardware like GPUs. Finally, **"Hands-On Practices"** presents a series of computational exercises to solidify your understanding of stability analysis, implementation, and [performance modeling](@entry_id:753340) for these essential numerical tools.

## Principles and Mechanisms

In the application of Discontinuous Galerkin (DG) and spectral methods to large-scale problems, the semi-discrete system of ordinary differential equations (ODEs), $\frac{d\boldsymbol{u}}{dt} = \mathcal{L}(\boldsymbol{u})$, often involves a vector of unknowns $\boldsymbol{u}$ with a very large number of degrees of freedom, $N$. When employing explicit Runge-Kutta (RK) [time integration schemes](@entry_id:165373), the management of memory becomes a critical performance bottleneck, often rivaling the computational cost itself. This chapter delves into the principles and mechanisms of **low-storage Runge-Kutta (LSRK) schemes**, a class of implementations designed specifically to alleviate this memory pressure without sacrificing accuracy.

### The Imperative for Low Storage: Memory as a Bottleneck

A standard, or "classical," implementation of an $s$-stage explicit Runge-Kutta method is derived directly from its Butcher tableau. The computation of the solution at time $t^{n+1}$ requires the evaluation of $s$ internal stage derivatives, $\boldsymbol{k}_i$:
$$
\boldsymbol{k}_i = \mathcal{L}\left(\boldsymbol{u}^n + \Delta t \sum_{j=1}^{i-1} a_{ij} \boldsymbol{k}_j\right), \quad i=1, \dots, s
$$
followed by a final update:
$$
\boldsymbol{u}^{n+1} = \boldsymbol{u}^n + \Delta t \sum_{i=1}^{s} b_i \boldsymbol{k}_i
$$
In a direct implementation, to compute the argument of $\mathcal{L}$ for stage $i$, one needs access to all preceding stage derivatives $\boldsymbol{k}_1, \dots, \boldsymbol{k}_{i-1}$. To perform the final update, one needs access to the initial state $\boldsymbol{u}^n$ and all $s$ stage derivatives. Consequently, a straightforward implementation must simultaneously store the initial [state vector](@entry_id:154607) $\boldsymbol{u}^n$ and all $s$ stage derivative vectors $\boldsymbol{k}_i$. This results in a total memory requirement for $s+1$ vectors, each of size $N$. The total memory footprint is therefore $(s+1)N$ scalar entries [@problem_id:3397092] [@problem_id:3397074].

For high-order DG methods in three dimensions, $N$ can easily be in the millions or billions, and high-order accurate RK schemes may require a significant number of stages (e.g., $s=5$ for a fourth-order method). The cost of storing $(s+1)N$ values can exceed the available memory on a compute node, forcing either a reduction in problem size or reliance on slower, out-of-core memory access.

Low-storage schemes address this challenge by reformulating the RK update process to use a fixed, minimal number of state-sized storage arrays, or **registers**, regardless of the number of stages. The most common and memory-efficient variant is the **two-register** or **$2N$-storage** scheme. By definition, this implementation requires only two vectors of size $N$ throughout the time step. The memory savings are substantial; the ratio of classical storage to two-register low-storage is $\frac{s+1}{2}$. For an $s=5$ stage method, a classical implementation requires three times the memory of its low-storage counterpart [@problem_id:3397092]. This efficiency is the primary motivation for the development and widespread adoption of LSRK methods in computational science.

### Canonical Low-Storage Formulations

LSRK schemes are not new numerical methods in the sense of having different order conditions or stability properties from their classical counterparts. Rather, they are an algebraic reorganization of existing explicit RK methods. Two canonical formulations are prevalent, distinguished by their storage count [@problem_id:3397067].

#### The Two-Register (2N) Formulation

The most memory-frugal variant operates on just two registers. One register holds the evolving solution vector, which we denote $\boldsymbol{u}$, and the second is an auxiliary work or [residual vector](@entry_id:165091), denoted $\boldsymbol{r}$. At each stage $i=1, \dots, s$, both registers are updated in place. A general recurrence for this family of schemes is:
$$
\boldsymbol{r} \leftarrow a_{i}\,\boldsymbol{r} + \Delta t\,\mathcal{L}(\boldsymbol{u})
$$
$$
\boldsymbol{u} \leftarrow \boldsymbol{u} + b_{i}\,\boldsymbol{r}
$$
Here, $a_i$ and $b_i$ are the low-storage coefficients, which are distinct from the Butcher tableau coefficients but are derived from them. A crucial feature of this formulation is that the initial state $\boldsymbol{u}^n$ is not preserved; it is immediately overwritten in the first stage update. The residual vector $\boldsymbol{r}$ accumulates a history of the stage derivatives, allowing the final update to be constructed without explicitly storing each one.

#### The Three-Register (3N) Formulation

A slightly less memory-efficient but more algebraically flexible variant uses three registers. These typically correspond to:
1.  The evolving stage solution, $\boldsymbol{u}$.
2.  A "frozen" copy of the solution at the beginning of the step, $\boldsymbol{u}^n$.
3.  A work vector, $\boldsymbol{w}$, to store the current stage derivative.

A general recurrence for this family takes the form:
$$
\boldsymbol{w} \leftarrow \mathcal{L}(\boldsymbol{u})
$$
$$
\boldsymbol{u} \leftarrow \alpha_{i}\,\boldsymbol{u} + \beta_{i}\,\boldsymbol{u}^{n} + \gamma_{i}\,\Delta t\,\boldsymbol{w}
$$
By preserving the initial state $\boldsymbol{u}^n$, this formulation can represent a broader class of explicit RK methods than the two-register form. The coefficients $\alpha_i, \beta_i, \gamma_i$ are chosen to match a target RK method. Both the two- and three-register formulations are fully explicit and are equally applicable to linear and nonlinear spatial operators $\mathcal{L}(\boldsymbol{u})$, as the operator is always evaluated using the most recently computed [state vector](@entry_id:154607) $\boldsymbol{u}$ [@problem_id:3397067].

### Mechanism and Equivalence: A Deeper Look at the 2N Scheme

To build confidence in these reformulations, it is instructive to demonstrate how a low-storage scheme is mathematically equivalent to a classical RK method. We will analyze the mechanism of a widely used family of 2N schemes, often associated with Carpenter and Kennedy, which have a slightly different but equivalent form to the one shown above [@problem_id:3397139] [@problem_id:3397150].

Let the two registers be the evolving solution $\boldsymbol{q}$ and an auxiliary accumulator $\boldsymbol{r}$. The process starts with $\boldsymbol{q}^{(0)} = \boldsymbol{q}^n$ and $\boldsymbol{r}^{(0)} = \boldsymbol{0}$. For each stage $i = 1, \dots, s$, the updates are:
$$
\boldsymbol{r}^{(i)} = \alpha_i \boldsymbol{r}^{(i-1)} + \Delta t \mathcal{L}(\boldsymbol{q}^{(i-1)})
$$
$$
\boldsymbol{q}^{(i)} = \boldsymbol{q}^{(i-1)} + \beta_i \boldsymbol{r}^{(i)}
$$
The final solution is $\boldsymbol{q}^{n+1} = \boldsymbol{q}^{(s)}$. Let's define the scaled stage derivative as $\boldsymbol{k}_i := \Delta t \mathcal{L}(\boldsymbol{q}^{(i-1)})$. The recurrence for the accumulator becomes $\boldsymbol{r}^{(i)} = \alpha_i \boldsymbol{r}^{(i-1)} + \boldsymbol{k}_i$. We can unroll this recurrence to see what $\boldsymbol{r}^{(i)}$ contains:
$$
\boldsymbol{r}^{(1)} = \alpha_1 \boldsymbol{r}^{(0)} + \boldsymbol{k}_1 = \boldsymbol{k}_1 \quad \text{(Note: } \alpha_1 \text{ is irrelevant)}
$$
$$
\boldsymbol{r}^{(2)} = \alpha_2 \boldsymbol{r}^{(1)} + \boldsymbol{k}_2 = \alpha_2 \boldsymbol{k}_1 + \boldsymbol{k}_2
$$
$$
\boldsymbol{r}^{(3)} = \alpha_3 \boldsymbol{r}^{(2)} + \boldsymbol{k}_3 = \alpha_3 (\alpha_2 \boldsymbol{k}_1 + \boldsymbol{k}_2) + \boldsymbol{k}_3 = \alpha_3 \alpha_2 \boldsymbol{k}_1 + \alpha_3 \boldsymbol{k}_2 + \boldsymbol{k}_3
$$
In general, the accumulator at stage $i$ is a linear combination of all preceding stage derivatives:
$$
\boldsymbol{r}^{(i)} = \sum_{j=1}^{i} \left( \prod_{l=j+1}^{i} \alpha_l \right) \boldsymbol{k}_j
$$
The total update to the solution is a [telescoping sum](@entry_id:262349):
$$
\boldsymbol{q}^{(s)} - \boldsymbol{q}^{(0)} = \sum_{i=1}^{s} (\boldsymbol{q}^{(i)} - \boldsymbol{q}^{(i-1)}) = \sum_{i=1}^{s} \beta_i \boldsymbol{r}^{(i)}
$$
Substituting the expression for $\boldsymbol{r}^{(i)}$ and collecting terms for each $\boldsymbol{k}_j$ demonstrates that the final update is a [linear combination](@entry_id:155091) of all $\boldsymbol{k}_j$, exactly like a classical RK method. For instance, for a 4-stage scheme ($s=4$), the total contribution from the first stage derivative $\boldsymbol{k}_1$ to the final update $\boldsymbol{q}^{(4)} - \boldsymbol{q}^{(0)}$ has a coefficient of $(\beta_1 + \alpha_2 \beta_2 + \alpha_2 \alpha_3 \beta_3 + \alpha_2 \alpha_3 \alpha_4 \beta_4)$ [@problem_id:3397150]. This confirms that by choosing the LSRK coefficients $\{\alpha_i, \beta_i\}$ appropriately, one can match any set of Butcher tableau coefficients $\{a_{ij}, b_i\}$, thereby achieving the same order of accuracy and stability properties.

To solidify the connection between the coefficients and accuracy, consider a hypothetical two-stage, two-register scheme [@problem_id:3397135]. Let the updates be:
$$
\boldsymbol{w}_{1} = \boldsymbol{L}\boldsymbol{y}^{n}, \quad \boldsymbol{y}_{1} = \boldsymbol{y}^{n} + b_{1}h\boldsymbol{w}_{1}
$$
$$
\boldsymbol{w}_{2} = a_{2}\boldsymbol{w}_{1} + \boldsymbol{L}\boldsymbol{y}_{1}, \quad \boldsymbol{y}^{n+1} = \boldsymbol{y}_{1} + b_{2}h\boldsymbol{w}_{2}
$$
Applying this to the scalar test equation $y' = \lambda y$ with $z = h\lambda$, we find the stability polynomial $R(z)$ relating $y^{n+1}$ to $y^n$ is $y^{n+1} = R(z)y^n$. After substitution, we get:
$$
R(z) = 1 + (b_1 + b_2 + a_2 b_2)z + (b_1 b_2)z^2
$$
For this scheme to be second-order accurate, its stability polynomial must match the Taylor series of $\exp(z)$ up to the $z^2$ term: $\exp(z) = 1 + z + \frac{1}{2}z^2 + \mathcal{O}(z^3)$. Comparing coefficients yields the order conditions:
1.  Coefficient of $z^1$: $b_1 + b_2 + a_2 b_2 = 1$
2.  Coefficient of $z^2$: $b_1 b_2 = \frac{1}{2}$

Any set of real coefficients $(a_2, b_1, b_2)$ satisfying these two equations produces a second-order accurate scheme. For instance, the choice $(a_2, b_1, b_2) = (-\frac{1}{2}, \frac{1}{2}, 1)$ satisfies the conditions. Importantly, regardless of the specific choice of coefficients that satisfy these equations, the resulting stability polynomial is uniquely determined to be $R(z) = 1 + z + \frac{1}{2}z^2$ [@problem_id:3397135]. This demonstrates that the properties of order and linear stability are fundamental to the underlying RK method, not the specific low-storage parameterization.

### Advanced Topics and Applications

The low-storage framework is not merely a memory-saving trick; its structured, stage-wise nature facilitates analysis and integration with other numerical components essential for solving challenging problems.

#### Strong Stability Preserving (SSP) Schemes

When solving [hyperbolic conservation laws](@entry_id:147752) with DG or other high-order methods, [spurious oscillations](@entry_id:152404) can arise near discontinuities. **Strong Stability Preserving (SSP)** [time-stepping methods](@entry_id:167527), also known as [total variation diminishing](@entry_id:140255) (TVD) RK methods, are designed to control these oscillations by ensuring that the time-stepping scheme does not increase the total variation (or some other convex functional) of the solution.

The theoretical foundation for SSP methods is the Shu-Osher representation, which expresses an RK method as a convex combination of forward Euler steps [@problem_id:3397081]. An $s$-stage method is SSP if each stage $\boldsymbol{u}^{(i)}$ can be written as:
$$
\boldsymbol{u}^{(i)} = \sum_{k=0}^{i-1} \left[ \alpha_{ik} \boldsymbol{u}^{(k)} + \beta_{ik} \left( \boldsymbol{u}^{(k)} + \frac{\Delta t}{C} \mathcal{L}(\boldsymbol{u}^{(k)}) \right) \right]
$$
where all coefficients $\alpha_{ik}, \beta_{ik}$ are non-negative and $\sum_{k=0}^{i-1} (\alpha_{ik} + \beta_{ik}) = 1$. If the simple forward Euler method is TVD under a time step restriction $\Delta t \le \Delta t_{\mathrm{FE}}$, then the SSP-RK method is guaranteed to be TVD for $\Delta t \le C \cdot \Delta t_{\mathrm{FE}}$. The value $C$ is the **SSP coefficient** of the RK method.

Many optimal SSP-RK methods have efficient low-storage implementations. A full stability analysis for such a scheme combines the properties of the RK method with the spectral properties of the spatial operator $\mathcal{L}$. As a concrete example, consider a popular three-stage, third-order SSP-LSRK scheme whose [stability function](@entry_id:178107) is $R(z) = 1 + z + \frac{1}{2}z^2 + \frac{1}{6}z^3$ [@problem_id:3397116]. To find the stability limit for a purely [dissipative operator](@entry_id:262598), we find the largest real value $r_s > 0$ such that $|R(-r_s)| \le 1$. This occurs when $R(-r_s) = -1$, which for this scheme gives $r_s \approx 2.51$.

For a DG discretization of the advection equation, the eigenvalues $\lambda$ of the operator $\mathcal{L}$ lie in the left-half of the complex plane, and their magnitudes are bounded by a [spectral radius](@entry_id:138984) $\rho$. A typical bound is $\rho \approx (2p+1) a/h$, where $p$ is the polynomial degree, $a$ is the advection speed, and $h$ is the element size. The [numerical stability condition](@entry_id:142239) requires that for all eigenvalues $\lambda$, the value $z=\lambda \Delta t$ must lie within the stability region of the RK method. A conservative condition is to require that the scaled spectral radius does not exceed the stability boundary along the negative real axis:
$$
\rho \Delta t \le r_s \implies \Delta t \le \frac{r_s}{\rho}
$$
This procedure allows for a precise calculation of the maximum stable time step, a critical step in any practical DG simulation [@problem_id:3397116].

#### Implicit-Explicit (IMEX) Schemes

Many physical systems involve both fast (stiff) and slow (non-stiff) processes. A common example is an [advection-diffusion](@entry_id:151021) or advection-reaction equation, where advection is non-stiff and diffusion or reaction is stiff. **Implicit-Explicit (IMEX) schemes** are designed for such problems, treating the non-stiff part $F(u)$ explicitly and the stiff part $G(u)$ implicitly:
$$
\frac{d\boldsymbol{u}}{dt} = F(\boldsymbol{u}) + G(\boldsymbol{u})
$$
The low-storage framework can be extended to IMEX methods. The explicit part $F(u)$ can be handled by a 2N-LSRK formulation, while the implicit part $G(u)$ is handled by a method suitable for [stiff systems](@entry_id:146021), such as a Singly Diagonally Implicit RK (SDIRK) method. The general stage update for such a scheme involves an explicit accumulation for $F$ and an implicit solve for $G$ [@problem_id:3397070].

The simplest one-stage IMEX method combines forward Euler for $F$ and backward Euler for $G$:
$$
\boldsymbol{u}^{n+1} = \boldsymbol{u}^n + \Delta t F(\boldsymbol{u}^n) + \Delta t G(\boldsymbol{u}^{n+1})
$$
Applying this to the scalar test equation $u' = \lambda_f u + \lambda_g u$, where $\lambda_f$ is treated explicitly and $\lambda_g$ implicitly, yields the [amplification factor](@entry_id:144315):
$$
R(z_f, z_g) = \frac{1 + z_f}{1 - z_g}
$$
where $z_f = \Delta t \lambda_f$ and $z_g = \Delta t \lambda_g$. The stability region of this method combines the stability requirement of forward Euler for $z_f$ (a disk in the left-half plane) with the [unconditional stability](@entry_id:145631) of backward Euler for $z_g$ (the entire exterior of a disk in the right-half plane). This illustrates the power of IMEX methods in handling stiffness without the prohibitive cost of a fully implicit scheme. More complex, higher-order IMEX-LSRK schemes are constructed on this same principle [@problem_id:3397070].

#### Positivity-Preserving Schemes

In problems where the solution represents a physical quantity like density or concentration, it is crucial that the numerical scheme preserves its non-negativity. For DG methods, this is often achieved by applying a **[positivity-preserving limiter](@entry_id:753609)** at each stage of the [time integration](@entry_id:170891). The structure of LSRK schemes is well-suited for analyzing and implementing such procedures. By ensuring that each stage update can be written as a convex combination of non-negative states, one can derive [sufficient conditions](@entry_id:269617) on the LSRK coefficients and the time step $\Delta t$ to guarantee that if $\boldsymbol{u}^n \ge 0$, then $\boldsymbol{u}^{n+1} \ge 0$. This analysis again highlights the utility of the stage-wise decomposition of LSRK schemes for proving complex, nonlinear stability properties [@problem_id:3397058].