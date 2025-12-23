## Introduction
Integer programming (IP) is a powerful framework for modeling and solving optimization problems with discrete choices, but finding optimal solutions is notoriously difficult. While the [linear programming](@entry_id:138188) (LP) relaxation of an IP can be solved efficiently, its solution is often fractional, rendering it useless for the original problem. Cutting plane methods provide a systematic and powerful solution to this challenge. This approach bridges the gap between the easy-to-solve continuous relaxation and the hard-to-solve discrete problem by iteratively "cutting off" regions of the continuous space that contain no integer solutions.

This article provides a comprehensive exploration of cutting plane methods, guiding you from fundamental theory to practical application.
- In **Principles and Mechanisms**, you will learn the core ideas behind generating [valid inequalities](@entry_id:636383), from foundational split cuts and Gomory's algebraic methods to powerful combinatorial cuts that exploit a problem's unique structure.
- **Applications and Interdisciplinary Connections** will demonstrate how these theoretical tools are applied to solve real-world problems in logistics, network design, scheduling, and engineering, showcasing the versatility and impact of [cutting planes](@entry_id:177960).
- Finally, **Hands-On Practices** will allow you to solidify your understanding by working through targeted exercises on generating, selecting, and evaluating different types of cuts.

We begin our journey by examining the fundamental principles that allow us to systematically refine an LP relaxation and converge toward an optimal integer solution.

## Principles and Mechanisms

The fundamental challenge of [integer programming](@entry_id:178386) lies in optimizing over a discrete set of points, a task for which the powerful tools of [continuous optimization](@entry_id:166666), such as the simplex method, are not directly applicable. The linear programming (LP) relaxation of an integer program (IP), obtained by dropping the integrality constraints, provides a convex feasible region that can be solved efficiently. However, its optimal solution is often fractional and thus infeasible for the original IP. The core principle of cutting plane methods is to systematically refine the LP relaxation by adding new linear inequalities, known as **cuts** or **[cutting planes](@entry_id:177960)**. A **[valid inequality](@entry_id:170492)** is any inequality that is satisfied by all feasible integer solutions. A cutting plane is a [valid inequality](@entry_id:170492) that is *violated* by the current fractional LP optimal solution. By adding such a cut, we "slice off" a portion of the LP relaxation's feasible set that contains the fractional optimum but contains no feasible integer points, thereby tightening the approximation of the **convex hull** of integer solutions, denoted $\operatorname{conv}(\mathcal{X})$, where $\mathcal{X}$ is the set of feasible integer points. This process is repeated until an integer [optimal solution](@entry_id:171456) to the LP relaxation is found, which is then guaranteed to be an [optimal solution](@entry_id:171456) for the original IP.

### The Foundation: Disjunctive Programming and Split Cuts

The most fundamental and general principle for generating [cutting planes](@entry_id:177960) arises from the inherent disjunctive nature of integer variables. If a variable $x_i$ is required to be an integer, then for any non-integer value $\bar{x}_i$, it must satisfy the disjunction $x_i \le \lfloor \bar{x}_i \rfloor \lor x_i \ge \lceil \bar{x}_i \rceil$. This is known as a **split disjunction**. This observation allows us to partition the [feasible region](@entry_id:136622) of the LP relaxation, $P$, into two [disjoint sets](@entry_id:154341) and then seek the convex hull of their union. The inequalities defining this new convex set are guaranteed to be valid for the IP and may cut off the current fractional solution.

Let's illustrate this with a foundational example. Consider a mixed-integer program where the continuous relaxation is the polyhedron $P = \{ (x,y) \in \mathbb{R}^2 : 2x+y \le 2, x+2y \le 2, x \ge 0, y \ge 0 \}$, and we require $x \in \mathbb{Z}$. The optimal solution to the LP relaxation occurs at the intersection of $2x+y=2$ and $x+2y=2$, which is $(x,y) = (2/3, 2/3)$. Since $x=2/3$ is fractional, we can impose the split disjunction $x \le \lfloor 2/3 \rfloor \lor x \ge \lceil 2/3 \rceil$, which simplifies to $x \le 0 \lor x \ge 1$.

To generate cuts from this disjunction, we form the two sets $P_1 = P \cap \{x \le 0\}$ and $P_2 = P \cap \{x \ge 1\}$.
- For $P_1$, the condition $x \le 0$ combined with the original constraint $x \ge 0$ forces $x=0$. The remaining constraints on $y$ become $y \le 2$ and $2y \le 2$, which simplify to $0 \le y \le 1$. Thus, $P_1$ is the line segment connecting $(0,0)$ and $(0,1)$.
- For $P_2$, the condition $x \ge 1$ combined with the original constraints $2x+y \le 2$ and $y \ge 0$ forces the single point $(1,0)$. Thus, $P_2 = \{(1,0)\}$.

The feasible integer solutions must lie within the set $P_1 \cup P_2$. The strongest [valid inequalities](@entry_id:636383) we can derive from this disjunction are those that define the [convex hull](@entry_id:262864) of this union, $\operatorname{conv}(P_1 \cup P_2)$. The [extreme points](@entry_id:273616) of $P_1 \cup P_2$ are $(0,0)$, $(0,1)$, and $(1,0)$. The convex hull is the triangle with these vertices. This triangle is described by the inequalities $x \ge 0$, $y \ge 0$, and a new inequality defined by the line segment connecting $(0,1)$ and $(1,0)$. This line has the equation $x+y=1$, and the resulting inequality is $x+y \le 1$.

This new inequality, $x+y \le 1$, is a **split cut**. It is valid for all integer solutions by construction. Crucially, it cuts off the fractional LP optimum $(2/3, 2/3)$, since $2/3 + 2/3 = 4/3 > 1$. By adding this single cut to the LP relaxation, we would obtain a new feasible region whose area is only $\frac{1}{2}$, significantly smaller than the original. In this simple case, adding this cut results in a polyhedron whose vertices are all integer, thereby solving the IP .

### Geometric Interpretation: Intersection Cuts from Lattice-Free Sets

The principle of disjunctive programming can be viewed through a powerful geometric lens. A convex set $K \subset \mathbb{R}^n$ is called a **lattice-free set** if its interior contains no points with integer coordinates. The region defined by a split disjunction, such as $S = \{x \in \mathbb{R}^n \mid \lfloor \bar{x}_i \rfloor \le x_i \le \lceil \bar{x}_i \rceil \}$, is a canonical example of a lattice-free set. If our current fractional LP solution $\boldsymbol{v}$ lies in the interior of a lattice-free set $K$, then any feasible integer solution must lie in the set $P \setminus K^\circ$, where $P$ is the LP feasible set and $K^\circ$ is the interior of $K$. The [convex hull](@entry_id:262864) of this set, $\operatorname{conv}(P \setminus K^\circ)$, provides a tighter approximation of the integer hull.

The **intersection cut** is a general method to generate a [valid inequality](@entry_id:170492) from this principle. Consider the corner of the LP polyhedron defined by the current basic feasible solution $\boldsymbol{v}$. This corner can be represented as a cone with apex $\boldsymbol{v}$ and extreme rays $\boldsymbol{r}^1, \boldsymbol{r}^2, \dots$. An intersection cut is generated by finding the points where these rays exit the lattice-free set $K$. The hyperplane passing through these exit points defines a valid cut.

For instance, consider a 2D problem where the current fractional solution is $\boldsymbol{v} = (\frac{1}{2}, \frac{1}{3})$ and the corner is defined by two extreme rays $\boldsymbol{r}^1 = (-1, 2)$ and $\boldsymbol{r}^2 = (2, 1)$. We wish to enforce integrality on $x_1$. The fractional value $x_1 = 1/2$ is in the interior of the lattice-free strip $\mathcal{L} = \{ (x_1, x_2) \mid 0 \le x_1 \le 1 \}$. We find the exit points of the rays from this strip :
- The first ray is parameterized by $\boldsymbol{x}(t) = \boldsymbol{v} + t\boldsymbol{r}^1 = (\frac{1}{2}-t, \frac{1}{3}+2t)$ for $t \ge 0$. It exits the strip when $x_1(t)$ hits $0$ or $1$. It hits $x_1=0$ at $t=1/2$, yielding the point $\boldsymbol{p}^1 = (0, 4/3)$.
- The second ray is $\boldsymbol{x}(t) = \boldsymbol{v} + t\boldsymbol{r}^2 = (\frac{1}{2}+2t, \frac{1}{3}+t)$. It exits when $x_1=1$ at $t=1/4$, yielding the point $\boldsymbol{p}^2 = (1, 7/12)$.

The intersection cut is the line passing through $\boldsymbol{p}^1$ and $\boldsymbol{p}^2$. This line, which has the equation $\frac{9}{16}x_1 + \frac{3}{4}x_2 = 1$, separates the fractional point $\boldsymbol{v}$ from the feasible integer region. The [valid inequality](@entry_id:170492) is $\frac{9}{16}x_1 + \frac{3}{4}x_2 \ge 1$, as $\boldsymbol{v}$ lies on the side of the origin.

### Algebraic Formulation: Gomory's Mixed-Integer Rounding (MIR) Cuts

While the geometric and disjunctive views provide deep intuition, practical implementation in solvers often relies on purely algebraic procedures that operate on the [simplex tableau](@entry_id:136786). The **Gomory Mixed-Integer Rounding (MIR) cut** is one of the most important and widely used classes of general-purpose cuts. It is derived from a single row of the [simplex tableau](@entry_id:136786) corresponding to a basic variable $x_i$ that is constrained to be integer but currently has a fractional value.

Consider a tableau row of the form:
$x = \bar{x} + \sum_{j \in N} r_j y_j$
where $x$ is an integer basic variable, $\bar{x}$ is its current fractional value, $N$ is the set of non-basic variables $y_j \ge 0$, and $r_j$ are the tableau coefficients. Let $f = \bar{x} - \lfloor \bar{x} \rfloor$ be the fractional part of $\bar{x}$. The MIR inequality derived from this row is:
$$ \sum_{j: r_j > 0} \frac{r_j}{1-f} y_j + \sum_{j: r_j  0} \frac{-r_j}{f} y_j \ge 1 $$

Remarkably, this algebraic formula is equivalent to the geometric intersection cut generated from the split disjunction $x \le \lfloor \bar{x} \rfloor \lor x \ge \lceil \bar{x} \rceil$. Let's demonstrate this with an example from a tableau where an integer variable $x$ has the fractional value $\bar{x} = 11/4$, given by the row $x = \frac{11}{4} + 3y_1 - 2y_2$ with non-basic variables $y_1, y_2 \ge 0$ . Here, $f = 11/4 - 2 = 3/4$.
- The geometric intersection cut, derived from the rays $(3,0)$ and $(-2,0)$ in the $(x,y_2)$ and $(x,y_1)$ planes relative to the non-basic variables, yields the inequality $12y_1 + \frac{8}{3}y_2 \ge 1$.
- Applying the MIR formula directly: The coefficient for $y_1$ (with $r_1=3 > 0$) is $\frac{3}{1-3/4} = 12$. The coefficient for $y_2$ (with $r_2=-2  0$) is $\frac{-(-2)}{3/4} = \frac{8}{3}$. The resulting MIR cut is $12y_1 + \frac{8}{3}y_2 \ge 1$.
The results are identical, showing that the MIR cut is the algebraic manifestation of the split intersection cut.

It is crucial to note that the MIR procedure generates a non-trivial cut only when the fractional part $f$ is non-zero. If the right-hand side of a constraint is already an integer in a particular representation, the standard MIR derivation yields a redundant inequality .

### Exploiting Problem Structure: Combinatorial Cuts

While general-purpose cuts like MIR are broadly applicable, they can be weak. For problems with specific combinatorial structures, it is often possible to derive much stronger, problem-specific [valid inequalities](@entry_id:636383).

#### Knapsack Constraints and Cover Inequalities

A common structure in integer programs is the **0-1 knapsack constraint**: $\sum_{i=1}^n a_i x_i \le b$, where $x_i \in \{0,1\}$. A key insight for this structure is the concept of a **cover**. A set of items $C \subseteq \{1, \dots, n\}$ is a **cover** if $\sum_{i \in C} a_i > b$. This means that not all items in the cover can be selected simultaneously. This immediately gives rise to the **[cover inequality](@entry_id:634882)**:
$$ \sum_{i \in C} x_i \le |C|-1 $$
This inequality is often strongest when the cover is **minimal**, meaning that if any single item is removed from $C$, it is no longer a cover.

A basic [cover inequality](@entry_id:634882) can be significantly strengthened through a procedure called **lifting**, where variables not in the original cover are incorporated into the inequality with non-zero coefficients. The logic is to analyze what happens to the cover if a non-cover item $j \notin C$ is selected ($x_j=1$). The available capacity reduces to $b - a_j$, and we can find the maximum number of items from $C$ that can now be selected. This determines the coefficient for $x_j$ in the lifted inequality.

Lifting is crucial because it can generate a cut that strictly dominates the original, unlifted one. For example, consider the knapsack constraint $9x_1 + 8x_2 + 6x_3 + 4x_4 \le 13$ . The set $C=\{1,2\}$ is a cover, yielding the basic [cover inequality](@entry_id:634882) $x_1+x_2 \le 1$. If we lift this inequality by considering $x_3$, we find that if $x_3=1$, the remaining capacity is $13-6=7$. With this capacity, neither item 1 (weight 9) nor item 2 (weight 8) can be selected. This leads to the lifted [cover inequality](@entry_id:634882) $x_1+x_2+x_3 \le 1$. The fractional point $x^* = (1/2, 1/2, 1/2, 0)$ is feasible for the LP relaxation and satisfies the basic [cover inequality](@entry_id:634882) ($1/2+1/2=1 \le 1$). However, it violates the lifted inequality ($1/2+1/2+1/2 = 1.5 > 1$), demonstrating that the lifted inequality is strictly stronger.

The strongest possible [valid inequalities](@entry_id:636383) are those that define a **facet** (an $(n-1)$-dimensional face) of the integer hull. For an unlifted [cover inequality](@entry_id:634882) to be facet-defining, the cover must be minimal, and an additional technical condition must hold related to the ability to "extend" solutions on the face with items not in the cover .

#### Stable Set Problems and Clique Inequalities

Another classic [combinatorial optimization](@entry_id:264983) problem is the **maximum weight stable set problem** on a graph $G=(V,E)$. A stable set is a subset of vertices where no two vertices are adjacent. If we let $x_i=1$ when vertex $i$ is in the set, the problem can be modeled with edge constraints $x_u+x_v \le 1$ for all $(u,v) \in E$.

A powerful class of cuts for this problem comes from **cliques**. A [clique](@entry_id:275990) $C \subseteq V$ is a set of vertices that are all pairwise adjacent. By definition, a stable set can contain at most one vertex from any clique. This gives the valid **[clique](@entry_id:275990) inequality**:
$$ \sum_{i \in C} x_i \le 1 $$
These inequalities are often much stronger than the basic edge inequalities (which are just clique inequalities for cliques of size 2). For example, consider a graph containing a triangle on vertices $\{1,2,3\}$. The LP relaxation with only edge constraints allows the fractional solution $x_1=x_2=x_3=1/2$. The [clique](@entry_id:275990) inequality $x_1+x_2+x_3 \le 1$ cuts this point off, as $1/2+1/2+1/2 = 3/2 > 1$ .

For a special class of graphs known as **[perfect graphs](@entry_id:276112)** (which includes [chordal graphs](@entry_id:275709)), the stable set polytope is completely described by the non-negativity constraints and the [clique](@entry_id:275990) inequalities for all maximal cliques. In such cases, adding all [clique](@entry_id:275990) cuts to the LP relaxation is sufficient to solve the problem to optimality.

### The Power of Multi-Row Cuts

The cuts discussed thus far, such as MIR and basic [cover inequalities](@entry_id:635816), are often derived from a single constraint of the IP. However, by aggregating or combining information from multiple constraints, we can often generate significantly stronger cuts.

Consider a simple problem with two constraints: $0.5x_1 + 0.7x_2 + y \le 1$ and $0.7x_1 + 0.5x_2 + y \le 1$, with $x_1, x_2 \in \{0,1\}$ and $y \ge 0$. The LP [optimal solution](@entry_id:171456) is $(x_1, x_2) = (5/6, 5/6)$, with an objective value of $95/6$, while the true integer optimum is $10$. Because the right-hand sides of both constraints are integers, single-row MIR cuts are trivial and provide no improvement.

However, if we sum the two constraints, we obtain $1.2x_1 + 1.2x_2 + 2y \le 2$. Since $y \ge 0$, this implies the [valid inequality](@entry_id:170492) $1.2x_1 + 1.2x_2 \le 2$, or $x_1+x_2 \le 5/3$. Because $x_1$ and $x_2$ must be integers, their sum must be an integer. We can therefore round down the right-hand side to obtain the valid integer inequality $x_1+x_2 \le \lfloor 5/3 \rfloor = 1$. This is an example of a **Chvátal-Gomory rounding cut**. Adding this single, two-row intersection cut to the LP relaxation is sufficient to find the true integer optimum, closing 100% of the [integrality gap](@entry_id:635752) that was untouchable by single-row methods . This demonstrates the immense potential of multi-row or aggregation-based cuts.

### Practical Considerations in Cut Selection

In a typical run of a cutting plane algorithm, a solver may generate dozens or even hundreds of candidate cuts at each node of the [branch-and-bound](@entry_id:635868) tree. Adding all of them would make the LP relaxation prohibitively large and slow to solve. Therefore, solvers employ sophisticated [heuristics](@entry_id:261307) to select a small subset of "good" cuts to add. The quality of a cut can be measured by several metrics .

- **Violation**: For a cut $a^\top x \le b$ and a fractional point $x^*$, the violation is $v = a^\top x^* - b$. This measures how infeasible $x^*$ is with respect to the cut. A larger violation is generally preferred, as it signals a "deeper" cut in some sense.

- **Efficacy**: This is the Euclidean distance from $x^*$ to the cut hyperplane, given by $e = v / \|a\|_2$. It normalizes the violation by the magnitude of the cut's coefficients, providing a scale-invariant measure of distance. It can be a more reliable indicator of the geometric distance by which the point is separated.

- **Depth**: This measures how far one can travel from $x^*$ along the cut's inward normal direction before hitting a boundary of the original LP feasible region. A cut that is nearly parallel to an existing active constraint will have a small depth, suggesting it might not alter the [feasible region](@entry_id:136622)'s geometry substantially.

There is often a trade-off between these metrics. For instance, a cut might have the highest violation but also be very "deep," meaning it is far from the existing boundaries. Another cut might have a smaller violation but be very "shallow," potentially leading to a larger improvement in the [objective function](@entry_id:267263) in the subsequent LP solve. Modern solvers use a combination of these and other metrics, such as the angle the cut makes with the objective function vector, to select a diverse and effective portfolio of cuts at each iteration. For example, when comparing three cuts, one might select the cut that offers the best compromise, such as having the highest violation among those with low depth, to maximize progress while maintaining a well-conditioned feasible set .