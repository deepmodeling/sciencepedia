## Introduction
High-order numerical methods, such as the Discontinuous Galerkin (DG) method, offer unparalleled accuracy for simulating complex physical phenomena. However, their reliance on high-degree polynomials introduces a critical vulnerability: the generation of spurious oscillations near sharp gradients, which can lead to solutions that violate fundamental physical laws like the positivity of density or the boundedness of a concentration. This lack of inherent physical robustness presents a significant knowledge gap, limiting the reliable application of these powerful methods. This article provides a comprehensive guide to bridging this gap through the use of positivity- and [boundedness](@entry_id:746948)-preserving limiters.

To build a complete understanding, this article is structured into three distinct chapters. First, in **"Principles and Mechanisms,"** we will explore the root cause of non-physical oscillations and introduce the mathematical principle of convexity as the cornerstone of robust scheme design. This chapter will detail the construction of conservative spatial limiters and the crucial role of Strong Stability Preserving (SSP) [time integrators](@entry_id:756005). Next, the **"Applications and Interdisciplinary Connections"** chapter will extend these core ideas to more complex scenarios, demonstrating how to handle curved geometries, systems of equations like the compressible Euler equations, and challenging [multiphysics](@entry_id:164478) problems through techniques like [operator splitting](@entry_id:634210). Finally, the **"Hands-On Practices"** section will offer a set of guided problems, allowing you to implement and solidify your understanding of these essential limiting techniques.

## Principles and Mechanisms

High-order numerical methods, such as the Discontinuous Galerkin (DG) method, are highly valued for their ability to achieve rapid convergence and accurately resolve complex solution features. However, this power comes with an inherent challenge: the tendency of high-degree polynomial approximations to produce spurious oscillations, particularly near sharp gradients or discontinuities. These oscillations are not merely cosmetic imperfections; they can lead to numerical solutions that violate fundamental physical laws, such as the positivity of mass density or the [boundedness](@entry_id:746948) of a tracer concentration. This chapter delves into the principles and mechanisms developed to address this critical issue, ensuring that [high-order schemes](@entry_id:750306) remain both accurate and physically robust.

### The Challenge of High-Order Methods: Spurious Oscillations

The core of the problem lies in the nature of high-order [polynomial interpolation](@entry_id:145762). While a polynomial is uniquely defined by its values at a set of nodes, its behavior *between* those nodes can be counter-intuitive. A polynomial representation of a physical quantity may respect physical bounds at all defining [nodal points](@entry_id:171339), yet dip into a non-[physical region](@entry_id:160106) in the interior of an element.

Consider, for instance, a simple scenario on a one-dimensional reference element $[-1, 1]$. Let us approximate a solution using a polynomial of degree three ($p=3$), defined by its values at the four Gauss-Lobatto-Legendre nodes: $x_0 = -1$, $x_1 = -1/\sqrt{5}$, $x_2 = 1/\sqrt{5}$, and $x_3 = 1$. Suppose that at a given moment, the solution values at these nodes are all positive, given by the data set $\{u_0, u_1, u_2, u_3\} = \{10, 1/5, 1/5, 10\}$. Intuitively, one might expect the interpolating polynomial $u_h(x)$ to remain positive throughout the element. However, a direct calculation of the polynomial's value at the element's center, $x=0$, reveals a startling result: $u_h(0) = -9/4$ [@problem_id:3409711].

This undershoot occurs because the value of the interpolating polynomial is a linear combination of the nodal values, $u_h(x) = \sum_{j} u_j L_j(x)$, where $L_j(x)$ are the Lagrange basis polynomials. For high-degree polynomials, these basis functions necessarily have "lobes" that take on negative values. In the example above, the basis functions associated with the endpoints, $L_0(x)$ and $L_3(x)$, are negative at $x=0$. The large positive nodal values at the endpoints, $u_0=10$ and $u_3=10$, are multiplied by these negative coefficients, overwhelming the positive contributions from the interior nodes and creating a non-physical negative value [@problem_id:3409711].

This phenomenon illustrates a failure to satisfy a **[discrete maximum principle](@entry_id:748510)**. While the exact solution to many conservation laws satisfies a maximum principle (i.e., if the initial data lies within an interval $[m, M]$, the solution remains in $[m, M]$ for all time), [high-order numerical methods](@entry_id:142601) do not automatically inherit this property. Even if the numerical scheme is constructed to preserve the bounds of the **cell averages**, the pointwise values of the polynomial solution can violate them [@problem_id:3409628]. To rectify this, we require a special intervention: a **[limiter](@entry_id:751283)**. A limiter is a procedure designed to modify the polynomial approximation to enforce physical bounds while maintaining the conservation of the underlying quantity.

### The Unifying Principle of Convexity

The design and analysis of bound-preserving schemes are elegantly unified by the mathematical concept of **[convexity](@entry_id:138568)**. An **admissible set**, denoted by $\mathcal{G}$, is the set of all physically meaningful states. For a scalar quantity required to be positive, the admissible set is $\mathcal{G} = [0, \infty)$. For a quantity bounded between $m$ and $M$, it is $\mathcal{G} = [m, M]$. Both of these sets are **convex**. A set is convex if for any two points within the set, the straight line segment connecting them is also entirely contained within the set. More formally, for any $v, w \in \mathcal{G}$ and any $\theta \in [0, 1]$, the convex combination $\theta v + (1-\theta)w$ must also be in $\mathcal{G}$.

This property is profoundly useful. If we can show that our numerical operations—both in space and time—are expressible as convex combinations of admissible states, we can guarantee that the solution will remain within the admissible set $\mathcal{G}$. For systems of equations, such as the compressible Euler equations, the set of admissible states is defined by positivity of density and pressure, $\mathcal{G} = \{ (\rho, \mathbf{m}, E) : \rho > 0, p = (\gamma - 1)(E - \frac{|\mathbf{m}|^2}{2\rho}) > 0 \}$. Remarkably, this set is also convex, allowing the same unifying principle to be applied [@problem_id:3409651].

The goal, therefore, is to construct a numerical scheme where every step of the computation can be viewed as a convex combination. This applies to the [time integration](@entry_id:170891), the [spatial discretization](@entry_id:172158), and the limiting procedure itself.

### Preserving Bounds in Time: Strong Stability Preserving (SSP) Methods

The preservation of physical bounds must hold as the solution evolves in time. This requires a [time integration](@entry_id:170891) scheme that is compatible with the convexity principle. **Strong Stability Preserving (SSP) Runge-Kutta methods** are specifically designed for this purpose.

Let the semi-discrete DG formulation be written as a system of [ordinary differential equations](@entry_id:147024) (ODEs), $\frac{\mathrm{d}u}{\mathrm{d}t} = L(u)$, where $u$ represents the vector of all degrees of freedom for the solution polynomial $u_h$. Let us assume we have designed a spatial operator $L$ (which may include a [limiter](@entry_id:751283)) that satisfies a crucial forward Euler property: if a state $u^n$ is in the admissible convex set $\mathcal{G}$, then a single forward Euler step also results in an admissible state, $u^n + \Delta t L(u^n) \in \mathcal{G}$, provided the time step $\Delta t$ is sufficiently small, i.e., $\Delta t \le \Delta t_{\mathrm{FE}}$. This $\Delta t_{\mathrm{FE}}$ is determined by a Courant-Friedrichs-Lewy (CFL) condition.

An SSP method advances the solution from $u^n$ to $u^{n+1}$ through a series of intermediate stages. The defining feature of these methods, in the Shu-Osher representation, is that every stage is calculated as a convex combination of previous stages and forward Euler-like steps applied to those previous stages [@problem_id:3409639]. For example, a second-order two-stage SSP method can be written as:
$u^{(1)} = u^n + \Delta t L(u^n)$
$u^{n+1} = \frac{1}{2} u^n + \frac{1}{2} (u^{(1)} + \Delta t L(u^{(1)}))$

We can prove by induction that this structure preserves the admissible set $\mathcal{G}$.
1.  **Base Case:** We start with an admissible state $u^n \in \mathcal{G}$.
2.  **Stage 1:** To ensure $u^{(1)} \in \mathcal{G}$, we require the forward Euler step to be property-preserving. This is true if $\Delta t \le \Delta t_{\mathrm{FE}}$.
3.  **Stage 2:** The final update $u^{n+1}$ is a convex combination of $u^n$ and $u^{(1)} + \Delta t L(u^{(1)})$. By the [inductive hypothesis](@entry_id:139767), $u^n \in \mathcal{G}$. The term $u^{(1)} + \Delta t L(u^{(1)})$ is another forward Euler step applied to an admissible state $u^{(1)}$, and thus it also lies in $\mathcal{G}$ (provided $\Delta t \le \Delta t_{\mathrm{FE}}$). Since $\mathcal{G}$ is convex, the convex combination of these two admissible states must also be in $\mathcal{G}$.

This logic extends to any SSP method. The full time step $\Delta t$ of the SSP method is related to the forward Euler time step limit $\Delta t_{\mathrm{FE}}$ by the **SSP coefficient** $C$, which is a property of the specific RK method: $\Delta t \le C \cdot \Delta t_{\mathrm{FE}}$. The essential conclusion is that if we can construct a spatial operator $L$ that preserves admissibility for a single forward Euler step, an SSP integrator will extend this property to a high-order-in-time update [@problem_id:3409639].

### Preserving Bounds in Space: Limiter Design

The main task is to design the spatial operator $L(u)$ such that it satisfies the forward Euler preservation property. This involves modifying the raw, oscillation-prone polynomial $u_h$ at each stage of the Runge-Kutta method.

#### Fundamental Requirements of a Limiter

A bound-preserving limiter must achieve two conflicting goals simultaneously [@problem_id:3409628]:
1.  **Enforce Bounds:** The modified polynomial, let's call it $\tilde{u}_h$, must satisfy the physical bounds pointwise (or at least at a carefully chosen set of points). For example, $\tilde{u}_h(x) \in [m, M]$ for all $x$ in the element.
2.  **Conservation:** The total amount of the conserved quantity within the element must not change. This means the cell average of the polynomial must be preserved: $\int_K \tilde{u}_h(x) dx = \int_K u_h(x) dx$.

A naive approach like "clipping" the polynomial, e.g., $\tilde{u}_h(x) = \max(m, \min(M, u_h(x)))$, will enforce the bounds but will not preserve the cell average. It is a non-conservative operation and is therefore unsuitable for solving conservation laws [@problem_id:3409628].

#### The Conservative Scaling Limiter

A widely used and effective approach that satisfies both requirements is the **conservative scaling [limiter](@entry_id:751283)**. This limiter modifies the polynomial by scaling its deviation from the cell average:
$$ \tilde{u}_h(x) = \bar{u}_h + \theta (u_h(x) - \bar{u}_h) $$
where $\bar{u}_h$ is the cell average and $\theta$ is a scaling factor in the range $[0, 1]$. This formulation is elegantly conservative by construction: since the integral of the deviation $(u_h(x) - \bar{u}_h)$ over the element is zero, the cell average of $\tilde{u}_h$ is always equal to $\bar{u}_h$, regardless of the choice of $\theta$ [@problem_id:3409702].

The problem thus reduces to finding the largest possible value of $\theta \in [0, 1]$ that ensures the modified polynomial $\tilde{u}_h$ respects the desired bounds. If the original polynomial $u_h$ is already within bounds, we choose $\theta=1$, leaving the solution unchanged. If not, we must reduce $\theta$ from 1 towards 0. A value of $\theta=0$ corresponds to replacing the high-order polynomial with its cell average (a constant), which is guaranteed to be within the bounds if a monotone flux and SSP integrator are used.

To enforce the bounds $m_K \le \tilde{u}_h(x) \le M_K$ at a set of quadrature points $\{x_i\}$, we analyze the required inequalities. For a point $x_i$ where the polynomial overshoots ($u_h(x_i) > M_K$), the condition $\tilde{u}_h(x_i) \le M_K$ leads to a constraint on $\theta$. Similarly, for a point where it undershoots ($u_h(x_i) < m_K$), we get another constraint. Combining all such constraints from all quadrature points, we arrive at the optimal choice for $\theta$ [@problem_id:3409702] [@problem_id:3409688]:
$$ \theta_K = \min\Bigg\{ 1, \min_{\substack{i \\ u_h(x_{i}) > M_K}} \frac{M_K - \bar{u}_h}{u_h(x_{i}) - \bar{u}_h}, \min_{\substack{i \\ u_h(x_{i}) < m_K}} \frac{m_K - \bar{u}_h}{u_h(x_{i}) - \bar{u}_h} \Bigg\} $$
The bounds $m_K$ and $M_K$ are typically taken from the minimum and maximum of the cell averages in the immediate neighborhood of cell $K$, as these are the bounds guaranteed for the updated cell average by the underlying first-order scheme.

#### The Crucial Role of Quadrature Rules

In multiple spatial dimensions, enforcing bounds *everywhere* within an element is computationally expensive. The standard practice is to enforce them only at a [finite set](@entry_id:152247) of quadrature points. This raises a critical consistency question: if we ensure $u_h \ge 0$ at the quadrature nodes, can we be sure that the *cell average* of $u_h$ is also non-negative? The cell average is an integral, which the DG scheme calculates using a numerical quadrature rule:
$$ \bar{u}_h = \frac{1}{|K|} \int_K u_h(\boldsymbol{x}) d\boldsymbol{x} \approx \frac{1}{|K|} \sum_{i=1}^N w_i u_h(\boldsymbol{x}_i) $$
For this consistency to hold, two conditions on the quadrature rule are essential [@problem_id:3409652]:
1.  **Exactness:** The [quadrature rule](@entry_id:175061) must integrate the polynomial $u_h$ exactly. If $u_h$ is of degree $k$, the quadrature rule must have a [degree of exactness](@entry_id:175703) $m \ge k$. If this holds, the integral *is* the quadrature sum.
2.  **Positive Weights:** All [quadrature weights](@entry_id:753910) $w_i$ must be strictly positive.

If both conditions are met, then the cell average is a convex combination of the nodal values: $\bar{u}_h = \sum_{i} \frac{w_i}{|K|} u_h(\boldsymbol{x}_i)$, where the coefficients $\frac{w_i}{|K|}$ are positive and sum to one. It follows directly that if $u_h(\boldsymbol{x}_i) \in [m, M]$ for all $i$, then $\bar{u}_h \in [m, M]$ [@problem_id:3409665].

This places important constraints on the choice of quadrature. Rules like Legendre-Gauss, Legendre-Gauss-Lobatto (in 1D), and certain Dunavant, Keast, or Xiao-Gimbutas rules (on triangles and tetrahedra) have positive weights and are suitable. In contrast, high-order closed Newton-Cotes rules (for $n \ge 9$ points) are known to have negative weights. Using such a rule is unsafe for a provably bound-preserving scheme, as it is possible to have positive values at all quadrature nodes but obtain a negative cell average, breaking the foundational assumptions of the limiter algorithm [@problem_id:3409665].

#### Alternative Strategy: Flux Limiting

An alternative to modifying the solution polynomial directly is to modify the numerical fluxes at the element interfaces. This approach, often associated with Flux-Corrected Transport (FCT) methods, blends a high-order, accurate flux $F^{HO}$ with a low-order, robustly monotone flux $F^{LO}$. The limited flux is a convex combination:
$$ F^{\alpha}_{i+1/2} = \alpha F^{HO}_{i+1/2} + (1-\alpha) F^{LO}_{i+1/2} $$
where $\alpha \in [0, 1]$ is a blending factor. The key idea is to use as much of the high-order flux as possible (i.e., keep $\alpha$ as close to 1 as possible) without violating the bounds on the updated cell averages. By expressing the updated cell average $U_i^{n+1}$ in terms of the guaranteed-admissible low-order update $U_i^{LO}$, one can derive a set of constraints on a single, global $\alpha$ that ensures all cell averages remain within their prescribed local bounds [@problem_id:3409632]. This provides a different pathway to achieving robustness, focused on the fluxes rather than the solution representation.

### Context and Comparison with Other Limiters

It is important to distinguish positivity- and boundedness-preserving limiters from other familiar limiting strategies [@problem_id:3409649].

*   **Total Variation Bounded (TVB) / Slope Limiters:** These limiters are primarily designed to control the [total variation](@entry_id:140383) of the solution and prevent the formation of new spurious oscillations, a property related to monotonicity. They typically act by modifying the first-degree mode (the slope) of the polynomial. However, they are not designed to enforce strict physical bounds. In fact, the "B" in TVB (for "bounded") allows for small, controlled oscillations near smooth [extrema](@entry_id:271659), meaning they can, by design, slightly violate a strict maximum principle. They also do not control [higher-order modes](@entry_id:750331) ($p \ge 2$), which can cause their own bound violations.

*   **Hierarchical Moment Limiters:** These limiters operate by progressively damping the higher-degree [modal coefficients](@entry_id:752057) of the polynomial solution. This is effective at reducing the visual appearance of Gibbs oscillations. However, like [slope limiters](@entry_id:638003), they provide no hard guarantee of bound preservation. Damping reduces the magnitude of oscillations but does not necessarily eliminate them entirely.

In conclusion, while slope and moment limiters are valuable tools for improving the qualitative behavior of high-order solutions, only limiters specifically designed with bound-preservation as their explicit goal can provide the rigorous guarantee needed for problems where physical admissibility is paramount. The conservative scaling limiter, built on the principle of [convexity](@entry_id:138568) and paired with an appropriate SSP time integrator and positive-weight quadrature, provides a powerful and provably robust framework for achieving this goal.