## Introduction
Gaussian elimination is a cornerstone of numerical linear algebra, providing a systematic approach to [solving systems of linear equations](@entry_id:136676). However, its naive implementation is numerically fragile. A zero pivot element will halt the algorithm, while a very small pivot can catastrophically magnify [rounding errors](@entry_id:143856), leading to completely inaccurate results. This issue of [numerical instability](@entry_id:137058) necessitates the use of [pivoting strategies](@entry_id:151584) to ensure the algorithm's reliability. This article focuses on the most robust of these strategies: **full pivoting**.

In the following sections, we will embark on a comprehensive exploration of this powerful technique. The "Principles and Mechanisms" section will dissect the algorithm, explaining how it controls element growth and leads to the fundamental $PAQ=LU$ factorization. Next, "Applications and Interdisciplinary Connections" will broaden our perspective, showcasing how this factorization is used for tasks beyond [solving linear systems](@entry_id:146035) and discussing its real-world performance trade-offs in fields from quantum physics to engineering. Finally, the "Hands-On Practices" section will provide an opportunity to solidify your understanding by applying the full pivoting method to concrete problems, bridging theory with practical skill.

## Principles and Mechanisms

In the preceding section, we introduced Gaussian elimination as a fundamental method for [solving systems of linear equations](@entry_id:136676) and for computing the LU factorization of a matrix. However, the naive application of this algorithm is fraught with peril. If a pivot element is zero, the algorithm fails entirely. If a pivot element is merely very small relative to other entries in its row, it can lead to the propagation and magnification of rounding errors, a phenomenon known as **[numerical instability](@entry_id:137058)**. To ensure the reliability and accuracy of Gaussian elimination in [finite-precision arithmetic](@entry_id:637673), we must employ a **[pivoting strategy](@entry_id:169556)**. This section delves into the principles and mechanisms of the most robust of these strategies: **full pivoting**.

### The Rationale for Pivoting: Controlling Element Growth

The core issue that pivoting addresses is the uncontrolled growth of [matrix elements](@entry_id:186505) during the elimination process. When a small pivot $a_{kk}^{(k)}$ is used to eliminate a larger element $a_{ik}^{(k)}$ below it, the multiplier $m_{ik} = a_{ik}^{(k)} / a_{kk}^{(k)}$ will be large. This large multiplier then scales the pivot row before it is subtracted from row $i$, potentially creating very large numbers in the updated row $i$. These large numbers can swamp the original information in the matrix and exacerbate the effect of [rounding errors](@entry_id:143856).

To make this concrete, consider a simple $2 \times 2$ matrix and its naive LU factorization without any pivoting [@problem_id:2174436]. Let the matrix be:
$$
A = \begin{pmatrix} 0.001 & 1.5 \\ 1.0 & 2.0 \end{pmatrix}
$$
A direct LU factorization seeks $A = LU$, where $L$ is unit lower triangular and $U$ is upper triangular. The multiplier for the first and only elimination step is $l_{21} = \frac{a_{21}}{a_{11}} = \frac{1.0}{0.001} = 1000$. The updated element $u_{22}$ is calculated as $a_{22} - l_{21} u_{12} = 2.0 - (1000)(1.5) = -1498$. The resulting factorization is:
$$
L_1 = \begin{pmatrix} 1 & 0 \\ 1000 & 1 \end{pmatrix}, \quad U_1 = \begin{pmatrix} 0.001 & 1.5 \\ 0 & -1498 \end{pmatrix}
$$
Notice the emergence of the large value $1000$ in $L_1$ and $-1498$ in $U_1$, despite the original matrix entries being small. This illustrates the problem of **element growth**. A measure for this is the **growth factor**, which we will define more formally later. For now, let's observe that the largest element in the factors is $1498$, a significant increase from the initial maximum of $2.0$.

Pivoting strategies are designed to prevent this by ensuring that the pivot element is as large as possible, thereby keeping the multipliers small.

### Full Pivoting: An Exhaustive Search for Stability

While partial pivoting—which searches for the largest pivot in the current column—is a common and effective strategy, **full pivoting** (or **complete pivoting**) offers an even more rigorous approach to ensuring [numerical stability](@entry_id:146550).

The procedure for Gaussian elimination with full pivoting at step $k$ (for $k = 1, \dots, n-1$) is as follows:
1.  **Search**: Identify the element with the largest absolute value in the entire remaining submatrix, which consists of rows $k$ through $n$ and columns $k$ through $n$. Let this element be $a_{ij}$ where $i, j \ge k$.
2.  **Swap**: Interchange row $k$ with row $i$ and column $k$ with column $j$. This moves the largest-magnitude element into the [pivot position](@entry_id:156455) $(k,k)$.
3.  **Eliminate**: Perform the standard elimination step, using the new pivot $a_{kk}$ to create zeros in the entries below it in column $k$.

By always choosing the largest possible pivot from the entire available submatrix, we ensure that all multipliers $l_{ik} = a_{ik}/a_{kk}$ (for $i > k$) have a magnitude less than or equal to 1. This systematically suppresses the element growth that can plague naive Gaussian elimination.

### The Algebraic Representation: PAQ = LU

The mechanical operations of full pivoting have a clean and elegant algebraic representation. The cumulative effect of all row interchanges throughout the elimination process can be represented by a single **row permutation matrix**, $P$. Similarly, the cumulative effect of all column interchanges can be represented by a single **column permutation matrix**, $Q$.

A row swap is equivalent to left-multiplication by a [permutation matrix](@entry_id:136841), while a column swap is equivalent to right-multiplication. Therefore, the process of applying Gaussian elimination with full pivoting to a matrix $A$ does not factorize $A$ itself, but rather a permuted version of it. The resulting factorization is not $A=LU$, but rather:
$$
PAQ = LU
$$
Here, $P$ is the [permutation matrix](@entry_id:136841) encoding all row swaps, $Q$ is the [permutation matrix](@entry_id:136841) encoding all column swaps, $L$ is a unit [lower triangular matrix](@entry_id:201877) containing the multipliers, and $U$ is the final [upper triangular matrix](@entry_id:173038) [@problem_id:2174439]. This equation is the fundamental algebraic identity for LU factorization with full pivoting.

It is crucial to understand the consequence of right-multiplying by $Q$. While left-multiplication by $P$ permutes the equations in the system $A\mathbf{x}=\mathbf{b}$, right-multiplication by $Q$ permutes the columns of $A$. This is equivalent to reordering the variables in the solution vector $\mathbf{x}$. For instance, if the first step of full pivoting on a $3 \times 3$ matrix involves swapping column 1 and column 3, the vector of variables being solved for is implicitly changed from $(x_1, x_2, x_3)^T$ to $(x_3, x_2, x_1)^T$ [@problem_id:2174470]. The matrix $Q$ keeps a record of this permutation.

### Solving Linear Systems using the PAQ = LU Factorization

Once the factorization $PAQ = LU$ is computed, we can efficiently solve the linear system $A\mathbf{x}=\mathbf{b}$. The key is to manipulate the original equation to incorporate the permutation matrices.

Starting from $A\mathbf{x}=\mathbf{b}$, we can write:
1.  Left-multiply by $P$: $PA\mathbf{x} = P\mathbf{b}$.
2.  Insert identity $I = QQ^T$ between $A$ and $\mathbf{x}$ (since $Q$ is a permutation matrix, it is orthogonal, so $Q^{-1} = Q^T$): $PA(QQ^T)\mathbf{x} = P\mathbf{b}$.
3.  Group the terms to match the factorization: $(PAQ)(Q^T \mathbf{x}) = P\mathbf{b}$.
4.  Substitute $LU$ for $PAQ$: $LU(Q^T \mathbf{x}) = P\mathbf{b}$.

This transformed system can be solved in three stages [@problem_id:2174417]:
1.  **Permute the right-hand side**: Calculate the vector $\mathbf{b}' = P\mathbf{b}$.
2.  **Forward and [backward substitution](@entry_id:168868)**: Define an intermediate vector $\mathbf{z} = Q^T \mathbf{x}$. The system becomes $LU\mathbf{z} = \mathbf{b}'$. This is solved in two steps:
    a. Solve $L\mathbf{w} = \mathbf{b}'$ for $\mathbf{w}$ using **[forward substitution](@entry_id:139277)**.
    b. Solve $U\mathbf{z} = \mathbf{w}$ for $\mathbf{z}$ using **[backward substitution](@entry_id:168868)**.
3.  **Recover the solution**: The vector $\mathbf{z}$ is a permuted version of the solution $\mathbf{x}$. To recover the final solution, we compute $\mathbf{x} = Q\mathbf{z}$.

Let's illustrate this with an example. Suppose we want to solve $A\mathbf{x}=\mathbf{b}$ where the decomposition $PAQ=LU$ yields [@problem_id:2174417]:
$$
P = \begin{pmatrix} 0 & 0 & 1 \\ 0 & 1 & 0 \\ 1 & 0 & 0 \end{pmatrix}, Q = \begin{pmatrix} 1 & 0 & 0 \\ 0 & 0 & 1 \\ 0 & 1 & 0 \end{pmatrix}, L = \begin{pmatrix} 1 & 0 & 0 \\ 2 & 1 & 0 \\ -1 & 3 & 1 \end{pmatrix}, U = \begin{pmatrix} 4 & 1 & -2 \\ 0 & 3 & 1 \\ 0 & 0 & 2 \end{pmatrix}
$$
and $\mathbf{b} = (2, -3, -1)^T$.

First, we compute $\mathbf{b}' = P\mathbf{b} = (-1, -3, 2)^T$.
Next, we solve $L\mathbf{w} = \mathbf{b}'$ by [forward substitution](@entry_id:139277):
$$
\begin{pmatrix} 1 & 0 & 0 \\ 2 & 1 & 0 \\ -1 & 3 & 1 \end{pmatrix} \begin{pmatrix} w_1 \\ w_2 \\ w_3 \end{pmatrix} = \begin{pmatrix} -1 \\ -3 \\ 2 \end{pmatrix} \implies \mathbf{w} = \begin{pmatrix} -1 \\ -1 \\ 4 \end{pmatrix}
$$
Then, we solve $U\mathbf{z} = \mathbf{w}$ by [backward substitution](@entry_id:168868):
$$
\begin{pmatrix} 4 & 1 & -2 \\ 0 & 3 & 1 \\ 0 & 0 & 2 \end{pmatrix} \begin{pmatrix} z_1 \\ z_2 \\ z_3 \end{pmatrix} = \begin{pmatrix} -1 \\ -1 \\ 4 \end{pmatrix} \implies \mathbf{z} = \begin{pmatrix} 1 \\ -1 \\ 2 \end{pmatrix}
$$
Finally, we recover the solution $\mathbf{x} = Q\mathbf{z}$:
$$
\mathbf{x} = \begin{pmatrix} 1 & 0 & 0 \\ 0 & 0 & 1 \\ 0 & 1 & 0 \end{pmatrix} \begin{pmatrix} 1 \\ -1 \\ 2 \end{pmatrix} = \begin{pmatrix} 1 \\ 2 \\ -1 \end{pmatrix}
$$
This procedure gives the correct solution vector for the original system.

### The Impact of Full Pivoting on Stability and Accuracy

We began by stating that full pivoting enhances numerical stability. Let's revisit our initial example and see how [@problem_id:2174436].
$$
A = \begin{pmatrix} 0.001 & 1.5 \\ 1.0 & 2.0 \end{pmatrix}
$$
With full pivoting, we first find the largest element in the matrix, which is $2.0$ at position $(2,2)$. We swap rows 1 and 2, and columns 1 and 2, to move this pivot to the $(1,1)$ position. The new matrix to be factored is:
$$
A' = P_1 A Q_1 = \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix} A \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix} = \begin{pmatrix} 2.0 & 1.0 \\ 1.5 & 0.001 \end{pmatrix}
$$
Factoring $A'$ gives a multiplier $l_{21} = 1.5/2.0 = 0.75$ and a new element $u_{22} = 0.001 - (0.75)(1.0) = -0.749$. The factorization is:
$$
L_2 = \begin{pmatrix} 1 & 0 \\ 0.75 & 1 \end{pmatrix}, \quad U_2 = \begin{pmatrix} 2.0 & 1.0 \\ 0 & -0.749 \end{pmatrix}
$$
The maximum absolute value in these factors is $2.0$. Compared to the maximum value of $1498$ from the naive factorization, the improvement is dramatic. Full pivoting successfully controlled the element growth.

This control of element growth is formalized by the **growth factor**, $\rho$. For an $n \times n$ matrix $A$, if $A^{(k)}$ is the matrix after $k-1$ steps of elimination, the [growth factor](@entry_id:634572) is defined as [@problem_id:2174467]:
$$
\rho = \frac{\max_{k,i,j} |a_{ij}^{(k)}|}{\max_{i,j} |a_{ij}^{(1)}|}
$$
A small [growth factor](@entry_id:634572) (close to 1) indicates a [stable process](@entry_id:183611). For full pivoting, it can be proven that the growth of elements is bounded, though the worst-case bound is still quite large. In practice, however, the growth factor for full pivoting is almost always small.

The benefit of full pivoting is not just theoretical; it can lead to more accurate solutions in [finite-precision arithmetic](@entry_id:637673). Consider solving a system on a hypothetical computer that rounds all results to three [significant figures](@entry_id:144089) [@problem_id:2174469]. For the system $x_1 + 100x_2 = 100$ and $x_1 + x_2 = 2$, whose exact solution is approximately $x_1 \approx 1.01$ and $x_2 \approx 0.990$:
- **Partial Pivoting**: Would choose $1$ as the pivot (no swap). The multiplier is $1$, leading to the new second equation $-99.0 x_2 = -98.0$. Back-substitution gives $x_2 = 0.990$ and $x_1 = 1.00$.
- **Full Pivoting**: Would choose $100$ as the pivot, requiring a column swap. The variables become $(x_2, x_1)$. The system is now $100x_2 + x_1 = 100$ and $x_2 + x_1 = 2$. The multiplier is $0.0100$. The new second equation becomes $0.990 x_1 = 1.00$. Back-substitution gives $x_1 = 1.01$.

In this case, the solution for $x_1$ obtained with full pivoting is significantly more accurate than that from partial pivoting, demonstrating its superiority in delicate numerical situations.

Finally, the full pivoting algorithm provides a robust method for detecting singularity. If, at any step $k$, the search for a pivot in the remaining submatrix yields only zeros, it means the submatrix is entirely zero. No non-zero pivot can be found, and the algorithm cannot proceed. This is not a failure of the method; rather, it is the method's way of demonstrating that the original matrix $A$ is singular (or, more precisely, that its rank is less than $k$) [@problem_id:2174457].

### The Practical Cost of Full Pivoting

Despite its superior numerical properties, full pivoting is rarely used in general-purpose numerical software. The reason is its **computational cost**. The arithmetic operations (multiplications and additions) in Gaussian elimination cost $O(n^3)$ [floating-point operations](@entry_id:749454). Let's analyze the cost of the pivot search [@problem_id:2174462] [@problem_id:1383160].

- **Partial Pivoting**: At step $k$, we search among $n-k+1$ elements in the current column. The total number of comparisons is $\sum_{k=1}^{n-1} (n-k) = \frac{n(n-1)}{2}$, which is an $O(n^2)$ cost.
- **Full Pivoting**: At step $k$, we search the entire $(n-k+1) \times (n-k+1)$ submatrix. Finding the maximum among these $(n-k+1)^2$ elements requires $(n-k+1)^2 - 1$ comparisons. The total number of comparisons is $$ \sum_{k=1}^{n-1} ((n-k+1)^2 - 1) = \frac{n(n+1)(2n+1)}{6} - n, $$ which is an $O(n^3)$ cost [@problem_id:1383160] [@problem_id:2174432].

The search for the pivot in full pivoting is of the same order of complexity as the arithmetic itself. This additional $O(n^3)$ work, along with the complex data access patterns from column swaps that disrupt [memory locality](@entry_id:751865) and hinder performance optimizations, makes full pivoting significantly slower in practice than [partial pivoting](@entry_id:138396). Since the cases where [partial pivoting](@entry_id:138396) is insufficiently stable are rare in practice, the substantial extra cost of full pivoting is not considered a worthwhile trade-off for most applications. Consequently, partial pivoting remains the standard in most numerical libraries.