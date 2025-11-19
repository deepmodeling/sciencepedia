## Introduction
Static condensation is a cornerstone technique in computational mechanics, offering a powerful method to reduce the size and complexity of models within the [finite element method](@entry_id:136884) (FEM). By systematically eliminating certain degrees of freedom (DOFs)—typically those internal to a finite element—engineers and scientists can solve vast, complex problems more efficiently. However, its application is often seen as a "black box" operation, obscuring the rich mathematical structure and the broad range of advanced methods it enables. This article aims to demystify [static condensation](@entry_id:176722), bridging the gap between its algebraic theory and its practical implementation.

Across three chapters, this article provides a comprehensive guide to the topic. The first chapter, **Principles and Mechanisms**, breaks down the procedure into its fundamental algebraic components—the Schur complement—and demonstrates how this is applied at the element level in FEM. It also covers the crucial back-substitution process for recovering the full solution. The second chapter, **Applications and Interdisciplinary Connections**, explores how this technique is the engine behind enhanced element formulations, [substructuring](@entry_id:166504), [model order reduction](@entry_id:167302) in dynamics, and even advanced multiphysics and multiscale simulations. Finally, the **Hands-On Practices** chapter offers practical exercises to solidify your understanding of the numerical workflow and its computational implications. To begin our exploration, we will first delve into the fundamental principles and mechanics of the procedure.

## Principles and Mechanisms

In the preceding chapter, we introduced the concept of [static condensation](@entry_id:176722) as a powerful technique for [model order reduction](@entry_id:167302) within the [finite element method](@entry_id:136884). This chapter delves into the underlying principles and mechanical interpretations of this procedure. We will begin by establishing its purely algebraic foundation as a form of block Gaussian elimination, known as Schur complementation. We will then ground this abstract algebra in the context of [finite element analysis](@entry_id:138109), demonstrating how it is used to eliminate local, internal degrees of freedom. Subsequently, we will explore the practical aspects of recovering the full solution, including strains and stresses, and discuss the computational trade-offs involved. Finally, we will examine advanced applications and generalizations, including [substructuring](@entry_id:166504), the treatment of internal mechanisms, and the interaction with various types of constraints.

### The Algebraic Foundation: Schur Complements

At its core, **[static condensation](@entry_id:176722)** is a direct algebraic manipulation of a [partitioned matrix](@entry_id:191785) equation. Consider a general system of linear equations, $\mathbf{K}\mathbf{u} = \mathbf{f}$, where $\mathbf{K}$ is a symmetric matrix. Suppose we partition the vector of unknowns $\mathbf{u}$ into two disjoint subsets: $\mathbf{u}_b$, which we wish to retain (often termed "boundary" or "master" degrees of freedom), and $\mathbf{u}_i$, which we wish to eliminate (the "internal" or "slave" degrees of freedom). The system can be reordered and written in block form:

$$
\begin{pmatrix}
\mathbf{K}_{bb} & \mathbf{K}_{bi} \\
\mathbf{K}_{ib} & \mathbf{K}_{ii}
\end{pmatrix}
\begin{pmatrix}
\mathbf{u}_b \\
\mathbf{u}_i
\end{pmatrix}
=
\begin{pmatrix}
\mathbf{f}_b \\
\mathbf{f}_i
\end{pmatrix}
$$

Here, $\mathbf{K}_{ib} = \mathbf{K}_{bi}^{\mathsf{T}}$ due to the symmetry of $\mathbf{K}$. This block equation represents two coupled [matrix equations](@entry_id:203695):

$$
\mathbf{K}_{bb} \mathbf{u}_b + \mathbf{K}_{bi} \mathbf{u}_i = \mathbf{f}_b \quad (1)
$$
$$
\mathbf{K}_{ib} \mathbf{u}_b + \mathbf{K}_{ii} \mathbf{u}_i = \mathbf{f}_i \quad (2)
$$

The goal is to find an equivalent system that involves only $\mathbf{u}_b$. To achieve this, we first use equation (2) to express $\mathbf{u}_i$ in terms of $\mathbf{u}_b$. Assuming the internal block $\mathbf{K}_{ii}$ is invertible, we can write:

$$
\mathbf{K}_{ii} \mathbf{u}_i = \mathbf{f}_i - \mathbf{K}_{ib} \mathbf{u}_b
$$
$$
\mathbf{u}_i = \mathbf{K}_{ii}^{-1} (\mathbf{f}_i - \mathbf{K}_{ib} \mathbf{u}_b) \quad (3)
$$

This expression for $\mathbf{u}_i$ is then substituted into equation (1):

$$
\mathbf{K}_{bb} \mathbf{u}_b + \mathbf{K}_{bi} \left( \mathbf{K}_{ii}^{-1} (\mathbf{f}_i - \mathbf{K}_{ib} \mathbf{u}_b) \right) = \mathbf{f}_b
$$

By rearranging terms to group coefficients of $\mathbf{u}_b$ on the left-hand side, we arrive at the condensed system:

$$
\left( \mathbf{K}_{bb} - \mathbf{K}_{bi} \mathbf{K}_{ii}^{-1} \mathbf{K}_{ib} \right) \mathbf{u}_b = \mathbf{f}_b - \mathbf{K}_{bi} \mathbf{K}_{ii}^{-1} \mathbf{f}_i
$$

This equation has the form $\mathbf{S} \mathbf{u}_b = \hat{\mathbf{f}}_b$, where:

*   $\mathbf{S} = \mathbf{K}_{bb} - \mathbf{K}_{bi} \mathbf{K}_{ii}^{-1} \mathbf{K}_{ib}$ is the **condensed [stiffness matrix](@entry_id:178659)**, more formally known as the **Schur complement** of the block $\mathbf{K}_{ii}$ in the matrix $\mathbf{K}$.

*   $\hat{\mathbf{f}}_b = \mathbf{f}_b - \mathbf{K}_{bi} \mathbf{K}_{ii}^{-1} \mathbf{f}_i$ is the **condensed [load vector](@entry_id:635284)**, which incorporates the effect of the internal loads $\mathbf{f}_i$ onto the boundary degrees of freedom.

This procedure is an exact algebraic transformation. If the original matrix $\mathbf{K}$ is symmetric and [positive definite](@entry_id:149459), the Schur complement $\mathbf{S}$ is also symmetric and positive definite. The primary advantage emerges when solving this system is computationally cheaper than solving the original, larger system.

To make this process concrete, consider a hypothetical $6 \times 6$ system partitioned into four boundary DoFs and two internal DoFs [@problem_id:2598740]. Let the blocks be defined as:
$$
K_{bb} = \begin{pmatrix}
6 & -2 & 0 & 0 \\
-2 & 5 & -1 & 0 \\
0 & -1 & 4 & -1 \\
0 & 0 & -1 & 3
\end{pmatrix}, \quad
K_{bi} = \begin{pmatrix}
1 & 0 \\
2 & -1 \\
0 & 1 \\
-1 & 2
\end{pmatrix}, \quad
K_{ii} = \begin{pmatrix}
4 & 1 \\
1 & 3
\end{pmatrix}
$$
and the load vectors be $f_b = \begin{pmatrix} 5 & 3 & 4 & 2 \end{pmatrix}^{\mathsf{T}}$ and $f_i = \begin{pmatrix} 1 & -2 \end{pmatrix}^{\mathsf{T}}$.
The first step is to compute the inverse of the internal block, $K_{ii}^{-1} = \frac{1}{11} \begin{pmatrix} 3 & -1 \\ -1 & 4 \end{pmatrix}$. The correction term for the stiffness matrix is $K_{bi} K_{ii}^{-1} K_{ib}$, which evaluates to $\frac{1}{11} \begin{pmatrix} 3 & 7 & -1 & -5 \\ 7 & 20 & -6 & -19 \\ -1 & -6 & 4 & 9 \\ -5 & -19 & 9 & 23 \end{pmatrix}$. The Schur complement is then $S = K_{bb} - K_{bi} K_{ii}^{-1} K_{ib} = \frac{1}{11} \begin{pmatrix} 63 & -29 & 1 & 5 \\ -29 & 35 & -5 & 19 \\ 1 & -5 & 40 & -20 \\ 5 & 19 & -20 & 10 \end{pmatrix}$. Similarly, the load modification term is $K_{bi} K_{ii}^{-1} f_i = \frac{1}{11} \begin{pmatrix} 5 & 19 & -9 & -23 \end{pmatrix}^{\mathsf{T}}$, yielding the condensed [load vector](@entry_id:635284) $\hat{f}_b = f_b - K_{bi} K_{ii}^{-1} f_i = \frac{1}{11} \begin{pmatrix} 50 & 14 & 53 & 45 \end{pmatrix}^{\mathsf{T}}$. The problem is thus reduced from solving a $6 \times 6$ system to solving a smaller, though denser, $4 \times 4$ system.

### Static Condensation in the Finite Element Method

The true power of [static condensation](@entry_id:176722) in [computational engineering](@entry_id:178146) arises when this algebraic procedure is applied to the specific structure of matrices generated by the finite element method (FEM). The key is the careful selection of which degrees of freedom (DoFs) to eliminate.

In the context of a [finite element discretization](@entry_id:193156), particularly with [higher-order elements](@entry_id:750328) ($p \ge 2$), it is natural to distinguish between two types of DoFs on each element [@problem_id:2598736]:

1.  **Boundary/Interface Degrees of Freedom ($u_b$)**: These are DoFs associated with basis functions whose trace is non-zero on the boundary of the element ($\partial K$). For standard nodal elements, these are the DoFs located at the vertices, edges, and faces of the element. These DoFs are typically shared between adjacent elements and are essential for enforcing inter-[element continuity](@entry_id:165046) and assembling the global problem.

2.  **Internal Degrees of Freedom ($u_i$)**: These are DoFs associated with basis functions whose support is contained strictly within a single element $K$. Their trace on the element boundary is zero. Such functions are often called **[bubble functions](@entry_id:176111)**. For nodal elements, these DoFs are located in the interior of the element.

When we partition the global DoFs into these two sets, the global internal stiffness block $K_{ii}$ acquires a crucial property: it becomes **block-diagonal**. This is because an internal basis function in element $K_1$ has no support overlap with an internal [basis function](@entry_id:170178) in a different element $K_2$. Consequently, the stiffness matrix entry coupling them, which is an integral over their overlapping support, is zero. The global $K_{ii}$ matrix is therefore a collection of small, uncoupled blocks, one for each element: $K_{ii} = \text{diag}(K_{ii}^{(1)}, K_{ii}^{(2)}, \dots)$.

This [block-diagonal structure](@entry_id:746869) means that its inverse, $K_{ii}^{-1}$, is also block-diagonal with $K_{ii}^{-1} = \text{diag}((K_{ii}^{(1)})^{-1}, (K_{ii}^{(2)})^{-1}, \dots)$. The expensive operation of inverting a large global matrix is replaced by the far cheaper task of inverting a series of small matrices, one for each element. This allows the condensation to be performed efficiently at the element level, **before** the global system is assembled.

It is critical to distinguish [static condensation](@entry_id:176722) from other [model reduction](@entry_id:171175) or solution strategies [@problem_id:2598778]:
*   It is not **mesh [coarsening](@entry_id:137440)**. Mesh coarsening is a modeling change that creates a new, fundamentally different (and less accurate) discrete problem. Static [condensation](@entry_id:148670) is an exact algebraic reduction of a given discrete system; it yields the same solution for the retained DoFs as solving the full system.
*   It is not **global reordering**. Global reordering is a solver-level permutation strategy applied to the fully assembled matrix, typically to reduce fill-in during factorization. Static [condensation](@entry_id:148670) is a pre-assembly modification of the element-level contributions.

A classic illustration is the 1D quadratic [bar element](@entry_id:746680) with [hierarchical shape functions](@entry_id:169076) [@problem_id:2538541]. For an element of length $L$, the displacement can be written as $u^e(\xi) = d_1 N_1(\xi) + d_2 N_2(\xi) + a N_b(\xi)$, where $d_1, d_2$ are nodal displacements and $a$ is the coefficient of an internal [bubble function](@entry_id:179039), $N_b(\xi) = 1 - \xi^2$. The key property of this hierarchical basis is that the strain field produced by the [bubble function](@entry_id:179039) is orthogonal to the strain field produced by the linear functions. This leads to the coupling block $K_{ib}$ being a [zero matrix](@entry_id:155836). The full $3 \times 3$ [element stiffness matrix](@entry_id:139369) is:
$$
\mathbf{K}^{e} = \frac{AE}{L} \begin{pmatrix} 1 & -1 & 0 \\ -1 & 1 & 0 \\ 0 & 0 & \frac{16}{3} \end{pmatrix}
$$
Here, the retained DoFs are $\mathbf{d}_b = \begin{pmatrix} d_1 & d_2 \end{pmatrix}^{\mathsf{T}}$ and the internal DoF is $\mathbf{d}_i = a$. The Schur complement formula $S^e = K_{bb}^e - K_{bi}^e (K_{ii}^e)^{-1} K_{ib}^e$ simplifies dramatically because $K_{bi}^e = \begin{pmatrix} 0 & 0 \end{pmatrix}^{\mathsf{T}}$. The correction term vanishes, and the condensed [stiffness matrix](@entry_id:178659) is simply the original linear block:
$$
\mathbf{S}^e = \mathbf{K}_{bb}^e = \frac{AE}{L} \begin{pmatrix} 1 & -1 \\ -1 & 1 \end{pmatrix}
$$
In this special but important case, adding a hierarchical [bubble function](@entry_id:179039) does not alter the condensed stiffness relating the nodal DoFs. It does, however, enrich the local [solution space](@entry_id:200470), which can improve accuracy, particularly in capturing local effects of [distributed loads](@entry_id:162746).

### Recovering the Full Solution and Physical Quantities

Solving the global condensed system yields the values of the boundary/interface DoFs, $\mathbf{u}_b$. However, for a complete analysis, particularly for computing [physical quantities](@entry_id:177395) like stress and strain, the full displacement field, including the internal DoFs $\mathbf{u}_i$, is required.

The internal DoFs are recovered on an element-by-element basis via a process called **back-substitution**. The relationship is given by equation (3), applied at the element level [@problem_id:2598758]:
$$
\mathbf{u}_i^e = (K_{ii}^e)^{-1} (\mathbf{f}_i^e - K_{ib}^e \mathbf{u}_b^e)
$$
This calculation is performed for each element after the [global solution](@entry_id:180992) $\mathbf{u}_b$ is known. In practice, one does not explicitly compute the inverse $(K_{ii}^e)^{-1}$. Instead, one first computes the effective right-hand side vector $\mathbf{y}^e = \mathbf{f}_i^e - K_{ib}^e \mathbf{u}_b^e$, and then solves the small linear system $K_{ii}^e \mathbf{u}_i^e = \mathbf{y}^e$. Since $K_{ii}^e$ is [symmetric positive definite](@entry_id:139466) for a well-posed element, this solve is efficient and numerically stable, often using a pre-computed Cholesky factorization.

Once the full displacement vector for the element, $\mathbf{u}^e = \begin{pmatrix} \mathbf{u}_b^e \\ \mathbf{u}_i^e \end{pmatrix}$, has been recovered, the strain and stress fields within the element can be computed using their standard definitions [@problem_id:2598772]. With the [strain-displacement matrix](@entry_id:163451) partitioned as $\mathbf{B} = \begin{pmatrix} \mathbf{B}_b & \mathbf{B}_i \end{pmatrix}$, the strain is:
$$
\boldsymbol{\epsilon} = \mathbf{B}_b \mathbf{u}_b^e + \mathbf{B}_i \mathbf{u}_i^e
$$
The stress then follows from the [constitutive relation](@entry_id:268485), $\boldsymbol{\sigma} = \mathbf{C} \boldsymbol{\epsilon}$. It is crucial to recognize that this procedure is exact; the resulting stress and strain fields are identical to those that would have been obtained by solving the full, uncondensed system.

An alternative, equivalent procedure combines the back-substitution and strain calculation into a single step. By substituting the expression for $\mathbf{u}_i^e$ directly into the strain definition, we get:
$$
\boldsymbol{\epsilon} = \mathbf{B}_b \mathbf{u}_b^e + \mathbf{B}_i \left( (K_{ii}^e)^{-1} (\mathbf{f}_i^e - K_{ib}^e \mathbf{u}_b^e) \right)
$$
$$
\boldsymbol{\epsilon} = \left( \mathbf{B}_b - \mathbf{B}_i (K_{ii}^e)^{-1} K_{ib}^e \right) \mathbf{u}_b^e + \mathbf{B}_i (K_{ii}^e)^{-1} \mathbf{f}_i^e
$$
This expression directly gives the strain from the boundary DoFs $\mathbf{u}_b^e$ and the local internal loads $\mathbf{f}_i^e$. This shows that neglecting the internal [load vector](@entry_id:635284) $\mathbf{f}_i^e$ during post-processing will, in general, lead to incorrect strain and stress results.

### Computational Considerations

The decision to use [static condensation](@entry_id:176722) involves a careful balance of computational costs. While it reduces the size of the global system to be solved, it introduces other complexities [@problem_id:2598752].

First, let us consider the effect on the global matrix. The process of [condensation](@entry_id:148670) is entirely local; it couples DoFs within a single element. It does **not** create new couplings between boundary DoFs that do not already share an element. Therefore, the sparsity pattern, or connectivity graph, of the global condensed matrix $\mathbf{S}$ is identical to that of the global $\mathbf{K}_{bb}$ block from the uncondensed system. However, the local Schur complement block, $S^e = K_{bb}^e - K_{bi}^e (K_{ii}^e)^{-1} K_{ib}^e$, is typically much denser than the original $K_{bb}^e$ block. The update term, $K_{bi}^e (K_{ii}^e)^{-1} K_{ib}^e$, is generally a dense matrix, which introduces non-zero entries (fill-in) where $K_{bb}^e$ may have had zeros. Consequently, the assembled global matrix $\mathbf{S}$ is not sparser than $\mathbf{K}_{bb}$ and often contains more non-zero entries.

For [iterative solvers](@entry_id:136910), which rely on repeated matrix-vector products, one can employ a **matrix-free** approach. Instead of explicitly forming and storing the dense Schur complement matrices $S^e$ or the global matrix $\mathbf{S}$, one can compute the action of $\mathbf{S}$ on a vector $\mathbf{v}_b$ "on the fly". The product $\mathbf{y}_b = \mathbf{S} \mathbf{v}_b$ is computed by looping over elements and accumulating the results of the local operations $\mathbf{y}_b^e = S^e \mathbf{v}_b^e$. Each local operation involves matrix-vector products with $K_{bb}^e$, $K_{bi}^e$, $K_{ib}^e$ and a linear solve with $K_{ii}^e$. This avoids the high memory cost of storing the dense condensed matrices but increases the computational cost of each matrix-vector product compared to a simple multiplication with the original, sparser, uncondensed matrix $\mathbf{K}$. The overall benefit depends on whether the reduction in the number of iterations required for the smaller system outweighs the increased cost per iteration.

Finally, the back-substitution step for post-processing has significant storage implications [@problem_id:2598758]. To recover the internal DoFs $\mathbf{u}_i$, one must have access to the element-level matrices $K_{ii}^e$ and $K_{ib}^e$, and the [load vector](@entry_id:635284) $\mathbf{f}_i^e$. If detailed local stress and strain fields are required, these quantities must be stored for every element after the initial [condensation](@entry_id:148670) step, typically written to disk for large problems. This represents a trade-off: minimizing memory during the global solve by forming and then discarding the condensed contributions, versus retaining substantial element-level data to enable full post-processing.

### Advanced Topics and Generalizations

The principles of [static condensation](@entry_id:176722) extend beyond the simple elimination of element-internal [bubble functions](@entry_id:176111). They form the basis for powerful techniques in domain decomposition and the analysis of complex [constrained systems](@entry_id:164587).

#### Substructuring and Domain Decomposition

The concept of eliminating "internal" DoFs can be generalized by partitioning the entire [computational mesh](@entry_id:168560) into a set of non-overlapping larger regions called **substructures** or subdomains [@problem_id:2598766]. In this context, the "interface unknowns" are the DoFs residing on the skeleton where these substructures meet, while the "internal unknowns" are all DoFs strictly inside each substructure.

The global stiffness matrix can be partitioned based on this interior/interface split. Just as with single elements, the global interior block $K_{II}$ becomes block-diagonal, where each block corresponds to the stiffness of an individual substructure with its boundary held fixed. This allows for a massive-scale [static condensation](@entry_id:176722), where all interior DoFs for all substructures are eliminated in parallel. This results in a Schur complement system defined only on the global interface mesh. This condensed interface problem is smaller but dense and represents the enforcement of [global equilibrium](@entry_id:148976) and compatibility between the subdomains. After solving the interface problem, the solution inside each substructure is recovered via a local back-substitution (solving a local Dirichlet problem). This is the fundamental idea behind [domain decomposition methods](@entry_id:165176) like FETI (Finite Element Tearing and Interconnecting) and BDD (Balancing Domain Decomposition).

#### Handling Singular Internal Blocks

A critical assumption so far has been the invertibility of the internal block $K_{ii}$. However, in [substructuring](@entry_id:166504), it is common for a substructure to be "floating," meaning it is not sufficiently constrained by Dirichlet boundary conditions on its own boundary to prevent [rigid-body motion](@entry_id:265795). In such cases, the local stiffness matrix $K_{II}^{(s)}$ is singular, and its null space consists of the discrete rigid-body modes.

Static [condensation](@entry_id:148670) can be generalized to handle this singular case, but only if certain [compatibility conditions](@entry_id:201103) are met [@problem_id:2598763]. The elimination of $\mathbf{u}_i$ is valid if and only if:
1.  The internal loads must be self-equilibrated: $\mathbf{f}_i \in \text{Range}(\mathbf{K}_{ii})$. This means the internal loads must be orthogonal to the internal rigid-body modes.
2.  The coupling from the boundary must not excite unbalanced [internal forces](@entry_id:167605): $\text{Range}(\mathbf{K}_{ib}) \subseteq \text{Range}(\mathbf{K}_{ii})$.
3.  The internal mechanisms must not induce forces on the boundary: $\mathbf{K}_{bi} \mathcal{N}(\mathbf{K}_{ii}) = \{\mathbf{0}\}$.

When these conditions hold, a unique condensed system can be formed using a [generalized inverse](@entry_id:749785) of $\mathbf{K}_{ii}$. These conditions ensure that the solution process is physically and mathematically consistent, even in the presence of internal mechanisms.

#### Interaction with Boundary Conditions and Constraints

The process of [static condensation](@entry_id:176722) must be performed carefully when other types of constraints are present.

For standard **essential (Dirichlet) boundary conditions** [@problem_id:2598764], the procedure is straightforward. If these conditions are enforced strongly, the corresponding DoFs, $\mathbf{u}_D$, are removed from the set of unknowns. Their prescribed values are moved to the right-hand side of the equations for the remaining free DoFs. Static condensation then proceeds on the resulting smaller system of free unknowns. The prescribed values simply contribute to the modified load vectors before [condensation](@entry_id:148670) begins.

A more subtle issue arises when [static condensation](@entry_id:176722) interacts with **global constraints** enforced by Lagrange multipliers [@problem_id:2598753]. Consider a system where a constraint, such as $G u = 0$, couples DoFs that are being partitioned. The full problem is a saddle-point system involving both $u$ and the Lagrange multiplier $\lambda$. A naive approach might be to first condense the stiffness matrix $K$ by eliminating $u_i$, and then apply the constraint to the remaining DoFs $u_b$. This is incorrect. The Lagrange multiplier represents a global entity, and the equation for eliminating $u_i$ is coupled to $\lambda$. The correct procedure is to perform [static condensation](@entry_id:176722) on the full augmented (saddle-point) system. This results not only in a condensed stiffness matrix but also in modified [constraint equations](@entry_id:138140). Failing to account for the coupling between the internal DoFs and the global constraint during elimination leads to an erroneous final system and an incorrect solution. This illustrates a fundamental rule: [static condensation](@entry_id:176722) is only valid for eliminating DoFs that are truly local to the block being operated on and are not coupled to other unknowns outside that block, unless that coupling is explicitly carried through the [condensation](@entry_id:148670) algebra.