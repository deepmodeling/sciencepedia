## Introduction
In computational fluid dynamics (CFD), accurately discretizing the convection term of transport equations is a central challenge, requiring a careful balance between numerical accuracy and stability. Low-order schemes like first-order upwind are stable but introduce excessive numerical diffusion, smearing sharp physical gradients. Conversely, standard [higher-order schemes](@entry_id:150564) like central differencing can be accurate in smooth regions but produce non-physical oscillations. This gap necessitates advanced methods that combine high accuracy with robustness. The Quadratic Upstream Interpolation for Convective Kinematics (QUICK) scheme emerges as a key development in this pursuit, offering a path to [second-order accuracy](@entry_id:137876) while respecting the direction of information flow. This article provides a comprehensive exploration of this pivotal scheme.

Across the following chapters, you will gain a deep understanding of the QUICK scheme. The "Principles and Mechanisms" chapter will deconstruct its quadratic formulation, analyze its accuracy and stability properties, and discuss its impact on the algebraic system. Following this, the "Applications and Interdisciplinary Connections" chapter will demonstrate its use in practical thermo-fluid problems, benchmark its performance, and explore its relevance in fields beyond traditional CFD. Finally, the "Hands-On Practices" section will provide opportunities to apply these concepts by deriving the scheme's core components for various scenarios.

## Principles and Mechanisms

In the numerical discretization of transport equations, the approximation of the convection term presents a fundamental challenge. The choice of scheme must navigate the delicate balance between accuracy, which demands higher-order approximations, and stability, which requires respecting the physical directionality of information flow. While the first-order upwind scheme guarantees [boundedness](@entry_id:746948) at the cost of excessive numerical diffusion, and the [second-order central difference](@entry_id:170774) scheme offers higher accuracy at the risk of non-physical oscillations, there is a clear need for methods that combine the virtues of both. The **Quadratic Upstream Interpolation for Convective Kinematics (QUICK)** scheme, introduced by Leonard (1979), represents a significant step in this direction. This chapter elucidates the principles and mechanisms of the QUICK scheme, from its construction and accuracy analysis to its inherent stability limitations and the implications for modern computational practice.

### The Foundation of QUICK: Upstream-Biased Quadratic Interpolation

At its core, the QUICK scheme is a higher-order method for estimating the value of a transported scalar, $\phi$, at the face of a control volume. Unlike the first-order upwind scheme which assumes a constant value (zeroth-order polynomial) extrapolated from the upstream cell, or the central difference scheme which assumes a linear profile (first-order polynomial) between bracketing cells, QUICK is based on a **quadratic (parabolic) profile**.

To achieve both higher accuracy and stability in [convection-dominated flows](@entry_id:169432), this quadratic interpolation is not centered on the face but is instead biased towards the **upstream** direction. For a uniform grid, the principle is as follows: to determine the value $\phi_f$ at a face $f$, a unique quadratic polynomial is fitted through the cell-center values of **two adjacent upstream nodes** and **one adjacent downstream node**.  This upwind bias is crucial as it respects the hyperbolic nature of convection, where information propagates predominantly along the direction of flow. 

Let us formalize this for a one-dimensional uniform grid with spacing $\Delta x$. Consider the east face, denoted by $e$, located at $x_e = x_P + \Delta x/2$ between cell centers $P$ (at $x_P$) and $E$ (at $x_E = x_P + \Delta x$). Let the cell center immediately to the west of $P$ be $W$ (at $x_W = x_P - \Delta x$).

**Case 1: Positive Velocity ($u > 0$)**

When the flow is from west to east ($u>0$), the upstream direction relative to face $e$ is towards $P$ and $W$. The QUICK stencil therefore uses the nodes $\{W, P, E\}$. The task is to find the value of the quadratic polynomial passing through $(\phi_W, \phi_P, \phi_E)$ at the location $x_e$.  This can be derived systematically using Lagrange interpolation or by solving for the polynomial coefficients.  The resulting expression for the face value $\phi_e$ is:

$$
\phi_e = \frac{6}{8}\phi_P + \frac{3}{8}\phi_E - \frac{1}{8}\phi_W
$$

This formula reveals the scheme's nature. The value is primarily an interpolation between the bracketing nodes $\phi_P$ and $\phi_E$, but with a crucial curvature correction term involving the far-upstream node $\phi_W$.

**Case 2: Negative Velocity ($u < 0$)**

If the flow reverses direction ($u0$), the upstream direction relative to face $e$ is now towards $E$. The two adjacent upstream nodes are $E$ and $EE$ (at $x_{EE} = x_P + 2\Delta x$), and the one downstream node is $P$. The stencil becomes $\{P, E, EE\}$. By symmetry, the derivation is analogous.   The face value $\phi_e$ is given by:

$$
\phi_e = \frac{6}{8}\phi_E + \frac{3}{8}\phi_P - \frac{1}{8}\phi_{EE}
$$

In both cases, the selection of the three-point stencil is dynamically adapted to the local flow direction, a hallmark of upwind-biased schemes.

### Accuracy Analysis: The Modified Equation

To understand the nature of the errors introduced by a numerical scheme, we employ **[modified equation analysis](@entry_id:752092)**. This technique uses Taylor series expansions to determine the partial differential equation that the discrete scheme effectively solves, including its leading-order truncation error terms. 

The leading truncation error profoundly influences the qualitative behavior of the numerical solution.
-   **Numerical Diffusion:** An even-order derivative in the error term (e.g., $\propto \frac{d^2\phi}{dx^2}$) acts like physical diffusion. A positive coefficient damps gradients, leading to the "smearing" or "blurring" of sharp fronts.
-   **Numerical Dispersion:** An odd-order derivative in the error term (e.g., $\propto \frac{d^3\phi}{dx^3}$) causes different Fourier components of the solution to propagate at incorrect phase speeds. This leads to non-physical oscillations or "wiggles," particularly near sharp gradients. 

For the **first-order upwind (FOU)** scheme, the modified equation reveals a leading error term of $+\frac{\rho u \Delta x}{2} \frac{d^2\phi}{dx^2}$. This is a significant numerical diffusion term, explaining the scheme's highly dissipative nature and its [first-order accuracy](@entry_id:749410). 

In contrast, when the full QUICK discretization of the convection term is analyzed, the second-derivative error term vanishes. The leading-order truncation error is found to be proportional to the third derivative:

$$
\text{Error}_{\text{QUICK}} \propto \rho u (\Delta x)^2 \frac{d^3\phi}{dx^3}
$$

This reveals two [critical properties](@entry_id:260687) of the QUICK scheme:
1.  It is formally **second-order accurate**, as the error is proportional to $(\Delta x)^2$.
2.  Its leading error is **dispersive**, not diffusive. By eliminating the dominant numerical diffusion of the FOU scheme, QUICK can resolve sharp gradients more accurately. However, this comes at the cost of introducing dispersive oscillations where the first-order scheme would produce smooth (though smeared) results. 

On a uniform grid, the interpolation for the face value itself is **third-order accurate**. The reduction to [second-order accuracy](@entry_id:137876) for the overall scheme occurs due to [error cancellation](@entry_id:749073) between adjacent faces when discretizing the full derivative term. 

### The Stability Dilemma: Overshoots and Monotonicity

While QUICK's higher accuracy is appealing, its stability properties are more complex. A robust scheme for a convection problem should be **monotone**, meaning it should not create new local maxima or minima in the solution. This property is closely related to the scheme being **Total Variation Diminishing (TVD)**.

The root of QUICK's stability issues lies in its interpolation formula. Notice the negative coefficient in the expression for $\phi_e$:

$$
\phi_e = \frac{6}{8}\phi_P + \frac{3}{8}\phi_E - \frac{1}{8}\phi_W
$$

Because of this negative weight, the face value $\phi_e$ is not a convex combination of the nodal values. Consequently, there is no guarantee that $\phi_e$ will remain bounded by the [local extrema](@entry_id:144991) of its neighboring cell values. This can lead to non-physical **overshoots** (where the interpolated value exceeds the [local maximum](@entry_id:137813)) and **undershoots** (where it drops below the local minimum). 

We can derive the precise condition for this non-monotonic behavior. Consider a monotonically increasing profile such that $\phi_W \le \phi_P \le \phi_E$. Let the local gradients be $\delta_1 = \phi_P - \phi_W \ge 0$ and $\delta_2 = \phi_E - \phi_P \ge 0$. An overshoot occurs ($\phi_e  \phi_E$) if the upstream gradient is significantly larger than the downstream gradient. A straightforward derivation shows that an overshoot is produced whenever:

$$
\frac{\delta_1}{\delta_2}  5
$$

This violation of monotonicity demonstrates that the unmodified QUICK scheme is not TVD and can produce oscillatory solutions, especially near sharp changes in gradient. 

### Implications for Numerical Solvers: The M-Matrix Property

The non-monotonic behavior of the QUICK scheme has profound consequences for the convergence and robustness of the [iterative linear solvers](@entry_id:1126792) used in most CFD codes. A desirable property for the matrix of a discretized convection-diffusion system is that it be an **M-matrix**. A [sufficient condition](@entry_id:276242) for a matrix to be an M-matrix is that it has positive diagonal entries, non-positive off-diagonal entries, and is [diagonally dominant](@entry_id:748380). M-matrices guarantee physically realistic solutions (satisfying a [discrete maximum principle](@entry_id:748510)) and are amenable to robust solution by a wide range of iterative methods, including classical [relaxation methods](@entry_id:139174) and advanced techniques like Algebraic Multigrid (AMG).

When we assemble the full discrete equation for the convection-diffusion problem using QUICK for the convective fluxes, the resulting algebraic system loses the M-matrix property, particularly at high cell **Peclet numbers** ($Pe = \rho u \Delta x / \Gamma$).  The negative interpolation weight on the far-upstream node translates into a **positive off-diagonal entry** in the [system matrix](@entry_id:172230) when convection dominates diffusion (specifically, for $Pe  8/7$ in the 1D case).

The loss of the M-matrix property and diagonal dominance leads to several practical problems:
-   The system matrix is no longer guaranteed to be [positive definite](@entry_id:149459), and its conditioning can degrade.
-   Classical [iterative solvers](@entry_id:136910) like Gauss-Seidel may fail to converge.
-   The performance of robust solvers like ILU-preconditioned Krylov methods and, most notably, AMG can be severely degraded. AMG, which relies on the M-matrix structure to build its hierarchy of coarse grids, may converge slowly or fail entirely. 

This analysis highlights that the choice of a discretization scheme is not merely an issue of local accuracy but has global implications for the solvability and efficiency of the entire numerical procedure.

### The Path Forward: Bounded High-Resolution Schemes

The unmodified QUICK scheme, while offering a significant reduction in numerical diffusion compared to first-order [upwinding](@entry_id:756372), suffers from dispersive errors that lead to non-physical oscillations and a poorly-conditioned algebraic system. The modern solution to this dilemma is to create adaptive, non-linear schemes.

This is achieved through the use of **flux limiters**. The core idea is to construct a scheme that behaves like QUICK in smooth regions of the flow to capitalize on its high accuracy, but adaptively blends towards a more robust, monotone scheme (like first-order upwind) near steep gradients to suppress oscillations. This ensures the solution remains bounded (TVD) while minimizing numerical diffusion where possible.  Furthermore, solution strategies like **[deferred correction](@entry_id:748274)**, which move the "problematic" higher-order terms to the right-hand side of the linear system, can be used to recover an M-matrix for the implicit solver, dramatically improving robustness.  These advanced techniques, which build upon the lessons learned from schemes like QUICK, form the foundation of modern high-resolution methods for computational thermal and fluid dynamics.