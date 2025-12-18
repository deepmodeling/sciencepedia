## Introduction
Integer programming is a powerful framework for modeling real-world problems with discrete decisions, from logistical planning to [financial modeling](@entry_id:145321). However, the inherent computational difficulty of finding optimal integer solutions presents a significant challenge. The standard approach is to first solve a simplified version of the problem, the [linear programming](@entry_id:138188) (LP) relaxation, which often yields fractional, non-implementable solutions. This creates a gap between the tractable relaxed problem and the difficult original problem. Valid inequalities are the fundamental tools used to bridge this gap.

This article provides a comprehensive exploration of valid inequalities, the cornerstone of modern integer optimization. You will learn how these mathematical constraints systematically refine a loose LP relaxation, guiding the solver toward an optimal integer solution. The journey begins in the "Principles and Mechanisms" chapter, where we will uncover the geometric intuition behind valid inequalities, classify their strength, and explore systematic generation procedures like the [cutting plane method](@entry_id:636911). Following this, the "Applications and Interdisciplinary Connections" chapter will demonstrate the remarkable versatility of these concepts, showing how they are used to model complex structures in scheduling, network design, machine learning, and beyond. Finally, the "Hands-On Practices" section offers a chance to apply these theoretical insights to practical problems, challenging you to identify and generate your own effective cuts.

## Principles and Mechanisms

In the study of [integer programming](@entry_id:178386), a central challenge arises from the computational difficulty of finding optimal solutions directly. A primary strategy involves solving a more tractable problem, the **linear programming (LP) relaxation**, and systematically refining it until an integer solution is found. The primary tools for this refinement are **valid inequalities**. This chapter delves into the principles that define valid inequalities and the mechanisms by which they are generated and applied to strengthen optimization models.

### The Geometry of Valid Inequalities

To understand valid inequalities, we must first appreciate the geometry of integer optimization. Consider an integer program (IP) whose feasible solutions form a discrete set of points, which we will denote by $S$. For example, $S = \{x \in \{0,1\}^n : Ax \leq b\}$. The optimization problem is to find a point in $S$ that maximizes or minimizes a linear [objective function](@entry_id:267263). While optimizing over the discrete set $S$ is computationally hard, optimizing a linear function over a convex set is relatively easy. This motivates the concept of the **[convex hull](@entry_id:262864)** of $S$, denoted $\text{conv}(S)$, which is the smallest convex set containing all points in $S$. A fundamental theorem of [integer programming](@entry_id:178386) states that the [optimal solution](@entry_id:171456) to the IP is one of the vertices of $\text{conv}(S)$. Therefore, if we could describe $\text{conv}(S)$ with a system of linear inequalities, we could solve the IP as a standard linear program.

In practice, obtaining a full description of $\text{conv}(S)$ is usually as hard as solving the original IP. Instead, we start with the LP relaxation, whose feasible set, $P_{LP}$, is obtained by relaxing the integrality constraints (e.g., $x_i \in \{0,1\}$ becomes $0 \leq x_i \leq 1$). This relaxation always contains the convex hull, such that $S \subseteq \text{conv}(S) \subseteq P_{LP}$. The goal of adding valid inequalities is to "trim" the larger set $P_{LP}$ to better approximate the true convex hull, $\text{conv}(S)$.

A **[valid inequality](@entry_id:170492)** for an integer program is any [linear inequality](@entry_id:174297) that is satisfied by all feasible integer solutions in $S$. By definition, if an inequality is valid for all points in $S$, it must also be valid for their convex hull, $\text{conv}(S)$.

The relationship between a [valid inequality](@entry_id:170492) and the convex hull can be categorized by its geometric proximity to $\text{conv}(S)$. This hierarchy is crucial for understanding the "quality" or "strength" of an inequality.

*   A **[valid inequality](@entry_id:170492)** $a^{\top}x \leq \beta$ is one for which all points $x \in \text{conv}(S)$ satisfy the inequality. If the hyperplane $H = \{x : a^{\top}x = \beta\}$ has no points in common with $\text{conv}(S)$, the inequality is valid but **not supporting**. It correctly constrains the feasible region but does not define any of its boundaries.

*   A [valid inequality](@entry_id:170492) is **supporting** if the hyperplane $H$ intersects $\text{conv}(S)$. The set of points in this intersection, $F = \text{conv}(S) \cap H$, is called a **face** of the [convex hull](@entry_id:262864).

*   A supporting inequality is **facet-defining** if the face $F$ it defines has a dimension of $\text{dim}(\text{conv}(S)) - 1$. Facets are the highest-dimensional faces of a [polytope](@entry_id:635803), other than the polytope itself. These are the "strongest" possible valid inequalities, as they define the boundary of the [convex hull](@entry_id:262864). The ultimate goal of this approach is to identify the set of all facet-defining inequalities of $\text{conv}(S)$.

To make these concepts concrete, consider the simple polyhedron $P = \{ (x_1, x_2) : x_1 \geq 0, x_2 \geq 0, x_1 + x_2 \leq 1 \}$, which is the [convex hull](@entry_id:262864) of the integer points $(0,0)$, $(1,0)$, and $(0,1)$ . This polyhedron is a two-dimensional triangle in $\mathbb{R}^2$.
*   The inequality $x_1 + x_2 \leq 1$ is **facet-defining**. It is valid for all points in the triangle. The face it defines is the set of points where $x_1 + x_2 = 1$, which is the line segment connecting $(1,0)$ and $(0,1)$. This is a face of dimension 1, which is $\text{dim}(P) - 1$.
*   The inequality $-x_1 - x_2 \leq 0$ (or $x_1 + x_2 \geq 0$) is **supporting but not facet-defining**. It is valid since all points in the triangle have non-negative coordinates. The face it defines is the set of points where $x_1 + x_2 = 0$, which for this polyhedron is only the single point $(0,0)$. The dimension of a single point is 0, which is not $\text{dim}(P) - 1$.
*   The inequality $x_1 + x_2 \leq 2$ is **valid but not supporting**. Every point in the triangle satisfies this, since the maximum value of $x_1+x_2$ on the set is $1$. However, the [hyperplane](@entry_id:636937) $x_1 + x_2 = 2$ never touches the triangle, so the inequality does not define any of its boundaries.

### The Mechanism of Cutting Planes

Valid inequalities are operationalized through a methodology known as the **[cutting plane method](@entry_id:636911)**. The process begins by solving the LP relaxation of an integer program. If the optimal solution, $x^*_{LP}$, is integer-feasible, then it is also the [optimal solution](@entry_id:171456) to the original IP. However, if $x^*_{LP}$ is fractional, it is not a valid solution to the IP. In this case, we seek to add one or more valid inequalities that are violated by $x^*_{LP}$ but are satisfied by all feasible integer solutions. These inequalities are called **[cutting planes](@entry_id:177960)** or **cuts** because they "cut off" the fractional solution from the feasible region of the relaxation, tightening the approximation of the convex hull.

Consider a simple zero-one program with the objective to maximize $x_1+x_2+x_3$ subject to a set of constraints that lead to an LP relaxation optimum at the fractional point $\hat{x} = (0.5, 0.5, 0.5)$, with an objective value of $1.5$ . The feasible integer solutions to this problem are only $(0,0,0), (1,0,0), (0,1,0)$, and $(0,0,1)$. We can observe that for all these integer points, the sum of the variables is at most 1. This suggests the inequality $x_1 + x_2 + x_3 \leq 1$ is a [valid inequality](@entry_id:170492). Crucially, the fractional solution $\hat{x}$ violates this inequality, since $0.5 + 0.5 + 0.5 = 1.5 > 1$.

By adding this single cut to the LP relaxation, we eliminate $\hat{x}$ from the feasible region. The new, augmented linear program now has an optimal objective value of $1$, achieved at the integer points $(1,0,0), (0,1,0)$, and $(0,0,1)$. In this instance, the addition of a single [valid inequality](@entry_id:170492) was sufficient to find the true integer optimum. This illustrates the power of [cutting planes](@entry_id:177960): they improve the objective bound of the relaxation (from $1.5$ to $1$) and guide the search toward an integer solution.

The effectiveness of a cut can be intuitively understood by its **violation** at the fractional point, or more formally, by the geometric distance it cuts off. A cut that is "deeper"—meaning the fractional point is further from the cutting [hyperplane](@entry_id:636937)—is often more effective at improving the LP relaxation . This also relates to the concept of **strength**; an inequality $a^{\top}x \leq b_1$ is stronger than $a^{\top}x \leq b_2$ if $b_1  b_2$, as it defines a smaller, more restrictive [feasible region](@entry_id:136622) .

### General Procedures for Generating Cuts

While some valid inequalities can be found by inspection, formal procedures are required for automated solvers. These procedures can be broadly divided into general-purpose methods that apply to any integer program and specialized methods that exploit specific problem structures.

#### Chvátal-Gomory Cuts

The **Chvátal-Gomory (CG) procedure** is a fundamental, general-purpose method for generating valid inequalities. It is based on two simple operations: non-negative linear combination and integer rounding. Given a system of inequalities $Ax \leq b$ that is valid for the LP relaxation, the procedure is as follows:

1.  **Aggregate:** Choose a vector of non-negative multipliers $\lambda \geq 0$ and form a linear combination of the inequalities: $\lambda^{\top}Ax \leq \lambda^{\top}b$. This aggregated inequality is also valid for the LP relaxation.

2.  **Round:** Since all feasible solutions $x$ must have integer components, the left-hand side $\lambda^{\top}Ax$ must satisfy $\lambda^{\top}Ax = (\sum_j (\lambda^{\top}A)_j x_j)$. If we round down the coefficients of $x$ on the left side, the value of the expression can only decrease for non-negative $x_j$. Specifically, for any integer vector $x \geq 0$, we have $\lfloor \lambda^{\top}A \rfloor x \leq \lambda^{\top}Ax$. Combining this with the aggregated inequality gives $\lfloor \lambda^{\top}A \rfloor x \leq \lambda^{\top}b$. Finally, since the left-hand side $\lfloor \lambda^{\top}A \rfloor x$ must be an integer, it cannot be greater than the right-hand side. Therefore, it must be less than or equal to the integer part of the right-hand side.

This yields the **Chvátal-Gomory cut**:
$$ \lfloor \lambda^{\top}A \rfloor x \leq \lfloor \lambda^{\top}b \rfloor $$
This inequality is guaranteed to be valid for all feasible integer solutions. The art of the CG procedure lies in choosing the multipliers $\lambda$ to generate a cut that is violated by the current fractional LP solution . Different choices of $\lambda$ can lead to cuts of varying strength, and finding the most effective cut is itself an optimization problem.

#### Split and Gomory Mixed-Integer Rounding (MIR) Cuts

For mixed-integer programs (MIPs), where some variables are integer and others are continuous, another powerful general principle is the **split disjunction**. For any integer variable $x_i$ and any integer $\pi$, any [feasible solution](@entry_id:634783) must satisfy either $x_i \leq \pi$ or $x_i \geq \pi+1$. This "splits" the [feasible region](@entry_id:136622) into two disjoint polyhedra. A **split cut** is any inequality that is valid for the convex hull of the union of these two [polyhedra](@entry_id:637910).

Consider a mixed-integer set defined by $3x_1 + x_2 \leq 4$, where $x_1 \in \{0,1\}$ and $x_2 \in [0,3]$ . The LP relaxation admits the fractional point $\hat{x}=(0.4, 2.4)$. We can apply the split disjunction on $x_1$: every feasible solution must satisfy either $x_1=0$ or $x_1=1$.
*   If $x_1=0$, the constraints become $x_2 \leq 4$ and $0 \leq x_2 \leq 3$, which simplifies to $0 \leq x_2 \leq 3$.
*   If $x_1=1$, the constraints become $3+x_2 \leq 4$ and $0 \leq x_2 \leq 3$, which simplifies to $0 \leq x_2 \leq 1$.

Any inequality that is valid for both the region where $x_1=0$ and $0 \leq x_2 \leq 3$, and the region where $x_1=1$ and $0 \leq x_2 \leq 1$, must be valid for the original MIP. The inequality $2x_1 + x_2 \leq 3$ satisfies this property. For the first region, it implies $x_2 \leq 3$, which holds. For the second region, it implies $2+x_2 \leq 3$, or $x_2 \leq 1$, which also holds. However, this split cut is violated by the fractional point $\hat{x}=(0.4, 2.4)$, since $2(0.4) + 2.4 = 3.2 > 3$.

The **Gomory Mixed-Integer Rounding (MIR)** inequality is a specific, widely-used class of split cut derived from a single-row constraint. For simple cases, it can be shown that the MIR cut is identical to the strongest cut obtainable from the split disjunction on that row .

### Problem-Specific Families of Valid Inequalities

While general procedures are powerful, a great deal of research in integer optimization has focused on identifying strong families of valid inequalities for specific, commonly occurring problem structures. These families often lead to facet-defining or near-facet-defining inequalities and are critical to the performance of modern solvers.

#### Knapsack Problems: Cover Inequalities

The [0-1 knapsack problem](@entry_id:262564) provides a canonical example of a problem-specific cut. The problem involves selecting items with given weights to maximize total value, subject to a single capacity constraint: $\sum w_i x_i \leq W$, where $x_i \in \{0,1\}$.

A **cover** is a set of items $C$ whose total weight exceeds the capacity: $\sum_{i \in C} w_i > W$. A cover is **minimal** if removing any single item from it makes it no longer a cover. Since it is impossible to select all items in a cover simultaneously, at most $|C|-1$ of them can be chosen. This gives rise to the **[cover inequality](@entry_id:634882)**:
$$ \sum_{i \in C} x_i \leq |C| - 1 $$
This simple inequality can be a powerful cut. However, it can be made even stronger through a process called **lifting**. Lifting involves incorporating variables not present in the original [cover inequality](@entry_id:634882) to tighten the constraint.

To lift a variable $x_j$ (where $j \notin C$) into the inequality, we derive a coefficient $\alpha_j$ such that $\sum_{i \in C} x_i + \alpha_j x_j \leq |C|-1$ remains valid . The coefficient $\alpha_j$ is determined by considering the case where $x_j=1$. When item $j$ is selected, the available capacity for the other items is reduced to $W - w_j$. We then find the maximum number of items from the original cover $C$ that can be selected with this reduced capacity. Let this number be $z_j$. The lifted inequality requires $\sum_{i \in C} x_i \leq |C|-1 - \alpha_j$. To make the inequality as strong as possible (i.e., maximize $\alpha_j$), we set $|C|-1 - \alpha_j = z_j$, which gives $\alpha_j = |C|-1 - z_j$. This sequential lifting procedure, when applied correctly, can transform a simple [cover inequality](@entry_id:634882) into a facet-defining inequality for the knapsack [polytope](@entry_id:635803) .

#### Set Packing Problems: Clique and Odd-Hole Inequalities

In the [set packing problem](@entry_id:636479), the goal is to select a maximum number of items subject to constraints that certain pairs of items cannot be selected together. These conflicts can be represented by a **[conflict graph](@entry_id:272840)**, where vertices represent items and edges connect incompatible pairs.

The most basic valid inequalities for set packing are **[clique](@entry_id:275990) inequalities** . A **[clique](@entry_id:275990)** in the [conflict graph](@entry_id:272840) is a set of vertices $Q$ where every pair is connected by an edge, meaning all items in $Q$ are mutually incompatible. Consequently, at most one item from a [clique](@entry_id:275990) can be chosen, leading to the [valid inequality](@entry_id:170492):
$$ \sum_{i \in Q} x_i \leq 1 $$
While fundamental, clique inequalities are often insufficient to define the convex hull. For example, if the [conflict graph](@entry_id:272840) is a chordless cycle of five vertices (a 5-hole), the maximal cliques are just the five edges. The LP relaxation with only these clique inequalities, $x_i + x_{i+1} \leq 1$, has an [optimal solution](@entry_id:171456) of $x_i=0.5$ for all $i$, with an objective value of $2.5$. However, it's easy to see that in a 5-cycle, at most two non-adjacent vertices can be selected, so the true integer optimum is 2.

This gap is closed by a stronger class of valid inequalities: **odd-hole inequalities**. For any odd, chordless cycle of length $2k+1$ in the [conflict graph](@entry_id:272840), the following inequality is valid:
$$ \sum_{i \in \text{Hole}} x_i \leq k $$
For the 5-cycle ($k=2$), this gives $\sum_{i=1}^5 x_i \leq 2$. This inequality cuts off the fractional solution $x_i=0.5$ and leads to an LP solution with the correct integer objective value of 2.

#### Traveling Salesman Problem: Subtour Elimination Constraints

The Traveling Salesman Problem (TSP) is one of the most famous problems in [combinatorial optimization](@entry_id:264983). A common relaxation for the symmetric TSP uses [binary variables](@entry_id:162761) $x_{ij}$ for each edge $\{i,j\}$ and enforces **degree constraints**: for each vertex $i$, the sum of selected edges connected to it must be two, i.e., $\sum_{j \neq i} x_{ij} = 2$.

This relaxation is notoriously weak because it permits solutions that consist of multiple disconnected cycles, known as **subtours**, which are not valid Hamiltonian cycles. To eliminate these, **[subtour elimination](@entry_id:637572) constraints (SECs)** are required . For any proper, non-empty subset of vertices $S \subset V$, an SEC takes the form:
$$ \sum_{i \in S, j \notin S} x_{ij} \geq 2 $$
The justification for this inequality is intuitive and elegant. Any valid tour is a single connected loop. As such, if the tour enters the set of vertices $S$, it must eventually leave $S$ to visit the remaining vertices. To complete the full tour, the path must ultimately return to its starting point. This implies that the number of times the tour crosses from outside $S$ to inside $S$ must equal the number of times it crosses from inside to outside. Since a tour must visit vertices both inside and outside any [proper subset](@entry_id:152276) $S$, there must be at least one entry and at least one exit. Thus, the total number of edges crossing the boundary of $S$ must be a positive even integer, meaning it must be at least 2. These inequalities effectively forbid disconnected subtours and are essential for solving the TSP.