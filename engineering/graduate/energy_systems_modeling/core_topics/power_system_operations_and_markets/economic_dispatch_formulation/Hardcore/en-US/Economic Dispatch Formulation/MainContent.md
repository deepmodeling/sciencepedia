## Introduction
The efficient and reliable operation of modern power grids hinges on solving a fundamental optimization problem: how to dispatch available generators to meet electricity demand at the lowest possible cost. This problem, known as Economic Dispatch (ED), is a cornerstone of energy [systems engineering](@entry_id:180583) and economics. While the basic concept appears straightforward, its formulation and solution involve a rich interplay of [optimization theory](@entry_id:144639), economic principles, and practical engineering constraints. This article addresses the need for a comprehensive understanding that bridges the foundational theory of ED with its complex, real-world applications. It is designed to guide you from first principles to the sophisticated models that shape modern electricity markets and grid operations.

The journey begins in the "Principles and Mechanisms" chapter, where we will construct the canonical [economic dispatch problem](@entry_id:195771), explore its mathematical properties like convexity, and derive the pivotal principle of equal incremental cost from the KKT [optimality conditions](@entry_id:634091). We will also uncover the deep economic meaning behind Lagrange multipliers. Next, the "Applications and Interdisciplinary Connections" chapter demonstrates how this foundational model is extended to solve practical challenges, from incorporating transmission network constraints in Optimal Power Flow (OPF) to ensuring grid reliability with Security-Constrained Economic Dispatch (SCED) and integrating new technologies and environmental policies. Finally, the "Hands-On Practices" section provides a series of targeted exercises that allow you to apply these concepts, cementing your understanding by solving dispatch problems with increasing levels of complexity.

## Principles and Mechanisms

The formulation of the Economic Dispatch (ED) problem is a cornerstone of power system operations, representing a foundational exercise in constrained optimization. This chapter delineates the core principles that govern the ED problem, beginning with its canonical formulation and the mathematical properties that ensure a well-posed problem. We will then explore the elegant economic interpretations that arise from the [optimality conditions](@entry_id:634091) of convex dispatch models, before extending the framework to account for practical complexities such as transmission losses and non-convex operating characteristics.

### The Canonical Economic Dispatch Problem

At its heart, the [economic dispatch problem](@entry_id:195771) addresses the question: for a given set of online generating units, what power output should each unit produce to meet the system's total electricity demand at the minimum possible cost? To formalize this, we define the objective function and the constraints that constitute the problem.

The **decision variables** are the real power outputs, denoted by $P_i$, for each generator $i$ in a set of $N$ available units. The objective is to minimize the total cost of generation, which is the sum of the individual cost functions $C_i(P_i)$ for each generator.

$$
\text{Minimize} \quad C_{total} = \sum_{i=1}^{N} C_i(P_i)
$$

This cost minimization is subject to two primary types of constraints: a system-wide power balance and individual generator limits.

**Power Balance Constraint**

The most fundamental constraint is the requirement that the total power generated must equal the total power consumed. For a simplified "copper plate" model where the transmission network is represented as a single, lossless node, this principle is a direct consequence of the conservation of energy. In a steady-state AC system, Kirchhoff's Current Law (KCL) dictates that the sum of all complex currents injecting into the node must be zero. This leads directly to a balance of [complex power](@entry_id:1122734), and consequently, a balance of real power . Assuming an inelastic demand $D$ and no transmission losses, this is expressed as an equality constraint:

$$
\sum_{i=1}^{N} P_i = D
$$

This single equation couples the decisions for all generators, making the ED problem a system-wide optimization rather than a series of independent decisions.

**Generator Capacity Constraints**

Each generator has physical limitations on its power output. There is a minimum stable generation level, $P_i^{\min}$, and a maximum capacity, $P_i^{\max}$. The output $P_i$ must lie within this range. These are represented by a set of **[box constraints](@entry_id:746959)**:

$$
P_i^{\min} \le P_i \le P_i^{\max} \quad \text{for all } i \in \{1, \dots, N\}
$$

Combining these elements, the canonical [economic dispatch problem](@entry_id:195771) is formulated as the following [continuous optimization](@entry_id:166666) problem :

$$
\begin{align*}
\text{minimize} \quad & \sum_{i=1}^N C_i(P_i) \\
\text{subject to} \quad & \sum_{i=1}^N P_i = D \\
& P_i^{\min} \le P_i \le P_i^{\max}, \quad i=1, \dots, N
\end{align*}
$$

### Mathematical Properties of the Dispatch Problem

The tractability and properties of the ED problem are determined by the mathematical characteristics of the cost functions and the feasible set.

#### Convexity in Economic Dispatch

An optimization problem is defined as **convex** if it involves minimizing a convex objective function over a convex feasible set. This property is paramount because it guarantees that any locally [optimal solution](@entry_id:171456) is also a globally [optimal solution](@entry_id:171456).

The feasible set of the ED problem, defined by the affine power balance equality and linear [box constraints](@entry_id:746959), is always a **[convex set](@entry_id:268368)**. Therefore, the convexity of the ED problem hinges entirely on the nature of the total cost function, $C_{total} = \sum_{i=1}^N C_i(P_i)$. Since the sum of [convex functions](@entry_id:143075) is itself convex, the ED problem is convex if and only if each individual generator cost function, $C_i(P_i)$, is convex .

In practice, generator cost functions, which model the fuel consumption or [heat rate](@entry_id:1125980), are often approximated by [convex functions](@entry_id:143075), such as quadratic polynomials ($C_i(P_i) = \alpha_i P_i^2 + \beta_i P_i + \gamma_i$ with $\alpha_i > 0$) or increasing piecewise linear functions.

#### Existence of an Optimal Solution

Beyond [convexity](@entry_id:138568), we must also be assured that an optimal solution exists. The **Weierstrass Extreme Value Theorem** provides a powerful guarantee: a continuous function on a nonempty, compact (i.e., closed and bounded) set will always attain a minimum.

In the ED problem:
1.  The feasible set is defined by [linear constraints](@entry_id:636966), making it a [closed set](@entry_id:136446). The [box constraints](@entry_id:746959) $P_i^{\min} \le P_i \le P_i^{\max}$ ensure the set is also bounded. A closed and bounded set in $\mathbb{R}^N$ is compact.
2.  The feasible set is nonempty provided the demand $D$ is serviceable, i.e., $\sum_{i=1}^N P_i^{\min} \le D \le \sum_{i=1}^N P_i^{\max}$.
3.  If the cost functions $C_i(P_i)$ are continuous, their sum is also continuous.

Under these standard conditions—continuous convex costs and a serviceable demand—the ED problem is a [convex optimization](@entry_id:137441) problem with a guaranteed optimal solution . More general conditions also ensure existence, such as a lower semicontinuous objective function on a [compact set](@entry_id:136957), or a coercive objective function on a [closed set](@entry_id:136446) .

### Optimality Conditions and Economic Interpretation for Convex Dispatch

For a convex ED problem, the Karush-Kuhn-Tucker (KKT) conditions provide a set of [necessary and sufficient conditions](@entry_id:635428) for optimality. These mathematical conditions give rise to a profound economic interpretation of the optimal dispatch.

#### The Principle of Equal Incremental Cost

Consider the common case of strictly convex, differentiable cost functions (e.g., quadratic). The Lagrangian function for the ED problem can be formulated to analyze the [optimality conditions](@entry_id:634091). The [stationarity condition](@entry_id:191085) derived from the KKT analysis yields a fundamental economic principle. Let the **incremental cost** (or marginal cost) of a generator be the derivative of its cost function, $\lambda_i(P_i) := \frac{dC_i}{dP_i}$. At the optimal solution, the incremental costs of all generators that are not operating at their minimum or maximum limits must be equal to a common value .

$$
\frac{dC_1}{dP_1}(P_1^*) = \frac{dC_2}{dP_2}(P_2^*) = \dots = \frac{dC_k}{dP_k}(P_k^*) = \lambda^*
$$

This common value, $\lambda^*$, is the Lagrange multiplier associated with the power balance constraint.

Intuitively, this makes sense. If two unconstrained generators had different incremental costs, say $\lambda_i > \lambda_j$, one could decrease the total system cost by slightly reducing the output of the more expensive unit $i$ and increasing the output of the cheaper unit $j$ by the same amount, while still satisfying the demand. This process can continue until their incremental costs are equalized. For generators operating at their limits, this equalization is not possible:
*   A generator at its maximum limit ($P_i = P_i^{\max}$) will have an incremental cost less than or equal to $\lambda^*$ ($\frac{dC_i}{dP_i} \le \lambda^*$). It is too "cheap" at its maximum output to be backed down.
*   A generator at its minimum limit ($P_i = P_i^{\min}$) will have an incremental cost greater than or equal to $\lambda^*$ ($\frac{dC_i}{dP_i} \ge \lambda^*$). It is too "expensive" at its minimum output to be ramped up.

#### The Economic Meaning of Lagrange Multipliers

The Lagrange multipliers in the ED problem are not just mathematical artifacts; they are **[shadow prices](@entry_id:145838)** that quantify the marginal value of their associated constraints.

The multiplier on the power balance constraint, $\lambda^*$, is the **system marginal cost** (or [locational marginal price](@entry_id:1127410) in a single-node system). It represents the cost to the system of supplying one additional infinitesimal unit (e.g., a megawatt) of demand. According to the envelope theorem, the derivative of the minimized total cost with respect to demand is precisely this multiplier, $\frac{dC_{total}^*}{dD} = \lambda^*$  .

Similarly, the multipliers associated with the generator capacity constraints, often denoted $\mu_i^+$ and $\mu_i^-$, represent the [shadow prices](@entry_id:145838) of capacity. For example, $\mu_i^+$ quantifies the reduction in total system cost that would be achieved by relaxing the maximum output limit $P_i^{\max}$ by one unit. It is a measure of the economic value of that constrained capacity, often referred to as a **scarcity rent** .

#### Duality, Markets, and Piecewise Linear Costs

For a [convex optimization](@entry_id:137441) problem satisfying certain regularity conditions (like Slater's condition, which holds for ED if a strictly [feasible solution](@entry_id:634783) exists), **[strong duality](@entry_id:176065)** is guaranteed. This means the optimal value of the primal problem (minimizing cost) is equal to the optimal value of its Lagrangian [dual problem](@entry_id:177454). There is no "[duality gap](@entry_id:173383)" .

This duality has a powerful market interpretation. The optimal Lagrange multiplier $\lambda^*$ acts as the **market-clearing price**. If this price were announced to the generators, and each generator, as an independent, price-taking agent, acted to maximize its own profit ($\text{profit}_i = \lambda^* P_i - C_i(P_i)$), the resulting power outputs would precisely match the optimal dispatch found by the centralized cost-minimization problem. This equivalence establishes a fundamental link between centralized planning and decentralized, competitive market outcomes .

This concept is particularly clear when using **piecewise linear cost functions**. A generator's convex piecewise linear cost function can be seen as a series of supply blocks, each with a quantity ($\Delta_{ik}$) and a price ($\alpha_{ik}$). The ED problem then becomes a linear program. The KKT conditions for this LP formalize the concept of a **merit-order dispatch**: the system accepts the cheapest blocks from across all generators in increasing order of price until demand is met. The price of the last block accepted sets the system marginal price $\lambda^*$, which is the optimal Lagrange multiplier on the power balance constraint .

### Practical Extensions to the Basic Model

The canonical ED formulation provides the foundation, but practical models often include additional complexities.

#### Incorporating Transmission Losses

In a real power system, transporting electricity over transmission lines incurs real power losses, primarily due to Joule heating ($I^2R$). The power balance equation must be modified to account for these losses, $P_L$:

$$
\sum_{i=1}^{N} P_i = D + P_L
$$

The complication is that $P_L$ is itself a complex, nonlinear function of all generator outputs. A classic method to handle this is the **Kron loss formula**, or B-coefficient method. This approach approximates the total loss as a quadratic function of the generator power outputs based on a linearization around a specific base-case operating point :

$$
P_L = \sum_{i=1}^N \sum_{j=1}^N P_i B_{ij} P_j + \sum_{i=1}^N B_{0i} P_i + B_{00}
$$

The **B-coefficients** ($B_{ij}, B_{0i}, B_{00}$) are treated as constants and encapsulate network physics under a set of strong assumptions, including a fixed network topology, fixed bus voltage magnitudes, and constant power factors for all injections. While an approximation, including this quadratic loss term preserves the [convexity](@entry_id:138568) of the ED problem (if the resulting cost function remains convex) but complicates the optimality condition, leading to a system of equations that must be solved iteratively.

#### Economic Dispatch versus Unit Commitment

It is crucial to distinguish [economic dispatch](@entry_id:143387) from the related but more complex **unit commitment (UC)** problem. ED assumes the set of online generators is fixed and determines their optimal output levels over a short interval (e.g., 5-15 minutes). UC, in contrast, is a planning problem over a longer horizon (e.g., a day or a week) that decides which units to turn on or off.

UC is a large-scale, mixed-integer optimization problem that includes:
*   **Binary variables** to model the on/off status of each unit in each time period.
*   **Start-up and shut-down costs**, which are fixed costs incurred when changing a unit's status.
*   **Intertemporal constraints** that link decisions across time, such as [ramping limits](@entry_id:1130533) (how fast a unit can change its output), minimum up-times, and minimum down-times.

ED can be seen as a subproblem within the UC framework: once the UC problem determines which units are online in a given hour, ED determines their precise output levels .

### Formulating and Solving Non-Convex Economic Dispatch Problems

While convex models are analytically convenient, real-world generator cost functions can exhibit non-convexities, fundamentally changing the nature of the optimization problem.

#### Valve-Point Effects: Modeling and Consequences

Large steam turbines admit steam through several valves that open sequentially to increase power output. Each time a valve is first opened, it causes a throttling loss that results in a temporary decrease in efficiency. This phenomenon is modeled by adding a "rippling" sinusoidal term to the smooth, convex quadratic cost function :

$$
C_i(P_i) = (\alpha_i P_i^2 + \beta_i P_i + \gamma_i) + |e_i \sin(f_i(P_i^{\min} - P_i))|
$$

The absolute value and sine function introduce two critical issues:
1.  **Non-[convexity](@entry_id:138568):** The oscillating term creates regions where the function's second derivative is negative, meaning the cost function is no longer convex.
2.  **Non-smoothness:** The [absolute value function](@entry_id:160606) creates "cusps" or points of non-[differentiability](@entry_id:140863) where its argument passes through zero.

The consequence of a non-convex objective function is profound: the problem may now have **multiple local minima**. For such problems, the KKT conditions are no longer sufficient for global optimality; they can only identify candidate points (local minima, local maxima, or saddle points). To find the global optimum, one must potentially identify all local minima and compare their cost values . Furthermore, non-convex problems may exhibit a **non-zero [duality gap](@entry_id:173383)**, meaning that solution methods based on Lagrangian duality may only provide a lower bound on the true minimum cost .

#### Prohibited Operating Zones

For mechanical or environmental reasons, a generator may have certain output ranges, or **prohibited operating zones (POZs)**, where continuous operation is forbidden. This means the [feasible operating region](@entry_id:1124878) for a generator is a union of disjoint intervals, e.g., $P_i \in [P_i^{\min}, \underline{P}_{i,POZ}] \cup [\overline{P}_{i,POZ}, P_i^{\max}]$.

This disjunctive constraint makes the feasible set of the ED problem non-convex. Such problems cannot be solved with standard convex [optimization algorithms](@entry_id:147840). The standard approach is to reformulate the problem as a **Mixed-Integer Program**. By introducing a binary variable $y_{ik}$ for each feasible operating interval $k$ of generator $i$, we can model the choice of interval. The constraint $\sum_k y_{ik} = 1$ ensures that exactly one interval is chosen. The power output $P_i$ is then linked to the bounds of the chosen interval using [linear constraints](@entry_id:636966) involving the $y_{ik}$ variables . This transforms the problem into a **Mixed-Integer Quadratic Program (MIQP)**, which can be solved to global optimality using sophisticated solvers that employ algorithms like [branch-and-bound](@entry_id:635868).