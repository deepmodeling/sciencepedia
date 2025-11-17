## Introduction
The [simplex algorithm](@entry_id:175128) is a cornerstone of [mathematical optimization](@entry_id:165540), renowned for its efficiency in solving [linear programming](@entry_id:138188) problems. At the heart of this algorithm lies an iterative process of moving from one vertex of a [feasible region](@entry_id:136622) to a better one. The critical question at each step is: which direction to move in, and how far? The answer is governed by two fundamental mechanisms: **pricing rules** and **ratio tests**. Understanding these components is the key to unlocking a deep, practical knowledge of not just the simplex method, but a wide range of optimization theories and applications. This article moves beyond a black-box understanding to illuminate the engine that drives this powerful algorithm.

This exploration is structured into three chapters. First, in **Principles and Mechanisms**, we will dissect the algebraic and geometric intuition behind a single pivot, formalizing how pricing rules use [reduced costs](@entry_id:173345) to select an entering variable and how the [ratio test](@entry_id:136231) determines the leaving variable. We will also address crucial theoretical issues like degeneracy and cycling. Next, the **Applications and Interdisciplinary Connections** chapter will demonstrate the real-world utility of these concepts, from economic planning and finance to advanced [large-scale optimization](@entry_id:168142) techniques like [column generation](@entry_id:636514). Finally, **Hands-On Practices** will offer a series of targeted problems designed to solidify your grasp of these mechanics and their subtleties. We begin by examining the intricate machinery of the simplex pivot.

## Principles and Mechanisms

The [simplex algorithm](@entry_id:175128) navigates the vertices of a feasible polyhedron, iteratively moving from one basic [feasible solution](@entry_id:634783) (BFS) to an adjacent one that improves the [objective function](@entry_id:267263) value. Each such move, or **pivot**, constitutes a single iteration of the algorithm. The efficacy and mechanics of the simplex method are fundamentally rooted in two critical decisions made at each step: which variable should enter the basis, and which should leave? These decisions are governed by what are known as **pricing rules** and **ratio tests**. This chapter elucidates the principles and mechanisms behind these core components of the [simplex algorithm](@entry_id:175128).

### The Anatomy of a Simplex Pivot

Imagine standing at a vertex of a [convex polyhedron](@entry_id:170947). To improve our position (i.e., the objective function value), we must travel along an edge to an adjacent vertex. This simple geometric intuition is the heart of a simplex pivot. In the algebraic context of a linear program in standard form, `minimize` $z = c^\top x$ subject to $Ax = b, x \ge 0$, this translates to:

1.  **Choosing an Edge (The Pricing Problem):** An edge corresponds to allowing a single nonbasic variable, currently at value zero, to increase. The decision of which nonbasic variable to increase is called **pricing**. It involves evaluating the potential impact of each nonbasic variable on the objective function.

2.  **Traveling Along the Edge (The Ratio Test):** Once a direction (an entering variable) is chosen, we must determine how far we can travel without leaving the [feasible region](@entry_id:136622). This means increasing the chosen nonbasic variable just enough until one of the current basic variables is driven to zero. This calculation is the **[ratio test](@entry_id:136231)**, and it identifies the variable that must leave the basis.

Let's formalize this. At a given BFS, the variables are partitioned into a set of $m$ basic variables, $x_B$, and $n-m$ nonbasic variables, $x_N$. The system $Ax=b$ can be written as $Bx_B + Nx_N = b$, where $B$ and $N$ are the matrices of basic and nonbasic columns, respectively. From this, we can express the basic variables and the objective function solely in terms of the nonbasic variables:

$x_B = B^{-1}b - B^{-1}Nx_N$

$z = c_B^\top x_B + c_N^\top x_N = c_B^\top(B^{-1}b - B^{-1}Nx_N) + c_N^\top x_N = z_0 + (c_N^\top - c_B^\top B^{-1}N)x_N$

where $z_0 = c_B^\top B^{-1}b$ is the objective value at the current BFS. This second equation is paramount, as it contains the keys to the pricing problem.

### The Pricing Problem: Selecting an Entering Variable

The term $(c_N^\top - c_B^\top B^{-1}N)$ in the [objective function](@entry_id:267263) expression reveals the rate of change of $z$ with respect to the nonbasic variables. We define the **[reduced cost](@entry_id:175813)** for each nonbasic variable $x_j$ (where $j \in \mathcal{N}$) as:

$\bar{c}_j = c_j - c_B^\top B^{-1} a_j$

where $a_j$ is the $j$-th column of the original matrix $A$. The vector of [dual variables](@entry_id:151022), or **shadow prices**, is defined as $y^\top = c_B^\top B^{-1}$. The [reduced cost](@entry_id:175813) can then be written compactly as $\bar{c}_j = c_j - y^\top a_j$. This expression gives the [reduced cost](@entry_id:175813) a powerful economic interpretation: it is the marginal cost $c_j$ of the variable $x_j$ adjusted by the value (imputed cost) of the resources it consumes, $y^\top a_j$ [@problem_id:3164034].

The [objective function](@entry_id:267263) can be expressed as $z = z_0 + \sum_{j \in \mathcal{N}} \bar{c}_j x_j$. For a minimization problem, if we select a nonbasic variable $x_j$ with a negative [reduced cost](@entry_id:175813) ($\bar{c}_j \lt 0$) and increase its value from $0$, the objective value $z$ will decrease. This is the fundamental condition for improving the solution.

If, at a BFS, all [reduced costs](@entry_id:173345) for nonbasic variables are non-negative ($\bar{c}_j \ge 0$ for all $j \in \mathcal{N}$), then no single nonbasic variable can be increased to decrease the objective value. Since any feasible move from the current BFS requires increasing at least one nonbasic variable (which are all non-negative), the term $\sum \bar{c}_j x_j$ will be non-negative. This means we cannot find a feasible direction that improves the objective. The current solution is therefore **optimal** [@problem_id:3164072].

#### Dantzig's Pricing Rule

The most common and historically significant pricing rule, proposed by George Dantzig, is to select the variable that promises the fastest rate of improvement.
- For minimization, select the entering variable $x_j$ with the most negative [reduced cost](@entry_id:175813): $j^* = \arg\min_{j \in \mathcal{N}} \{\bar{c}_j\}$.
- For maximization, select the entering variable $x_j$ with the most positive [reduced cost](@entry_id:175813): $j^* = \arg\max_{j \in \mathcal{N}} \{\bar{c}_j\}$.

For example, consider an initial BFS where the [slack variables](@entry_id:268374) are basic. In this common starting scenario, the [basis matrix](@entry_id:637164) $B$ is the identity matrix $I$, and the costs of the basic [slack variables](@entry_id:268374) are typically zero, so $c_B = 0$. This simplifies the calculations greatly: the dual variables are $y^\top = 0^\top I^{-1} = 0^\top$, and the [reduced costs](@entry_id:173345) become $\bar{c}_j = c_j$ for all nonbasic structural variables [@problem_id:3164122] [@problem_id:3164034]. If a maximization problem has an objective $z = 3x_1 + 5x_2$, the initial [reduced costs](@entry_id:173345) are $\bar{c}_1 = 3$ and $\bar{c}_2 = 5$. Dantzig's rule would select $x_2$ to enter the basis.

#### Beyond Dantzig's Rule: Is Steepest Edge Always Best?

Dantzig's rule is often called a "steepest edge" rule because it chooses the direction of the greatest [instantaneous rate of change](@entry_id:141382). However, this does not guarantee the greatest total improvement in a single pivot. The total improvement is the product of the rate of change ($\bar{c}_j$) and the distance traveled ($\theta_j$, the step length from the [ratio test](@entry_id:136231)). A direction with a very steep descent might be very short, leading to a smaller overall improvement than a less steep but longer edge.

Consider a minimization problem with two candidate entering variables, $x_1$ and $x_2$ [@problem_id:3164152]. Suppose $\bar{c}_1 = -5$ and $\bar{c}_2 = -1.2$. Dantzig's rule would unequivocally choose $x_1$. However, if the geometry of the [feasible region](@entry_id:136622) allows a step of only $\theta_1 = 1$ for $x_1$ but a much larger step of $\theta_2 = 10$ for $x_2$, the total objective changes would be:
- $\Delta z_1 = \theta_1 \bar{c}_1 = 1 \times (-5) = -5$
- $\Delta z_2 = \theta_2 \bar{c}_2 = 10 \times (-1.2) = -12$

In this scenario, choosing $x_2$ would have produced a much larger one-step improvement. This illustrates a key subtlety: the choice of an entering variable and the resulting step length are intertwined. Rules that attempt to find the pivot with the **greatest improvement** would need to compute the step length $\theta_j$ for each candidate $j$, a computationally expensive task.

Other rules exist, such as **normalized pricing**, which attempts to balance the rate of improvement with the "length" of the step in the variable space. For instance, one could select the entering variable that maximizes the objective decrease per unit of Euclidean distance traversed by the basic variables, a metric given by $-\bar{c}_j / \|p_j\|_2$, where $p_j = B^{-1}a_j$ is the pivot column [@problem_id:3164043].

### The Ratio Test: Selecting a Leaving Variable

Once an entering variable $x_j$ is selected, we must determine the maximum step size $\theta$ it can be increased by before violating primal feasibility. The values of the basic variables change according to the equation:

$x_B(\theta) = B^{-1}b - \theta (B^{-1}a_j) = x_B^{\text{current}} - \theta p_j$

where $p_j = B^{-1}a_j$ is the **pivot column** (or direction in the basic space). The requirement that all variables remain non-negative, specifically $x_B(\theta) \ge 0$, imposes constraints on $\theta$:

$x_{B,i}^{\text{current}} - \theta (p_j)_i \ge 0$ for all basic variables $i$.

If $(p_j)_i \le 0$, the corresponding basic variable $x_{B,i}$ will only increase or stay the same as $\theta$ increases, so this constraint imposes no upper bound on $\theta$. However, for every component $i$ where $(p_j)_i > 0$, we have a bound:

$\theta \le \frac{x_{B,i}^{\text{current}}}{(p_j)_i}$

To maintain feasibility for all basic variables simultaneously, $\theta$ must be less than or equal to the smallest of these ratios. This gives rise to the **[minimum ratio test](@entry_id:634935)**:

$\theta^* = \min \left\{ \frac{x_{B,i}}{(p_j)_i} \quad \middle| \quad (p_j)_i > 0 \right\}$

This maximum allowable step size, $\theta^*$, is the value the entering variable will take in the new BFS. The basic variable $x_{B,r}$ corresponding to the row $r$ that produces this minimum ratio is the **leaving variable**, as it is the first to be driven to zero [@problem_id:3164036] [@problem_id:3164122]. In the new basis, $x_j$ will replace $x_{B,r}$.

### Degeneracy, Cycling, and Anti-Cycling Rules

A complication arises when a basic variable in the current BFS is already at zero, i.e., $x_{B,i} = 0$. If the corresponding pivot column entry $(p_j)_i$ is positive, the [ratio test](@entry_id:136231) for that row will yield a ratio of $0/ (p_j)_i = 0$. This forces the step length to be $\theta^* = 0$ [@problem_id:3164063] [@problem_id:3164045]. This situation is known as **degeneracy**.

A pivot with a step size of zero is a **[degenerate pivot](@entry_id:636499)**. Its consequences are:
1.  The [objective function](@entry_id:267263) value does not change: $\Delta z = \theta^* \bar{c}_j = 0$.
2.  The numerical values of the variables do not change, and the algorithm does not move to a new point in the feasible space.
3.  The basis *does* change. A basic variable at value zero is replaced by the entering variable, also at value zero.

While a [degenerate pivot](@entry_id:636499) may seem like a step that makes no progress, it is often a necessary intermediate step. However, it opens up a theoretical risk known as **cycling**: a sequence of degenerate pivots could lead the algorithm back to a basis it has already visited, causing it to loop infinitely without ever reaching the optimum.

To guarantee termination, **[anti-cycling rules](@entry_id:637416)** are employed. These are systematic tie-breaking procedures for the [ratio test](@entry_id:136231).
- **Bland's Rule:** A simple and elegant rule that chooses the entering variable $x_k$ with the smallest index $k$ among those with favorable [reduced costs](@entry_id:173345). If there is a tie in the [ratio test](@entry_id:136231) for the leaving variable, it chooses the basic variable $x_j$ with the smallest index $j$.
- **Lexicographic Rule:** This method breaks ties by augmenting the [ratio test](@entry_id:136231). It conceptually perturbs the right-hand side vector $b$ to eliminate degeneracy, ensuring all ratios are unique. In practice, this is achieved by comparing tied rows lexicographically. For instance, if rows $i$ and $r$ both yield the minimum ratio, we would compare the vectors $(1/(p_j)_i) \cdot (\text{row } i)$ and $(1/(p_j)_r) \cdot (\text{row } r)$ of the full [simplex tableau](@entry_id:136786), column by column, and select the one that is lexicographically smaller. This ensures a unique choice for the leaving variable and guarantees that the algorithm will terminate [@problem_id:3164148].

### The Dual Simplex Method

The logic of pricing and ratio tests can be inverted to create the **[dual simplex method](@entry_id:164344)**. This method is applicable when a basic solution is dual-feasible but primal-infeasible. In a minimization problem, this means all [reduced costs](@entry_id:173345) are non-negative ($\bar{c}_j \ge 0$), but at least one basic variable is negative ($x_{B,i}  0$) [@problem_id:3164072].

The pivot logic is reversed:
1.  **Select the Leaving Variable (Dual Pricing):** First, we choose a basic variable to remove from the basis. The natural choice is one that violates primal feasibility. A standard rule is to select the basic variable with the most negative value: $x_{B,i^*}$ where $i^* = \arg\min_i \{x_{B,i}\}$.

2.  **Select the Entering Variable (Dual Ratio Test):** Next, we must choose a nonbasic variable $x_j$ to enter the basis. The pivot element must be in the row $i^*$ of the leaving variable. The choice of $j$ must (a) move the leaving variable $x_{B,i^*}$ towards feasibility (i.e., increase its value from negative towards zero) and (b) maintain [dual feasibility](@entry_id:167750) (i.e., keep all [reduced costs](@entry_id:173345) non-negative after the pivot).

    Condition (a) requires the pivot element $p_{i^*j}$ to be negative. Condition (b) leads to a [ratio test](@entry_id:136231). As derived from first principles, the update rule for the [reduced costs](@entry_id:173345) is $\bar{c}_k' = \bar{c}_k - (\bar{c}_j / p_{i^*j}) p_{i^*k}$. To maintain $\bar{c}_k' \ge 0$ for all $k$, we must select the entering variable $j$ according to the **dual [ratio test](@entry_id:136231)**:

    $j^* = \arg\min \left\{ \frac{\bar{c}_k}{-(p_{i^*k})} \quad \middle| \quad p_{i^*k}  0 \right\}$

The [dual simplex method](@entry_id:164344) is not just a theoretical curiosity; it is immensely practical, especially in re-optimization after a change in the model (e.g., adding a constraint) and in algorithms for integer and [mixed-integer programming](@entry_id:173755). The pivot mechanics, though inverted, are still a systematic exchange of variables driven by the dual goals of attaining primal feasibility while maintaining [dual feasibility](@entry_id:167750) [@problem_id:3164126].