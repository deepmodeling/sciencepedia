## Introduction
The simplex method provides a powerful, step-by-step procedure for solving linear programming problems by moving between [vertices of a feasible region](@entry_id:174284). But how does the algorithm intelligently choose its path? At the heart of this decision-making process lies the concept of **[reduced costs](@entry_id:173345)**, a measure that quantifies the potential for improvement at every step. This article addresses the fundamental question of how the simplex method evaluates and achieves optimality by dissecting the theory and application of [reduced costs](@entry_id:173345).

To build a complete understanding, we will explore this topic across three distinct chapters. The first, **Principles and Mechanisms**, will uncover the algebraic and geometric foundations of [reduced costs](@entry_id:173345), explaining how they are calculated and used to define the [simplex](@entry_id:270623) [optimality conditions](@entry_id:634091). Next, **Applications and Interdisciplinary Connections** will showcase the practical power of [reduced costs](@entry_id:173345), translating them into economic concepts like [shadow prices](@entry_id:145838) and demonstrating their role in [strategic decision-making](@entry_id:264875) across fields from finance to power grid management. Finally, **Hands-On Practices** will provide opportunities to apply these concepts, solidifying your intuition through targeted exercises that bridge theory and practical implementation.

## Principles and Mechanisms

Having established the foundational mechanics of the [simplex method](@entry_id:140334), which navigates from one vertex of the feasible polyhedron to an adjacent one, we now delve into the core decision-making engine of the algorithm. How does the simplex method "know" whether the current solution can be improved? And if so, which direction of movement promises such an improvement? The answers to these questions lie in the elegant concept of **[reduced costs](@entry_id:173345)**. This chapter will elucidate the principles and mechanisms of [reduced costs](@entry_id:173345), exploring their algebraic definition, their profound geometric and economic interpretations, and their role in determining optimality.

### The Reduced Cost: Quantifying Improvement

Imagine we are at a given Basic Feasible Solution (BFS), denoted by $x$. This solution is partitioned into basic variables, $x_B$, and nonbasic variables, $x_N$, where all nonbasic variables are set to zero. The objective function is $z = c^T x = c_B^T x_B + c_N^T x_N$. To see how the objective value changes as we move away from this vertex, we must express $z$ solely in terms of the nonbasic variables, which act as the independent drivers of any change.

From the standard form constraints $Ax = b$, we have the partitioned system $A_B x_B + A_N x_N = b$. Since the [basis matrix](@entry_id:637164) $A_B$ is invertible, we can express the basic variables in terms of the nonbasic ones:
$$
x_B = A_B^{-1} b - A_B^{-1} A_N x_N
$$
The first term, $A_B^{-1} b$, is simply the value of the basic variables at the current BFS. The second term shows how the basic variables must adjust to maintain feasibility as the nonbasic variables are increased from zero.

Substituting this expression for $x_B$ into the objective function yields:
$$
z = c_B^T (A_B^{-1} b - A_B^{-1} A_N x_N) + c_N^T x_N
$$
Rearranging this equation separates the constant term from the terms involving the nonbasic variables:
$$
z = c_B^T A_B^{-1} b + (c_N^T - c_B^T A_B^{-1} A_N) x_N
$$
This equation is the key to understanding the [simplex method](@entry_id:140334)'s logic. The term $z_0 = c_B^T A_B^{-1} b$ is the [objective function](@entry_id:267263) value at the current BFS. The vector of coefficients, $(c_N^T - c_B^T A_B^{-1} A_N)$, tells us exactly how $z$ changes as we change the values of the nonbasic variables in $x_N$.

To formalize this, we first define the vector of **[simplex multipliers](@entry_id:177701)** (also known as **dual variables** or **shadow prices**), denoted by the row vector $y^T$, associated with the current basis:
$$
y^T = c_B^T A_B^{-1}
$$
With this definition, the [objective function](@entry_id:267263) becomes:
$$
z = z_0 + (c_N^T - y^T A_N) x_N
$$
The coefficient of each nonbasic variable $x_j$ (where $j$ is a nonbasic index) in this expression is called its **[reduced cost](@entry_id:175813)**, denoted $\bar{c}_j$. Formally, for any variable $x_j$ (basic or nonbasic), its [reduced cost](@entry_id:175813) is defined as:
$$
\bar{c}_j = c_j - y^T A_j
$$
where $A_j$ is the $j$-th column of the constraint matrix $A$.

By definition, the [reduced costs](@entry_id:173345) of the basic variables are always zero. This is because $y^T A_B = (c_B^T A_B^{-1}) A_B = c_B^T$, so for any basic index $j \in B$, we have $\bar{c}_j = c_j - y^T A_j = 0$. For nonbasic variables $j \in N$, the [reduced cost](@entry_id:175813) $\bar{c}_j$ is the rate of change of the objective function $z$ with respect to a unit increase in $x_j$. The [objective function](@entry_id:267263) can be written compactly as:
$$
z = z_0 + \sum_{j \in N} \bar{c}_j x_j
$$
This shows that the [reduced cost](@entry_id:175813) of a nonbasic variable is precisely the quantity we need to decide which variable, if any, should enter the basis to improve the objective value.

A concrete calculation illustrates this fundamental process. Consider a maximization problem with a given basis $B = \{2,4,5\}$ [@problem_id:3171547]. To assess this basis, one would first form the [basis matrix](@entry_id:637164) $A_B$ and the basic cost vector $c_B$. The [simplex multipliers](@entry_id:177701) $y^T$ are found by solving the system $y^T A_B = c_B^T$. Once $y^T$ is known, the [reduced cost](@entry_id:175813) for each nonbasic variable, for instance $\bar{c}_1$, is computed as $\bar{c}_1 = c_1 - y^T A_1$. The sign of this value will then determine if increasing $x_1$ from zero is a profitable move.

### The Simplex Optimality Conditions

The relationship $z = z_0 + \sum_{j \in N} \bar{c}_j x_j$ immediately gives us the conditions for determining if a BFS is optimal. These conditions depend on whether we are maximizing or minimizing the objective.

For a **maximization problem**, our goal is to increase $z$. If we find a nonbasic variable $x_j$ with a positive [reduced cost](@entry_id:175813) ($\bar{c}_j > 0$), increasing $x_j$ from zero will increase the total objective value $z$. Therefore, the current solution cannot be optimal. An optimal solution is reached only when no such improvement is possible.

*   **Optimality Condition for Maximization**: A basic [feasible solution](@entry_id:634783) is optimal if and only if all [reduced costs](@entry_id:173345) are non-positive, i.e., $\bar{c}_j \le 0$ for all variables $j$. Since basic variables always have $\bar{c}_j=0$, this condition applies specifically to the nonbasic variables.

Conversely, for a **minimization problem**, our goal is to decrease $z$. If we find a nonbasic variable $x_j$ with a negative [reduced cost](@entry_id:175813) ($\bar{c}_j < 0$), increasing $x_j$ from zero will decrease $z$. Thus, the solution is not optimal.

*   **Optimality Condition for Minimization**: A basic [feasible solution](@entry_id:634783) is optimal if and only if all [reduced costs](@entry_id:173345) are non-negative, i.e., $\bar{c}_j \ge 0$ for all variables $j$.

It is crucial to note the symmetry between maximization and minimization. The problem of maximizing $c^T x$ is mathematically equivalent to minimizing $(-c)^T x$. If we consider the same basis for both problems, the [reduced cost](@entry_id:175813) for the minimization problem, let's call it $\bar{c}_j'$, is calculated using the cost vector $-c$:
$$
\bar{c}_j' = (-c_j) - (-c_B)^T A_B^{-1} A_j = -(c_j - c_B^T A_B^{-1} A_j) = -\bar{c}_j
$$
Thus, changing the objective from maximization to minimization simply flips the sign of all [reduced costs](@entry_id:173345) [@problem_id:3171554]. The set of optimal solutions remains the same, but the optimality condition on the sign of the [reduced costs](@entry_id:173345) is reversed, as expected.

### Uniqueness, Alternate Optima, and the Optimal Face

The [reduced costs](@entry_id:173345) at an [optimal solution](@entry_id:171456) do more than just confirm optimality; they also reveal whether the optimal solution is unique. The set of all optimal solutions to an LP forms a **face** of the feasible polyhedron (which could be a vertex, an edge, or a higher-dimensional face).

If, at an optimal BFS for a maximization problem, all nonbasic variables have **strictly negative** [reduced costs](@entry_id:173345) ($\bar{c}_j < 0$ for all $j \in N$), then increasing any nonbasic variable would necessarily decrease the objective function. This means that any move away from the current vertex leads to a strictly worse solution. Provided the optimal BFS is non-degenerate (i.e., all basic variables are strictly positive), this is a [sufficient condition](@entry_id:276242) to guarantee that the solution is the **unique optimal solution** [@problem_id:3171548]. The optimal face is a single point (a vertex), having dimension zero.

The more interesting case arises when an optimal BFS has one or more nonbasic variables with a **zero [reduced cost](@entry_id:175813)**. Suppose for a nonbasic variable $x_k$, we have $\bar{c}_k = 0$. This indicates that we can potentially increase $x_k$ from zero without changing the [objective function](@entry_id:267263) value. If we can increase $x_k$ by a strictly positive amount before a basic variable drops to zero (i.e., the pivot is non-degenerate), we will move along an edge of the feasible set to a new, distinct BFS that has the same optimal objective value. This signals the existence of **alternate optimal solutions**.

The set of all optimal solutions is the convex hull of all optimal BFSs. For instance, if two products in a manufacturing problem have the same maximum revenue-to-resource ratio, it might be possible to produce either one or any feasible combination of the two, all yielding the same maximum revenue [@problem_id:3171559]. When this occurs, the optimal face is an edge or a higher-dimensional face of the polyhedron.

In a remarkable special case, it is possible for the [objective function](@entry_id:267263) to be constant over the entire feasible region. This occurs when the cost vector $c$ can be expressed as a [linear combination](@entry_id:155091) of the rows of the constraint matrix $A$, i.e., $c^T = y^T A$ for some vector $y$. In this situation, for any [feasible solution](@entry_id:634783) $x$, the objective value is fixed: $z = c^T x = y^T A x = y^T b$. Consequently, every feasible point is an optimal point, and the optimal face is the entire feasible region itself. At any BFS for such a problem, the [reduced costs](@entry_id:173345) of all nonbasic variables will be zero [@problem_id:3171613].

### Deeper Interpretations of Reduced Costs

The algebraic definition of [reduced cost](@entry_id:175813) is powerful, but its full utility is best appreciated through its geometric and economic interpretations.

#### Geometric Interpretation: The Directional Derivative

The [simplex algorithm](@entry_id:175128) moves from vertex to adjacent vertex along the edges of the feasible polyhedron. A [reduced cost](@entry_id:175813) can be understood as the rate of change of the objective function along one of these edges.

Consider a nonbasic variable $x_j$. The [simplex](@entry_id:270623) direction associated with increasing $x_j$ is a vector $d^{(j)}$ that represents movement along the edge emanating from the current vertex. This direction is constructed such that $d_j^{(j)}=1$, all other nonbasic components are zero, and the basic components are adjusted to maintain feasibility ($Ad^{(j)}=0$). This implies that the basic components of the [direction vector](@entry_id:169562) are $d_B^{(j)} = -A_B^{-1} A_j$.

The directional derivative of the objective function $z=c^Tx$ along this direction vector $d^{(j)}$ is given by the dot product $c^T d^{(j)}$. Let's expand this:
$$
c^T d^{(j)} = c_B^T d_B^{(j)} + c_j d_j^{(j)} = c_B^T (-A_B^{-1} A_j) + c_j(1) = c_j - (c_B^T A_B^{-1}) A_j
$$
Recognizing $y^T = c_B^T A_B^{-1}$, we arrive at a fundamental identity:
$$
c^T d^{(j)} = c_j - y^T A_j = \bar{c}_j
$$
This proves that the [reduced cost](@entry_id:175813) $\bar{c}_j$ is precisely the directional derivative of the [objective function](@entry_id:267263) along the edge corresponding to the nonbasic variable $x_j$ [@problem_id:3171543]. For a minimization problem, a negative [reduced cost](@entry_id:175813) means that moving in this direction will decrease the objective, which is geometrically intuitive—we are moving "downhill" along an edge of the feasible set [@problem_id:3171595].

#### Economic Interpretation: Shadow Prices and Net Profitability

In many applications, linear programs model resource allocation. For example, a firm might maximize revenue ($c^Tx$) subject to limitations on resources like labor or raw materials ($Ax \le b$) [@problem_id:3171559]. In this context, the [simplex multipliers](@entry_id:177701) $y$ have a powerful economic interpretation as **shadow prices** (or marginal values) of the resources. The value $y_i$ represents the increase in the optimal objective value that would result from a one-unit increase in the availability of resource $i$. It is the price the firm would be willing to pay for an additional unit of that resource.

With this interpretation of $y$, the term $y^T A_j$ represents the **imputed cost** of producing one unit of product $j$. The column $A_j$ lists the amount of each resource consumed by product $j$, and $y^T$ prices those resources at their marginal value. The [reduced cost](@entry_id:175813) formula,
$$
\bar{c}_j = c_j - y^T A_j
$$
can now be read as:
$$
\text{Reduced Cost} = \text{Unit Revenue} - \text{Imputed Cost of Resources}
$$
The [reduced cost](@entry_id:175813) is the **net profitability** of product $j$ at the current [shadow prices](@entry_id:145838).
- If $\bar{c}_j > 0$ (in a max problem), the product's revenue exceeds the [opportunity cost](@entry_id:146217) of the resources it consumes. It is "profitable" to introduce this product into the production plan.
- If $\bar{c}_j < 0$, the product is "unprofitable" at these shadow prices and should not be produced.
- If $\bar{c}_j = 0$, the product breaks even. Complementary slackness implies that only products that break even can be produced in an optimal plan (i.e., if $x_j > 0$ at optimum, then $\bar{c}_j=0$).

This interpretation extends beautifully to the **[slack variables](@entry_id:268374)**. Consider a constraint for resource $i$, $a_{i1}x_1 + \dots \le b_i$, which becomes $a_{i1}x_1 + \dots + s_i = b_i$ in standard form. The cost of the [slack variable](@entry_id:270695) $s_i$ is $c_{s_i} = 0$, and its column in the constraint matrix is the identity vector $e_i$. Its [reduced cost](@entry_id:175813) is therefore:
$$
\bar{c}_{s_i} = c_{s_i} - y^T e_i = 0 - y_i = -y_i
$$
The [reduced cost](@entry_id:175813) of a [slack variable](@entry_id:270695) is the negative of the shadow price of the corresponding constraint [@problem_id:3171540]. For a maximization problem, the optimality condition $\bar{c}_{s_i} \le 0$ implies $-y_i \le 0$, or $y_i \ge 0$. This provides an intuitive justification for why the dual variables associated with 'less-than-or-equal-to' constraints in a maximization problem must be non-negative. If a resource is not fully used ($s_i>0$), it is not a bottleneck, and its marginal value must be zero ($y_i=0$).

### Connections to General Optimality Theory

The principles of the simplex method, which were developed independently, can be elegantly unified with the broader theory of constrained optimization through the **Karush-Kuhn-Tucker (KKT) conditions**. To align with the standard KKT formulation for minimization, we consider the equivalent problem of minimizing $-c^Tx$ subject to $Ax=b$ and $x \ge 0$. The KKT conditions stipulate that for a solution $x$ to be optimal, there must exist multipliers $y$ (for $Ax=b$) and $\sigma \ge 0$ (for $x \ge 0$) such that:
1.  **Primal Feasibility**: $Ax=b$, $x \ge 0$.
2.  **Stationarity**: The gradient of the Lagrangian with respect to $x$ is zero. The Lagrangian is $L(x,y,\sigma) = -c^Tx + y^T(Ax-b) - \sigma^T x$. Thus, $\nabla_x L = -c + A^Ty - \sigma = 0$, which implies $\sigma = A^Ty - c$.
3.  **Complementary Slackness**: $\sigma_j x_j = 0$ for all $j$.

Now, let's connect this to the simplex method's [reduced costs](@entry_id:173345). The vector of [reduced costs](@entry_id:173345) for the original maximization problem is defined as $\bar{c} = c - A^Ty$. From the [stationarity condition](@entry_id:191085), we see that $\sigma = -(c - A^Ty) = -\bar{c}$.

The KKT conditions can now be restated in the familiar language of the simplex method for a maximization problem [@problem_id:3171532]:
1.  **Primal Feasibility**: $Ax=b, x \ge 0$. This is maintained at every step of the [simplex algorithm](@entry_id:175128).
2.  **Dual Feasibility / Optimality Condition**: $\bar{c} \le 0$. This comes from the KKT requirement $\sigma \ge 0$, which translates to $-\bar{c} \ge 0$, or $\bar{c} \le 0$. The [simplex algorithm](@entry_id:175128) terminates when this condition is met.
3.  **Complementary Slackness**: $\bar{c}_j x_j = 0$ for all $j$. This is also maintained by the [simplex method](@entry_id:140334): for basic variables, $\bar{c}_j=0$, and for nonbasic variables, $x_j=0$.

This reveals that the [simplex algorithm](@entry_id:175128), at each step, maintains primal feasibility and [complementary slackness](@entry_id:141017). It iterates by seeking to satisfy [dual feasibility](@entry_id:167750) (the optimality condition $\bar{c} \le 0$).

### Special Topic: Degeneracy and Zero Reduced Costs

A final nuance arises when the [simplex method](@entry_id:140334) encounters a **degenerate BFS**, where one or more basic variables are equal to zero. This can lead to interesting behavior, particularly when combined with zero [reduced costs](@entry_id:173345).

Consider a pivot where the entering variable $x_k$ has a [reduced cost](@entry_id:175813) $\bar{c}_k = 0$. The change in the objective function is $\Delta z = \theta \bar{c}_k$, where $\theta$ is the step size determined by the [minimum ratio test](@entry_id:634935). If the pivot is degenerate, the minimum ratio is $\theta=0$. In this case, $\Delta z = 0 \times 0 = 0$.

What occurs is a pivot with zero step length [@problem_id:3171632]:
- The basis changes: $x_k$ enters the basis, and some basic variable $x_B_r$ (which was already at value zero) leaves.
- The solution point in $\mathbb{R}^n$ **does not change**. We simply have a different basis representation for the same [degenerate vertex](@entry_id:636994).
- The objective value remains the same.

This type of pivot does not make progress toward the optimum in terms of objective value or position, but it changes the algebraic representation of the current vertex. While often benign, a sequence of such degenerate pivots can, in rare, specially constructed cases, lead to **cycling**, where the algorithm repeats a sequence of bases without ever improving the objective or terminating. Modern [simplex](@entry_id:270623) solvers employ [anti-cycling rules](@entry_id:637416) (like Bland's rule) to prevent this.