## Introduction
In [energy systems optimization](@entry_id:1124494), the accurate representation of generator production costs is fundamental to achieving economic efficiency. However, a significant challenge arises from the inherent conflict between the non-linear, often convex, nature of these cost functions and the computational power of Linear and Mixed-Integer Linear Programming (MILP) solvers, which demand linear relationships. This article addresses this critical gap by providing a comprehensive exploration of Piecewise Linear Approximation (PLA), a powerful technique used to transform non-linear cost curves into a format that is tractable for [large-scale optimization](@entry_id:168142).

This exploration is structured to build a robust understanding from theory to practice. The first chapter, **Principles and Mechanisms**, delves into the mathematical underpinnings of PLA, explaining why production costs are convex and detailing key MILP formulations such as the convex combination (SOS2) and incremental methods. The second chapter, **Applications and Interdisciplinary Connections**, expands on these foundations to showcase PLA's indispensable role in core power system problems like Economic Dispatch and Unit Commitment, and its surprising relevance in diverse fields from electronic circuit design to artificial intelligence. Finally, the **Hands-On Practices** chapter offers a series of targeted problems to reinforce these concepts and develop practical modeling skills. By navigating through these sections, the reader will gain a deep, functional knowledge of how to effectively model non-linear costs in complex optimization frameworks.

## Principles and Mechanisms

In the optimization of energy systems, accurately modeling the production cost of generating units is of paramount importance. While the underlying physical processes are often nonlinear, the most powerful and scalable optimization tools are designed for linear problems. This necessitates the approximation of nonlinear cost functions using piecewise linear constructs. This chapter elucidates the fundamental principles governing these approximations and the primary mechanisms used to embed them within Mixed-Integer Linear Programming (MILP) frameworks.

### The Convex Nature of Production Costs

The production cost of a thermal generator is primarily determined by two factors: its efficiency in converting fuel into electricity and the price of that fuel. The generator's efficiency is characterized by its **heat-rate curve**, denoted as $H(p)$, which specifies the thermal energy input (e.g., in MMBtu/h) required to produce a given electrical power output $p$ (e.g., in MW). Given a constant fuel price $\pi_f$ (e.g., in $/MMBtu), the production cost function, $C(p)$, is simply the product of the heat rate and the fuel price:

$C(p) = \pi_f H(p)$

A crucial characteristic of most thermal generators, especially when operating away from complex valve-point effects, is that they become less efficient at the margin as their output increases. This means that producing an additional megawatt of power requires a progressively larger increase in fuel consumption. This physical property is captured by the **incremental heat-rate**, $dH/dp$, which is an increasing function of the power output $p$.

From the principles of calculus, if the first derivative of a function is strictly increasing, the function itself is **strictly convex**. Since the cost function $C(p)$ is a positive constant multiple of the heat-rate curve $H(p)$, its derivatives follow the same pattern. The first derivative of the cost function, $C'(p) = \pi_f (dH/dp)$, is the incremental cost. If the incremental heat-rate is increasing, then the incremental cost is also increasing. This implies that the second derivative of the cost function is positive:

$C''(p) = \pi_f \frac{d^2H}{dp^2} > 0$

Therefore, under the common condition of an increasing incremental heat-rate, the generator production cost function $C(p)$ is strictly convex . This convexity is a desirable property, as it guarantees that a local minimum is also a global minimum, but it simultaneously poses a challenge for linear programming solvers that cannot directly handle such nonlinearities. This is the primary motivation for developing piecewise linear approximations.

### Constructing a Piecewise Linear Function

A continuous, convex piecewise linear function can be systematically constructed from a set of segment slopes and breakpoints. Let us consider an ordered set of breakpoints $p_1, p_2, \dots, p_n$ partitioning the generator's operating range $[P_{\min}, P_{\max}]$, where $p_1 = P_{\min}$ and $p_n = P_{\max}$. We can define the approximate cost function, $\hat{C}(p)$, by specifying its value at the start, $\hat{C}(p_1) = C_0$, and the slope of each linear segment.

For any segment $i$ on the interval $[p_i, p_{i+1}]$, the function is defined by the point-slope form of a line:

$\hat{C}(p) = \hat{C}(p_i) + m_i (p - p_i)$

where $m_i$ is the constant slope (marginal cost) on this segment. To ensure the function is continuous across the entire domain, the value at the end of one segment must match the value at the beginning of the next. This is achieved by defining the cost at each subsequent breakpoint recursively:

$\hat{C}(p_{i+1}) = \hat{C}(p_i) + m_i (p_{i+1} - p_i)$

This recursive construction guarantees that the function has no "jumps" at the breakpoints. Furthermore, for the resulting piecewise linear function to be convex—mirroring the property of the original cost function—its slope must be non-decreasing. This imposes a simple algebraic condition on the segment slopes :

$m_1 \le m_2 \le \dots \le m_{n-1}$

This set of conditions provides a complete and rigorous blueprint for defining a continuous, convex, piecewise linear cost function.

### Formulations for Mathematical Optimization

Once a piecewise linear approximation is defined, it must be translated into a set of equations and inequalities that a MILP solver can understand. Several standard formulations exist, each with distinct properties and performance implications.

#### The Convex Combination (Lambda) Formulation with SOS2

Perhaps the most elegant and widely used method is the **convex combination formulation**, also known as the $\lambda$-formulation. This approach introduces a set of non-negative weight variables, $\lambda_i$, one for each breakpoint $(p_i, C(p_i))$. The power output $p$ and its corresponding cost $\hat{C}$ are represented as weighted averages of the breakpoint coordinates:

$p = \sum_{i=0}^{N} \lambda_i p_i$

$\hat{C} = \sum_{i=0}^{N} \lambda_i C(p_i)$

These equations are constrained by the conditions that define a convex combination:

$\sum_{i=0}^{N} \lambda_i = 1$

$\lambda_i \ge 0 \quad \forall i \in \{0, \dots, N\}$

Geometrically, these constraints alone define the **convex hull** of the set of breakpoint vertices $\{(p_i, C(p_i))\}$. For a convex function, a line segment (or chord) connecting any two points on its graph will always lie on or above the function's curve. This is a direct consequence of Jensen's inequality . The approximation $\hat{C}$ formed by taking a convex combination of the breakpoint costs is therefore an **overestimator** of the true cost function, meaning $\hat{C}(p) \ge C(p)$ for all $p$ in the domain .

To restrict the representation to the piecewise linear function itself (the boundary of the convex hull), rather than the entire convex hull, we must ensure that any point $(p, \hat{C})$ is a combination of at most two *adjacent* breakpoints. This is achieved by imposing a **Special Ordered Set of Type 2 (SOS2)** constraint on the ordered set of variables $\{\lambda_0, \lambda_1, \dots, \lambda_N\}$. An SOS2 constraint mandates that at most two variables in the set can be non-zero, and if two are non-zero, they must be adjacent in the specified order .

This single constraint elegantly enforces the desired piecewise linear structure. For any $p$ in a segment $[p_k, p_{k+1}]$, the only feasible solution involves positive weights $\lambda_k$ and $\lambda_{k+1}$ such that $\lambda_k + \lambda_{k+1} = 1$. The resulting cost $\hat{C} = \lambda_k C(p_k) + \lambda_{k+1} C(p_{k+1})$ is precisely the linear interpolation of the cost between the two adjacent breakpoints . This formulation is powerful because it avoids the need for explicit binary variables and allows the variable $p$ to be used in other linear constraints of a larger model simply by substituting its definition in terms of the $\lambda_i$ variables.

#### The Incremental (Delta) Formulation and Choice of Slopes

An alternative approach is the **incremental formulation**, sometimes called the $\Delta$-formulation. Here, the total production $p$ is expressed as a sum of power increments across the segments:

$p = p_0 + \sum_{i=1}^{N} x_i$

where $x_i$ is a continuous variable representing the amount of power produced within segment $i$, bounded by $0 \le x_i \le p_i - p_{i-1}$. Contiguity must be enforced (e.g., using SOS2 logic or binary variables) to ensure that segment $i$ is only used if all preceding segments $j  i$ are full. The cost is then modeled as:

$\hat{C}(p) = C(p_0) + \sum_{i=1}^{N} m_i x_i$

This formulation highlights the critical role of the chosen segment slopes, $m_i$. Different choices for $m_i$ result in fundamentally different approximations :

1.  **Secant Slopes**: If the slopes are chosen to be the slopes of the secant lines connecting the breakpoints, $m_i = \frac{C(p_i) - C(p_{i-1})}{p_i - p_{i-1}}$, the resulting function $\hat{C}(p)$ is the piecewise linear interpolant that passes through all points $(p_i, C(p_i))$. As established earlier, for a convex function $C(p)$, this approximation is an **overestimator**, or an upper bound.

2.  **Left-Derivative Slopes**: If the slopes are chosen to be the derivatives of the true cost function at the start of each segment, $m_i = C'(p_{i-1})$, the approximation becomes a chain of tangent lines. A core property of convex functions is that they lie on or above any of their tangents. Consequently, this construction creates a piecewise linear **underestimator**, or a lower bound, for the true cost function $C(p)$.

#### The Epigraph Formulation

A third approach, closely related to the tangent-based underestimator, is the **epigraph formulation**. The epigraph of a function is the set of all points lying on or above its graph. For a convex function, this set is convex and can be described by the intersection of all half-spaces defined by its supporting tangent lines. In practice, we can approximate this by using a finite set of tangent lines at selected breakpoints $p_i$:

$y \ge C(p_i) + C'(p_i)(p - p_i) \quad \forall i \in \{0, \dots, N\}$

Here, $y$ is a variable representing the cost. This set of linear inequalities defines a convex piecewise linear underestimator of $C(p)$. When minimizing $y$ in an optimization problem, the solution will be driven down to the tightest of these bounds, effectively tracing the lower envelope formed by these tangents . This method is powerful because it requires neither binary variables nor special ordered sets and is naturally suited for convex functions .

### A Comparative Analysis for MILP Modeling

The choice of formulation has significant implications for solver performance. A crucial concept in MILP is the **strength of the linear programming (LP) relaxation**. This refers to how closely the feasible region of the problem, after relaxing all integrality constraints (e.g., binaries become continuous in $[0,1]$), approximates the true convex hull of integer solutions. A tighter relaxation provides better objective bounds and enables the solver to prune the search tree more effectively.

When modeling a convex cost function, the SOS2-based convex combination formulation is considered an **ideal formulation** . Its LP relaxation (achieved by simply ignoring the SOS2 adjacency rule) defines the convex hull of the function's graph. Since the function is already convex, its graph forms the lower boundary of this hull. Therefore, when minimizing cost, the solution to the LP relaxation naturally falls on the piecewise linear curve, providing a very strong (tight) bound.

In contrast, a common alternative to SOS2 involves using binary variables $y_k$ to select which single segment is active, often implemented with so-called **big-M constraints**. The LP relaxation of a big-M formulation is notoriously weak. When the binary variables become fractional, the big-M terms effectively disable the constraints, creating a much larger relaxed feasible region that allows the cost to be significantly underestimated. This results in poor objective bounds and often leads to much longer solve times .

Furthermore, modern MILP solvers have specialized algorithms for handling SOS2 constraints. Instead of naive branching on individual variables, they employ **specialized branching** strategies that divide the ordered set, which is typically more efficient than branching on individual binary variables in a big-M model [@problem_id:4111511, @problem_id:4111572]. In terms of model size, the SOS2 formulation adds $\mathcal{O}(N)$ continuous variables, whereas the binary formulation adds $\mathcal{O}(N)$ integer variables, which are generally more computationally expensive.

### Practical Considerations in Model Design

Beyond the choice of formulation, two practical questions arise: how many segments are needed, and where should the breakpoints be placed?

#### The Trade-off Between Accuracy and Computation

Increasing the number of linear segments, $k$, will always improve the accuracy of the approximation, reducing the gap between the piecewise linear function $\hat{C}(p)$ and the true curve $C(p)$. However, each additional segment introduces more variables and/or constraints, making the resulting MILP more complex and time-consuming to solve. This creates a critical trade-off between model fidelity and computational tractability.

A pragmatic approach to managing this trade-off is to perform a marginal analysis . One can empirically measure the reduction in approximation error (the marginal benefit) against the increase in solver time (the marginal cost) for each added segment. A rational stopping rule is to continue adding segments only as long as the "return on investment" is above a certain threshold. For example, one could stop at the smallest number of segments $k$ where the ratio of gap reduction to the additional time required falls below a predefined tolerance $\theta$:

$\frac{G(k) - G(k+1)}{T(k+1) - T(k)} \le \theta$

Here, $G(k)$ is the approximation error with $k$ segments and $T(k)$ is the corresponding solve time. This ensures that the computational effort is spent where it yields the most significant improvements in accuracy.

#### Optimal Breakpoint Placement

For a fixed number of segments, the accuracy of the approximation depends heavily on the placement of the breakpoints. The error of linear interpolation is highest in regions where the function's curvature is greatest. The standard error bound for linear interpolation on an interval of length $h_i$ shows that the maximum error is approximately proportional to $h_i^2 \max(C''(p))$ on that interval.

To minimize the worst-case error across the entire domain (a minimax objective), the ideal strategy is to place breakpoints such that the maximum error on each segment is equalized. This leads to the optimal condition that segment lengths should be inversely proportional to the square root of the local curvature :

$h_i \propto \frac{1}{\sqrt{C''(p)}}$

This means placing more breakpoints (shorter segments) in regions of high curvature and fewer breakpoints (longer segments) where the function is flatter.

Common heuristics for breakpoint placement include:
- **Uniform-in-power spacing**: Here, all segments have the same length in power, $h_i = \text{constant}$. This is simple but non-adaptive, and its worst-case error is dictated entirely by the region with the highest curvature.
- **Uniform-in-marginal-cost spacing**: Here, breakpoints are chosen so that the change in marginal cost, $C'(p_{i+1}) - C'(p_i)$, is constant across segments. By the Mean Value Theorem, this implies that $h_i \propto 1/C''(p)$. This scheme is adaptive, as it places more points where curvature is high. While not minimax-optimal, it often yields a significantly lower [worst-case error](@entry_id:169595) than the naive uniform-in-power scheme, especially for cost functions with highly variable curvature .

In conclusion, the [piecewise linear approximation](@entry_id:177426) of production costs is a rich and essential topic in energy systems modeling. A thorough understanding of the underlying principles of convexity, the mechanisms of different optimization formulations, and the practical trade-offs in model design is crucial for building accurate, efficient, and reliable energy system models.