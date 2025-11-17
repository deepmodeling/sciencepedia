## Introduction
The [simplex algorithm](@entry_id:175128) is a cornerstone of linear programming, celebrated for its efficiency in navigating the [vertices of a feasible region](@entry_id:174284) to find an [optimal solution](@entry_id:171456). However, its guaranteed termination hinges on a critical assumption: the absence of degeneracy. When a basic feasible solution is degenerate, the algorithm can perform pivots that fail to improve the objective function, opening the door to a rare but fatal flaw known as cycling, where the algorithm loops through bases indefinitely. This article tackles this fundamental challenge head-on, providing the tools to ensure the [simplex method](@entry_id:140334) is robust and reliable in all cases.

Across the following chapters, you will gain a comprehensive understanding of this critical topic. In **Principles and Mechanisms**, we will dissect the problem of degeneracy, explain how it leads to cycling, and introduce the elegant logic of anti-cycling procedures like Bland's rule and the lexicographical method. Next, in **Applications and Interdisciplinary Connections**, we will explore why these theoretical rules are indispensable in practice, examining their role in solving highly degenerate problems in [network optimization](@entry_id:266615), game theory, and large-scale [decomposition methods](@entry_id:634578). Finally, **Hands-On Practices** will provide opportunities to solidify your knowledge by tracing a cycling example, comparing pivot rules through simulation, and designing an experiment to investigate the link between degeneracy and cycling. This journey will equip you with a deep appreciation for the theoretical guarantees that underpin modern optimization solvers.

## Principles and Mechanisms

The [simplex algorithm](@entry_id:175128), in its standard form, proceeds by moving from one vertex of the [feasible region](@entry_id:136622) to an adjacent one, with each step strictly improving the [objective function](@entry_id:267263) value. This process guarantees that we never revisit a vertex, and since there is a finite number of vertices, the algorithm must terminate. However, this guarantee of strict improvement relies on a crucial assumption: that every basic feasible solution is **non-degenerate**. In this chapter, we will explore what happens when this assumption is violated and introduce the formal mechanisms required to ensure the [simplex method](@entry_id:140334)'s termination even in these challenging cases.

### The Problem of Degeneracy

In the context of [linear programming](@entry_id:138188), a **basic feasible solution (BFS)** is defined as **degenerate** if at least one of its basic variables has a value of zero. Geometrically, this corresponds to a vertex of the feasible polytope where more than the minimum required number of constraint [hyperplanes](@entry_id:268044) intersect. While degeneracy is common in many practical problems, it introduces a potential complication for the [simplex method](@entry_id:140334).

The core of the issue arises during the **[minimum ratio test](@entry_id:634935)**, which is used to determine the leaving variable. The minimum ratio, denoted by $\theta$, represents the maximum step size we can take along an edge from the current vertex before violating a feasibility constraint. If the current BFS is non-degenerate, all basic variables are strictly positive, and the minimum ratio $\theta$ will also be strictly positive. This ensures that the [objective function](@entry_id:267263) improves by a non-zero amount (specifically, by $\bar{c}_j \theta$, where $\bar{c}_j > 0$ is the [reduced cost](@entry_id:175813) of the entering variable).

However, if a basic variable $x_{B_i}$ is zero and the corresponding coefficient $a_{ij}$ for the entering variable $x_j$ is positive, the [ratio test](@entry_id:136231) will yield a ratio of $\frac{x_{B_i}}{a_{ij}} = \frac{0}{a_{ij}} = 0$. If this is the minimum ratio, the step size $\theta$ becomes zero.

A [pivot operation](@entry_id:140575) with a step size of $\theta = 0$ is known as a **[degenerate pivot](@entry_id:636499)**. Such a pivot has a distinct and problematic characteristic: the basis changes (one variable enters, another leaves), but the numerical values of the variables do not. The algorithm performs an algebraic [change of basis](@entry_id:145142) without actually moving to a new geometric point. Consequently, the objective function value does not improve.

Consider a scenario where we are maximizing an [objective function](@entry_id:267263) and have a degenerate BFS where basic variables $s_1$ and $s_3$ are currently zero. The dictionary might look like this:
$s_1 = -x_1 - x_2$
$s_2 = 2 - x_1 - 2x_2$
$s_3 = -2x_1 - x_2$
If we choose $x_1$ to enter the basis, the [ratio test](@entry_id:136231) requires us to find the maximum step size $\theta$ for $x_1$ that keeps all basic variables non-negative.
$s_1 = -\theta \ge 0 \implies \theta \le 0$
$s_2 = 2 - \theta \ge 0 \implies \theta \le 2$
$s_3 = -2\theta \ge 0 \implies \theta \le 0$
The only value satisfying these conditions is $\theta = 0$. This corresponds to a minimum ratio of zero, caused by the basic variables $s_1$ and $s_3$ being zero.

When a [degenerate pivot](@entry_id:636499) occurs, we obtain a new basis representing the same vertex. While a single [degenerate pivot](@entry_id:636499) is not a problem, it opens the door to a dangerous phenomenon known as **cycling**. Cycling is a sequence of degenerate pivots that eventually returns to a basis that has been visited before. Once the algorithm enters such a cycle, it will loop through the same sequence of bases indefinitely, never improving the objective function and thus never terminating. While cycling is rare in practice, its theoretical possibility means that the standard [simplex method](@entry_id:140334) is not, in the strictest sense, a finite algorithm. To guarantee termination, we must employ an **anti-cycling rule**.

### Bland's Rule: A Guarantee of Termination

The most well-known and simplest-to-implement anti-cycling rule was developed by Robert G. Bland. **Bland's rule**, also known as the smallest-index rule, provides a deterministic way to choose entering and leaving variables that provably prevents cycling. The rule is composed of two simple, sequential parts:

1.  **Entering Variable Selection**: Among all non-basic variables that are eligible to enter the basis (i.e., those with an improving [reduced cost](@entry_id:175813)), choose the one with the **smallest index**.

2.  **Leaving Variable Selection**: If the [minimum ratio test](@entry_id:634935) results in a tie for the leaving variable, choose the basic variable with the **smallest index** to leave the basis.

For these rules, it is assumed that all variables in the problem (decision, slack, surplus, etc.) are assigned a unique fixed index, for example, $x_1, x_2, \dots, x_n, s_1, \dots, s_m$.

Let's illustrate Bland's rule with a concrete example. Suppose for a maximization problem, we have the following [simplex tableau](@entry_id:136786) where the non-basic variables are $x_2$ and $x_4$:
```
| Basis |  z  |  x1 |  x2 |  x3 |  x4 |  x5 | Value |
|-------|-----|-----|-----|-----|-----|-----|-------|
|   z   |  1  |  0  | -2  |  0  | -5  |  0  |  20   |
|  x1   |  0  |  1  |  3  |  0  |  1  |  0  |   6   |
|  x3   |  0  |  0  |  4  |  1  |  2  |  0  |   0   |
|  x5   |  0  |  0  | -1  |  0  |  3  |  1  |   2   |
```
The standard rule for entering variables might be to choose the one with the most negative coefficient in the z-row, which would be $x_4$ (with coefficient -5). However, Bland's rule dictates a different choice. The non-basic variables with negative coefficients are $x_2$ (index 2) and $x_4$ (index 4). Bland's rule requires us to select the one with the smallest index, so **$x_2$ enters the basis**.

Next, we perform the [minimum ratio test](@entry_id:634935) for the $x_2$ column:
-   Row $x_1$: Ratio = $\frac{6}{3} = 2$.
-   Row $x_3$: Ratio = $\frac{0}{4} = 0$.
The minimum ratio is $0$. This is a [degenerate pivot](@entry_id:636499). The leaving variable is $x_3$. In this case there was no tie in the [ratio test](@entry_id:136231), but if there had been, we would have chosen the leaving variable with the smaller index to break the tie.

Let's consider another example where both parts of Bland's rule are needed. Suppose in a minimization problem, we have non-basic variables $x_1, x_2, x_3$ with [reduced costs](@entry_id:173345) $\bar{c}_1 = -3$, $\bar{c}_2 = -3$, and $\bar{c}_3 = -1$. All are negative, so all are candidates to enter. Bland's rule breaks the tie by selecting the one with the smallest index: **$x_1$ enters**. Now suppose the [ratio test](@entry_id:136231) for $x_1$ yields a tie:
- Row 1 (basic variable $s_1$, index 4): Ratio = $4/2 = 2$.
- Row 2 (basic variable $s_2$, index 5): Ratio = $6/3 = 2$.
To break this tie, Bland's rule instructs us to choose the leaving variable with the smallest index. Comparing the indices of the basic variables, $s_1$ (index 4) and $s_2$ (index 5), we see that $4 \lt 5$. Therefore, **$s_1$ leaves the basis**.

While the full proof is beyond the scope of this chapter, the intuition behind Bland's rule is that it imposes a strict, consistent ordering on the sequence of pivots. By always choosing the smallest-indexed variable, it ensures that the algorithm can never return to a basis it has previously visited. This guarantees that the [simplex method](@entry_id:140334) will always terminate at an [optimal solution](@entry_id:171456) or correctly identify the problem as unbounded.

### Properties and Consequences of Bland's Rule

The primary virtue of Bland's rule is its guarantee of termination. However, this safety comes at a price. The rule's logic is "lexicographical" rather than "greedy." It does not consider the magnitude of potential improvement when selecting an entering variable.

A more common [pivoting strategy](@entry_id:169556), often called **Dantzig's rule**, is to choose the entering variable that offers the greatest rate of improvement—that is, the one with the most favorable [reduced cost](@entry_id:175813) (largest positive for maximization, most negative for minimization). This greedy approach often leads to faster convergence in practice on non-degenerate problems.

Bland's rule, in contrast, may select a variable that offers only a minuscule improvement in the [objective function](@entry_id:267263). Consider a maximization problem with the objective $z = \epsilon x_1 + x_2$, where $0 \lt \epsilon \ll 1$. The non-basic variables are $x_1$ and $x_2$, with [reduced costs](@entry_id:173345) $\epsilon$ and $1$, respectively. Dantzig's rule would choose $x_2$ to enter, as its [reduced cost](@entry_id:175813) is much larger. Bland's rule, however, must choose $x_1$ because it has the smaller index. If the subsequent [ratio test](@entry_id:136231) yields a small value of $\theta$, the total improvement to the objective, $\Delta z = \epsilon \theta$, could be extremely small. This illustrates that Bland's rule prioritizes theoretical robustness over the speed of convergence on a per-pivot basis.

Because Bland's rule and Dantzig's rule can select different entering variables, they can trace entirely different paths along the vertices of the feasible [polytope](@entry_id:635803) to reach the optimum. While Dantzig's rule might take a more direct "steepest ascent" path, Bland's rule takes a path dictated by its strict indexing logic, which is guaranteed to be cycle-free.

### The Lexicographical Method: A Geometric Interpretation

An alternative anti-cycling procedure, which provides a beautiful geometric intuition for Bland's rule, is the **lexicographical method**. This method addresses degeneracy by creating a "perturbed" version of the problem where degeneracy is impossible.

The idea is to replace the right-hand-side vector $\boldsymbol{b}$ with a symbolic polynomial in a small, positive parameter $\epsilon$:
$$ \boldsymbol{b}(\epsilon) = \boldsymbol{b} + \begin{pmatrix} \epsilon \\ \epsilon^2 \\ \vdots \\ \epsilon^m \end{pmatrix} $$
where $m$ is the number of constraints. This perturbation effectively shifts each constraint [hyperplane](@entry_id:636937) by an infinitesimally different amount, ensuring that no more than the required number of planes intersect at any single point. This eliminates all degenerate vertices from the feasible region.

With this perturbed RHS, the [minimum ratio test](@entry_id:634935) will never result in a tie (for a sufficiently small $\epsilon$). The leaving variable is chosen by finding the minimum of the ratios $R_i(\epsilon) = \frac{b_i(\epsilon)}{a_{ij}}$ using **lexicographical comparison**. To compare two ratios, we expand them as power series in $\epsilon$ and compare their coefficients term by term, from the lowest power of $\epsilon$ to the highest.

For instance, suppose we need to compare three ratios from a pivot step:
-   $R_1(\epsilon) = \frac{4 + \epsilon + \epsilon^2}{2} = 2 + \frac{1}{2}\epsilon + \frac{1}{2}\epsilon^2$
-   $R_2(\epsilon) = \frac{4 + 3\epsilon}{2} = 2 + \frac{3}{2}\epsilon$
-   $R_3(\epsilon) = \frac{7 + \epsilon}{3} = \frac{7}{3} + \frac{1}{3}\epsilon \approx 2.33 + \frac{1}{3}\epsilon$

The lexicographical comparison proceeds as follows:
1.  **Compare constant terms ($\epsilon^0$):** The coefficients are $2$, $2$, and $\frac{7}{3}$. Since $2  \frac{7}{3}$, $R_3$ is eliminated. We have a tie between $R_1$ and $R_2$.
2.  **Compare $\epsilon^1$ terms for the tied rows:** The coefficients are $\frac{1}{2}$ for $R_1$ and $\frac{3}{2}$ for $R_2$. Since $\frac{1}{2}  \frac{3}{2}$, $R_1$ is lexicographically smaller than $R_2$.

Therefore, the lexicographically minimal ratio is $R_1(\epsilon)$, and the basic variable in the first row is chosen to leave the basis.

A remarkable theorem states that if the rows of the [simplex tableau](@entry_id:136786) are ordered according to the indices of their basic variables, the lexicographical method is equivalent to the leaving-variable rule in Bland's rule. This provides a deep connection between a simple combinatorial rule (smallest index) and a geometric perturbation that resolves degeneracy.

### Case Study: A Predictable Simplex Path

To see the deterministic power of Bland's rule, consider a linear program whose [feasible region](@entry_id:136622) in the decision variables $x_1, \dots, x_N$ is the standard [simplex](@entry_id:270623), defined by $\sum_{i=1}^{N} x_{i} = 1$ and $x_i \ge 0$. The vertices of this region are the [standard basis vectors](@entry_id:152417) $\boldsymbol{e}_k$ (where $x_k=1$ and all other $x_j=0$). Let the objective be to maximize $\sum c_i x_i$ where the costs are strictly increasing, $c_1  c_2  \dots  c_N$.

If we start the [simplex method](@entry_id:140334) at the vertex $\boldsymbol{e}_1$ (where $x_1=1$) and apply Bland's rule, the algorithm will trace a completely predictable path. At the first step, the [reduced costs](@entry_id:173345) for all $x_j$ ($j  1$) will be positive ($c_j - c_1  0$). Bland's rule will select $x_2$ to enter. A tie in the [ratio test](@entry_id:136231) will be broken by Bland's rule, causing $x_1$ to leave. The new vertex is $\boldsymbol{e}_2$.

At the next step, from vertex $\boldsymbol{e}_2$, the eligible entering variables will be $x_3, \dots, x_N$. Bland's rule will select $x_3$ to enter, which will in turn cause $x_2$ to leave. The new vertex is $\boldsymbol{e}_3$.

This process continues sequentially. At each vertex $\boldsymbol{e}_k$, Bland's rule forces the simplex method to pivot to the next vertex in the sequence, $\boldsymbol{e}_{k+1}$. The algorithm marches along the vertices in the order of their indices, $\boldsymbol{e}_1 \to \boldsymbol{e}_2 \to \dots \to \boldsymbol{e}_N$, never cycling, and terminates at the optimal vertex $\boldsymbol{e}_N$ after exactly $N-1$ pivots. This case study powerfully illustrates how Bland's rule imposes a disciplined, cycle-free progression, even in a highly degenerate setting.

In summary, while degeneracy poses a theoretical threat to the termination of the simplex method, anti-cycling rules like Bland's rule provide a robust and easy-to-implement safeguard. By trading greedy improvement for a strict, index-based selection logic, these rules ensure that the algorithm always makes forward progress and is guaranteed to find a solution in a finite number of steps.