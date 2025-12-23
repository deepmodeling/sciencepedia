## Introduction
In many areas of science and engineering, from real-time signal processing to online machine learning, computational models must adapt to constantly evolving data. These dynamic systems are often described by matrices that undergo frequent but small modifications, such as the addition or removal of a data point. While matrix factorizations like QR or Cholesky are essential tools for solving the linear algebra problems at the heart of these models, recomputing them from scratch with every change is often prohibitively expensive. This creates a critical knowledge gap: how can we efficiently and reliably modify an existing factorization to reflect changes in the original matrix?

This article addresses this challenge by providing a comprehensive exploration of algorithms for updating and downdating matrix factorizations. You will learn not just how to save flops, but also how to navigate the subtle trade-offs between computational cost, memory bandwidth, and numerical stability. The following chapters are structured to build your expertise from the ground up.

*   **Principles and Mechanisms** delves into the core algorithms for updating and downdating QR and Cholesky factorizations. It explains the rationale behind these methods, the mechanics of transformations like Givens rotations, and the stability considerations that distinguish robust techniques from hazardous ones.
*   **Applications and Interdisciplinary Connections** showcases how these numerical methods serve as the engine for a wide range of applications, including [recursive least squares](@entry_id:263435), online regression, [constrained optimization](@entry_id:145264), and the analysis of dynamic networks.
*   **Hands-On Practices** provides concrete problems that allow you to apply the theoretical concepts, reinforcing your understanding of how to handle column deletions, manage [numerical stability](@entry_id:146550), and update solutions to statistical problems.

## Principles and Mechanisms

The decision to update a [matrix factorization](@entry_id:139760) rather than recompute it from scratch is a fundamental consideration in computational science, driven by the ever-present tension between arithmetic cost and data movement. In dynamic applications where matrices evolve through low-rank modifications, re-factorization can be prohibitively expensive. Update and downdate algorithms offer an alternative by directly transforming the existing factors to reflect changes in the original matrix, often with a significantly lower computational workload. This chapter elucidates the core principles and mechanisms governing these algorithms, focusing on the widely used QR and Cholesky factorizations.

### The Rationale for Updating: A Cost-Benefit Analysis

At its core, updating a factorization is an exercise in computational economy. Consider a dense matrix $A \in \mathbb{R}^{m \times n}$. Recomputing its QR factorization from scratch using, for instance, Householder transformations requires $\Theta(mn^2)$ [floating-point operations](@entry_id:749454) ([flops](@entry_id:171702)). Similarly, recomputing the Cholesky factorization of a [symmetric positive definite](@entry_id:139466) (SPD) matrix $A \in \mathbb{R}^{n \times n}$ costs approximately $\frac{1}{3}n^3$ flops, a workload of order $\Theta(n^3)$.

In contrast, a rank-1 modification, such as replacing $A$ with $\widehat{A} = A + u v^{\top}$, can often be incorporated into the factorization at a much lower cost. A typical [rank-1 update](@entry_id:754058) to a dense QR factorization costs $\Theta(mn)$ [flops](@entry_id:171702), while a rank-1 Cholesky update costs $\Theta(n^2)$ flops. For large matrices, the asymptotic advantage is substantial—a reduction in arithmetic by a factor of $\Theta(n)$. This reduction in floating-point work is the primary motivation for developing and using update algorithms .

However, a more nuanced analysis must also consider data movement, a critical bottleneck on modern computer architectures. The **[arithmetic intensity](@entry_id:746514)** of an algorithm, defined as the ratio of floating-point operations to bytes of data moved between main memory and processing units, provides a deeper measure of efficiency.

- **Recomputation** of a QR factorization of $A \in \mathbb{R}^{m \times n}$ performs $\Theta(mn^2)$ flops on $\Theta(mn)$ words of data, yielding an arithmetic intensity of $\Theta(n)$.
- **Updating** the QR factorization performs $\Theta(mn)$ flops while still touching the $\Theta(mn)$ words of data in the factors, resulting in an [arithmetic intensity](@entry_id:746514) of $\Theta(1)$.

This reveals that recomputation performs more arithmetic work for each word of data it accesses, making it a **compute-bound** task on many systems. Conversely, the update procedure is often **[memory-bound](@entry_id:751839)**, with its execution time dominated by waiting for data from memory rather than by performing calculations. While updates reduce the total number of flops, their lower arithmetic intensity means they may not always achieve a performance improvement proportional to the flop reduction, especially on systems where [memory bandwidth](@entry_id:751847) is the primary performance limiter [@problem_id:3600347; @problem_id:3600396].

### Mechanisms for Orthogonal (QR) Factorizations

Algorithms for updating QR factorizations are prized for their [numerical stability](@entry_id:146550), a property derived from their reliance on orthogonal transformations. These transformations preserve the geometric structure of the problem and control the propagation of [roundoff error](@entry_id:162651).

#### General Rank-k Updates

Consider a matrix $A = QR$ that undergoes a rank-$k$ update $A_{\text{new}} = A + UV^{\top}$, where $U \in \mathbb{R}^{m \times k}$ and $V \in \mathbb{R}^{n \times k}$. The update problem can be formulated as:
$$ A_{\text{new}} = QR + UV^{\top} = Q(R + Q^{\top}UV^{\top}) $$
Letting $W = Q^{\top}U$, the challenge reduces to finding an efficient and stable method to restore the triangular structure of the matrix $H = R + WV^{\top}$. $H$ is the sum of an [upper triangular matrix](@entry_id:173038) and a rank-$k$ matrix, and is generally not triangular. The goal is to find an [orthogonal matrix](@entry_id:137889) $\Omega \in \mathbb{R}^{n \times n}$ such that $\widehat{R} = \Omega H$ is upper triangular. The new factorization is then $A_{\text{new}} = (Q\Omega^{\top})\widehat{R}$, with updated factors $\widehat{Q} = Q\Omega^{\top}$ and $\widehat{R}$ . The remainder of this section explores how to construct such transformations for common update scenarios.

#### Appending a Column

A frequent operation in recursive applications, such as sequential least-squares estimation, is the appending of a new column $a \in \mathbb{R}^{m}$ to a matrix $A \in \mathbb{R}^{m \times n}$, forming $A_{+} = [A \; a]$. Given the thin QR factorization $A=QR$, where $Q \in \mathbb{R}^{m \times n}$ has orthonormal columns and $R \in \mathbb{R}^{n \times n}$ is upper triangular, we seek factors $Q_{+} \in \mathbb{R}^{m \times (n+1)}$ and $R_{+} \in \mathbb{R}^{(n+1) \times (n+1)}$ for $A_{+}$.

This update can be elegantly derived from the principles of the Gram-Schmidt process. We seek factors of the form:
$$ Q_{+} = [Q \; q_{n+1}] \quad \text{and} \quad R_{+} = \begin{pmatrix} R  & b \\ 0^{\top} & \rho \end{pmatrix} $$
For this structure to satisfy $A_{+} = Q_{+}R_{+}$, we must have $[A \; a] = [QR \; Qb + \rho q_{n+1}]$. This yields the equation $a = Qb + \rho q_{n+1}$. To find the unknown quantities $b$, $\rho$, and $q_{n+1}$, we enforce orthogonality. The vector $Qb$ represents the projection of $a$ onto the column space of $Q$, so $b = Q^{\top}a$. The vector $\rho q_{n+1}$ must be the component of $a$ orthogonal to the column space of $Q$, which is the residual $r = a - Q(Q^{\top}a)$. To satisfy the [normalization condition](@entry_id:156486) $\|q_{n+1}\|_2 = 1$ and the convention of a positive diagonal for $R_{+}$, we set $\rho = \|r\|_2$ and $q_{n+1} = r/\rho$.

This procedure is well-defined as long as $\rho > 0$, which is true if and only if the new column $a$ is linearly independent of the columns of $A$. If $\rho = 0$, the matrix $A_{+}$ is rank-deficient .

#### Inserting or Deleting a Row

Modifying the rows of $A$ induces a more complex perturbation on the QR factors. The primary tool for restoring structure in this context is the **Givens rotation**, an [orthogonal transformation](@entry_id:155650) that acts on a two-dimensional plane to selectively introduce a zero in a vector or matrix.

- **Row Insertion**: Suppose a new row $p^{\top}$ is inserted into $A$. A stable procedure involves first permuting the problem so that the new row is appended to the bottom. The transformed matrix, $\begin{pmatrix} R \\ p^{\top} \end{pmatrix}$, is upper trapezoidal except for the dense final row. A sequence of Givens rotations can then be applied to annihilate the entries of $p^{\top}$ from left to right, transforming it into a multiple of a basis vector. Each rotation introduces a new subdiagonal element, creating a "bulge" that is immediately annihilated by the next rotation. This process, often called "[bulge chasing](@entry_id:151445)," restores the upper trapezoidal form. The product of these Givens rotations is then used to update the $Q$ factor .

- **Row Deletion**: Deleting a row from $A$ is a more delicate operation. A naive [deletion](@entry_id:149110) of a row from $R$ would invalidate the factorization. Instead, the correct procedure first applies a series of Givens rotations to the $Q$ factor to isolate the information of the row-to-be-deleted into a single row of the $R$ factor (typically the last). This initial transformation disrupts the upper triangular structure of $R$, creating a subdiagonal bulge. This bulge is then "chased" down and out of the matrix with another sequence of Givens rotations, restoring the required upper trapezoidal form.

The choice of Givens rotations for these fine-grained updates is natural. However, they are Level-1 BLAS operations with low [arithmetic intensity](@entry_id:746514), leading to memory-bound performance. In contrast, **Householder reflectors**, which operate on entire vectors, can be grouped into blocked (Level-3 BLAS) operations. These blocked updates offer superior performance on modern hardware by maximizing data reuse and achieving high [arithmetic intensity](@entry_id:746514), making them compute-bound. For highly structured updates that introduce many non-zeros at once, blocked Householder methods are preferred, while for sparse, targeted modifications like [bulge chasing](@entry_id:151445), sequences of Givens rotations remain a fundamental tool .

### Mechanisms for Cholesky Factorization

Cholesky factorization applies to [symmetric positive definite](@entry_id:139466) (SPD) matrices, a structure that arises in statistics, optimization, and physical modeling. Update algorithms for Cholesky factors must preserve this SPD structure.

#### The Symmetric Rank-1 Update

The update $A_{\text{new}} = A + uu^{\top}$ is always guaranteed to yield an SPD matrix if $A$ is SPD. Given the factorization $A = R^{\top}R$, we seek a new upper triangular factor $\widehat{R}$ such that $\widehat{R}^{\top}\widehat{R} = R^{\top}R + uu^{\top}$. This can be achieved through an elegant constructive method. Observe that the right-hand side is the Gram matrix of an [augmented matrix](@entry_id:150523):
$$ R^{\top}R + uu^{\top} = \begin{pmatrix} R^{\top} & u \end{pmatrix} \begin{pmatrix} R \\ u^{\top} \end{pmatrix} $$
We can compute the QR factorization of the [augmented matrix](@entry_id:150523) $\begin{pmatrix} R \\ u^{\top} \end{pmatrix}$. That is, we find an orthogonal matrix $\Omega$ such that:
$$ \Omega \begin{pmatrix} R \\ u^{\top} \end{pmatrix} = \begin{pmatrix} \widehat{R} \\ 0^{\top} \end{pmatrix} $$
where $\widehat{R}$ is upper triangular. Since $\Omega$ is orthogonal, $\Omega^{\top}\Omega = I$, and we have:
$$ A_{\text{new}} = \left( \Omega \begin{pmatrix} R \\ u^{\top} \end{pmatrix} \right)^{\top} \left( \Omega \begin{pmatrix} R \\ u^{\top} \end{pmatrix} \right) = \begin{pmatrix} \widehat{R}^{\top} & 0 \end{pmatrix} \begin{pmatrix} \widehat{R} \\ 0^{\top} \end{pmatrix} = \widehat{R}^{\top}\widehat{R} $$
The new Cholesky factor $\widehat{R}$ can be computed stably using a sequence of Givens rotations to zero out the appended row $u^{\top}$. The entire procedure costs $\Theta(n^2)$ [flops](@entry_id:171702) [@problem_id:3600347; @problem_id:3600351].

#### The Symmetric Rank-1 Downdate

The downdate operation, $A_{\text{new}} = A - uu^{\top}$, is significantly more challenging because the result is not guaranteed to remain positive definite. A Cholesky factor with real entries exists if and only if $A_{\text{new}}$ is SPD. This is not a numerical artifact to be overcome by a clever algorithm, but a fundamental mathematical precondition .

The necessary and sufficient condition for $A - uu^{\top}$ to remain [positive definite](@entry_id:149459) is:
$$ u^{\top}A^{-1}u  1 $$
Given the Cholesky factor $R$, this condition is equivalent to $\|R^{-T}u\|_2^2  1$, or simply $\|R^{-T}u\|_2  1$. This provides a computable diagnostic: one can solve the triangular system $R^{\top}z = u$ for $z$ and check if its Euclidean norm is less than 1. If $\|z\|_2 \ge 1$, the downdate is not feasible in the realm of real Cholesky factorization .

When the downdate is feasible, the mechanism for computing $\widehat{R}$ cannot use standard orthogonal transformations. The classical method involves **[hyperbolic rotations](@entry_id:271877)**, which preserve an indefinite inner product associated with the signature matrix $J = \text{diag}(I, -1)$. While effective, this approach is known to have inferior [numerical stability](@entry_id:146550) compared to methods based on orthogonal rotations .

If the feasibility condition is not met, one practical approach is to regularize the problem. Instead of downdating by $u$, we can find a slightly perturbed vector $\tilde{u}$ that is "close" to $u$ but satisfies the feasibility condition with a safety margin, e.g., $\|R^{-1}\tilde{u}\|_2 \le 1-\eta$ for some small $\eta  0$. If "closeness" is measured in the norm $\|R^{-1}(\cdot)\|$, the optimal $\tilde{u}$ is a simple scaling of the original vector: $\tilde{u} = \alpha u$, where $\alpha = \min\left(1, \frac{1 - \eta}{\|R^{-1}u\|_2}\right)$. This minimally adjusts the problem to ensure a stable downdate is possible .

### On Stability, Conditioning, and Structure Preservation

The design of robust update algorithms is guided by principles of numerical stability. The central goal is to preserve key [structural invariants](@entry_id:145830) of the factorization, as this is intrinsically linked to controlling error growth.

- **Orthogonality and Backward Stability**: The insistence on preserving strict orthogonality ($Q^{\top}Q=I$) is paramount. Algorithms for QR updates based on products of orthogonal transformations (Givens, Householder) are **backward stable**. This means that the computed factors, though containing small [floating-point](@entry_id:749453) errors, are the *exact* factors of a matrix that is very close to the original. This is a powerful guarantee, as it recasts the effect of [roundoff error](@entry_id:162651) as a small perturbation to the input data .
- **Uniqueness and Continuity**: For a full-rank matrix, the QR factorization is unique if we enforce a convention, such as requiring the diagonal elements of $R$ to be strictly positive. Maintaining this convention during updates ensures that the factors evolve continuously with smooth changes in the matrix, preventing arbitrary sign flips in the basis vectors of $Q$ .
- **The Peril of the Normal Equations**: In [least-squares problems](@entry_id:151619), one might be tempted to work with the [normal equations](@entry_id:142238) matrix $C = A^{\top}A$ and update its Cholesky factorization. This is a numerically hazardous approach for [ill-conditioned problems](@entry_id:137067). The condition number of the normal equations matrix is the square of the condition number of the original matrix: $\kappa(A^{\top}A) = (\kappa(A))^2$. Explicitly forming $A^{\top}A$ squares the sensitivity of the problem to perturbations, leading to a potential loss of [significant figures](@entry_id:144089) and amplifying the effect of [roundoff error](@entry_id:162651). QR-based methods avoid this by working directly with $A$, whose conditioning is not squared. Therefore, even though Cholesky updates can be stable for the matrix $C$, the initial formation of $C$ can be an irreversible, information-destroying step .
- **The LU Update Challenge**: In stark contrast to QR and Cholesky factorizations, updating an LU factorization with partial pivoting ($PA=LU$) is notoriously difficult. The underlying transformations (Gaussian elimination) are not norm-preserving, and stability depends entirely on the [pivoting strategy](@entry_id:169556). A [rank-1 update](@entry_id:754058) can fundamentally alter the properties of the matrix, often invalidating the original permutation $P$. Finding a new, stable, pivot sequence efficiently without resorting to a full re-factorization is an unsolved problem for general matrices. This lack of a stable, local, pivot-free update mechanism is why LU updates are far less common in practice than their QR and Cholesky counterparts .

### High-Performance Implementations: The Role of Blocked Algorithms

To translate the asymptotic flop reduction of update algorithms into real-world performance gains, implementations must be optimized for modern computer architectures, which are characterized by a deep memory hierarchy. The key to performance is maximizing data reuse to minimize costly communication with main memory.

This is achieved by reformulating algorithms to use **Level-3 BLAS** (Basic Linear Algebra Subprograms), which are matrix-matrix operations. A sequence of $k$ rank-1 updates, each a Level-2 BLAS (matrix-vector) operation, can be **blocked** into a single rank-$k$ update. This blocked operation can be implemented using tile-based strategies. For instance, in a rank-$k$ Cholesky update $A_{\text{new}} = A + UU^{\top}$, panels of the matrix $U$ can be held in fast [cache memory](@entry_id:168095) and reused to update multiple tiles of the main matrix $A$.

By doing so, the [arithmetic intensity](@entry_id:746514) of the operation increases from $\mathcal{O}(1)$ for an unblocked algorithm to $\mathcal{O}(b)$ for a blocked algorithm with tile size $b$. This shifts the operational bottleneck from [memory bandwidth](@entry_id:751847) toward computation, allowing the algorithm to run closer to the processor's peak [floating-point](@entry_id:749453) performance. This principle of blocking is a cornerstone of high-performance libraries like LAPACK and is essential for realizing the full potential of factorization update algorithms .