## Introduction
Integer Linear Programming (ILP) is a powerful framework for solving decision-making problems where variables must be whole numbers. A common approach to solving an ILP is to first solve its Linear Program (LP) relaxation, but this often yields fractional, non-implementable solutions. This raises a critical question: how can we systematically refine the problem to exclude these fractional results without eliminating any valid integer solutions?

The answer lies in the [cutting plane method](@entry_id:636911), and at its core is the elegant and powerful Gomory cut. This article provides a thorough exploration of this pivotal technique in integer optimization. First, the "Principles and Mechanisms" chapter will guide you through the fundamental algebraic derivation of the Gomory [fractional cut](@entry_id:637648), explaining how the properties of integers are used to generate [valid inequalities](@entry_id:636383). Next, "Applications and Interdisciplinary Connections" will demonstrate the method's real-world impact in fields from logistics to finance and its synergistic role within advanced algorithms like [branch-and-cut](@entry_id:169438). Finally, the "Hands-On Practices" section will offer exercises to solidify your ability to derive and apply these cuts, bridging theory with practical skill.

## Principles and Mechanisms

In the preceding chapter, we established that the solution to an Integer Linear Program (ILP) can be pursued by first solving its Linear Program (LP) relaxation. If the [optimal solution](@entry_id:171456) to the LP relaxation happens to be integer-valued, it is also the optimal solution to the original ILP. However, it is common for the LP relaxation to yield a solution with fractional values for variables that are constrained to be integers. This chapter details the foundational principles and mechanisms of the **[cutting-plane method](@entry_id:635930)**, a technique for systematically refining the feasible region to exclude such fractional solutions without eliminating any valid integer solutions. At the heart of this method lies the **Gomory [fractional cut](@entry_id:637648)**.

### The Fundamental Derivation of the Gomory Fractional Cut

Imagine we have arrived at an optimal tableau for our LP relaxation, but a basic variable $x_B$, which is required to be an integer, has a fractional value. Let us select the corresponding row from the [simplex tableau](@entry_id:136786). This row can be expressed as an equation:

$x_B + \sum_{j \in N} \bar{a}_{Bj} x_j = \bar{b}_B$

Here, $x_B$ is the basic variable, $N$ is the set of indices for the non-basic variables $x_j$, $\bar{a}_{Bj}$ are the tableau coefficients, and $\bar{b}_B$ is the right-hand side value, which is currently fractional. All variables $x_j$ are non-negative.

The ingenuity of the Gomory cut lies in a simple yet powerful observation about the properties of integers. The derivation begins by decomposing every coefficient $\bar{a}_{Bj}$ and the right-hand side $\bar{b}_B$ into their integer and fractional parts. For any real number $y$, we can write $y = \lfloor y \rfloor + \{y\}$, where $\lfloor y \rfloor$ is the **floor** of $y$ (the greatest integer less than or equal to $y$) and $\{y\}$ is the **[fractional part](@entry_id:275031)** of $y$, satisfying $0 \le \{y\} \lt 1$.

Substituting this decomposition into our tableau equation yields:

$x_B + \sum_{j \in N} (\lfloor \bar{a}_{Bj} \rfloor + \{\bar{a}_{Bj}\}) x_j = \lfloor \bar{b}_B \rfloor + \{\bar{b}_B\}$

We can rearrange this equation to separate the terms that are guaranteed to be integers from the others. We move all terms with integer coefficients and all integer variables to one side:

$x_B + \sum_{j \in N} \lfloor \bar{a}_{Bj} \rfloor x_j - \lfloor \bar{b}_B \rfloor = \{\bar{b}_B\} - \sum_{j \in N} \{\bar{a}_{Bj}\} x_j$

Now, let us analyze this equation from first principles  . In any [feasible solution](@entry_id:634783) to the original ILP, the variable $x_B$ and any integer-constrained non-basic variables $x_j$ must take integer values. If we consider a pure ILP where all variables must be integers, the left-hand side of the equation is a sum and difference of integers and products of integers, and thus must itself be an integer.

Since the left-hand side is an integer, the right-hand side must also be an integer for any feasible integer solution. Let's examine the right-hand side:

$\{\bar{b}_B\} - \sum_{j \in N} \{\bar{a}_{Bj}\} x_j$

By definition, the [fractional part](@entry_id:275031) $\{y\}$ is always non-negative. Since the non-basic variables $x_j$ are also non-negative in a standard [simplex tableau](@entry_id:136786) ($x_j \ge 0$), the summation $\sum_{j \in N} \{\bar{a}_{Bj}\} x_j$ must be non-negative. This is a critical step that relies on the non-negativity of the non-basic variables .

Because the summation term is non-negative, the entire right-hand side expression is less than or equal to $\{\bar{b}_B\}$:

$\{\bar{b}_B\} - \sum_{j \in N} \{\bar{a}_{Bj}\} x_j \le \{\bar{b}_B\}$

We have established two facts about the right-hand side for any valid integer solution:
1.  It must be an integer.
2.  It must be less than or equal to $\{\bar{b}_B\}$, which by definition is strictly less than 1 (since $\bar{b}_B$ is fractional).

The only integer that is strictly less than 1 and can satisfy this condition is 0 or any negative integer. Therefore, the right-hand side must be less than or equal to 0.

$\{\bar{b}_B\} - \sum_{j \in N} \{\bar{a}_{Bj}\} x_j \le 0$

Rearranging this inequality gives us the celebrated **Gomory [fractional cut](@entry_id:637648)**:

$\sum_{j \in N} \{\bar{a}_{Bj}\} x_j \ge \{\bar{b}_B\}$

This new inequality is a **valid cutting plane**. It is satisfied by every feasible integer solution of the original problem, yet it is violated by the current fractional LP solution. The current solution has $x_j = 0$ for all non-basic variables $j \in N$. Substituting these values into the cut yields $0 \ge \{\bar{b}_B\}$. Since we generated the cut from a row where $\bar{b}_B$ was fractional, we know $\{\bar{b}_B\} \gt 0$. The inequality $0 \ge \{\bar{b}_B\}$ is therefore false, proving that the current fractional solution is "cut off" by this new constraint.

### Applying the Gomory Cut: Practical Considerations

The derivation provides a clear formula, but its application requires careful attention to detail. Let us explore some practical examples and conditions.

#### A Basic Calculation

Consider an optimal [simplex tableau](@entry_id:136786) for a pure integer program where one row corresponds to the equation:
$x_1 + \frac{7}{5}x_2 + \frac{2}{5}s_1 = \frac{13}{5}$

Here, $x_1$ is a basic variable with a fractional value of $\frac{13}{5}$, and $x_2$ and $s_1$ are non-basic variables. All variables are non-negative integers. To derive the Gomory cut, we apply the formula $\sum_{j \in N} \{\bar{a}_{Bj}\} x_j \ge \{\bar{b}_B\}$ .

-   The non-basic variables are $x_2$ and $s_1$.
-   The coefficients are $\bar{a}_{1,2} = \frac{7}{5}$ and $\bar{a}_{1,s_1} = \frac{2}{5}$.
-   The right-hand side is $\bar{b}_1 = \frac{13}{5}$.

We compute the fractional parts:
-   $\{\bar{a}_{1,2}\} = \{\frac{7}{5}\} = \{1.4\} = 0.4 = \frac{2}{5}$
-   $\{\bar{a}_{1,s_1}\} = \{\frac{2}{5}\} = \{0.4\} = 0.4 = \frac{2}{5}$
-   $\{\bar{b}_1\} = \{\frac{13}{5}\} = \{2.6\} = 0.6 = \frac{3}{5}$

The resulting Gomory cut is:
$\frac{2}{5}x_2 + \frac{2}{5}s_1 \ge \frac{3}{5}$

For convenience, this inequality can be multiplied by a constant to clear the denominators, yielding $2x_2 + 2s_1 \ge 3$.

#### Handling Negative Coefficients

A common point of confusion arises when tableau coefficients are negative. It is essential to strictly follow the definition of the [floor function](@entry_id:265373). For a negative number $y$, $\lfloor y \rfloor$ is the first integer to its *left* on the number line. For example, $\lfloor -0.4 \rfloor = -1$, not 0.

Consider a tableau row given by :
$x_1 + \frac{3}{5}s_2 - \frac{2}{5}s_3 = \frac{12}{5}$

The coefficients are $\bar{a}_{1,s_2} = \frac{3}{5}$ and $\bar{a}_{1,s_3} = -\frac{2}{5}$. Let's compute their fractional parts:
-   $\{\frac{3}{5}\} = \frac{3}{5}$
-   $\{-\frac{2}{5}\} = \{ -0.4 \} = -0.4 - \lfloor -0.4 \rfloor = -0.4 - (-1) = 0.6 = \frac{3}{5}$

The fractional part of the right-hand side is $\{\frac{12}{5}\} = \frac{2}{5}$. The Gomory cut is therefore:
$\frac{3}{5}s_2 + \frac{3}{5}s_3 \ge \frac{2}{5}$

#### The Trigger Condition for Generating a Cut

The Gomory [fractional cut](@entry_id:637648) method is driven by the presence of fractional values for integer-constrained variables. What happens if a basic variable $x_B$, which must be an integer, already has an integer value $\bar{b}_B$ in the LP optimal tableau?

In this case, the fractional part of the right-hand side is $\{\bar{b}_B\} = 0$. The derived Gomory cut becomes:
$\sum_{j \in N} \{\bar{a}_{Bj}\} x_j \ge 0$

Since $\{\bar{a}_{Bj}\} \ge 0$ and the non-basic variables $x_j \ge 0$, this inequality is always satisfied for any [feasible solution](@entry_id:634783). It is a **trivial inequality** that adds no new information and does not cut off any part of the [feasible region](@entry_id:136622). Therefore, a useful Gomory [fractional cut](@entry_id:637648) can *only* be generated from a tableau row where an integer-constrained basic variable has a fractional value . If all integer-constrained variables have integer values in the LP solution, the algorithm terminates successfully, as an integer-feasible solution has been found.

### Geometric and Theoretical Foundations

While the algebraic manipulation is straightforward, a deeper understanding of Gomory cuts comes from their geometric and theoretical context.

#### Geometric Interpretation: The Integer Hull

The feasible region of the LP relaxation is a **polyhedron**. The feasible integer solutions are a discrete set of points lying within this polyhedron. The **integer hull** is defined as the convex hull of these integer points. The integer hull is itself a polyhedron, and its vertices are all integer-valued. The ultimate goal of any cutting-plane algorithm is to describe the integer hull by adding a set of inequalities to the initial problem formulation.

Each Gomory cut is an inequality that defines a half-space. The key property is that this half-space contains the entire integer hull. The boundary of this half-space, a hyperplane, is a **[supporting hyperplane](@entry_id:274981)** for the integer hull, meaning it "touches" the integer hull without cutting through it . By adding successive cuts, we methodically "shave off" portions of the LP relaxation's [feasible region](@entry_id:136622) that do not contain any integer solutions, bringing us progressively closer to the shape of the integer hull.

To visualize these cuts, it is often necessary to express them in terms of the original decision variables. This is achieved by substituting the definitions of the [slack variables](@entry_id:268374) back into the cut inequality  . For example, the cut $\frac{3}{5}s_2 + \frac{3}{5}s_3 \ge \frac{2}{5}$ derived earlier, after substituting $s_2 = 12 - 3x_1 - 2x_2$ and $s_3 = 12 - 2x_1 - 3x_2$ and simplifying, becomes the inequality $3x_1 + 3x_2 \le 14$. This represents a line in the $(x_1, x_2)$ plane that separates the fractional LP optimum from the integer hull.

#### Deeper Connections: Chvátal-Gomory Cuts and Subadditivity

The Gomory [fractional cut](@entry_id:637648) is not an isolated trick but an elegant instance of more general theoretical principles.

One such principle is the **Chvátal-Gomory (C-G) rounding procedure**. A C-G cut is generated by taking a non-negative linear combination of the original problem constraints to form a new [valid inequality](@entry_id:170492), $\mathbf{a}^T\mathbf{x} \le \beta$. If all components of the vector $\mathbf{a}$ are integer, then for any integer solution $\mathbf{x}$, the left side $\mathbf{a}^T\mathbf{x}$ must be an integer. Thus, it must be less than or equal to the floor of the right side, yielding a new, stronger inequality: $\mathbf{a}^T\mathbf{x} \le \lfloor\beta\rfloor$. It can be shown that any Gomory [fractional cut](@entry_id:637648) can be derived through this more general C-G procedure by choosing the correct [linear combination](@entry_id:155091) of the original constraints . This demonstrates a profound unity between these two methods.

At an even deeper level, the validity of [cutting planes](@entry_id:177960) can be established using the theory of **subadditive functions**. A function $\psi: \mathbb{R} \to \mathbb{R}$ is subadditive if $\psi(u+v) \le \psi(u) + \psi(v)$ for all $u,v$. The [fractional part](@entry_id:275031) function, $\psi(t) = \{t\}$, is a subadditive function. The Gomory [fractional cut](@entry_id:637648) is a special case of a general family of cuts derived from the equation $\sum \alpha_j x_j = \beta$ using a subadditive function $\psi$ to generate the [valid inequality](@entry_id:170492) $\sum \psi(\alpha_j)x_j \ge \psi(\beta)$. The Gomory [fractional cut](@entry_id:637648) corresponds precisely to the choice $\psi(t) = \{t\}$ . Other choices of subadditive functions lead to different families of [valid inequalities](@entry_id:636383), forming the basis for much of modern [integer programming](@entry_id:178386) theory.