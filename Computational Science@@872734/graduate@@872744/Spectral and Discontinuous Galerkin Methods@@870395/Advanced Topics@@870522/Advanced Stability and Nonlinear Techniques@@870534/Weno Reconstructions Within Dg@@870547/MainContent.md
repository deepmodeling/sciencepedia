## Introduction
High-order Discontinuous Galerkin (DG) methods are renowned for their efficiency and accuracy when simulating problems with smooth solutions. However, their application to [hyperbolic conservation laws](@entry_id:147752), which govern phenomena like [shock waves](@entry_id:142404) in fluid dynamics, presents a significant challenge: the emergence of spurious, non-physical oscillations near discontinuities. This issue undermines the solution's physical fidelity and can lead to numerical instability. To overcome this limitation, a sophisticated stabilization technique is required—one that can selectively suppress oscillations without sacrificing the [high-order accuracy](@entry_id:163460) that makes DG methods so attractive.

This is precisely the role of Weighted Essentially Non-Oscillatory (WENO) reconstructions within the DG framework. The DG-WENO approach acts as an intelligent [limiter](@entry_id:751283), identifying problematic regions of the solution and locally rebuilding the polynomial representation to be non-oscillatory while strictly preserving fundamental physical principles like conservation. This article provides a graduate-level exploration of this powerful numerical methodology.

Throughout the following sections, you will gain a comprehensive understanding of the DG-WENO method. **Principles and Mechanisms** will dissect the core theory, from the four foundational principles—conservation, accuracy, non-oscillation, and compactness—to the detailed mechanics of troubled-cell indication and the step-by-step WENO reconstruction process. **Applications and Interdisciplinary Connections** will showcase the method's versatility, demonstrating its use in complex gas dynamics, its extension to unstructured meshes using concepts from [differential geometry](@entry_id:145818), and its role in multi-[physics simulations](@entry_id:144318) and advanced mathematical systems. Finally, **Hands-On Practices** will provide opportunities to engage with the material through challenging exercises focused on analysis, implementation, and advanced applications like [adjoint-based sensitivity analysis](@entry_id:746292).

## Principles and Mechanisms

The Discontinuous Galerkin (DG) method, while offering excellent accuracy for smooth solutions, is known to produce spurious, Gibbs-type oscillations near discontinuities when using high-order polynomial approximations. To render the method suitable for problems with shocks or sharp gradients, such as those governed by [hyperbolic conservation laws](@entry_id:147752), a nonlinear stabilization mechanism is required. This mechanism must be able to suppress oscillations without compromising the [high-order accuracy](@entry_id:163460) of the DG scheme in regions where the solution is smooth. This is typically achieved by applying a **[limiter](@entry_id:751283)** only in cells where it is needed.

The Weighted Essentially Non-Oscillatory (WENO) reconstruction provides a sophisticated and widely used framework for such a limiting procedure within DG methods. Instead of using a simple slope-[limiter](@entry_id:751283) that reduces the polynomial degree, the DG-WENO approach aims to replace the oscillatory polynomial in a "troubled" cell with a new, non-oscillatory polynomial of the same degree, constructed from information in neighboring cells. This chapter elucidates the core principles and key mechanisms that govern this process.

### The DG-WENO Limiting Strategy: Core Principles

The DG-WENO procedure is an *a posteriori* [limiter](@entry_id:751283), meaning it is applied after a provisional DG solution update, and only within elements, or "cells," that are identified as being "troubled" by the presence of a potential discontinuity. Within each troubled cell, the existing DG polynomial is discarded and replaced by a new one constructed via the WENO methodology. A robust DG-WENO limiting scheme is built upon a foundation of several key design principles [@problem_id:3429530].

1.  **Local Conservation**: The conservation law $u_t + \nabla \cdot \mathbf{f}(u) = 0$ dictates that the rate of change of the total amount of a quantity $u$ in a volume is equal to the flux of that quantity across the boundary. A numerical scheme must respect this principle at the discrete level. For a DG-WENO limiter, this means that the cell average of the solution must be strictly preserved during the replacement step. If $u_h$ is the original DG polynomial on a cell $I_j$ and $\tilde{u}_h^{\mathrm{WENO}}$ is the new, limited polynomial, this principle requires:
    $$
    \frac{1}{|I_j|} \int_{I_j} \tilde{u}_h^{\mathrm{WENO}}(x) \, dx = \frac{1}{|I_j|} \int_{I_j} u_h(x) \, dx
    $$
    This ensures that the limiter redistributes the solution *within* the cell without artificially adding or removing mass, which is crucial for computing correct shock speeds and maintaining physical fidelity.

2.  **High-Order Accuracy**: The primary motivation for using a high-order DG method is to achieve rapid convergence for smooth problems. A limiter should not destroy this property. The WENO reconstruction is designed such that in regions where the exact solution is smooth, the nonlinear limiting process gracefully reverts to an underlying high-order linear scheme. This ensures that the overall DG-WENO method retains the formal $(k+1)$-th order of accuracy of the parent DG scheme with degree-$k$ polynomials.

3.  **Essentially Non-Oscillatory (ENO) Property**: Near a true discontinuity, the goal is to avoid oscillations. The WENO reconstruction achieves this by constructing several candidate polynomials from different overlapping stencils of cells. It then forms the final polynomial as a nonlinear convex combination of these candidates. The "non-oscillatory" magic lies in the weights of this combination: they are designed to be close to zero for candidates that are oscillatory (i.e., those built on stencils that cross the discontinuity) and large for candidates that are smooth. The scheme thus adaptively and automatically favors the smoothest possible reconstruction.

4.  **Compactness and Locality**: For efficiency and to respect the [finite propagation speed](@entry_id:163808) of information inherent in hyperbolic problems, the reconstruction process must be local. The stencils used to build candidate polynomials for a cell $I_j$ should only involve $I_j$ and a small, bounded number of its immediate neighbors. The size of this neighborhood, or stencil radius, is independent of the mesh size $\Delta x$.

Any valid DG-WENO implementation must adhere to these four principles. Methods that violate them, for instance by only enforcing conservation globally, by using non-convex combinations that can create new [extrema](@entry_id:271659), or by relying on global information, are generally not considered robust or correct [@problem_id:3429530].

### Mechanism 1: Troubled-Cell Indicators

The WENO reconstruction procedure is computationally more expensive than a standard DG update. Applying it uniformly across the entire domain would be wasteful, as it is only needed in a small fraction of cells near discontinuities. Therefore, the first step in a DG-WENO scheme is to identify the troubled cells using a **shock sensor** or **[troubled-cell indicator](@entry_id:756187)**. A robust indicator should reliably flag cells containing discontinuities while leaving cells in smooth regions untouched, especially as the mesh is refined ($h \to 0$).

A powerful class of indicators for DG methods is based on the distribution of energy across the polynomial modes. For a DG solution $u_h$ on a cell $K$ represented in an orthonormal [modal basis](@entry_id:752055) $\{\varphi_{m,K}\}_{m=0}^k$, the solution is $u_h(x) = \sum_{m=0}^k a_{m,K} \varphi_{m,K}(x)$. For a smooth solution, approximation theory tells us that the [modal coefficients](@entry_id:752057) $a_{m,K}$ decay rapidly with the mode number $m$. Specifically, the energy in each mode, $E_m(K) = \int_K (a_{m,K} \varphi_{m,K}(x))^2 dx$, scales with the mesh size $h$ as $E_m(K) \sim \mathcal{O}(h^{2m+1})$. The total energy, $E(K) = \sum_m E_m(K)$, is dominated by the lowest mode, $E(K) \sim \mathcal{O}(h)$. In contrast, when a cell contains a discontinuity, Gibbs phenomenon pollutes all modes, and the energy is distributed more evenly, with $E_m(K) \sim \mathcal{O}(h)$ for all $m$ [@problem_id:3429533].

This difference in scaling behavior is the basis for a robust indicator. We seek an indicator that is **asymptotically amplitude-[scale-invariant](@entry_id:178566)**, meaning its value should not depend on whether we are solving for $u$ or $1000u$, and it should reliably distinguish smooth from non-smooth solutions. An excellent candidate that satisfies these criteria is the ratio of the energy in the highest mode(s) to the total energy in the cell. For example, consider the indicator:
$$
S_K := \frac{E_k(K)}{E(K)}
$$
Let's analyze its [asymptotic behavior](@entry_id:160836) [@problem_id:3429533]:

-   In a **smooth region**, $S_K \sim \frac{\mathcal{O}(h^{2k+1})}{\mathcal{O}(h)} = \mathcal{O}(h^{2k})$.
-   Near a **discontinuity**, $S_K \sim \frac{\mathcal{O}(h)}{\mathcal{O}(h)} = \mathcal{O}(1)$.

We can then flag a cell as troubled if $S_K > C h^{k}$ for some user-defined constant $C$. For a smooth cell, as $h \to 0$, $S_K$ will eventually fall below the threshold, so the cell will not be flagged. For a discontinuous cell, $S_K$ remains $\mathcal{O}(1)$ and will always be flagged. Furthermore, since $S_K$ is a ratio of energies, it is invariant to the amplitude of the solution. Other indicators, such as those based on unnormalized energy or interface jumps, often lack this crucial [scale-invariance](@entry_id:160225) property and are less robust [@problem_id:3429533].

### Mechanism 2: The WENO Reconstruction Process

Once a cell $I_j$ is flagged as troubled, the core WENO reconstruction procedure is initiated. It consists of four main steps: constructing candidate polynomials, measuring their smoothness, computing nonlinear weights, and forming the final reconstruction.

#### Step A: Constructing Candidate Polynomials

The WENO reconstruction is a convex combination of several candidate polynomials, $\tilde{u}_h^{\mathrm{WENO}} = \sum_r \omega_r p_r$. In the context of DG, a common and effective way to construct these candidates for a troubled cell $I_j$ is to utilize the existing DG polynomials from a stencil of neighboring cells, for example $\{I_{j-1}, I_j, I_{j+1}\}$.

This involves two key operations [@problem_id:3429541]:

1.  **Mapping**: The polynomials from the neighboring cells, say $u_{j-1}$ and $u_{j+1}$, are originally defined in their own local [coordinate systems](@entry_id:149266). They must first be mapped into the [local coordinate system](@entry_id:751394) of the target cell $I_j$. For a uniform grid, this corresponds to a simple shift. For example, if $u_{j-1}(\eta)$ is defined for $\eta \in [-1,1]$ on cell $I_{j-1}$, its representation on cell $I_j$ (with local coordinate $\xi \in [-1,1]$) would be $q_L(\xi) = u_{j-1}(\xi+2)$.

2.  **Enforcing Conservation**: The mapped polynomials $q_L(\xi)$ and $q_R(\xi)$ do not, in general, have the same cell average as the original polynomial $u_j(\xi)$ on cell $I_j$. To satisfy the crucial principle of [local conservation](@entry_id:751393), each candidate polynomial $p_r$ must be constrained to have the same cell average as the original solution on $I_j$. This is typically achieved by adding a constant shift. For instance, the left-biased candidate $p_0$ is constructed from the mapped polynomial $q_L$ as:
    $$
    p_0(\xi) = q_L(\xi) + C_0, \quad \text{where} \quad C_0 = \bar{u}_j - \bar{q}_L
    $$
    Here, $\bar{u}_j$ is the cell average of the original polynomial $u_j$ and $\bar{q}_L$ is the cell average of the mapped polynomial $q_L$. A similar procedure is used for the right-biased candidate, while the central candidate is often simply the original polynomial, $p_1(\xi) = u_j(\xi)$, which already satisfies the conservation constraint.

This procedure yields a set of candidate polynomials $\{p_r\}$ that are all of degree $k$ and all share the same cell average on $I_j$. Consequently, any convex combination of them will automatically preserve the cell average, robustly satisfying the conservation principle [@problem_id:3429530].

#### Step B: Measuring Smoothness with Indicators

The next step is to quantify the "smoothness" or "oscillatoriness" of each candidate polynomial $p_r$. This is done using **smoothness indicators**, denoted by $\beta_r$. A larger $\beta_r$ value signifies a less smooth polynomial. The most common choice is the Jiang-Shu smoothness indicator, which is a weighted sum of the squared $L^2$-norms of the derivatives of the polynomial over the cell. For a degree-$k$ polynomial on a one-dimensional cell $I_j$, it is defined as:
$$
\beta_r = \sum_{l=1}^{k} (\Delta x)^{2l-1} \int_{I_j} \left( \frac{d^l p_r}{dx^l}(x) \right)^2 \, dx
$$
This definition may seem complex, but its structure is elegant. By performing a change of variables from the physical coordinate $x$ to the reference coordinate $\xi \in [-1,1]$, the definition simplifies considerably. Using the relations $dx = (\Delta x/2) d\xi$ and $d/dx = (2/\Delta x) d/d\xi$, each term in the sum becomes:
$$
(\Delta x)^{2l-1} \int_{-1}^{1} \left( \left(\frac{2}{\Delta x}\right)^l \frac{d^l p_r}{d\xi^l}(\xi) \right)^2 \left(\frac{\Delta x}{2} d\xi\right) = 2^{2l-1} \int_{-1}^{1} \left( \frac{d^l p_r}{d\xi^l}(\xi) \right)^2 \, d\xi
$$
This reveals a crucial property: the smoothness indicator $\beta_r$ is actually independent of the mesh size $\Delta x$ [@problem_id:3429552]. Its value depends only on the shape of the polynomial on the [reference element](@entry_id:168425). This is by design, ensuring that the measure of smoothness is intrinsic to the function's behavior, not the grid scale.

When the polynomial $p_r(\xi)$ is expressed in an orthogonal basis like Legendre polynomials, the integrals of squared derivatives can be computed exactly and efficiently using the properties of the basis functions. For example, if $p_r'(\xi) = \sum_m c_m P_m(\xi)$, then due to orthogonality, $\int_{-1}^1 (p_r'(\xi))^2 d\xi = \sum_m c_m^2 \int_{-1}^1 P_m(\xi)^2 d\xi$, where the latter integrals are known constants. This makes the computation of $\beta_r$ a straightforward algebraic operation on the polynomial's [modal coefficients](@entry_id:752057) [@problem_id:3429552].

Another way to define smoothness indicators is directly from the [modal coefficients](@entry_id:752057) of the DG representation. For instance, a simple and effective indicator can be defined as the sum of the squared high-order [modal coefficients](@entry_id:752057) [@problem_id:3429526]. For a degree-2 polynomial $p(\xi) = c_0 \phi_0(\xi) + c_1 \phi_1(\xi) + c_2 \phi_2(\xi)$ in an orthonormal basis, one might define $\beta = c_1^2 + c_2^2$. This captures the energy in the non-constant modes, serving as a proxy for oscillation.

#### Step C: Calculating the Nonlinear Weights

With smoothness indicators $\beta_r$ in hand, we can compute the nonlinear weights $\omega_r$. The classic Jiang-Shu formulation is:
$$
\omega_r = \frac{\alpha_r}{\sum_{s} \alpha_s}, \quad \text{where} \quad \alpha_r = \frac{d_r}{(\varepsilon + \beta_r)^p}
$$
Let's dissect this formula:
-   **Linear Weights ($d_r$)**: These are a set of fixed, positive numbers that sum to one. They are chosen such that if the weights were fixed to these values ($\omega_r = d_r$), the resulting combination $\sum d_r p_r$ would be a higher-order approximation to the true solution than any individual candidate. For example, in a fifth-order finite volume WENO scheme, three third-order candidates are combined with specific linear weights to yield a fifth-order reconstruction in smooth regions.
-   **Smoothness Indicators ($\beta_r$)**: As computed in the previous step.
-   **Regularization Parameter ($\varepsilon$)**: This is a small positive number (e.g., $\varepsilon = 10^{-6}$) to avoid division by zero in the case where a smoothness indicator for a perfectly smooth polynomial (like a constant) is zero.
-   **Exponent ($p$)**: This integer (typically $p=2$) controls the sensitivity of the weights to the smoothness indicators. A larger $p$ more aggressively penalizes non-smooth candidates.

The brilliance of this formulation is its adaptive behavior. If the solution is smooth, all candidate polynomials will be similarly smooth, and all $\beta_r$ values will be small and of the same [order of magnitude](@entry_id:264888). In this case, $\omega_r \approx d_r$, and the reconstruction achieves its designed high order of accuracy. However, if the stencil for a candidate $p_s$ crosses a shock, its smoothness indicator $\beta_s$ will become very large. The term $(\varepsilon + \beta_s)^p$ will dominate, causing the intermediate weight $\alpha_s$ to become very small, and consequently the final weight $\omega_s \approx 0$. The oscillatory candidate is effectively removed from the final reconstruction, which is now dominated by the smoother candidates from the other stencils. This mechanism robustly prevents oscillations while preserving high accuracy where possible [@problem_id:3429526].

#### Step D: Forming the Final Reconstruction

The final step is to assemble the new polynomial for the troubled cell and use it to compute the [numerical fluxes](@entry_id:752791). The new polynomial is simply the convex combination of the candidates:
$$
\tilde{u}_h^{\mathrm{WENO}}(\xi) = \sum_{r} \omega_r p_r(\xi)
$$
This new polynomial replaces the original, oscillatory polynomial $u_h(\xi)$ in the troubled cell. The numerical fluxes at the cell interfaces, e.g., at $x_{j+1/2}$ (or $\xi=1$), are then computed using the trace values from this new, non-oscillatory representation, i.e., using $\tilde{u}_h^{\mathrm{WENO}}(1)$ [@problem_id:3429541]. This completes the limiting process for one time step.

### Advanced Topics and Practical Considerations

#### Accuracy at Smooth Critical Points

While WENO schemes are designed to be high-order in smooth regions, their accuracy can degrade at points where one or more derivatives of the solution vanish. A common case is a smooth local extremum, or critical point, where $u'(x_c)=0$ and $u''(x_c) \neq 0$.

At such a point, the leading-order behavior of the smoothness indicators changes. For a standard finite volume WENO-JS scheme, the indicators $\beta_r$ typically scale as $\mathcal{O}((\Delta x)^2)$ away from a critical point, but scale as $\mathcal{O}((\Delta x)^4)$ at a critical point. Because the nonlinear weights $\omega_r$ depend on ratios of the $\beta_r$, this change in scaling can cause the weights to converge to values different from the ideal linear weights $d_r$, even though the solution is perfectly smooth. This failure to recover the linear weights prevents the [error cancellation](@entry_id:749073) that provides the high [order of accuracy](@entry_id:145189). Consequently, a fifth-order WENO scheme may see its accuracy drop to third-order at smooth critical points [@problem_id:3429544]. This is a well-known limitation of the standard WENO formulation, and various modified "WENO-Z" or "mapped WENO" schemes have been developed to address it.

#### Modal versus Nodal Formulations

In implementing a DG method, the polynomial solution within a cell can be represented using a **[modal basis](@entry_id:752055)** (e.g., coefficients of an orthogonal polynomial expansion) or a **nodal basis** (e.g., point values at a set of interpolation nodes). This choice has implications for the implementation of the WENO reconstruction.

The smoothness indicator $\beta[p]$ is a functional defined on the polynomial $p$ itself, independent of its representation. This means that, in exact arithmetic, the value of $\beta[p]$ is the same whether it is calculated from a modal or a nodal representation of $p$ [@problem_id:3429545]. In a modal formulation with an [orthonormal basis](@entry_id:147779), $\beta[p]$ can be computed exactly via algebraic operations on the coefficients. In a nodal formulation, the integrals in the definition of $\beta[p]$ are typically computed via quadrature. For this to be equivalent, the [quadrature rule](@entry_id:175061) must be sufficiently accurate. For a degree-$k$ polynomial and the standard Jiang-Shu indicator, the integrand is a polynomial of degree at most $2k-2$. A $(k+1)$-point Gauss-Lobatto [quadrature rule](@entry_id:175061) is exact for polynomials of degree up to $2k-1$, and is therefore sufficient to compute the smoothness indicator exactly [@problem_id:3429545].

Since the smoothness indicators, and thus the nonlinear weights and the final reconstructed polynomial, are identical in exact arithmetic regardless of the basis choice, the modal and nodal DG-WENO formulations are mathematically equivalent. The choice between them becomes a practical matter of implementation complexity, [computational efficiency](@entry_id:270255), and [cache performance](@entry_id:747064).

#### An Optimization-Based View of WENO Weights

The classic Jiang-Shu formula for WENO weights is somewhat ad-hoc. A more rigorous perspective frames the weight selection as a constrained convex optimization problem [@problem_id:3429521]. The goal is to find a weight vector $\boldsymbol{\omega}$ that minimizes an objective function, for instance:
$$
J(\boldsymbol{\omega}) = \frac{\gamma}{2} \lVert \boldsymbol{\omega} - \boldsymbol{d} \rVert_2^2 + \kappa \sum_{r=0}^{m-1} \varphi(\beta_r) \omega_r
$$
subject to the constraints $\sum \omega_r = 1$ and $\omega_r \ge 0$. The first term in $J(\boldsymbol{\omega})$ penalizes deviation from the ideal linear weights $\boldsymbol{d}$, promoting accuracy. The second term penalizes giving weight to candidates with large smoothness indicators $\beta_r$, promoting non-oscillation. The solution to this problem, derived via Karush-Kuhn-Tucker (KKT) theory, has the structure $\omega_r = \max(0, c_r - \tau)$, where $\tau$ is a single threshold value. This provides a deeper mathematical justification for the thresholding behavior of WENO schemes and allows for a systematic analysis of their properties, such as sensitivity to data perturbations.

#### Parallel Implementation Considerations

On modern supercomputers, DG-WENO solvers are implemented on distributed-memory parallel architectures using a [domain decomposition](@entry_id:165934) approach. Each processor is responsible for a subdomain of cells and communicates with its neighbors to exchange boundary information.

A key difference between a standard DG update and a DG-WENO update is the size of the [data dependency](@entry_id:748197) stencil. A standard DG flux calculation at a face requires data from only the two cells sharing that face. In contrast, a WENO reconstruction with a stencil radius of $r$ cells requires data from neighbors up to $r$ cells away. This has a direct impact on the parallel implementation [@problem_id:3429560]:

-   **Halo Layers**: To perform a correct WENO reconstruction for cells near a subdomain boundary, each processor must maintain a "halo" or "[ghost cell](@entry_id:749895)" region containing copies of cell data from its neighbors. The required width of this halo region is determined by the WENO stencil radius, $r$. A halo of width $r$ is both necessary and sufficient to replicate the serial result.

-   **Communication-Computation Overlap**: The exchange of halo data introduces communication latency. This latency can be hidden by overlapping it with useful computation. A common strategy is to first initiate the non-blocking [halo exchange](@entry_id:177547), then perform all computations that do not depend on the halo data—specifically, the WENO reconstructions for "interior" cells that are more than $r$ cells away from any boundary. Once the communication is complete, the remaining reconstructions for the boundary-adjacent cells can be performed. This is a crucial optimization for achieving good [parallel scalability](@entry_id:753141) [@problem_id:3429560].