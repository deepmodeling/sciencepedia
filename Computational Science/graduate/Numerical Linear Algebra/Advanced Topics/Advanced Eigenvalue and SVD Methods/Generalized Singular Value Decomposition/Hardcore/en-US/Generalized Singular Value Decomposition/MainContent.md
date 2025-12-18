## Introduction
While the Singular Value Decomposition (SVD) provides profound insight into the structure and properties of a single matrix, many problems in science and engineering involve the interplay between two distinct [linear operators](@entry_id:149003). How can we simultaneously analyze a data-fitting operator and a regularization operator, or compare the characteristics of two different datasets? The answer lies in the Generalized Singular Value Decomposition (GSVD), a powerful extension of the SVD that provides a canonical form for a pair of matrices sharing a common number of columns. This decomposition is the key to understanding and solving problems where the relationship or trade-off between two matrices is the central concern.

This article provides a comprehensive exploration of the GSVD, designed for graduate-level practitioners in [numerical linear algebra](@entry_id:144418) and related computational fields. It bridges the gap between theoretical definition and practical application, showing how the GSVD framework unlocks solutions to complex problems. Across three chapters, you will gain a deep understanding of this essential [matrix factorization](@entry_id:139760).

*   **Principles and Mechanisms:** We begin by establishing the formal definition of the GSVD, interpreting its components, and exploring its fundamental connection to the generalized eigenvalue problem. This chapter also delves into the numerical mechanisms of stable computation, highlighting why certain theoretical approaches are avoided in practice.

*   **Applications and Interdisciplinary Connections:** Next, we showcase the GSVD in action. We focus on its cornerstone application in solving general-form Tikhonov regularization for [inverse problems](@entry_id:143129) and explore its use as a tool for comparative spectral analysis in fields ranging from machine learning to [computational finance](@entry_id:145856).

*   **Hands-On Practices:** Finally, you will solidify your knowledge through a series of guided problems. These exercises will walk you through computing the GSVD by hand, interpreting its structure in rank-deficient cases, and connecting it to its variational properties.

## Principles and Mechanisms

The Generalized Singular Value Decomposition (GSVD) extends the concept of the Singular Value Decomposition (SVD) from a single matrix to a pair of matrices, $(A, B)$, that share a common number of columns. It serves as a powerful analytical and computational tool for understanding the relationship between the two matrices. The GSVD is particularly indispensable in the analysis and solution of [linear inverse problems](@entry_id:751313), especially those involving regularization, where it provides a coordinate system that simultaneously diagonalizes both the data-fitting term and the regularization term. This chapter elucidates the fundamental principles of the GSVD, its structural interpretation, its connection to generalized eigenvalue problems, its role in regularization, and the key numerical mechanisms underlying its computation.

### The Formal Definition of the GSVD

The GSVD of a matrix pair $(A, B)$ with $A \in \mathbb{C}^{m \times n}$ and $B \in \mathbb{C}^{p \times n}$ is a factorization that reveals their shared and distinct structural properties. There are several formulations of the GSVD; we present the widely used Paige-Saunders formulation, which is particularly insightful for its connection to null spaces and rank properties.

The decomposition asserts the existence of [unitary matrices](@entry_id:200377) $U \in \mathbb{C}^{m \times m}$ and $V \in \mathbb{C}^{p \times p}$, and a nonsingular (invertible) matrix $X \in \mathbb{C}^{n \times n}$, such that:
$$
U^\ast A X = \Sigma_A \quad \text{and} \quad V^\ast B X = \Sigma_B
$$
where $\Sigma_A$ and $\Sigma_B$ are "generalized diagonal" matrices. Their structure is not strictly diagonal but is sparse and block-structured in a way that reveals the relationship between $A$ and $B$.

To define this structure precisely, let $r_A = \mathrm{rank}(A)$, $r_B = \mathrm{rank}(B)$, and $k = \mathrm{rank}\left(\begin{bmatrix} A \\ B \end{bmatrix}\right)$. The dimensions of the blocks are determined by these ranks as follows :
- $s = r_A + r_B - k$
- $k_A = r_A - s$
- $k_B = r_B - s$
- $q = n - k$

The matrix $X$ acts as a [change of basis](@entry_id:145142) for the domain $\mathbb{C}^n$, and its columns can be partitioned into four groups corresponding to these dimensions. The matrices $\Sigma_A = U^\ast A X$ and $\Sigma_B = V^\ast B X$ take on a specific block structure based on this partition. A common convention presents these matrices in a form that reveals their shared null space and their individual actions. For instance, they can be structured as follows:
$$
\Sigma_A = U^\ast A X = \begin{pmatrix} C  & 0 & 0 \\ 0 & I_{k_A} & 0 \\ 0 & 0 & 0 \end{pmatrix} \quad \text{with column partition corresponding to } s, k_A, n-r_A
$$
$$
\Sigma_B = V^\ast B X = \begin{pmatrix} S  & 0 & 0 \\ 0 & 0 & 0 \\ 0 & I_{k_B} & 0 \end{pmatrix} \quad \text{with column partition corresponding to } s, k_A, k_B, q
$$
A more comprehensive form that aligns both matrices is given by :
$$
U^\ast A X = \big[ \ldots C \ldots I_{k_A} \ldots 0 \ldots \big] \quad \text{and} \quad V^\ast B X = \big[ \ldots S \ldots 0 \ldots I_{k_B} \ldots \big]
$$
where $C = \mathrm{diag}(c_1, \dots, c_s)$ and $S = \mathrm{diag}(s_1, \dots, s_s)$ are real, non-negative [diagonal matrices](@entry_id:149228) of size $s \times s$. The crucial property linking them is the **cosine-sine relationship**:
$$
C^2 + S^2 = I_s
$$
This means that for each $i=1, \dots, s$, we have $c_i^2 + s_i^2 = 1$. This allows us to think of $c_i$ and $s_i$ as the cosine and sine of an angle, which is the origin of the term "CS decomposition" for a related factorization.

### Interpretation of Generalized Singular Values

The **[generalized singular values](@entry_id:749794)** of the pair $(A,B)$ are the ratios $\gamma_i$ derived from the diagonal entries of $C$ and $S$. For $i=1, \dots, s$, they are defined as:
$$
\gamma_i = \frac{c_i}{s_i}, \quad \text{for } s_i \neq 0
$$
The set of [generalized singular values](@entry_id:749794) may also include values of $0$ (from the $k_A$ block) and $\infty$ (from the $k_B$ block). These special values have important structural interpretations .

Let $x_j$ be the $j$-th column of the matrix $X$. The GSVD equations imply $A x_j = c_j u_j$ and $B x_j = s_j v_j$ for some columns $u_j$ of $U$ and $v_j$ of $V$.

-   **Finite, Nonzero $\gamma_i$:** These correspond to vectors $x_i$ that are mapped non-trivially by both $A$ and $B$. The value $\gamma_i$ represents the ratio of the "gains" $\|Ax_i\|_2 / \|Bx_i\|_2$ in the transformed coordinate system.

-   **Zero $\gamma_i$:** A generalized [singular value](@entry_id:171660) is zero if its corresponding $c_i=0$ while $s_i>0$. This corresponds to a vector $x_i$ such that $Ax_i=0$ but $Bx_i \neq 0$. In other words, such vectors lie in the [null space](@entry_id:151476) of $A$ but not in the [null space](@entry_id:151476) of $B$.

-   **Infinite $\gamma_i$:** Conversely, a generalized [singular value](@entry_id:171660) is infinite if $s_i=0$ while $c_i>0$. This corresponds to a vector $x_i$ such that $Bx_i=0$ but $Ax_i \neq 0$. These vectors lie in the null space of $B$ but not in the null space of $A$.

To illustrate the case of an infinite [singular value](@entry_id:171660), consider the matrix pair :
$$
A = \begin{pmatrix} 0 & 1 \\ 0 & 1 \\ 0 & 1 \end{pmatrix}, \quad B = \begin{pmatrix} 1 & 0 \\ 0 & 0 \\ 0 & 0 \end{pmatrix}
$$
The vector $x = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$ lies in the null space of $B$, since $Bx = 0$. However, $Ax = \begin{pmatrix} 1 \\ 1 \\ 1 \end{pmatrix} \neq 0$. Therefore, this vector $x$ must be associated with an infinite generalized singular value of the pair $(A,B)$.

### Connection to the Generalized Eigenvalue Problem

The GSVD is fundamentally linked to a generalized symmetric/Hermitian-definite [eigenvalue problem](@entry_id:143898). To see this, we start with the GSVD relations $U^\ast A X = \Sigma_A$ and $V^\ast B X = \Sigma_B$. Rearranging gives $A = U \Sigma_A X^{-1}$ and $B = V \Sigma_B X^{-1}$. Now, let's form the Gram matrices $A^\ast A$ and $B^\ast B$:
$$
A^\ast A = (X^{-1})^\ast \Sigma_A^\ast U^\ast U \Sigma_A X^{-1} = (X^{-1})^\ast (\Sigma_A^\ast \Sigma_A) X^{-1}
$$
$$
B^\ast B = (X^{-1})^\ast \Sigma_B^\ast V^\ast V \Sigma_B X^{-1} = (X^{-1})^\ast (\Sigma_B^\ast \Sigma_B) X^{-1}
$$
For the "cosine-sine" part of the decomposition, $\Sigma_A^\ast \Sigma_A = C^2$ and $\Sigma_B^\ast \Sigma_B = S^2$. Let $y = X^{-1}x$. Substituting these into the [generalized eigenvalue problem](@entry_id:151614) $A^\ast A x = \lambda B^\ast B x$ gives:
$$
(X^{-1})^\ast C^2 X^{-1} x = \lambda (X^{-1})^\ast S^2 X^{-1} x
$$
Multiplying by $X^\ast$ on the left and setting $x=Xy$, we obtain:
$$
C^2 y = \lambda S^2 y
$$
Since $C$ and $S$ are diagonal, this decouples into scalar equations for each component $y_i$:
$$
c_i^2 y_i = \lambda_i s_i^2 y_i
$$
If $s_i \neq 0$ and $y_i \neq 0$, we can divide to find the relationship:
$$
\lambda_i = \frac{c_i^2}{s_i^2} = \left(\frac{c_i}{s_i}\right)^2 = \gamma_i^2
$$
This proves that the squares of the finite [generalized singular values](@entry_id:749794), $\gamma_i^2$, are precisely the finite generalized eigenvalues of the pencil $(A^\ast A, B^\ast B)$ . This connection is fundamental, but as we will see, it also points to a numerically fraught computational strategy.

This principle extends to the **weighted GSVD**, where we introduce [symmetric positive definite](@entry_id:139466) weight matrices $M$ and $N$ and seek factors satisfying $U^\top M U = I$ and $V^\top N V = I$. The squared weighted [generalized singular values](@entry_id:749794) $\gamma_i^2$ are then the generalized eigenvalues of the weighted pencil $(A^\top M A, B^\top N B)$ .

### The GSVD as a Mechanism for Regularization

One of the most important applications of the GSVD is in solving Tikhonov-regularized [least-squares problems](@entry_id:151619), which are common in science and engineering for dealing with [ill-posed inverse problems](@entry_id:274739). A general-form Tikhonov problem is stated as:
$$
\min_{x \in \mathbb{R}^n} \|Ax - b\|_2^2 + \lambda^2 \|Lx\|_2^2
$$
Here, $A$ is the model matrix, $b$ is the observed data (often contaminated with noise), $L$ is a regularization operator (e.g., a derivative operator), and $\lambda > 0$ is the regularization parameter that balances the trade-off between fitting the data and smoothing the solution.

The GSVD of the matrix pair $(A,L)$ provides a coordinate system that perfectly decouples this minimization problem. Let the GSVD be $A=UCQ^\top$ and $L=VSQ^\top$. Let us perform a change of variables $y = Q^\top x$, so $x = Qy$ (since $Q$ is orthogonal). The [objective function](@entry_id:267263) becomes :
$$
J(y) = \|UCQ^\top(Qy) - b\|_2^2 + \lambda^2 \|VSQ^\top(Qy)\|_2^2
$$
$$
J(y) = \|UCy - b\|_2^2 + \lambda^2 \|VSy\|_2^2
$$
Since $U$ and $V$ are orthogonal, we can multiply by $U^\top$ and $V^\top$ inside the norms:
$$
J(y) = \|C y - U^\top b\|_2^2 + \lambda^2 \|S y\|_2^2
$$
Let $\tilde{b} = U^\top b$ be the data vector in the new coordinate system. Since $C$ and $S$ are diagonal, the objective function separates into a sum of $n$ independent scalar problems:
$$
J(y) = \sum_{i=1}^n \left[ (c_i y_i - \tilde{b}_i)^2 + (\lambda s_i y_i)^2 \right]
$$
The solution for each component $y_i$ is found by setting the derivative to zero:
$$
y_i = \left( \frac{c_i}{c_i^2 + \lambda^2 s_i^2} \right) \tilde{b}_i
$$
The terms $f_i(\lambda) = \frac{c_i}{c_i^2 + \lambda^2 s_i^2}$ are known as the **GSVD filter factors**. They reveal the mechanism of Tikhonov regularization with remarkable clarity. The solution is obtained by filtering the transformed data coefficients $\tilde{b}_i$.

For a component where the generalized [singular value](@entry_id:171660) $\gamma_i = c_i/s_i$ is very large, the filter factor is approximately $f_i \approx c_i / c_i^2 = 1/c_i$. For components where $\gamma_i$ is very small, the filter factor is approximately $f_i \approx c_i / (\lambda^2 s_i^2) = (\gamma_i^2/\lambda^2) (1/c_i)$. The [regularization parameter](@entry_id:162917) $\lambda$ thus selectively [damps](@entry_id:143944) the components corresponding to small [generalized singular values](@entry_id:749794), which are precisely the components that are unstable and tend to be amplified by noise. This framework allows for a rigorous analysis of parameter choice rules, such as the Morozov [discrepancy principle](@entry_id:748492) .

### Numerical Mechanisms and Computational Strategies

While the connection to the [generalized eigenproblem](@entry_id:168055) $(A^\ast A, B^\ast B)$ is theoretically elegant, it forms the basis of a numerically unstable computational method.

#### The Perils of Forming Gram Matrices

The explicit formation of the Gram matrices $A^\ast A$ and $B^\ast B$ is generally discouraged in high-precision numerical computation. The reason is that this process **squares the condition number** of the matrices. For a [non-singular matrix](@entry_id:171829) $M$, its [2-norm](@entry_id:636114) condition number is $\kappa_2(M) = \sigma_{\max}(M) / \sigma_{\min}(M)$. The condition number of its Gram matrix is :
$$
\kappa_2(M^\ast M) = (\kappa_2(M))^2
$$
If $A$ is ill-conditioned (i.e., $\kappa_2(A)$ is large), $\kappa_2(A^\ast A)$ will be dramatically larger. In [floating-point arithmetic](@entry_id:146236), this can lead to a severe loss of information. Small singular values of $A$ may become smaller than machine precision when squared, making the computed $A^\ast A$ numerically singular. This loss of definiteness can cause algorithms for the [generalized eigenproblem](@entry_id:168055), such as those based on Cholesky factorization, to fail entirely .

For this reason, robust GSVD algorithms work directly on the matrices $A$ and $B$ using sequences of numerically stable orthogonal transformations, such as Householder reflections or Givens rotations. These methods avoid the formation of Gram matrices and are backward stable.

#### Practical QR-Based Algorithms

A common class of stable algorithms for the GSVD begins with an orthogonal factorization of the stacked matrix $G = \begin{pmatrix} A \\ B \end{pmatrix}$. A typical procedure is :
1.  Compute a QR factorization of $G$, often with [column pivoting](@entry_id:636812), to get $G\Pi = QR$, where $R$ is upper triangular and $\Pi$ is a [permutation matrix](@entry_id:136841). This step effectively finds an [orthonormal basis](@entry_id:147779) for the range of $G$.
2.  Partition the orthogonal matrix $Q$ and use its blocks to set up a CS decomposition problem, which is then solved iteratively.

The leading-order computational cost of such an algorithm for $m,p \ge n$ is typically $O((m+p)n^2 + n^3)$. Column pivoting is crucial when $G$ is nearly rank-deficient; it helps to isolate the ill-conditioned parts of the problem and improves the accuracy of the computed finite [generalized singular values](@entry_id:749794).

Proper **pre-scaling** is also a critical mechanism. If the norms of $A$ and $B$ are vastly different, information in the smaller-norm matrix can be lost in the initial QR factorization. A sound strategy is to apply a common right diagonal [scaling matrix](@entry_id:188350) $D$ to work with the pair $(AD, BD)$, chosen to equilibrate the column norms of $\begin{pmatrix} A \\ B \end{pmatrix}$. This transformation does not change the [generalized singular values](@entry_id:749794) and can significantly improve numerical stability .

Finally, even with stable algorithms, the computed factors may not perfectly satisfy the $c_i^2 + s_i^2 = 1$ constraint due to [rounding errors](@entry_id:143856). A simple and robust post-processing step can enforce this. For each pair $(\widehat{c}_i, \widehat{s}_i)$, one can compute $r_i = \sqrt{\widehat{c}_i^2 + \widehat{s}_i^2}$ and replace them with $c_i' = \widehat{c}_i/r_i$ and $s_i' = \widehat{s}_i/r_i$. This small correction can be absorbed by scaling the corresponding column of the matrix $X$, thus restoring the GSVD structure with only minimal perturbation to the computed factors .

### Advanced Topic: Block-Diagonal GSVD

In some applications, such as [domain decomposition](@entry_id:165934), the matrices $A$ and $B$ may have a natural block-column structure, e.g., $A = [A_1, A_2, \dots, A_q]$. It is of great interest to know when the GSVD itself decouples according to this partition. This occurs if the matrix pencils $(A^\top A, B^\top B)$ are block-diagonal with respect to the partition. This condition is met if and only if the column blocks are mutually orthogonal in the sense that :
$$
A_i^\top A_j = 0 \quad \text{and} \quad B_i^\top B_j = 0 \quad \text{for all } i \neq j.
$$
When these conditions hold, the GSVD can be computed independently for each pair $(A_i, B_i)$, and the global decomposition can be assembled from these smaller problems. The matrix $X$ will be block-diagonal, and the global set of [generalized singular values](@entry_id:749794) is simply the union of the singular values from each block. This provides a powerful mechanism for [parallel computation](@entry_id:273857), confining the "global" coupling to the orthogonal row transformations embodied by $U$ and $V$.