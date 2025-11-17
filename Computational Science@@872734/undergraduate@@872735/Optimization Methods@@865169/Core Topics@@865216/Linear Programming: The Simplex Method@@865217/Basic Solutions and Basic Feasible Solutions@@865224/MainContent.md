## Introduction
Linear programming provides a powerful framework for optimizing a linear objective function subject to linear constraints. The set of all permissible solutions forms a geometric shape called a feasible region, which often contains an infinite number of points. The central challenge, then, is to develop a systematic method for navigating this space to find an [optimal solution](@entry_id:171456). Instead of checking every point, the theory of linear programming provides a shortcut by focusing on a finite set of special points: the "corners" or vertices of the [feasible region](@entry_id:136622). This article introduces the algebraic counterparts to these geometric corners—basic solutions and basic feasible solutions.

This article will guide you through the essential theory and application of these fundamental concepts. In the "Principles and Mechanisms" chapter, you will learn the precise algebraic definition of basic and basic feasible solutions, understand their connection to the vertices of the [feasible region](@entry_id:136622), and explore important special cases like degeneracy. Following that, "Applications and Interdisciplinary Connections" will reveal how these concepts are not just theoretical constructs but the cornerstone of solving real-world problems in engineering, data science, and economics. Finally, the "Hands-On Practices" section will allow you to solidify your understanding by applying these principles to concrete examples.

## Principles and Mechanisms

In the study of [linear programming](@entry_id:138188), our focus is typically on problems expressed in **standard form**: maximizing a linear objective function subject to a set of [linear equality constraints](@entry_id:637994) and non-negativity conditions on the variables. For a vector of variables $x \in \mathbb{R}^n$, a [coefficient matrix](@entry_id:151473) $A \in \mathbb{R}^{m \times n}$, a right-hand side vector $b \in \mathbb{R}^m$, and an objective function vector $c \in \mathbb{R}^n$, the standard form is:

Maximize $c^T x$
Subject to $Ax = b$ and $x \ge 0$.

We generally assume that $n > m$ and that the matrix $A$ has full row rank, meaning its $m$ rows are linearly independent. This ensures there are no redundant or contradictory constraints. The set of all points $x$ satisfying $Ax=b$ and $x \ge 0$ is known as the **[feasible region](@entry_id:136622)**, a geometric object called a polyhedron. The core insight of [linear programming](@entry_id:138188) is that optimal solutions lie at special points within this region. This chapter introduces the algebraic counterparts of these special geometric points: basic solutions and basic feasible solutions.

### Defining the Basic Solution

The constraint system $Ax=b$ is an underdetermined [system of linear equations](@entry_id:140416), meaning it typically has infinitely many solutions. To find specific, structured solutions, we employ a strategy of variable partitioning. The $n$ variables are divided into two sets: $m$ **basic variables** and the remaining $n-m$ **non-basic variables**.

The key to this partition lies in the columns of the matrix $A$. A set of $m$ column indices, denoted by an [index set](@entry_id:268489) $B \subset \{1, 2, \dots, n\}$, is chosen to form a **basis**. The fundamental requirement for a valid basis is that the corresponding columns of $A$, when grouped together, form an invertible $m \times m$ matrix. This matrix is called the **[basis matrix](@entry_id:637164)**, denoted $A_B$ (or simply $B$).

A square matrix is invertible if and only if its columns are linearly independent, which is equivalent to its determinant being non-zero. This provides a direct method for verifying if a chosen set of columns constitutes a valid basis [@problem_id:2156419]. For example, given a constraint matrix like:
$$
A = \begin{pmatrix}
1  0  1  1  2 \\
0  1  1  2  4 \\
1  1  2  0  0
\end{pmatrix}
$$
To check if the columns $\{1, 2, 4\}$ can form a basis, we construct the corresponding [basis matrix](@entry_id:637164) $A_B$ and compute its determinant:
$$
A_B = \begin{pmatrix}
1  0  1 \\
0  1  2 \\
1  1  0
\end{pmatrix}
$$
The determinant is $\det(A_B) = 1(0-2) - 0 + 1(0-1) = -3$. Since $\det(A_B) \neq 0$, the matrix is invertible, and $\{1, 2, 4\}$ is a valid basis. In contrast, the set $\{1, 2, 3\}$ would not be a valid basis because the third column is the sum of the first two, making them linearly dependent and the determinant of the corresponding matrix zero.

Once a valid basis $B$ is chosen, a **basic solution** is defined by a two-step procedure:
1.  Set all non-basic variables (those with indices not in $B$) to zero.
2.  Solve the resulting $m \times m$ system for the basic variables, denoted $x_B$.

Let the set of indices for non-basic variables be $N$. We set $x_N = 0$. The system $Ax=b$ simplifies to $A_B x_B + A_N x_N = b$, which becomes $A_B x_B = b$. Since $A_B$ is invertible, this system has a unique solution for the basic variables:
$$
x_B = A_B^{-1} b
$$
The full solution vector $x$ is then formed by combining the values of $x_B$ and the zeros for $x_N$.

For instance, consider the system [@problem_id:2156452]:
$$ A = \begin{pmatrix} 2  1  1  0  3 \\ 1  0  2  1  1 \\ 1  1  0  0  1 \\ \end{pmatrix}, \quad b = \begin{pmatrix} 9 \\ 7 \\ 4 \end{pmatrix} $$
If we choose the basis to correspond to variables $\{x_1, x_3, x_5\}$, the non-basic variables are $x_2$ and $x_4$, which we set to zero. The system reduces to:
$$
\begin{pmatrix} 2  1  3 \\ 1  2  1 \\ 1  0  1 \\ \end{pmatrix} \begin{pmatrix} x_1 \\ x_3 \\ x_5 \end{pmatrix} = \begin{pmatrix} 9 \\ 7 \\ 4 \end{pmatrix}
$$
Solving this system yields the basic variable values $x_1 = \frac{9}{2}$, $x_3 = \frac{3}{2}$, and $x_5 = -\frac{1}{2}$. The complete basic solution vector is $x = (\frac{9}{2}, 0, \frac{3}{2}, 0, -\frac{1}{2})^T$.

### The Basic Feasible Solution (BFS)

The basic solution derived above is a valid solution to the equality constraints $Ax=b$, but it may violate the non-negativity constraint $x \ge 0$. In our example, $x_5 = -\frac{1}{2}$, which is not permissible in a standard form LP. This leads to a critical distinction.

A **basic [feasible solution](@entry_id:634783) (BFS)** is a basic solution that also satisfies the non-negativity constraints. That is, all its components must be non-negative. Since non-basic variables are already zero, this condition simplifies to requiring that all basic variables are non-negative: $x_B = A_B^{-1}b \ge 0$.

Let's analyze some candidate solutions for a given system to solidify these concepts [@problem_id:2156468]. Consider the system $Ax=b$ with:
$$
A = \begin{pmatrix} 1  2  1  0 \\ 1  1  0  1 \\ \end{pmatrix}, \quad b = \begin{pmatrix} 4 \\ 3 \end{pmatrix}
$$
Here, $m=2$ and $n=4$.
- The vector $x_A = (0, 3, -2, 0)^T$ is a solution since $A x_A = b$. Its non-zero components are $x_2$ and $x_3$. The corresponding columns of $A$, $\begin{pmatrix} 2 \\ 1 \end{pmatrix}$ and $\begin{pmatrix} 1 \\ 0 \end{pmatrix}$, are linearly independent. Thus, $x_A$ is a basic solution. However, since $x_3 = -2  0$, it is not a basic *feasible* solution.
- The vector $x_C = (2, 1, 0, 0)^T$ is also a solution ($A x_C = b$). The non-zero components are $x_1$ and $x_2$, whose columns are [linearly independent](@entry_id:148207). Since all components of $x_C$ are non-negative, it is a **basic [feasible solution](@entry_id:634783)**.
- The vector $x_D = (1, 1, 1, 1)^T$ is a [feasible solution](@entry_id:634783), but it has four non-zero components, which is greater than $m=2$. The four corresponding columns of $A$ (which are vectors in $\mathbb{R}^2$) must be linearly dependent. Therefore, by definition, $x_D$ is not a basic solution [@problem_id:2156425].

A key property of a basic solution is that it can have at most $m$ non-zero components. If a feasible solution has more than $m$ non-zero components, the columns of $A$ corresponding to these components cannot be [linearly independent](@entry_id:148207), and thus the solution is not basic.

### Geometric Interpretation: Vertices of the Feasible Polyhedron

The true power of basic feasible solutions comes from their deep connection to the geometry of the [feasible region](@entry_id:136622). This connection is formalized by the **Fundamental Theorem of Linear Programming**:

*A point $x$ is an extreme point (vertex) of the [feasible region](@entry_id:136622) $P = \{x \in \mathbb{R}^n : Ax=b, x \ge 0\}$ if and only if it is a basic [feasible solution](@entry_id:634783).*

An **extreme point**, or **vertex**, is a "corner" of the [feasible region](@entry_id:136622). Formally, a point $x \in P$ is a vertex if it cannot be represented as a convex combination $x = \lambda y + (1-\lambda)z$ for two *distinct* points $y, z \in P$ and a scalar $\lambda \in (0, 1)$. This theorem establishes a [one-to-one correspondence](@entry_id:143935) between the algebraic objects (BFS) and the geometric objects (vertices) [@problem_id:2446114]. This is why the Simplex algorithm, which examines only basic feasible solutions, is guaranteed to find an optimal solution if one exists—because optimal solutions always occur at vertices.

Consider a simple 2D problem to visualize this correspondence [@problem_id:2156431]. A [feasible region](@entry_id:136622) defined by $x_1 + 2x_2 \le 6$, $2x_1 + x_2 \le 8$, and $x_1, x_2 \ge 0$. The vertices of this polygon are found at the intersections of the boundary lines: $(0,0)$, $(4,0)$, $(0,3)$, and $(\frac{10}{3}, \frac{4}{3})$. Let's examine the vertex $(\frac{10}{3}, \frac{4}{3})$. To express this in standard form, we introduce non-negative **[slack variables](@entry_id:268374)** $x_3$ and $x_4$:
$$
\begin{cases}
x_1 + 2x_2 + x_3 = 6 \\
2x_1 + x_2 + x_4 = 8
\end{cases}
$$
At the point $(\frac{10}{3}, \frac{4}{3})$, both original [inequality constraints](@entry_id:176084) are met with equality. This means the corresponding [slack variables](@entry_id:268374) must be zero: $x_3=0$ and $x_4=0$. The non-zero variables are $x_1$ and $x_2$. The number of constraints is $m=2$, and we have two non-zero variables. The columns for $x_1$ and $x_2$ in the standard form matrix, $\begin{pmatrix} 1  2 \\ 2  1 \end{pmatrix}$, are linearly independent. Thus, the vertex $(\frac{10}{3}, \frac{4}{3}, 0, 0)^T$ is indeed a BFS with the basis $\{1, 2\}$. Each vertex of the polygon corresponds to a unique BFS.

The edges of the polyhedron also have an algebraic interpretation. Two vertices are **adjacent** if they are connected by an edge. Algebraically, two BFSs are adjacent if their bases share $m-1$ common indices, meaning one can be obtained from the other by swapping a single column in the basis [@problem_id:2156420]. A non-[degenerate pivot](@entry_id:636499) in the Simplex algorithm corresponds to moving from one vertex along an edge to an adjacent vertex [@problem_id:2446114].

### Special Cases and Degeneracy

While the correspondence between vertices and BFSs is elegant, several important special cases merit discussion.

#### Feasible Regions Without Vertices

Is it possible for a non-empty feasible region to have no basic feasible solutions? Yes. This occurs if the feasible region contains no [extreme points](@entry_id:273616). The Fundamental Theorem still holds; it simply implies that if there are no vertices, there are no BFSs. A classic example is a region defined by two parallel [hyperplanes](@entry_id:268044), such as the strip $-3 \le x_1 - x_2 \le 2$ in $\mathbb{R}^2$ [@problem_id:2156445]. This region is non-empty (e.g., $(0,0)$ is a point), but it is unbounded and has no "corners." Any point in this strip can be expressed as the midpoint of two other points in the strip, meaning no point is a vertex. Consequently, a linear program defined over such a region cannot be solved using the standard Simplex method, which relies on traversing vertices.

#### Degeneracy

A basic solution is called **degenerate** if at least one of its *basic* variables is equal to zero.
This might seem counterintuitive, as we typically associate zero values with non-basic variables. However, it is entirely possible for a variable in the basis to have a value of zero. For example, for a particular system, choosing $\{x_1, x_2\}$ as the basis might result in the basic solution $x = (3, 0, 0, 0)^T$ [@problem_id:2156450]. Here, $x_2$ is a basic variable, but its value is 0. This solution has three zero components, which is more than the $n-m = 4-2=2$ non-basic variables. A non-degenerate BFS has exactly $m$ positive components, while a degenerate BFS has fewer than $m$.

Degeneracy has a significant geometric implication: **multiple bases can correspond to the same vertex**. If a vertex is degenerate, it represents a point where more than the necessary $m$ constraints are active (i.e., hold with equality). Each combination of $m$ of these [active constraints](@entry_id:636830) that defines a valid basis will result in the same BFS.

For example, consider the system with $A = \begin{pmatrix} 2  1  4  -1 \\ 1  1  3  0 \end{pmatrix}$ and $b = \begin{pmatrix} 6 \\ 3 \end{pmatrix}$. The vector $x = (3, 0, 0, 0)^T$ is a degenerate BFS. It can be generated by choosing the basis $\{1, 2\}$, which yields the solution $(x_1, x_2) = (3, 0)$. It can also be generated by choosing the basis $\{1, 3\}$, which yields the solution $(x_1, x_3) = (3, 0)$. Both bases produce the same point in $\mathbb{R}^4$ [@problem_id:2156438]. Geometrically, one vertex is described by two different algebraic bases.

In the context of the Simplex algorithm, degeneracy can lead to "degenerate pivots," where a basis change occurs but the solution vector (the vertex) remains the same. This can potentially cause the algorithm to cycle through different bases for the same vertex without improving the objective function.

In summary, basic feasible solutions are the algebraic pillars upon which the theory and practice of the Simplex method are built. They provide a [finite set](@entry_id:152247) of candidate solutions—the vertices of the [feasible region](@entry_id:136622)—allowing for a systematic search for the optimum. Understanding their properties, their geometric meaning, and the nuances of degeneracy is essential for mastering the principles of [linear optimization](@entry_id:751319).