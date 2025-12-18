## Introduction
The [simplex method](@entry_id:140334) is a cornerstone algorithm for solving linear programming problems, and its analysis is often simplified by the assumption of non-degeneracy. However, in many real-world and theoretical problems, this assumption does not hold. The presence of **degeneracy**—where a basic [feasible solution](@entry_id:634783) includes basic variables with a value of zero—introduces significant complexities that can hinder the algorithm's performance and even prevent it from terminating. This article addresses the knowledge gap between the idealized, non-degenerate simplex method and its behavior in the face of this common and challenging condition.

Across three chapters, this article provides a comprehensive exploration of degeneracy and its consequences. The first chapter, **"Principles and Mechanisms,"** delves into the fundamental nature of degeneracy from both algebraic and geometric perspectives, explaining how it leads to stalling and the more severe issue of cycling. The second chapter, **"Applications and Interdisciplinary Connections,"** reveals how degeneracy is not just a theoretical edge case but a prevalent feature in problems across financial modeling, [network optimization](@entry_id:266615), and game theory, offering insights into both problem structure and algorithmic behavior. Finally, the **"Hands-On Practices"** chapter provides opportunities to engage directly with these concepts through targeted exercises. By navigating these sections, you will gain a robust understanding of why degeneracy occurs, how it impacts the simplex method, and the essential techniques used to overcome it.

## Principles and Mechanisms

In the study of the simplex method, the assumption of non-degeneracy simplifies the analysis of the algorithm's convergence and behavior. However, in both theoretical and practical linear programming problems, this assumption is frequently violated. This chapter delves into the principle of **degeneracy**, exploring its fundamental nature, its mechanistic effects on the [simplex algorithm](@entry_id:175128), and the profound consequences it holds for both theoretical analysis and practical implementation.

### The Nature of Degeneracy: Algebraic and Geometric Perspectives

We begin with the formal definition of degeneracy in the context of a linear program in standard form: minimize $c^{\top} x$ subject to $A x = b$ and $x \ge 0$, where $A \in \mathbb{R}^{m \times n}$ has full row rank.

A **basic [feasible solution](@entry_id:634783) (BFS)** is defined by a basis—a set of $m$ linearly independent columns from $A$. The variables corresponding to these columns are the **basic variables**, while the remaining $n-m$ are **non-basic variables**. The BFS is found by setting the non-basic variables to zero and solving for the basic variables. Algebraically, a BFS is **degenerate** if at least one of its basic variables has a value of zero.

This simple algebraic definition has a deep geometric interpretation. A BFS corresponds to a vertex of the feasible polyhedron. In an $n$-dimensional space, a vertex is typically defined by the intersection of $n$ [linearly independent](@entry_id:148207) constraint hyperplanes. For a standard form LP, any feasible point $x$ must satisfy the $m$ equality constraints $Ax=b$. A constraint $x_j \ge 0$ is considered **active** at $x$ if $x_j=0$. For any BFS, the $n-m$ non-negativity constraints corresponding to the non-basic variables are active by definition. Together with the $m$ equality constraints, this provides the requisite $n$ [active constraints](@entry_id:636830) to define a vertex.

In a non-degenerate BFS, all basic variables are strictly positive, so exactly $n-m$ non-negativity constraints are active. The total number of [active constraints](@entry_id:636830) is precisely $m+(n-m)=n$. However, if a BFS is degenerate, at least one basic variable, say $x_k$, is zero. This means that in addition to the $n-m$ non-negativity constraints for non-basic variables, at least one extra non-negativity constraint, $x_k=0$, is also active. Consequently, a [degenerate vertex](@entry_id:636994) is a point where more than $n$ constraint hyperplanes of the [feasible region](@entry_id:136622) intersect. It is an "over-determined" point. 

This geometric property can be used to detect degeneracy. A given BFS is degenerate if and only if the set of gradients of all its [active constraints](@entry_id:636830) is linearly dependent. Equivalently, the number of [active constraints](@entry_id:636830), $k_{active}$, is strictly greater than the rank of the matrix formed by their gradients. 

To make this concrete, consider the [feasible region](@entry_id:136622) in $\mathbb{R}^3$ defined by the inequality $|x_1| + |x_2| + |x_3| \le 1$. This shape is a regular octahedron. A vertex of a polyhedron in $\mathbb{R}^3$ is non-degenerate if it is the intersection of exactly three faces (facets). Let us examine the vertex $v = (1, 0, 0)$. By substituting these coordinates into the eight inequalities that define the octahedron (e.g., $x_1+x_2+x_3 \le 1$, $x_1+x_2-x_3 \le 1$, etc.), we find that this vertex lies on four distinct facets:
- $x_1 + x_2 + x_3 \le 1$
- $x_1 + x_2 - x_3 \le 1$
- $x_1 - x_2 + x_3 \le 1$
- $x_1 - x_2 - x_3 \le 1$

Since the vertex $(1,0,0)$ is the meeting point of four facets, which is more than the dimension of the space (three), it is a [degenerate vertex](@entry_id:636994). 

### Multiple Bases for a Single Vertex

A critical consequence of a vertex being over-determined is that it can be represented by multiple, distinct bases in the [simplex algorithm](@entry_id:175128). If a vertex is the intersection of more than $n$ constraint hyperplanes, we can select different subsets of $n$ [linearly independent](@entry_id:148207) [hyperplanes](@entry_id:268044) from this larger collection to define the very same point. Each such selection corresponds to a different basis.

Consider a simple LP with constraints in $\mathbb{R}^2$ ($m=2$) and three variables ($n=3$):
$$A = \begin{pmatrix} 1  & 0 & 0 \\ 0 & 1 & 1 \end{pmatrix}, \quad b = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$$
Let's find the BFS for this system. There are two valid bases:
1.  Basis $B_1$ from columns $\{A_1, A_2\}$: The basic variables are $\{x_1, x_2\}$. Setting the non-basic variable $x_3=0$, we solve $B_1 x_B = b$, yielding $x_1=1, x_2=0$. The BFS is $x^\star = (1, 0, 0)^{\top}$. Notice the basic variable $x_2$ is zero.
2.  Basis $B_2$ from columns $\{A_1, A_3\}$: The basic variables are $\{x_1, x_3\}$. Setting the non-basic variable $x_2=0$, we solve $B_2 x_B = b$, yielding $x_1=1, x_3=0$. The BFS is also $x^\star = (1, 0, 0)^{\top}$. Here, the basic variable $x_3$ is zero.

In this case, two different bases correspond to the exact same vertex, $x^\star$. This is the algebraic manifestation of degeneracy.  Returning to our geometric octahedron example, the four active facets at vertex $v=(1,0,0)$ have [linearly independent](@entry_id:148207) normal vectors. Any subset of three of these four facet normals also constitutes a [linearly independent](@entry_id:148207) set and their intersection uniquely defines the point $v$. There are $\binom{4}{3} = 4$ such subsets. This means the single [degenerate vertex](@entry_id:636994) $v=(1,0,0)$ corresponds to four distinct basic feasible solutions in the associated LP formulation. 

### Degenerate Pivots and Stalling

The presence of degeneracy has a direct and observable impact on the execution of the [simplex algorithm](@entry_id:175128). When the algorithm is at a degenerate BFS, it can perform what is known as a **[degenerate pivot](@entry_id:636499)**.

In a [simplex tableau](@entry_id:136786), a degenerate BFS is identified by one or more zero entries in the right-hand-side (RHS) column for rows corresponding to basic variables. When selecting a leaving variable, the [simplex method](@entry_id:140334) employs the **[minimum ratio test](@entry_id:634935)**. The step length, $\theta$, for the entering variable is the minimum of the ratios of RHS values to positive coefficients in the pivot column. If the RHS value for a potential leaving variable is zero, the minimum ratio will be zero.

A [pivot operation](@entry_id:140575) where the step length $\theta = 0$ is a [degenerate pivot](@entry_id:636499). The change in the [objective function](@entry_id:267263) value, $\Delta z$, is calculated as the product of the entering variable's [reduced cost](@entry_id:175813) and the step length $\theta$. In a [degenerate pivot](@entry_id:636499), $\Delta z = \bar{c}_j \cdot 0 = 0$. The [objective function](@entry_id:267263) does not improve. 

Furthermore, since the step length is zero, the values of the variables in the BFS do not change either. The algorithm pivots to a new basis, but it remains at the exact same vertex in the [feasible region](@entry_id:136622).  This phenomenon, where the algorithm performs one or more pivots that change the basis but do not change the objective value or the solution vector, is known as **stalling**.

For instance, consider an LP where the initial BFS is degenerate, with basic variables $s_2=0$ and $s_3=0$. A particular pivot rule might select $x_1$ to enter the basis. If the [minimum ratio test](@entry_id:634935) determines that $s_2$ must leave, and the ratio is $0$, the algorithm performs a [degenerate pivot](@entry_id:636499). The basis changes from $\{s_1, s_2, s_3\}$ to $\{s_1, x_1, s_3\}$, but the solution vector and objective value remain unchanged. In the next iteration, the algorithm might again perform a [degenerate pivot](@entry_id:636499), for example by having $x_2$ enter and $s_3$ leave. Only on a subsequent pivot might the algorithm encounter a non-zero minimum ratio, finally allowing it to move to a new vertex and improve the [objective function](@entry_id:267263). This sequence of pivots with no objective improvement is a clear demonstration of stalling. 

### From Stalling to Cycling

While stalling merely slows down the algorithm's progress, it is a symptom of a more severe potential pathology: **cycling**. Cycling occurs when a sequence of degenerate pivots leads the simplex method back to a basis it has previously visited. Once the algorithm re-enters a basis in a cycle, it will follow the same sequence of pivots indefinitely, never terminating.

We can visualize the process of the simplex method as a path on a directed graph, where the vertices represent all possible bases and the directed edges represent valid simplex pivots. A pivot from basis $B$ to $B'$ results in an objective value change $\Delta z = \bar{c}_j \theta$. For a maximization problem with a standard pivot rule (entering variable has $\bar{c}_j > 0$), any pivot that strictly increases the objective value ($\theta > 0$) must lead to a new vertex that has not been visited before. Therefore, a cycle in this basis graph can only consist of edges for which $\Delta z = 0$. This requires that all pivots in the cycle must be degenerate pivots ($\theta=0$). This, in turn, can only happen if the algorithm is at a degenerate BFS. 

Thus, the necessary conditions for cycling are:
1.  The linear program must have at least one degenerate BFS.
2.  The pivot rule used must be able to select a sequence of basis changes that loops back on itself.

Cycling is not just a theoretical curiosity. The choice of pivot rule is critical. For example, **Dantzig's rule**, which selects the entering variable with the largest positive [reduced cost](@entry_id:175813), is susceptible to cycling. A famous problem constructed by E. M. L. Beale provides a concrete instance where, starting from a degenerate BFS, applying Dantzig's rule leads to a cycle of six degenerate pivots, after which the algorithm returns to the initial basis and loops forever. 

### Anti-Cycling Rules: Guaranteeing Finiteness

To ensure that the [simplex method](@entry_id:140334) always terminates, we must use a pivot rule that provably avoids cycles. Such rules are known as **[anti-cycling rules](@entry_id:637416)**. They do not eliminate degeneracy or prevent degenerate pivots; rather, they provide a systematic way of choosing variables during ties so that returning to a previous basis is impossible.

The most famous anti-cycling procedure is **Bland's rule**, or the smallest index rule. It consists of two parts:
1.  **Entering Variable Choice**: Among all non-basic variables with a favorable [reduced cost](@entry_id:175813) (e.g., positive for maximization), choose the one with the smallest index to enter the basis.
2.  **Leaving Variable Choice**: If two or more variables tie for the [minimum ratio test](@entry_id:634935), choose the one with the smallest index to leave the basis.

It can be proven that the simplex method, when equipped with Bland's rule, will always terminate in a finite number of iterations. Applying Bland's rule to Beale's cycling example successfully breaks the cycle and guides the algorithm to the optimal solution.  Other [anti-cycling rules](@entry_id:637416), such as the **lexicographic (or perturbation) method**, also exist and provide the same guarantee of finiteness.

### Broader Consequences of Degeneracy

The impact of degeneracy extends beyond the behavior of the [simplex algorithm](@entry_id:175128). It has fundamental implications for [duality theory](@entry_id:143133) and presents significant challenges for numerical implementation.

#### Duality and Sensitivity Analysis

In the theory of [linear programming](@entry_id:138188), the [dual variables](@entry_id:151022) are often interpreted as **[shadow prices](@entry_id:145838)**, representing the marginal value of each resource corresponding to the constraints. For a non-degenerate optimal solution, these shadow prices are unique. However, if the primal [optimal solution](@entry_id:171456) is degenerate, the dual [optimal solution](@entry_id:171456) may not be unique.

This non-uniqueness arises from the [complementary slackness](@entry_id:141017) conditions. For an optimal primal-dual pair $(x^*, y^*)$, if a primal variable $x_j^*$ is positive, the corresponding dual constraint must be tight. Degeneracy means that some basic variables are zero, which relaxes the requirement for their corresponding dual constraints to be tight. This can create a space of feasible dual solutions that all achieve the optimal dual objective value.

For example, in a resource allocation problem with a degenerate [optimal solution](@entry_id:171456), we might find that the optimal [shadow prices](@entry_id:145838) $(y_1, y_2)$ are not a single point but rather a line segment, say connecting $(3,0)$ to $(0,3)$. This implies an ambiguity in the marginal valuation of the resources. One set of prices, $(3,0)$, suggests resource 1 is the sole bottleneck with a high marginal value, while resource 2 is in surplus. Another valid set, $(0,3)$, suggests the opposite. This ambiguity makes standard [sensitivity analysis](@entry_id:147555) difficult, as the [marginal value of a resource](@entry_id:634589) depends on the direction in which its availability is perturbed. 

#### Numerical Stability and Robust Implementation

In practice, computations are performed using [floating-point arithmetic](@entry_id:146236), where exact zeros are rare. Problems are often not perfectly degenerate but **nearly degenerate**, with some basic variables being very small positive numbers (e.g., $10^{-9}$). This situation is often linked to **[ill-conditioning](@entry_id:138674)** of the [basis matrix](@entry_id:637164), where columns are nearly linearly dependent. Such problems pose significant numerical challenges.

A robust implementation of the simplex method must therefore go beyond theoretical [anti-cycling rules](@entry_id:637416) and incorporate strategies to handle the realities of [floating-point arithmetic](@entry_id:146236). Key practices include:
- **Scaling**: Before starting the algorithm, the rows and columns of the constraint matrix are scaled to have similar magnitudes. This improves the [numerical conditioning](@entry_id:136760) and makes subsequent choices more reliable.
- **Tolerances**: Instead of testing for exact equality to zero, robust codes use tolerances. For example, a value is considered zero if its absolute value is less than a feasibility tolerance (e.g., $10^{-12}$), and a [reduced cost](@entry_id:175813) is considered non-positive if it is less than an optimality tolerance. These prevent the algorithm from chasing insignificant improvements caused by [rounding errors](@entry_id:143856).
- **Pivot Threshold**: To avoid catastrophic [error propagation](@entry_id:136644), pivot elements with a magnitude below a certain threshold (e.g., $10^{-10}$) are rejected. Division by a near-zero number that is mostly noise can corrupt the entire computation.

A state-of-the-art [simplex](@entry_id:270623) solver combines a theoretically sound anti-cycling rule like Bland's rule with these essential numerical hygiene techniques to ensure both guaranteed termination and [numerical stability](@entry_id:146550), even in the face of degeneracy and [ill-conditioning](@entry_id:138674). 