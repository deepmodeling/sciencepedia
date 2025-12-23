## Introduction
The numerical solution of [hyperbolic conservation laws](@entry_id:147752) is a cornerstone of computational science, but it presents a formidable challenge: the [faithful representation](@entry_id:144577) of discontinuous solutions, or shocks. While high-order linear schemes excel in smooth regions, they often produce spurious, non-physical oscillations near these sharp gradients, corrupting the solution and violating physical principles. This raises a critical question: how can we design numerical methods that are both highly accurate and robustly non-oscillatory?

This article delves into the rigorous mathematical framework developed to address this very problem, focusing on the core concepts of [monotonicity](@entry_id:143760) and the Total Variation Diminishing (TVD) property. These principles provide a powerful lens through which to analyze and control the oscillatory behavior of numerical schemes. By understanding this framework, you will gain insight into the fundamental limitations of linear methods and the motivation behind the sophisticated nonlinear schemes that define the state of the art in shock capturing.

Across the following chapters, you will build a comprehensive understanding of this essential topic. We will begin in "Principles and Mechanisms" by defining [total variation](@entry_id:140383) as a measure of oscillation, introducing the TVD condition, and exploring its deep connection to scheme monotonicity and the accuracy limitations imposed by Godunov's theorem. Next, in "Applications and Interdisciplinary Connections," we will see how these theoretical ideas are put into practice to construct modern, high-order methods, including limited Discontinuous Galerkin schemes and Strong Stability Preserving (SSP) [time integrators](@entry_id:756005). Finally, "Hands-On Practices" will provide opportunities to solidify your knowledge through targeted analytical and computational exercises.

## Principles and Mechanisms

The [numerical approximation](@entry_id:161970) of [hyperbolic conservation laws](@entry_id:147752) presents a unique set of challenges, foremost among them the presence of discontinuous solutions, or shocks. While linear analysis, based on Fourier modes and Taylor series expansions, provides a powerful framework for assessing the accuracy and stability of schemes for smooth solutions, it falls short in predicting the behavior of these schemes near sharp gradients. A key failing of many otherwise accurate methods is the generation of spurious, non-physical oscillations in the vicinity of discontinuities. This chapter introduces the theoretical framework developed to analyze and control this oscillatory behavior, focusing on the core principles of monotonicity and total variation.

### The Challenge of Discontinuities: Spurious Oscillations

A desirable property of any numerical scheme is that it should not introduce new features into the solution that are not present in the underlying physics. For hyperbolic problems, this means that if the initial data is monotone (e.g., a simple step function), the numerical solution should remain monotone. Furthermore, the scheme should not create new local maxima or minima in the solution profile.

Consider a simple second-order accurate linear scheme, such as the Lax-Wendroff method. For the [linear advection equation](@entry_id:146245) $u_t + a u_x = 0$, the scheme can be derived from a Taylor [series expansion](@entry_id:142878) and is given by:
$$
u_{j}^{n+1} = u_{j}^{n} - \frac{\nu}{2}(u_{j+1}^{n} - u_{j-1}^{n}) + \frac{\nu^{2}}{2}(u_{j+1}^{n} - 2u_{j}^{n} + u_{j-1}^{n})
$$
where $\nu = a \Delta t / \Delta x$ is the Courant number. While this scheme is celebrated for its [second-order accuracy](@entry_id:137876) and its favorable stability properties in the $\ell^2$-norm for $\nu \le 1$, its performance on discontinuous data is poor. When applied to a sharp interface, such as a step function, the Lax-Wendroff scheme notoriously produces oscillations, often referred to as Gibbs-type phenomena, on both sides of the discontinuity . These oscillations are not merely numerical artifacts that decay with [grid refinement](@entry_id:750066); they are an inherent property of the scheme, and their presence can corrupt the solution globally and lead to violations of physical principles, such as positivity for density or concentration.

This behavior highlights a fundamental tension between the [order of accuracy](@entry_id:145189) of a *linear* scheme and its qualitative behavior near discontinuities. To systematically study and prevent such oscillations, we need a quantitative measure of the "oscillatoriness" of a discrete solution.

### Quantifying Oscillations: The Total Variation

A powerful and intuitive measure of the oscillatory content of a discrete function is its **total variation (TV)**. For a one-dimensional grid function $u^n = \{u_i^n\}_{i \in \mathbb{Z}}$ defined on a uniform mesh, the discrete [total variation](@entry_id:140383) is defined as the sum of the [absolute values](@entry_id:197463) of the jumps between adjacent grid points:
$$
TV(u^n) = \sum_{i} |u_{i+1}^n - u_i^n|
$$
This quantity provides a scalar measure of the "total movement" or "jumpiness" in the data. A smooth, non-oscillatory function will have a relatively small [total variation](@entry_id:140383), while a highly oscillatory function will have a large one.

This discrete definition is intimately connected to its continuous counterpart. If we construct a piecewise-constant function $\tilde{u}^n(x)$ from the cell-average data $u_i^n$, where $\tilde{u}^n(x) = u_i^n$ for $x$ in cell $i$, the continuous total variation of this reconstructed function is precisely the sum of the jump magnitudes at the cell interfaces. On an interior domain, this is identical to the discrete [total variation](@entry_id:140383) of the cell averages . If the domain is periodic, the definition is extended to include the "wrap-around" jump between the last and first cells:
$$
TV_{\text{periodic}}(u^n) = \left(\sum_{i=1}^{N-1} |u_{i+1}^n - u_i^n|\right) + |u_1^n - u_N^n|
$$
Furthermore, in the limit of [grid refinement](@entry_id:750066) ($\Delta x \to 0$), if the grid values $u_i^n$ are cell averages of a smooth function $u(x, t^n)$, the discrete [total variation](@entry_id:140383) converges to the total variation of the continuous function, which is given by the integral of the absolute value of its derivative:
$$
\lim_{\Delta x \to 0} TV(u^n) = \int |u_x(x, t^n)| \, dx
$$
This convergence establishes that the discrete [total variation](@entry_id:140383) is a consistent measure of the [spatial variability](@entry_id:755146) of the solution .

### The Total Variation Diminishing (TVD) Property

With [total variation](@entry_id:140383) as our metric for oscillation, we can now define a highly desirable property for a numerical scheme. A scheme is said to be **Total Variation Diminishing (TVD)** if the [total variation](@entry_id:140383) of the numerical solution is non-increasing in time:
$$
TV(u^{n+1}) \le TV(u^n)
$$
This simple inequality is a powerful statement. It guarantees that the numerical method, by its very construction, cannot generate new oscillations or amplify existing ones. If the initial data is non-oscillatory, a TVD scheme ensures the solution remains non-oscillatory for all time. For a semi-discrete finite volume scheme expressed as a system of [ordinary differential equations](@entry_id:147024), $\frac{d}{dt}u_i(t) = L(u)_i$, the TVD condition is expressed in continuous time as :
$$
\frac{d}{dt} TV(u(t)) \le 0
$$

Let us revisit the Lax-Wendroff scheme in this light. By applying it to a [unit step function](@entry_id:268807) ($u_j^0 = 1$ for $j \le 0$, $u_j^0 = 0$ for $j > 0$), one can explicitly calculate the [total variation](@entry_id:140383) after a single time step. The initial [total variation](@entry_id:140383) is $TV(u^0) = |0-1| = 1$. After one step, the solution profile is smeared, and small over- and under-shoots are created. A direct calculation reveals that the new [total variation](@entry_id:140383) is $TV(u^1) = 1 + \nu - \nu^2$. For any Courant number $\nu \in (0,1)$, the term $\nu(1-\nu)$ is strictly positive, meaning $TV(u^1) > TV(u^0)$ . This analytical result confirms that the Lax-Wendroff scheme is not TVD and formally explains its oscillatory nature.

It is crucial to distinguish the TVD property from standard $\ell^2$-stability. The Lax-Wendroff scheme is $\ell^2$-stable for $\nu \le 1$, meaning the energy of the solution does not grow. However, as we have seen, it is not TVD. This demonstrates that stability in the sense of bounded energy is not sufficient to prevent the formation of spurious oscillations . The TVD condition imposes a much stronger, nonlinear constraint on the behavior of the scheme.

### Monotonicity: A Pathway to TVD

A key question arises: how can we design schemes that are guaranteed to be TVD? A powerful sufficient condition is **[monotonicity](@entry_id:143760)**. A scheme is said to be **monotone** if its update formula expresses the new value $u_i^{n+1}$ as a [non-decreasing function](@entry_id:202520) of the values at the previous time step, $\{u_j^n\}$. For a linear scheme of the form $u_i^{n+1} = \sum_j c_j u_{i+j}^n$, [monotonicity](@entry_id:143760) is equivalent to the requirement that all coefficients $c_j$ are non-negative. A scheme with this property is also called **monotonicity-preserving**, as it guarantees that if the initial data $\{u_j^0\}$ is a [monotone sequence](@entry_id:191462), then $\{u_j^1\}$ will also be monotone. In the semi-discrete context, a scheme is monotonicity-preserving if it is **locally extremum diminishing (LED)**: local maxima do not increase in time, and local minima do not decrease .

A cornerstone result by Harten (1983) establishes the link:
**Theorem (Harten): A monotone scheme is TVD.**

This provides a clear design principle. For example, the [first-order upwind scheme](@entry_id:749417) for $u_t + a u_x = 0$ (with $a>0$) is $u_j^{n+1} = (1-\nu)u_j^n + \nu u_{j-1}^n$. If the CFL condition $0 \le \nu \le 1$ is satisfied, both coefficients $(1-\nu)$ and $\nu$ are non-negative. The scheme is thus a convex combination of previous values, which immediately shows it is monotone and therefore TVD .

However, this path to non-oscillatory behavior comes at a steep price. The celebrated **Godunov's Order Barrier Theorem** (1959) states that any linear monotone scheme cannot be more than first-order accurate . This fundamental theorem explains the dilemma we face: to achieve higher accuracy with a linear scheme (like Lax-Wendroff), we must sacrifice [monotonicity](@entry_id:143760) and accept oscillations. To eliminate oscillations with a linear scheme, we must accept the low accuracy and high numerical diffusion of a [first-order method](@entry_id:174104). This impasse is the primary motivation for the development of modern [high-resolution schemes](@entry_id:171070), which cleverly bypass Godunov's barrier by being *nonlinear*, even when applied to a linear PDE.

### Analyzing Numerical Fluxes for Monotonicity

For a general conservative finite volume scheme, $u_i^{n+1} = u_i^n - \lambda (F_{i+1/2} - F_{i-1/2})$, where the [numerical flux](@entry_id:145174) $F_{i+1/2}$ depends on a stencil of neighboring states (e.g., $F_{i+1/2} = F(u_i^n, u_{i+1}^n)$), the property of [monotonicity](@entry_id:143760) translates into specific requirements on the flux function $F$ and the time step $\Delta t$. A scheme based on a two-point flux $F(u_L, u_R)$ can be shown to be monotone if two conditions are met:

1.  **Monotone Flux Condition:** The [numerical flux](@entry_id:145174) $F(u_L, u_R)$ must be a [non-decreasing function](@entry_id:202520) of its left argument $u_L$ and a non-increasing function of its right argument $u_R$.
2.  **CFL Condition:** The time step must be sufficiently small, with the specific constraint depending on the [partial derivatives](@entry_id:146280) of the flux function. The TVD property is never independent of the CFL number .

Let us examine this with the **Rusanov (or local Lax-Friedrichs) flux**, a common building block for numerical schemes:
$$
F_{\mathrm{Rus}}(u_L, u_R) = \frac{1}{2}\left( f(u_L) + f(u_R) \right) - \frac{\alpha}{2}\left( u_R - u_L \right)
$$
Here, $\alpha$ is a [numerical dissipation](@entry_id:141318) parameter, which must be chosen appropriately. For the resulting scheme to be monotone, an analysis of the update formula shows that $\alpha$ must be at least as large as the maximum local [wave speed](@entry_id:186208), i.e., $\alpha \ge \sup|f'(u)|$ over the relevant range of $u$. This ensures the "monotone flux condition". Additionally, a CFL condition of the form $\lambda \alpha \le 1$ must be satisfied. If the dissipation parameter $\alpha$ is underestimated (e.g., chosen smaller than the true maximum wave speed), the scheme is no longer guaranteed to be monotone, and the TVD property can be lost, leading to the re-emergence of oscillations .

Not all flux functions satisfy the monotone flux condition. A prominent example is the **Roe flux**. For the inviscid Burgers equation ($f(u) = u^2/2$), the Roe flux can be analyzed at a state corresponding to a "[transonic rarefaction](@entry_id:756129)," for example, with $u_L = -2$ and $u_R = 1$. The [characteristic speed](@entry_id:173770) $f'(u) = u$ changes sign between these states. A direct calculation shows that at this point, the derivative $\partial F_{\mathrm{Roe}} / \partial u_R$ is positive, violating the condition for a monotone flux. This failure is the root cause of the Roe scheme's ability to admit non-physical "entropy-violating" solutions and necessitates the use of an "[entropy fix](@entry_id:749021)" .

### The Broader Context and Limitations of TVD

The TVD property is not merely a theoretical curiosity; it has profound implications for the convergence and reliability of numerical methods, but it is not a panacea.

**Convergence to the Entropy Solution**: The TVD property is a critical ingredient in proofs of convergence for numerical schemes. A TVD scheme, combined with an $L^\infty$ bound, ensures that the sequence of numerical solutions has uniformly bounded total variation. By Helly's Selection Theorem, this guarantees the existence of a subsequence that converges in $L^1_{loc}$. If the scheme is also consistent and conservative, the Lax-Wendroff theorem ensures this limit is a weak solution to the PDE. However, [weak solutions](@entry_id:161732) are not unique. To guarantee convergence to the single, physically relevant **entropy solution**, an additional condition is required: the scheme must satisfy a [discrete entropy inequality](@entry_id:748505). Monotone schemes (like Godunov's) are special because they can be shown to satisfy this condition automatically. A TVD scheme that is not monotone may converge to a [weak solution](@entry_id:146017) that is not the entropy solution (e.g., a "[rarefaction](@entry_id:201884) shock") .

**Challenges in Higher Dimensions**: The TVD concept, so powerful in one dimension, loses some of its strength in multiple spatial dimensions. A common approach for multi-dimensional problems is **[dimensional splitting](@entry_id:748441)**, where one applies a sequence of 1D operators. However, even if each 1D operator is TVD, their composition is not guaranteed to be TVD in two or more dimensions. A 1D sweep in the $x$-direction, while non-increasing the [total variation](@entry_id:140383) along $x$-grid lines, can create new variations in the orthogonal $y$-direction. The net effect can be an increase in the total 2D variation .

**Challenges for Systems of Equations**: The situation is even more complex for [systems of conservation laws](@entry_id:755768), such as the Euler equations of gas dynamics. A popular strategy is to project the equations into characteristic fields, advance each scalar characteristic variable with a 1D TVD scheme, and then project back to the physical variables. This component-wise TVD approach does *not* guarantee that the physical variables (like density or momentum) will be TVD. The nonlinear transformation from [characteristic variables](@entry_id:747282) back to physical variables can itself generate oscillations and increase total variation, even when the variation of each individual characteristic component does not .

Finally, it is worth noting that while monotonicity is a sufficient condition for a scheme to be TVD, the properties are not strictly equivalent. It is possible to construct contrived schemes that satisfy a local maximum principle (a form of [monotonicity](@entry_id:143760)) but are not TVD. Such examples underscore that the precise structure of the scheme's stencil is critical .

In summary, the TVD property provides a rigorous mathematical framework for designing non-oscillatory numerical methods. It formalizes the intuitive goal of preventing spurious wiggles near shocks. While first-order [monotone schemes](@entry_id:752159) are robustly TVD, Godunov's theorem shows they are limited in accuracy. This limitation has driven the field toward the development of nonlinear high-resolution TVD schemes, which are the subject of subsequent chapters.