## Introduction
The simplex method is a cornerstone of [mathematical optimization](@entry_id:165540), providing a systematic way to solve linear programming problems. However, when applied to the large-scale problems common in modern industry and science, the standard tableau-based approach can become computationally slow and memory-intensive. This creates a critical challenge: how can we harness the power of the [simplex algorithm](@entry_id:175128) for problems with thousands of variables without being overwhelmed by the computational cost? The **Revised Simplex Method (RSM)** provides the answer. It is a refined and more efficient implementation that achieves the same results by focusing only on the essential information needed at each step.

This article provides a comprehensive exploration of the Revised Simplex Method, structured to build both theoretical understanding and practical skill. The first chapter, **Principles and Mechanisms**, will dissect the core mechanics of the algorithm, explaining how it leverages the basis inverse to gain a significant computational edge over the standard method. Next, **Applications and Interdisciplinary Connections** will demonstrate the RSM's power beyond simple problem-solving, showcasing its indispensable role in sensitivity analysis, economic interpretation, and as a foundational engine for advanced [optimization techniques](@entry_id:635438). Finally, **Hands-On Practices** will offer a set of guided problems to help you apply the concepts and solidify your mastery of the algorithm's execution. By the end, you will understand not just how the Revised Simplex Method works, but why it is a fundamental tool for optimizers today.

## Principles and Mechanisms

The standard [simplex method](@entry_id:140334), with its iterative updates to a full tableau, provides a complete and intuitive picture of the algorithm's progression. However, for large-scale linear programming problems, especially those where the number of variables significantly exceeds the number of constraints, manipulating the entire tableau at each step becomes computationally prohibitive. The **Revised Simplex Method (RSM)** offers a more efficient alternative by maintaining and updating only the essential information required for each iteration. Instead of transforming the entire constraint matrix, the RSM focuses on the basis inverse, a much smaller $m \times m$ matrix, where $m$ is the number of constraints. This chapter elucidates the core principles and computational mechanisms that underpin the efficiency and power of the Revised Simplex Method.

### Computational Efficiency: A Tale of Two Methods

The primary motivation for the Revised Simplex Method is its computational superiority over the standard tableau method for a wide class of problems. An iteration in the standard simplex method requires updating every entry in the tableau, which typically has dimensions of $(m+1) \times (n+1)$, where $m$ is the number of constraints and $n$ is the number of decision variables. The computational work is therefore proportional to $m \times n$.

In contrast, the Revised Simplex Method avoids forming the full tableau. Its computational effort is dominated by operations involving the $m \times m$ basis inverse. Consider a problem with $m$ constraints and $N$ total variables (decision plus slack/[surplus variables](@entry_id:167154)), where $N \gg m$.

*   The cost of a **standard [simplex](@entry_id:270623)** iteration is roughly proportional to updating the tableau, which can be modeled as $C_S \propto mN$.
*   The cost of a **revised simplex** iteration involves two main parts: operations with the $m \times m$ basis inverse (e.g., updating it and calculating [simplex multipliers](@entry_id:177701)), which cost on the order of $m^2$, and the pricing step to calculate [reduced costs](@entry_id:173345) for all non-basic variables, which costs on the order of $m(N-m)$.

As demonstrated in a comparative analysis , the RSM becomes dramatically more efficient as the disparity between $N$ and $m$ grows. By focusing only on the necessary matrix-vector products involving the basis inverse, the RSM avoids the costly updates of the $(N-m)$ columns corresponding to non-basic variables, most of which will not change from one iteration to the next.

### The Anatomy of a Revised Simplex Iteration

An iteration of the Revised Simplex Method can be deconstructed into three main phases: pricing, the [ratio test](@entry_id:136231), and the pivot update. We begin by assuming we have a current [basis matrix](@entry_id:637164) $B$, its inverse $B^{-1}$, and the corresponding basic feasible solution $x_B = B^{-1}b$.

#### Phase 1: Pricing and Selecting the Entering Variable

The first step is to determine if the current basic [feasible solution](@entry_id:634783) is optimal and, if not, to select a non-basic variable to enter the basis that will improve the objective function value. This is achieved by computing the **[reduced cost](@entry_id:175813)** for each non-basic variable.

The key to this process is a vector known as the **[simplex multipliers](@entry_id:177701)** or **[dual variables](@entry_id:151022)**, denoted by the row vector $\pi^T$. This vector is computed using the inverse of the current [basis matrix](@entry_id:637164), $B^{-1}$, and the row vector of objective function coefficients for the basic variables, $c_B^T$. The defining formula is:

$$
\pi^T = c_B^T B^{-1}
$$

For instance, in an optimization problem to schedule microprocessor production, if the basic variables are $x_1$ and $x_2$ with [objective coefficients](@entry_id:637435) $c_B^T = \begin{pmatrix} 5 & 8 \end{pmatrix}$ and the basis inverse is $B^{-1} = \begin{pmatrix} -1/7 & 3/7 \\ 3/7 & -2/7 \end{pmatrix}$, the [simplex multipliers](@entry_id:177701) are calculated as $\pi^T = \begin{pmatrix} 5 & 8 \end{pmatrix} B^{-1} = \begin{pmatrix} 19/7 & -1/7 \end{pmatrix}$ .

Once $\pi^T$ is known, the [reduced cost](@entry_id:175813), $\bar{c}_j$, for any non-basic variable $x_j$ can be efficiently calculated. The [reduced cost](@entry_id:175813) represents the change in the [objective function](@entry_id:267263) for each unit increase of the variable $x_j$, while holding all other non-basic variables at zero. It is given by:

$$
\bar{c}_j = c_j - \pi^T a_j
$$

Here, $c_j$ is the original objective coefficient of $x_j$, and $a_j$ is the corresponding column vector from the original constraint matrix $A$.

For a maximization problem, if all [reduced costs](@entry_id:173345) are non-positive ($\bar{c}_j \le 0$ for all non-basic $j$), the current solution is optimal. If one or more [reduced costs](@entry_id:173345) are positive, we can improve the solution. Typically, the non-basic variable with the most positive [reduced cost](@entry_id:175813) is selected as the **entering variable**. For example, having computed the [simplex multipliers](@entry_id:177701), we can find the [reduced cost](@entry_id:175813) for a non-basic variable $x_2$ by computing $\bar{c}_2 = c_2 - \pi^T a_2$ . A positive $\bar{c}_2$ would indicate that increasing $x_2$ from zero will increase the total profit.

#### Phase 2: The Ratio Test and Selecting the Leaving Variable

After selecting an entering variable, say $x_q$, we must determine which current basic variable will leave the basis. Increasing $x_q$ from zero will cause the values of the current basic variables, $x_B$, to change in order to maintain feasibility (i.e., continue satisfying the equation $Ax=b$). The rate of this change is determined by the **updated column** vector $d$, which represents the column $a_q$ in terms of the current basis:

$$
d = B^{-1} a_q
$$

This vector $d$ tells us how the basic variables must be adjusted: for every unit increase in $x_q$, the vector of basic variables $x_B$ changes by $-d$. That is, if $x_q$ increases by an amount $\theta$, the new vector of basic variables will be $x_B - \theta d$.

An interesting property arises when we compute the updated column for a variable that is already in the basis. If the $k$-th basic variable is $x_j$, then its column $a_j$ is the $k$-th column of the [basis matrix](@entry_id:637164) $B$. Therefore, $d = B^{-1} a_j = B^{-1} (k\text{-th column of } B)$, which results in a vector of zeros with a 1 in the $k$-th position .

To find the **leaving variable**, we must ensure that all variables remain non-negative. We increase the entering variable $x_q$ by an amount $\theta$ until one of the current basic variables is driven to zero. The new values of the basic variables will be $(x_B)_i - \theta d_i$. To maintain non-negativity, we require $(x_B)_i - \theta d_i \ge 0$. This condition is only restrictive for components where $d_i > 0$. The maximum possible increase $\theta$ is therefore determined by the **min-[ratio test](@entry_id:136231)**:

$$
\theta = \min \left\{ \frac{(x_B)_i}{d_i} \mid d_i > 0 \right\}
$$

The basic variable $(x_B)_r$ in the row $r$ that yields this minimum ratio is the one that will reach zero first. It is designated as the leaving variable.

#### Phase 3: The Pivot and Updating the Basis

The final step in the iteration is the pivot. The set of basic variables is updated by removing the leaving variable and adding the entering variable. The values of the new set of basic variables are updated accordingly. The crucial task, however, is to compute the inverse of the new [basis matrix](@entry_id:637164), $(B_{\text{new}})^{-1}$, to prepare for the next iteration. This update is the central theme of the next section.

### Managing the Basis Inverse

The efficiency of the Revised Simplex Method hinges on how it handles the basis inverse. There are two primary strategies: explicitly updating the inverse at each step, or representing it as a product of simpler matrices.

#### Explicit Inverse Update via Rank-One Modification

When a column $a_q$ enters the basis and replaces the $r$-th column of the old basis $B$, the new [basis matrix](@entry_id:637164) $B_{\text{new}}$ can be seen as a rank-one modification of $B$. Specifically, we can write:

$$
B_{\text{new}} = B + (a_q - b_r) e_r^T
$$

where $b_r$ is the leaving column from $B$ and $e_r$ is a standard [basis vector](@entry_id:199546) with a 1 in the $r$-th position. The inverse of such a matrix can be found efficiently using the **Sherman-Morrison-Woodbury formula**:

$$
(M + uv^T)^{-1} = M^{-1} - \frac{M^{-1}uv^T M^{-1}}{1 + v^T M^{-1}u}
$$

By setting $M=B$, $u = a_q - b_r$, and $v = e_r$, we can derive the new inverse $(B_{\text{new}})^{-1}$ directly from the old inverse $B^{-1}$ . While elegant, this method can lead to a loss of sparsity and the accumulation of [numerical errors](@entry_id:635587) over many iterations as the inverse becomes fully dense.

#### The Product Form of the Inverse (PFI)

A more common and robust approach in modern solvers is the **Product Form of the Inverse (PFI)**. Instead of storing $B^{-1}$ as a single [dense matrix](@entry_id:174457), it is represented as a product of elementary transformation matrices, known as **eta matrices**. After $k$ iterations starting from an initial basis $B_0$, the inverse is represented as:

$$
B_k^{-1} = E_k E_{k-1} \cdots E_1 B_0^{-1}
$$

Each **eta matrix** $E_i$ corresponds to the pivot of the $i$-th iteration. An eta matrix is an identity matrix except for one column, which is called the **eta vector**. This structure is highly efficient for storage, especially if the eta vectors are sparse. Instead of storing an entire $m \times m$ matrix for each iteration, we only need to store the non-identity column and its position.

This [sparse representation](@entry_id:755123) can lead to significant memory savings compared to storing the explicit inverse. The ratio of memory required for PFI after $k$ iterations to that of an explicit $m \times m$ inverse can be expressed as $R = \frac{k(2p+1)}{m^2}$, where $p$ is the number of non-unity entries in each eta vector . If $k$ and $p$ are small relative to $m$, PFI is far more memory-efficient.

The real power of PFI lies in how it transforms the core calculations of the RSM. The required matrix-vector products are not performed by first forming $B^{-1}$ but by applying the sequence of eta matrices. This gives rise to two fundamental procedures:

1.  **BTRAN (Backward Transformation):** This procedure is used in the pricing phase to compute the [simplex multipliers](@entry_id:177701) $\pi^T = c_B^T B^{-1}$. It is equivalent to solving the system $\pi^T B = c_B^T$. With PFI, this is computed as $\pi^T = (((c_B^T E_k)E_{k-1})\cdots)E_1$. The multiplications are applied sequentially from right to left, or "backwards" through the eta chain .

2.  **FTRAN (Forward Transformation):** This procedure is used in the [ratio test](@entry_id:136231) phase to compute the updated column $d = B^{-1} a_q$. It is equivalent to solving the system $Bd = a_q$. With PFI, this is computed as $d = E_k(E_{k-1}(\cdots(E_1 a_q)\cdots))$. The multiplications are applied from left to right, or "forwards" .

In summary, each RSM iteration using PFI consists of a BTRAN for pricing and an FTRAN for the [ratio test](@entry_id:136231) .

#### Practical Necessity: Basis Reinversion

While PFI is efficient, it is not without its own challenges. As the number of iterations $k$ increases, the chain of eta matrices grows longer, and the BTRAN and FTRAN operations become more time-consuming. Furthermore, each matrix multiplication can introduce small floating-point errors, which can accumulate and compromise the numerical accuracy of the solution.

To counteract these issues, solvers perform periodic **basis reinversion**. After a certain number of iterations, the PFI representation is discarded. The current [basis matrix](@entry_id:637164) $B$ is explicitly reconstructed from the columns of the original constraint matrix $A$, and its inverse $B^{-1}$ is computed from scratch using a numerically stable method like LU factorization. This new, accurate inverse (which can itself be represented in a compact factored form) becomes the starting point for a new chain of eta matrices. This crucial housekeeping step ensures long-term numerical stability and computational efficiency .

### Theoretical Foundations and Geometric Interpretation

The algebraic manipulations of the Revised Simplex Method have a profound geometric interpretation. Each iteration corresponds to moving from one vertex of the feasible polytope to an adjacent one along an edge.

Consider the primal search direction $p$ in the full $n$-dimensional space, defined by setting the component for the entering variable $p_q=1$, the components for all other non-basic variables to zero, and the components for the basic variables as $p_B = -d = -B^{-1}a_q$. This direction is specifically constructed to lie in the [nullspace](@entry_id:171336) of the constraint matrix $A$, meaning it satisfies $Ap=0$. Consequently, moving from a feasible point $x$ in the direction $p$ to a new point $x' = x + \theta p$ preserves the equality constraints, since $Ax' = A(x+\theta p) = Ax + \theta Ap = b + 0 = b$. The vector $p$ is a **feasible direction** along an edge of the [polytope](@entry_id:635803).

Furthermore, the [reduced cost](@entry_id:175813) $\bar{c}_j$ is not merely an algebraic artifact; it is the **directional derivative** of the [objective function](@entry_id:267263) $c^T x$ along the feasible direction $p$ associated with variable $x_j$. That is, $\bar{c}_j = c^T p$. This provides a clear justification for the algorithm's logic: if $\bar{c}_j > 0$ in a maximization problem, moving in the direction $p$ (i.e., increasing $x_j$) will increase the [objective function](@entry_id:267263) value .

It is important to distinguish this from a [steepest descent method](@entry_id:140448). The [simplex algorithm](@entry_id:175128) does not move in the direction of the projected negative gradient of the objective function. Instead, it restricts its movement to the edges of the [feasible region](@entry_id:136622), examining only a specific subset of [feasible directions](@entry_id:635111)—those aligned with the axes of the non-basic variables. This edge-following strategy is what guarantees that the algorithm finds a [vertex solution](@entry_id:637043), which, for linear programs, is sufficient to guarantee optimality.