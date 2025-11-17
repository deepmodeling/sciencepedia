## Introduction
The field of [mathematical optimization](@entry_id:165540) is central to solving complex resource allocation, scheduling, and planning problems across science and industry. At the heart of this field lies linear programming, and for decades, the [simplex method](@entry_id:140334) has been a cornerstone algorithm for its solution. However, as problem sizes have grown exponentially, the standard tableau-based [simplex method](@entry_id:140334) often becomes computationally prohibitive. This creates a critical need for a more efficient approach capable of handling the large-scale models that define modern challenges.

The Revised Simplex Method (RSM) is the answer to this need. It's not just an alternative implementation but a fundamental reconceptualization that prioritizes speed and scalability. This article demystifies the RSM, revealing how it achieves its remarkable efficiency without sacrificing the theoretical elegance of the [simplex algorithm](@entry_id:175128).

Across the following chapters, you will gain a comprehensive understanding of this powerful technique. In "Principles and Mechanisms," we will dissect the core logic of the RSM, exploring how it leverages the basis inverse to drive the optimization process. Next, "Applications and Interdisciplinary Connections" will demonstrate the method's practical utility, from conducting sensitivity analysis to serving as the engine for advanced decomposition frameworks. Finally, you can solidify your knowledge with "Hands-On Practices," which present targeted exercises on the method's key aspects.

## Principles and Mechanisms

The Revised Simplex Method is not merely an alternative implementation of the [simplex algorithm](@entry_id:175128); it is a fundamental reconceptualization that prioritizes computational efficiency for the large-scale [linear programming](@entry_id:138188) problems encountered in modern science and industry. While the standard [simplex method](@entry_id:140334), with its full tableau, provides an excellent pedagogical tool for understanding the geometry of pivoting, the revised method offers a leaner, more powerful engine for solving real-world problems. This chapter delves into the principles that grant the revised method its power and the mechanisms through which it operates.

### The Motivation: Computational Efficiency

The primary driver for developing the Revised Simplex Method (RSM) is the computational burden associated with the standard [simplex tableau](@entry_id:136786), particularly for problems where the number of variables significantly exceeds the number of constraints. Consider a linear program in standard form, $A\boldsymbol{x} = \boldsymbol{b}$, with $m$ constraints and a total of $N$ variables (original plus slack/surplus). The [simplex tableau](@entry_id:136786) is an $m \times (N+1)$ matrix. Each iteration requires updating most of this matrix, a computational task with a cost roughly proportional to the size of the tableau, on the order of $O(mN)$ [floating-point operations](@entry_id:749454).

For many practical applications, such as resource allocation or [network flow problems](@entry_id:166966), the number of variables $N$ can be vast, while the number of constraints $m$ remains comparatively modest. In this regime, where $N \gg m$, the $O(mN)$ cost of updating the full tableau at every step becomes prohibitively expensive.

The Revised Simplex Method circumvents this by recognizing that the full tableau contains redundant information. All the data required to perform a [simplex](@entry_id:270623) pivot can be recovered from the original problem data ($A$, $\boldsymbol{b}$, $\boldsymbol{c}$) and one crucial piece of information: the inverse of the current [basis matrix](@entry_id:637164), $B^{-1}$. The [basis matrix](@entry_id:637164) $B$ is an $m \times m$ matrix formed by the columns of $A$ corresponding to the current basic variables.

To formalize this efficiency gain, consider a simplified cost model [@problem_id:2197691]. Let the cost of a standard tableau iteration be $C_S = mN$. The cost of a revised simplex iteration, $C_R$, is composed of two main parts: operations involving the $m \times m$ basis inverse (e.g., updating it, calculating the basic solution), which might cost approximately $C_{R,1} = 3m^2$, and the "pricing" step to evaluate all $N-m$ non-basic variables, which costs $C_{R,2} = \alpha m(N-m)$ for some implementation efficiency factor $\alpha$. The total cost is $C_R(\alpha) = 3m^2 + \alpha m(N-m)$. For RSM to be superior, we need $C_R  C_S$:

$3m^2 + \alpha m(N-m)  mN$

Solving for $\alpha$, we find that the revised method is more efficient if $\alpha  \frac{N-3m}{N-m}$. When $N$ is much larger than $m$, this critical value approaches $1$, indicating that even a straightforward implementation of the RSM is likely to outperform the tableau method. The core insight is that RSM shifts the computational focus from manipulating a large $m \times N$ tableau to operations centered around the much smaller $m \times m$ basis inverse.

### The Core Logic: An Iteration with the Basis Inverse

The central strategy of the Revised Simplex Method is to maintain and utilize the basis inverse $B^{-1}$ to generate only the essential components for a pivot on demand. Let us outline the key quantities required for one iteration and how they are derived.

Assume we are at a basic [feasible solution](@entry_id:634783) where the set of basic variables is indexed by $\mathcal{B}$. The [basis matrix](@entry_id:637164) is $B = [A_j]_{j \in \mathcal{B}}$, and we have its inverse, $B^{-1}$.

1.  **Current Basic Feasible Solution ($\boldsymbol{x_B}$):** The values of the basic variables are computed as $\boldsymbol{x_B} = B^{-1}\boldsymbol{b}$.

2.  **Simplex Multipliers ($\boldsymbol{\pi}$):** To decide which non-basic variable should enter the basis, we must compute the [reduced costs](@entry_id:173345). This is facilitated by a vector of **[simplex multipliers](@entry_id:177701)**, denoted $\boldsymbol{\pi}$ (or often $\boldsymbol{y}$). For a maximization problem, this is a row vector calculated as:
    $$ \boldsymbol{\pi}^T = \boldsymbol{c}_B^T B^{-1} $$
    where $\boldsymbol{c}_B^T$ is the row vector of [objective function](@entry_id:267263) coefficients for the basic variables. These multipliers are also the solution to the dual problem corresponding to the current basis, a connection we will explore later. As an example, if at some iteration the basic variables are $\{x_1, x_2\}$ with coefficients $\boldsymbol{c}_B^T = \begin{pmatrix} 5  8 \end{pmatrix}$ and the basis inverse is $B^{-1} = \begin{pmatrix} -1/7  3/7 \\ 3/7  -2/7 \end{pmatrix}$, the [simplex multipliers](@entry_id:177701) are computed as $\boldsymbol{\pi}^T = \begin{pmatrix} 5  8 \end{pmatrix} B^{-1} = \begin{pmatrix} 19/7  -1/7 \end{pmatrix}$ [@problem_id:2197664].

3.  **Reduced Costs ($\bar{c}_j$):** With the [simplex multipliers](@entry_id:177701), we can efficiently "price out" any non-basic variable $x_j$. The [reduced cost](@entry_id:175813) is:
    $$ \bar{c}_j = c_j - \boldsymbol{\pi}^T A_j $$
    where $A_j$ is the column for variable $x_j$ in the original constraint matrix $A$. For a maximization problem, if any $\bar{c}_j > 0$, the objective function can be improved by bringing $x_j$ into the basis. Typically, the variable with the largest positive [reduced cost](@entry_id:175813) is chosen to enter. For instance, given $\boldsymbol{\pi}^T$ (which is $c_B^T B^{-1}$), the [reduced cost](@entry_id:175813) for a non-basic variable $x_2$ with coefficient $c_2=8$ and column $A_2 = \begin{pmatrix} 1  2  1 \end{pmatrix}^T$ can be found directly without reference to a full tableau [@problem_id:2197699].

4.  **Pivot Column Representation ($\boldsymbol{y}_k$):** Once an entering variable $x_k$ is selected, we must determine which basic variable will leave. This requires finding how the current basic variables change as $x_k$ increases. This relationship is captured by the vector $\boldsymbol{y}_k$, which is the representation of the entering column $A_k$ in terms of the current basis:
    $$ \boldsymbol{y}_k = B^{-1} A_k $$
    This vector $\boldsymbol{y}_k$ is precisely the pivot column as it would appear in the [simplex tableau](@entry_id:136786). It is used in the [ratio test](@entry_id:136231) to determine the leaving variable. It is a fundamental property that if we apply this formula to a variable $x_j$ that is already the $i$-th variable in the basis, the result is the $i$-th elementary vector, $\boldsymbol{e}_i$. For example, if the basis is $(x_1, x_3)$ and we compute the representation for $A_3$, the result must be $\boldsymbol{y}_3 = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$ [@problem_id:2197650].

### The Revised Simplex Algorithm: A Complete Iteration

With these components, we can now assemble the steps for a single iteration of the Revised Simplex Method for a maximization problem [@problem_id:2197669].

**Initialization:** Given a set of basic variables $\mathcal{B}$, the corresponding [basis matrix](@entry_id:637164) $B$, and its inverse $B^{-1}$.

**Step 1: Pricing and Selection of Entering Variable**
   a. Compute the [simplex multipliers](@entry_id:177701): $\boldsymbol{\pi}^T = \boldsymbol{c}_B^T B^{-1}$.
   b. For each non-basic variable $x_j$, calculate its [reduced cost](@entry_id:175813): $\bar{c}_j = c_j - \boldsymbol{\pi}^T A_j$.
   c. If all $\bar{c}_j \le 0$, the current solution is optimal. Terminate.
   d. Otherwise, select the entering variable $x_k$ corresponding to the largest positive [reduced cost](@entry_id:175813), $\bar{c}_k = \max_j \{\bar{c}_j\}$.

**Step 2: Ratio Test and Selection of Leaving Variable**
   a. Compute the updated pivot column: $\boldsymbol{y}_k = B^{-1} A_k$.
   b. If all elements of $\boldsymbol{y}_k$ are non-positive ($y_{ik} \le 0$ for all $i$), the problem is unbounded. Terminate.
   c. Otherwise, compute the current values of the basic variables: $\boldsymbol{x}_B = B^{-1}\boldsymbol{b}$.
   d. Find the leaving variable by performing the [minimum ratio test](@entry_id:634935):
      $$ \theta^* = \min_{i: y_{ik} > 0} \left\{ \frac{(\boldsymbol{x}_B)_i}{y_{ik}} \right\} $$
      Let $r$ be the index of the basic variable that yields this minimum. This variable will leave the basis.

**Step 3: Update**
   a. The new set of basic variables is formed by replacing the leaving variable (at position $r$) with the entering variable $x_k$.
   b. Update the basis inverse $B^{-1}$ to obtain the new inverse, $(B_{\text{new}})^{-1}$. This is the most intricate step and is discussed next.
   c. Repeat from Step 1.

### Implementing the Pivot: Efficiently Updating the Inverse

A naive update would be to form the new [basis matrix](@entry_id:637164) $B_{\text{new}}$ and compute its inverse from scratch. This is computationally expensive. The efficiency of the RSM hinges on updating from $B^{-1}$ to $(B_{\text{new}})^{-1}$ directly. This can be accomplished in several ways, with two prominent methods being the Product Form of the Inverse and applying the Sherman-Morrison-Woodbury formula.

#### The Product Form of the Inverse (PFI)

The [pivot operation](@entry_id:140575) can be represented as a pre-multiplication of $B^{-1}$ by a special [elementary matrix](@entry_id:635817) known as an **eta matrix**, $E$. If the entering column $A_k$ replaces the $r$-th column of the basis, the new inverse is given by:
$$ (B_{\text{new}})^{-1} = E B^{-1} $$
The eta matrix $E$ is an identity matrix except for its $r$-th column, which is replaced by the **eta vector** $\boldsymbol{\eta}$. This vector is derived from the updated pivot column $\boldsymbol{y}_k = B^{-1} A_k$:
$$ \eta_i = \begin{cases} -\frac{y_{ik}}{y_{rk}}  \text{if } i \neq r \\ \frac{1}{y_{rk}}  \text{if } i = r \end{cases} $$
If we start with an identity [basis matrix](@entry_id:637164), $B_0 = I$, then after $k$ iterations, the inverse is not stored explicitly but represented as a product:
$$ B_k^{-1} = E_k E_{k-1} \cdots E_1 $$
This is the **Product Form of the Inverse (PFI)**. To compute a quantity like $\boldsymbol{y}_j = B_k^{-1} A_j$, we do not form the product, but rather apply the transformations sequentially: $\boldsymbol{y}_j = (E_k (E_{k-1} \cdots (E_1 A_j)\cdots))$. For example, after one iteration where $x_1$ enters and replaces a [slack variable](@entry_id:270695) (from an initial identity basis), the new inverse is just $B_1^{-1}=E_1$. To find the updated column for the next entering variable, say $x_2$, we simply compute $\boldsymbol{d} = E_1 A_2$ [@problem_id:2197665].

#### Theoretical Underpinning: The Sherman-Morrison-Woodbury Formula

The process of updating the inverse can also be understood through matrix algebra. A change of one column in the [basis matrix](@entry_id:637164) $B$ is a [rank-one update](@entry_id:137543). Let the entering column be $A_k$ and the leaving column (the $r$-th column of $B$) be $A_r$. The new [basis matrix](@entry_id:637164) is $B_{\text{new}} = B - A_r \boldsymbol{e}_r^T + A_k \boldsymbol{e}_r^T = B + (A_k - A_r)\boldsymbol{e}_r^T$.

This is of the form $B + \boldsymbol{u}\boldsymbol{v}^T$, where $\boldsymbol{u} = A_k - A_r$ and $\boldsymbol{v} = \boldsymbol{e}_r$. The inverse of this updated matrix can be found using the **Sherman-Morrison-Woodbury formula**:
$$ (M + \boldsymbol{u}\boldsymbol{v}^T)^{-1} = M^{-1} - \frac{M^{-1}\boldsymbol{u}\boldsymbol{v}^T M^{-1}}{1 + \boldsymbol{v}^T M^{-1}\boldsymbol{u}} $$
By substituting $M=B$, $\boldsymbol{u}=A_k - A_r$, and $\boldsymbol{v}=\boldsymbol{e}_r$, and carrying out the algebra, we can derive the formula for $(B_{\text{new}})^{-1}$ directly from $B^{-1}$. This provides a rigorous mathematical justification for the pivot update procedure and demonstrates that the update is indeed a low-rank correction to the existing inverse [@problem_id:2197672].

### Practical Considerations in Implementation

The choice of how to represent and maintain the basis inverse has significant practical consequences for solver performance.

#### Memory Usage and Basis Reinversion

The PFI is particularly attractive because eta matrices are sparse; they are identity matrices with one non-standard column. Instead of storing $m^2$ values for an explicit inverse, we only need to store the non-trivial column of each eta matrix. Let's assume an eta vector has $p$ non-unity elements. To store it, we need $p$ values and their $p$ row indices, plus the column index it replaces, for a total of $2p+1$ storage units. After $k$ iterations, the PFI representation requires $k(2p+1)$ units, whereas the explicit inverse requires $m^2$ units [@problem_id:2197689]. When $k$ is small compared to $m$, and the basis matrices are sparse (leading to small $p$), the PFI offers substantial memory savings.

However, the PFI is not a panacea. As the number of iterations $k$ grows, the chain of eta matrices $E_k \cdots E_1$ becomes long.
1.  **Computational Cost:** Applying the full sequence of transformations to a vector becomes progressively slower as $k$ increases.
2.  **Numerical Stability:** Each [matrix multiplication](@entry_id:156035) can introduce small floating-point errors. Over many iterations, these errors can accumulate, leading to an inaccurate representation of the true inverse and potentially causing the algorithm to fail.

To combat these issues, practical RSM solvers perform periodic **basis reinversion**. After a certain number of iterations (e.g., every 50 or 100 pivots), the algorithm pauses. It takes the current list of basic variables, forms the [basis matrix](@entry_id:637164) $B$ from the original data, and computes its inverse $B^{-1}$ from scratch using highly stable numerical methods like LU factorization. This new, accurate inverse then replaces the long PFI chain, and the iteration count for PFI purposes is reset to zero. This process, illustrated in [@problem_id:2197693], is crucial for maintaining both speed and numerical integrity in [large-scale optimization](@entry_id:168142).

### A Deeper Perspective: The Connection to Duality

The Revised Simplex Method also provides a transparent window into the deep connection between the primal and dual [linear programming](@entry_id:138188) problems. The vector of [simplex multipliers](@entry_id:177701), $\boldsymbol{\pi}^T = \boldsymbol{c}_B^T B^{-1}$, is more than just a computational tool. The vector $\boldsymbol{\pi}$ is precisely the basic solution to the dual LP associated with the primal basis $B$.

The primal problem can be stated as:
Maximize $\boldsymbol{c}^T \boldsymbol{x}$ subject to $A\boldsymbol{x} \le \boldsymbol{b}, \boldsymbol{x} \ge 0$.

Its dual is:
Minimize $\boldsymbol{b}^T \boldsymbol{y}$ subject to $A^T\boldsymbol{y} \ge \boldsymbol{c}, \boldsymbol{y} \ge 0$.

At each iteration, the [simplex method](@entry_id:140334) identifies a basic [feasible solution](@entry_id:634783) for the primal. The corresponding [simplex multipliers](@entry_id:177701) $\boldsymbol{\pi}$ form a basic solution for the dual (though it may not be feasible until the optimum is reached). The [reduced costs](@entry_id:173345), $\bar{c}_j = c_j - \boldsymbol{\pi}^T A_j$, measure the violation of the dual constraints ($A^T\boldsymbol{\pi} \ge \boldsymbol{c}$). When all $\bar{c}_j \le 0$, it means $c_j \le \boldsymbol{\pi}^T A_j$ for all $j$, which is equivalent to $A^T\boldsymbol{\pi} \ge \boldsymbol{c}$. At this point, the dual solution $\boldsymbol{\pi}$ has become feasible. Since the primal solution is also feasible, we have achieved optimality.

Therefore, each pivot of the revised simplex method can be viewed not just as moving from one vertex to another on the primal feasible [polytope](@entry_id:635803), but also as taking a step in the space of the [dual variables](@entry_id:151022). A single iteration transforms the current dual basic solution $\boldsymbol{\pi}$ into a new dual basic solution $\boldsymbol{\pi}_{\text{new}}$ [@problem_id:2197701]. This dual perspective provides a powerful framework for understanding the algorithm's convergence and for developing advanced techniques like the [dual simplex method](@entry_id:164344) and [sensitivity analysis](@entry_id:147555).