## Introduction
Eigenvalues and eigenvectors are fundamental properties of a matrix, revealing critical information about the linear systems they represent, from the stability of a bridge to the dynamics of a population. While they are defined elegantly in algebraic terms, their actual computation is fraught with numerical peril. Naive methods, such as finding the roots of the characteristic polynomial, are notoriously unstable and fail in practice. This gap between theoretical definition and practical computation necessitates a robust, efficient, and reliable algorithm.

This article explores the QR algorithm, the modern workhorse for solving the [eigenvalue problem](@entry_id:143898). Across three chapters, you will gain a comprehensive understanding of this cornerstone of [numerical linear algebra](@entry_id:144418). The first chapter, "Principles and Mechanisms," delves into the construction of the QR algorithm, explaining why it is numerically stable and how it is made efficient through strategies like Hessenberg reduction and shifts. The second chapter, "Applications and Interdisciplinary Connections," showcases the algorithm's far-reaching impact in fields from physics and engineering to economics and data science. Finally, "Hands-On Practices" provides opportunities to apply these concepts and build a tangible intuition for the method's mechanics. We begin by examining the core computational challenge and the elegant principles that make the QR algorithm the definitive solution.

## Principles and Mechanisms

Having established the fundamental importance of [eigenvalues and eigenvectors](@entry_id:138808) in the introductory chapter, we now turn to the central computational problem: how can we reliably and efficiently compute them? This chapter delves into the principles and mechanisms of the modern workhorse for this task, the QR algorithm. We will explore why simpler, intuitive methods fail, how the QR algorithm is constructed from fundamental principles of linear algebra, and what refinements are necessary to transform it into the robust and efficient tool used across scientific and engineering disciplines today.

### The Instability of the Characteristic Polynomial

A direct approach to finding the eigenvalues of a matrix $A \in \mathbb{R}^{n \times n}$ stems from their definition as the roots of the **[characteristic polynomial](@entry_id:150909)**, $p(\lambda) = \det(A - \lambda I)$. One might propose a two-step method: first, compute the coefficients $c_0, \dots, c_{n-1}$ of $p(\lambda) = \lambda^n + c_{n-1}\lambda^{n-1} + \dots + c_0$; second, find the roots of this polynomial. While algebraically sound, this method is fundamentally flawed from a numerical standpoint, especially for matrices of even moderate size (e.g., $n \ge 20$).

The first issue is that computing the coefficients $c_i$ from the entries of $A$ is a numerically delicate task, prone to significant rounding errors. More critically, however, the problem of finding the roots of a polynomial from its coefficients is notoriously **ill-conditioned**. This means that minuscule perturbations in the coefficients, such as those inevitably introduced by [floating-point arithmetic](@entry_id:146236), can lead to enormous changes in the computed roots. This sensitivity is particularly severe when eigenvalues are close to one another, or "clustered". The classic example provided by J.H. Wilkinson involves a polynomial of degree 20 whose roots are the integers $1, 2, \dots, 20$. A single perturbation of about $10^{-10}$ to one coefficient is sufficient to transform many of the real roots into complex-conjugate pairs with large imaginary parts. For these reasons, computing eigenvalues by finding the roots of the [characteristic polynomial](@entry_id:150909) is an unreliable method and is never used in serious computational practice [@problem_id:3121800].

### The QR Iteration: An Orthogonally Stable Approach

The modern approach, the **QR algorithm**, abandons the path through coefficients and instead works directly with the matrix. It generates a sequence of matrices, $A_0, A_1, A_2, \dots$, starting with $A_0 = A$, such that each matrix in the sequence is orthogonally similar to the previous one. The sequence is constructed to converge to a form—typically upper triangular or quasi-triangular—from which the eigenvalues can be easily read.

A single step of the basic QR algorithm is defined as follows:
1.  Compute the **QR factorization** of the current matrix $A_k = Q_k R_k$, where $Q_k$ is an **orthogonal** matrix ($Q_k^T Q_k = I$) and $R_k$ is an [upper triangular matrix](@entry_id:173038).
2.  Form the next matrix in the sequence by multiplying the factors in reverse order: $A_{k+1} = R_k Q_k$.

The genius of this construction lies in the fact that each step is an **orthogonal similarity transformation**. We can see this by substituting $R_k = Q_k^T A_k$ (derived from the factorization step) into the update formula:
$$ A_{k+1} = R_k Q_k = (Q_k^T A_k) Q_k = Q_k^T A_k Q_k $$
Since $Q_k^{-1} = Q_k^T$, this is precisely a [similarity transformation](@entry_id:152935). Consequently, $A_{k+1}$ has the same eigenvalues as $A_k$, and by induction, all matrices in the sequence $\{A_k\}$ share the same eigenvalues as the original matrix $A$. This process avoids computing a matrix inverse explicitly; it only requires the transpose, a computationally trivial operation [@problem_id:3121848].

The numerical power of the QR algorithm derives from its exclusive use of orthogonal transformations. An [orthogonal matrix](@entry_id:137889) $Q$ has a Euclidean condition number $\kappa_2(Q) = \|Q\|_2 \|Q^{-1}\|_2 = 1$, the lowest possible value. This perfect conditioning means that applying $Q$ or its transpose preserves the Euclidean norm of any vector $x$:
$$ \|Qx\|_2^2 = (Qx)^T(Qx) = x^T Q^T Q x = x^T I x = \|x\|_2^2 $$
In [finite-precision arithmetic](@entry_id:637673), this property is crucial because it prevents the systematic amplification of [rounding errors](@entry_id:143856) during the iteration. While a general similarity transformation $P^{-1}AP$ also preserves eigenvalues in exact arithmetic, it can be numerically disastrous if the matrix $P$ is ill-conditioned (i.e., has a large condition number $\kappa_2(P)$), as this can magnify errors. The QR algorithm's reliance on perfectly conditioned [orthogonal matrices](@entry_id:153086) is the key to its celebrated numerical stability [@problem_id:3121848] [@problem_id:3121826].

### The Two-Phase Strategy: Hessenberg and Tridiagonal Reduction

While stable, the basic QR algorithm as described is too slow for practical use. The QR factorization of a dense $n \times n$ matrix requires $\mathcal{O}(n^3)$ [floating-point operations](@entry_id:749454) (FLOPs). Performing many such iterations would be prohibitively expensive.

The solution is a two-phase strategy. In the first phase, we perform a one-time, direct transformation of the original dense matrix $A$ into a much simpler form that is cheaper to iterate on. This is achieved using a finite sequence of orthogonal similarity transformations, for instance, using **Householder reflectors**. The resulting matrix, let's call it $H$, is orthogonally similar to $A$ ($H = Q^T A Q$) and thus has the same eigenvalues. The structure of $H$ depends on whether $A$ is symmetric.

-   For a **general (non-symmetric) matrix $A$**, it is reduced to an **upper Hessenberg form** $H$, where all entries below the first subdiagonal are zero ($h_{ij} = 0$ for $i > j+1$).
-   For a **symmetric matrix $A$**, it is reduced to a **symmetric tridiagonal form** $T$, where the only non-zero entries are on the main diagonal and the first super- and sub-diagonals.

In the second phase, the QR iteration is applied to this reduced form ($H$ or $T$). The key insight is that the QR algorithm preserves these special structures. If $A_k$ is upper Hessenberg, then $A_{k+1}$ will also be upper Hessenberg. This is not true for a general similarity transformation [@problem_id:3121848], but it is a special property of the QR step. This structure preservation is what makes the two-phase approach efficient. The cost of a QR factorization of an $n \times n$ Hessenberg matrix is only $\mathcal{O}(n^2)$ FLOPs, a dramatic improvement over the $\mathcal{O}(n^3)$ cost for a dense matrix. For a [tridiagonal matrix](@entry_id:138829), the cost is even lower, at just $\mathcal{O}(n)$ FLOPs per iteration [@problem_id:3121826].

The initial reduction to Hessenberg or tridiagonal form costs $\mathcal{O}(n^3)$ operations. However, this is a one-time investment. The subsequent iterative phase, which may require many steps, benefits from the vastly lower per-iteration cost. For large $n$, the total time is dominated by the initial reduction. For a [symmetric matrix](@entry_id:143130), for example, the [reduction to tridiagonal form](@entry_id:754185) has a leading-order cost of $\frac{4}{3}n^3$ FLOPs, while the entire subsequent iterative phase to find all eigenvalues costs only $\mathcal{O}(n^2)$, which is asymptotically negligible [@problem_id:3121835]. This two-phase strategy is therefore overwhelmingly more efficient than applying the QR algorithm directly to the [dense matrix](@entry_id:174457) $A$.

### Accelerating Convergence: The Power of Shifts

The convergence of the basic QR algorithm can be unacceptably slow. For a symmetric matrix with eigenvalues ordered $|\lambda_1| > |\lambda_2| > \dots > |\lambda_n|$, the subdiagonal entry $A_k(j+1, j)$ converges to zero at a rate proportional to $(|\lambda_{j+1}/\lambda_j|)^k$. If two eigenvalues have nearly equal magnitudes, the ratio $|\lambda_{j+1}/\lambda_j|$ is close to 1, leading to very slow convergence [@problem_id:3121866].

To accelerate convergence, the QR algorithm is used with **shifts of origin**. The iteration is modified to:
1.  Choose a shift $\mu_k$ (a scalar close to an eigenvalue of $A_k$).
2.  Factorize the shifted matrix: $A_k - \mu_k I = Q_k R_k$.
3.  Update: $A_{k+1} = R_k Q_k + \mu_k I$.

This new iterate $A_{k+1}$ remains orthogonally similar to $A_k$. A good choice of shift can lead to spectacular acceleration. A particularly powerful strategy for symmetric tridiagonal matrices is the **Wilkinson shift**. At each step, one considers the trailing $2 \times 2$ submatrix:
$$ B = \begin{pmatrix} a  b \\ b  c \end{pmatrix} $$
The Wilkinson shift is defined as the eigenvalue of this block that is closer to the corner entry $c$. This simple choice has a profound effect. It breaks the symmetry in cases where eigenvalues are nearly symmetric about a point (a "symmetric doublet"), a scenario that can stall simpler shift strategies. With the Wilkinson shift, the QR algorithm for symmetric tridiagonal matrices achieves, on average, an asymptotic cubic rate of convergence, meaning the number of correct digits in the subdiagonal entry triples at each step. This ensures that eigenvalues are found with remarkable speed and robustness [@problem_id:3121828] [@problem_id:3121866].

### Practical Implementation: Implicit Shifts and Deflation

In a production-level implementation, the matrices $Q_k$ and $R_k$ are never explicitly formed. Instead, the shifted QR step is performed **implicitly**. For a Hessenberg matrix $H$, the process begins by choosing a shift (or a pair of shifts for the non-symmetric case) and computing the first column of the matrix $(H-\mu I)$. A single $2 \times 2$ Givens rotation $G_1$ is then applied to the first two rows to zero out the second element of this column vector. This [similarity transformation](@entry_id:152935) $H \rightarrow G_1 H G_1^T$ preserves the Hessenberg structure except for creating an unwanted nonzero entry at position $(3,1)$, known as a "bulge".

The rest of the implicit step consists of "chasing the bulge". A sequence of further Givens rotations, $G_2, G_3, \dots, G_{n-1}$, is applied, each designed to zero out the bulge created by the previous step, propagating it one position down and to the right. When the bulge is chased off the bottom-right corner of the matrix, one implicit QR step is complete. The resulting matrix is exactly the one that would have been obtained by the explicit shifted QR step, but it has been computed more efficiently and with fewer rounding errors [@problem_id:3121890].

As the algorithm proceeds, subdiagonal entries converge to zero. When an entry $h_{k+1, k}$ becomes negligibly small, we can effectively set it to zero. This is called **deflation**. It decouples the matrix into two smaller, independent subproblems (a $k \times k$ block and an $(n-k) \times (n-k)$ block) that can be solved separately, greatly improving efficiency. A robust criterion for deflation is to set $h_{k+1, k}$ to zero when its magnitude is on the order of the roundoff uncertainty in its diagonal neighbors:
$$ |h_{k+1,k}| \le u (|h_{k,k}| + |h_{k+1,k+1}|) $$
where $u$ is the [unit roundoff](@entry_id:756332) of the machine arithmetic. This ensures that the introduced perturbation is "in the noise" and does not compromise the [backward stability](@entry_id:140758) of the overall computation [@problem_id:3121874].

### Symmetric versus Non-Symmetric Matrices: A Tale of Two Decompositions

The behavior and output of the QR algorithm differ fundamentally for symmetric and [non-symmetric matrices](@entry_id:153254), reflecting the underlying structure of their eigensystems.

For a **real symmetric matrix $A$**, the QR algorithm computes its **spectral decomposition**.
- The iterates $A_k$ remain symmetric and converge to a **[diagonal matrix](@entry_id:637782)** $D$ containing the real eigenvalues.
- The accumulated product of the orthogonal transformations, $\mathcal{Q} = Q_0 Q_1 Q_2 \dots$, converges to an [orthogonal matrix](@entry_id:137889) whose columns are the **orthonormal eigenvectors** of $A$.
The algorithm is a [constructive proof](@entry_id:157587) of the spectral theorem for [symmetric matrices](@entry_id:156259).

For a **general real non-[symmetric matrix](@entry_id:143130) $A$**, the QR algorithm computes its **real Schur decomposition**.
- The matrix may have complex eigenvalues, which occur in conjugate pairs. Such a matrix cannot be diagonalized using a real [similarity transformation](@entry_id:152935).
- The iterates $A_k$ converge to a **quasi-upper triangular matrix** $T$, also known as the real Schur form. This is an [upper triangular matrix](@entry_id:173038) with the addition of $2 \times 2$ blocks on the diagonal, which correspond to complex-conjugate eigenpairs.
- A $2 \times 2$ block of the form $$ B = \begin{pmatrix} a  -b \\ b  a \end{pmatrix} $$ has eigenvalues $a \pm ib$ and represents a composition of a rotation and a uniform scaling in a 2D [invariant subspace](@entry_id:137024) [@problem_id:3121881].
- The accumulated [orthogonal matrix](@entry_id:137889) $\mathcal{Q}$ does **not** contain eigenvectors. Its columns are **Schur vectors**, which form an [orthonormal basis](@entry_id:147779) for a set of nested [invariant subspaces](@entry_id:152829) of $A$.

In [finite precision arithmetic](@entry_id:142321), if a [symmetric matrix](@entry_id:143130) is processed by an implementation that does not enforce symmetry, small perturbations can destroy it. The algorithm will then behave as if it were for a non-[symmetric matrix](@entry_id:143130), converging to a quasi-triangular form of a nearby perturbed matrix. This highlights the [backward stability](@entry_id:140758) of the algorithm: it always computes the exact decomposition of a slightly different initial matrix [@problem_id:3121829].