## Introduction
High-order numerical methods, such as Discontinuous Galerkin (DG) schemes, offer unparalleled accuracy for simulating smooth solutions to [hyperbolic conservation laws](@entry_id:147752). However, this advantage is compromised when solutions contain discontinuities like [shock waves](@entry_id:142404), where high-degree polynomials produce spurious, non-physical oscillations. While traditional limiters can suppress these oscillations, they often do so at a great cost, reducing the scheme's accuracy to first-order at smooth peaks and valleys. This article addresses this critical challenge by providing an in-depth exploration of Total Variation Bounded (TVB) limiters, a sophisticated class of methods designed to maintain stability without sacrificing accuracy.

This guide will equip you with a comprehensive understanding of TVB limiters, from their theoretical underpinnings to their practical implementation and broad applicability. The first chapter, **Principles and Mechanisms**, will dissect the core TVB principle, explaining how it overcomes the failures of simpler limiters and detailing its implementation for both scalar and systems of equations. Next, **Applications and Interdisciplinary Connections** will showcase the power of TVB methods in real-world [computational fluid dynamics](@entry_id:142614) simulations and explore their surprising relevance in fields like [geophysics](@entry_id:147342) and [computational finance](@entry_id:145856). Finally, **Hands-On Practices** will offer a set of targeted problems to solidify your grasp of the key theoretical and practical concepts. Through this structured approach, you will gain the expertise to implement and leverage robust, high-order, non-oscillatory schemes in your own scientific computations.

## Principles and Mechanisms

High-order numerical methods, such as Discontinuous Galerkin (DG) schemes, are designed to achieve rapid convergence for smooth solutions of [hyperbolic conservation laws](@entry_id:147752). However, when solutions contain discontinuities like shock waves, the high-order polynomial approximations within each element can produce non-physical oscillations, a manifestation of the Gibbs phenomenon. To ensure stability and physical realism, these oscillations must be controlled. The classical approach is to employ limiters that enforce a Total Variation Diminishing (TVD) property on the numerical solution. While effective at suppressing oscillations, TVD schemes suffer from a critical flaw: they degenerate to [first-order accuracy](@entry_id:749410) at smooth, [local extrema](@entry_id:144991). This chapter elucidates the principles behind a more advanced class of limiters—Total Variation Bounded (TVB) limiters—which are designed to overcome this deficiency, and details the mechanisms for their implementation in modern DG methods.

### The Failure of TVD Schemes at Smooth Extrema

The total variation of a one-dimensional function $u(x)$ is a measure of its oscillatory content, defined for a discrete solution $\{\bar{u}_i\}$ on a mesh as $\mathrm{TV}_h = \sum_i |\bar{u}_{i+1} - \bar{u}_i|$. A numerical scheme is TVD if the total variation of the solution does not increase in time. This property is sufficient to prevent the generation of new [spurious oscillations](@entry_id:152404). Many limiters, such as the widely used [minmod limiter](@entry_id:752002), are designed to enforce this condition.

The fundamental problem arises when these schemes encounter smooth solutions with [local extrema](@entry_id:144991). Consider, for example, the [linear advection](@entry_id:636928) of a smooth parabolic profile, such as the solution to $u_t + a u_x = 0$ with initial data $u(x,0) = \gamma x^2$ . Near the extremum (a minimum in this case), the cell averages will exhibit a [local minimum](@entry_id:143537), meaning for some cell $j$, we have $\bar{u}_{j-1} > \bar{u}_j$ and $\bar{u}_j < \bar{u}_{j+1}$. Consequently, the one-sided differences of the cell averages, $\bar{u}_j - \bar{u}_{j-1}$ and $\bar{u}_{j+1} - \bar{u}_j$, will have opposite signs.

A [slope limiter](@entry_id:136902) for a piecewise linear reconstruction $u_h(x) = \bar{u}_j + \sigma_j (x-x_j)$ in cell $I_j$ determines the slope $\sigma_j$ by comparing it to slopes constructed from these neighboring differences. A typical TVD [limiter](@entry_id:751283), such as [minmod](@entry_id:752001), when presented with arguments of opposite signs, will return zero. This action, often called **clipping**, sets the reconstruction slope $\sigma_j$ to zero, reducing the local approximation to a piecewise constant. This degenerates the scheme to [first-order accuracy](@entry_id:749410) at the extremum, effectively flattening the smooth peak or valley. This [order reduction](@entry_id:752998) is a catastrophic failure for a method intended to be high-order accurate.

### The Total Variation Bounded (TVB) Principle

The remedy for the order-reduction problem is to relax the strict TVD condition. The **Total Variation Bounded (TVB)** principle does not demand that total variation be non-increasing at every time step, but rather that it remains uniformly bounded for all time, $\mathrm{TV}_h(t) \le B$, where $B$ is a constant that may depend on the initial data but not on the mesh size $h$. This relaxation allows for small, controlled increases in total variation, which is precisely what is required to represent the natural curvature of a smooth extremum without generating spurious oscillations.

The mechanism to achieve this is a modification to a standard [limiter](@entry_id:751283). A TVB [limiter](@entry_id:751283) first detects whether the local solution variation is small enough to be consistent with a smooth profile rather than a sharp, incipient oscillation. If the variation is below a certain threshold, the limiter is deactivated, and the original high-order polynomial representation is retained, thereby preserving the scheme's formal [order of accuracy](@entry_id:145189). If the variation exceeds the threshold, a conventional TVD-type limiter is activated to suppress a potential oscillation.

### The TVB Correction: A Mechanism for Accuracy Preservation

The core of a TVB limiter is its detection mechanism. How can the limiter distinguish between the benign curvature of a smooth extremum and a non-physical oscillation? The answer lies in a careful analysis of the solution's local behavior using Taylor series expansions.

For a sufficiently smooth solution $u(x)$ and a uniform mesh of size $h$, the cell average $\bar{u}_j$ in cell $I_j$ is related to the point value at the cell center $x_j$ by:
$$
\bar{u}_j = u(x_j) + \frac{h^2}{24} u''(x_j) + \mathcal{O}(h^4)
$$
By expanding the neighboring cell averages $\bar{u}_{j\pm 1}$ around $x_j$, we can analyze the differences between them. At a generic point, the [first difference](@entry_id:275675) $\bar{u}_{j+1} - \bar{u}_j$ is dominated by the first derivative:
$$
\bar{u}_{j+1} - \bar{u}_j = h u'(x_j) + \frac{h^2}{2} u''(x_j) + \mathcal{O}(h^3)
$$
However, precisely at a smooth extremum where $u'(x_j) = 0$, the leading term vanishes. The differences in cell averages are then governed by the second derivative :
$$
\bar{u}_{j\pm 1} - \bar{u}_j = \pm \frac{h^2}{2} u''(x_j) + \mathcal{O}(h^3)
$$
This insight is fundamental. It tells us that the cell-average differences, which have opposite signs at an extremum, should be small, specifically on the order of $\mathcal{O}(h^2)$. This provides a clear signature of a smooth extremum that can be distinguished from a large, $\mathcal{O}(1)$ jump at a shock or a spurious $\mathcal{O}(h)$ oscillation.

A TVB [limiter](@entry_id:751283) operationalizes this by introducing a threshold proportional to $h^2$. For instance, a **TVB-modified [minmod limiter](@entry_id:752002)** is defined as follows: if the local differences (e.g., $|\bar{u}_{j\pm 1} - \bar{u}_j|$) are smaller than a threshold $Mh^2$, the original unlimited slope is used. Otherwise, the standard [minmod limiter](@entry_id:752002) is applied.
$$
\tilde{\sigma}_j =
\begin{cases}
\sigma_j,  & \text{if one-sided differences are } \le M h^2 \\
\operatorname{minmod}(\sigma_j, \dots),  & \text{otherwise}
\end{cases}
$$
The parameter $M$ is a user-defined constant that must be chosen carefully. A rigorous analysis via Taylor expansions can provide an estimate for $M$ based on bounds for the solution's higher derivatives . For example, if $|u''(x)| \le U_2$ and $|u'''(x)| \le U_3$, one can show that discrepancies between quantities used in limiting decisions are bounded, leading to a choice for $M$ on the order of $M \approx C_1 U_2 + C_2 U_3 h_0$, where $C_1, C_2$ are constants and $h_0$ is a reference mesh size. This confirms that $M$ is fundamentally linked to the curvature of the underlying solution.

### TVB Limiting in the Discontinuous Galerkin Framework

In the context of a DG method, limiting is performed on the polynomial coefficients within each cell. For a degree $p$ [polynomial approximation](@entry_id:137391), the coefficients of the basis functions of degree $1$ to $p$ represent the higher-order content of the solution and are the targets for the limiter. The degree-0 coefficient, which is proportional to the cell average, must be preserved to ensure conservation.

#### Piecewise Linear ($p=1$) Case

For a $p=1$ DG method, the local solution is a linear polynomial, $u_h(x) = \bar{u}_j + \sigma_j(x-x_j)$. The quantity to be limited is the physical slope $\sigma_j$. In a practical DG implementation, the solution is often represented in a [modal basis](@entry_id:752055), typically using Legendre polynomials on a [reference element](@entry_id:168425) $\xi \in [-1,1]$. For $p=1$, we have $u_h(\xi) = \hat{u}_{j,0} P_0(\xi) + \hat{u}_{j,1} P_1(\xi)$, where $P_0(\xi)=1$ and $P_1(\xi)=\xi$. The cell average is $\bar{u}_j = \hat{u}_{j,0}$, and the first modal coefficient $\hat{u}_{j,1}$ is directly proportional to the physical slope $\sigma_j$. Through a [change of variables](@entry_id:141386) and $L^2$ projection, one can derive the precise relationship :
$$
\hat{u}_{j,1} = \frac{1}{2} \sigma_j h_j
$$
This simple mapping shows that limiting the physical slope is entirely equivalent to limiting the first modal coefficient. A practical TVB limiting procedure for a $p=1$ DG scheme is as follows :

1.  For a cell $I_j$, calculate the unlimited slope $\sigma_j$ (or equivalently, $\hat{u}_{j,1}$) from the DG formulation.
2.  Compute a measure of local variation, such as the discrete second difference of cell averages $\Delta^2 \bar{u}_j = \bar{u}_{j+1} - 2\bar{u}_j + \bar{u}_{j-1}$.
3.  Check the TVB condition: If $|\Delta^2 \bar{u}_j| \le M h^2$, set the limited slope $\tilde{\sigma}_j = \sigma_j$.
4.  If the condition is not met, compute the limited slope $\tilde{\sigma}_j$ using a standard limiter, e.g.,
    $$
    \tilde{\sigma}_j = \operatorname{minmod}\left(\sigma_j, \frac{\bar{u}_j - \bar{u}_{j-1}}{h}, \frac{\bar{u}_{j+1} - \bar{u}_j}{h}\right)
    $$
5.  Update the local solution to $u_h^{\text{lim}}(x) = \bar{u}_j + \tilde{\sigma}_j(x-x_j)$. This modification affects the extrapolated values at the cell interfaces, $u_{j\pm 1/2}^{\mp}$, which are used in the [numerical flux](@entry_id:145174) calculation.

#### Higher-Order ($p > 1$) Case

For polynomial degrees $p \ge 2$, the concept is similar, but the TVB parameter $M$ can no longer be a global constant. For optimal performance, $M$ should adapt to the local smoothness of the solution. The guiding principle is to set $M_j$ on each cell proportional to the local curvature, $M_j \propto \max_{x \in I_j} |u_h''(x)|$. This local second derivative can be estimated directly from the known DG polynomial coefficients.

For a solution expanded in an orthonormal Legendre basis, $u_h(x) = \sum_{k=0}^p \beta_{j,k} \phi_k(\xi)$, the second derivative is:
$$
u_h''(x) = \left(\frac{2}{h_j}\right)^2 \frac{d^2}{d\xi^2} u_h(x(\xi)) = \frac{4}{h_j^2} \sum_{k=2}^p \beta_{j,k} \phi_k''(\xi)
$$
Using the properties of Legendre polynomials and the [triangle inequality](@entry_id:143750), one can derive a rigorous upper bound for $|u_h''(x)|$ in terms of the [modal coefficients](@entry_id:752057) $\beta_{j,k}$ . This leads to an explicit formula for $M_j$ that can be computed on the fly, for instance:
$$
M_j = \frac{c}{h_j^2} \sum_{k=2}^{p} |\beta_{j,k}| \sqrt{\frac{2k+1}{2}} (k+2)(k+1)k(k-1)
$$
where $c$ is a constant. This provides a systematic way to adapt the TVB limiter's sensitivity to the local features of the numerical solution in a high-order context.

### Extension to Hyperbolic Systems: Characteristic Limiting

When dealing with [systems of conservation laws](@entry_id:755768), such as the Euler equations of gas dynamics, the scalar limiting procedure cannot be applied naively to each component of the conserved state vector $(\rho, m, E)^{\top}$. Doing so ignores the underlying physics of [wave propagation](@entry_id:144063), where information travels along characteristic fields. A component-wise approach can lead to incorrect wave speeds and even violate fundamental physical principles.

A striking example is the failure to preserve **Galilean invariance** . The Euler equations' physics are independent of the constant velocity of the observer's reference frame. A numerical scheme should respect this symmetry. However, due to the nonlinear nature of limiters like [minmod](@entry_id:752001) and the coupling in the transformation of [conserved variables](@entry_id:747720) (e.g., $m' = m - U\rho$), applying the [limiter](@entry_id:751283) component-wise in one frame yields a different physical result than applying it in a boosted frame. This violation makes component-wise limiting physically untenable.

The correct and standard procedure is **characteristic-based limiting**. The philosophy is to transform the problem locally into a basis where the system approximately decouples into a set of scalar advection equations. This is achieved via the eigen-decomposition of the flux Jacobian, $A(u) = R(u)\Lambda(u)R(u)^{-1}$. The procedure in a given cell $I_j$ is as follows  :

1.  **Localize**: Choose a [reference state](@entry_id:151465) in the cell, typically the cell average $\bar{u}_j$.
2.  **Decompose**: Compute the Jacobian $A(\bar{u}_j)$ and its right and left eigenvector matrices, $R_j$ and $R_j^{-1}$.
3.  **Project**: Transform the DG [modal coefficients](@entry_id:752057) (both for the cell $I_j$ and its neighbors' averages) from conservative variables $u$ to [characteristic variables](@entry_id:747282) $w$ using the left eigenvectors: $\hat{w}_k = R_j^{-1} \hat{u}_k$.
4.  **Limit**: For each characteristic field $\ell = 1, \dots, m$, apply the *scalar* TVB limiting procedure described previously to the corresponding [modal coefficients](@entry_id:752057) $\hat{w}_k^{(\ell)}$.
5.  **Reconstruct**: Transform the limited characteristic [modal coefficients](@entry_id:752057) $\hat{w}_{k, \text{lim}}$ back to conservative variables using the right eigenvectors: $\hat{u}_{k, \text{lim}} = R_j \hat{w}_{k, \text{lim}}$.

To ensure that machine precision errors in the projection and reconstruction steps do not violate conservation, a robust implementation explicitly restores the original cell average: $\bar{u}_{j, \text{lim}} \leftarrow \bar{u}_j$. By operating on the characteristic fields, which are Galilean invariant (e.g., the strength of a contact wave is invariant), this procedure correctly preserves the physical symmetries of the governing equations.

### Ensuring Physical Admissibility: Positivity-Preserving Limiters

For systems like the Euler equations, numerical solutions must satisfy certain physical constraints, such as positivity of density $\rho$ and pressure $p$. Even with a TVB limiter, the resulting high-order polynomial may dip into non-physical states at certain points within a cell, particularly near strong shocks.

When this occurs, an additional limiting step is required to enforce physical admissibility. A common and effective method is a **[positivity-preserving limiter](@entry_id:753609)** based on convex scaling . If the polynomial state $U^{\mathrm{HO}}$ at some point (e.g., an interface quadrature point) is found to be non-physical (e.g., $p(U^{\mathrm{HO}})  0$), it is modified by pulling it back towards the cell average $\bar{U}$, which is assumed to be physically admissible. The new state $U_{\theta}$ is defined as a convex combination:
$$
U_{\theta} = (1-\theta)\bar{U} + \theta U^{\mathrm{HO}}, \quad \text{for some } \theta \in [0, 1]
$$
One must find the smallest modification (i.e., the largest $\theta$) that restores positivity. This often involves solving a small nonlinear (e.g., quadratic for pressure) inequality for $\theta$.

Crucially, this positivity-fixing step is compatible with the TVB property. The TVB condition essentially requires the solution at cell boundaries to lie within the convex hull of neighboring cell averages. The cell average $\bar{U}$ is, by definition, within this hull. The scaling operation moves the state $U^{\mathrm{HO}}$ along a line segment towards $\bar{U}$. This can only move the state closer to satisfying the TVB bounds, or keep it within them. It cannot increase the total variation or degrade the TVB property. This demonstrates how TVB limiters can be integrated into a hierarchy of limiting procedures to create a numerical scheme that is not only high-order and non-oscillatory but also robust and physically sound.