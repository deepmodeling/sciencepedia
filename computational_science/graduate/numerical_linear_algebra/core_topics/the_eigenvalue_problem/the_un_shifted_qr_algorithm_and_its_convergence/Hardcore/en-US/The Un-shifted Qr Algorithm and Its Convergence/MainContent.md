## Introduction
The QR algorithm stands as a cornerstone of numerical linear algebra, representing one of the most significant algorithmic developments of the 20th century for computing the eigenvalues of a matrix. While modern computational libraries employ highly sophisticated, shifted versions of this algorithm, a deep understanding of its foundational form—the un-shifted QR iteration—is indispensable for any serious practitioner or student of the field. This basic algorithm, though often too slow for direct practical use, exposes the core mathematical principles and convergence behaviors that underpin all its powerful successors. This article addresses the crucial knowledge gap between using a black-box eigenvalue solver and truly understanding the mechanics that make it work.

This article will guide you through a comprehensive exploration of the un-shifted QR algorithm. The journey begins in the **Principles and Mechanisms** chapter, where we will dissect the iterative process, establish its connection to the Schur decomposition, and unravel the elegant theory that explains why and how it converges by linking it to the power method. Next, the **Applications and Interdisciplinary Connections** chapter will bridge theory with practice. We will explore the critical two-phase strategy involving Hessenberg reduction that makes the algorithm practical, analyze the dynamics of convergence, and see how this foundational method connects to real-world problems in fields like machine learning and [computational mechanics](@entry_id:174464). Finally, the **Hands-On Practices** section provides an opportunity to solidify these concepts through guided computational exercises, from basic iteration to analyzing more complex convergence scenarios.

## Principles and Mechanisms

The un-shifted QR algorithm provides a foundational method for computing the eigenvalues and, ultimately, the Schur decomposition of a matrix. While its basic form is often too slow for practical use, a thorough understanding of its operational principles and convergence characteristics is indispensable. It forms the intellectual bedrock upon which more sophisticated and efficient variants, such as the shifted QR algorithm, are built. This chapter elucidates the core mechanics, convergence theory, and inherent limitations of the un-shifted QR iteration.

### The Un-shifted QR Iteration: Definition and Properties

The algorithm is an iterative procedure that generates a sequence of matrices, $\{A_k\}_{k=0}^{\infty}$, starting with $A_0 = A$. Each step of the iteration, for $k=0, 1, 2, \dots$, consists of two fundamental operations:

1.  **QR Factorization:** The matrix $A_k$ is decomposed into the product of an [orthogonal matrix](@entry_id:137889) $Q_k$ (or unitary in the complex case, satisfying $Q_k^\ast Q_k = I$) and an [upper triangular matrix](@entry_id:173038) $R_k$. This gives the relation $A_k = Q_k R_k$.

2.  **Matrix Update:** The order of the factors is reversed to form the next matrix in the sequence, $A_{k+1} = R_k Q_k$.

A crucial property of this process is that each iterate $A_{k+1}$ is orthogonally similar to its predecessor $A_k$. This can be shown by substituting the QR factorization into the update rule. Since $Q_k$ is orthogonal, we can write $Q_k^\top A_k = Q_k^\top (Q_k R_k) = (Q_k^\top Q_k) R_k = I R_k = R_k$. Substituting this expression for $R_k$ into the update formula yields:

$A_{k+1} = R_k Q_k = (Q_k^\top A_k) Q_k = Q_k^\top A_k Q_k$

This relationship reveals that the entire sequence $\{A_k\}$ consists of matrices that are orthogonally similar to the original matrix $A_0$. A direct consequence is that all matrices in the sequence share the same eigenvalues. The goal of the algorithm is to iteratively transform $A$ into a form where the eigenvalues are readily visible, namely an upper triangular or block-upper triangular form.

Let us illustrate the process with a concrete example. Consider the [symmetric matrix](@entry_id:143130) from :
$A_0=\begin{pmatrix} 2  & 1 \\ 1  & 2 \end{pmatrix}$

For the first iteration ($k=0$), we compute the QR decomposition $A_0 = Q_0 R_0$. Using the Gram-Schmidt process on the columns of $A_0$, we find:
$Q_0 = \frac{1}{\sqrt{5}} \begin{pmatrix} 2  & -1 \\ 1  & 2 \end{pmatrix}$ and $R_0 = Q_0^\top A_0 = \frac{1}{\sqrt{5}} \begin{pmatrix} 5  & 4 \\ 0  & 3 \end{pmatrix}$

Next, we form $A_1$ by reversing the factors:
$A_1 = R_0 Q_0 = \frac{1}{5} \begin{pmatrix} 14  & 3 \\ 3  & 6 \end{pmatrix} \approx \begin{pmatrix} 2.8  & 0.6 \\ 0.6  & 1.2 \end{pmatrix}$

Notice that the off-diagonal entries have decreased from $1$ to $0.6$, and the diagonal entries have moved closer to the true eigenvalues of $A_0$, which are $\lambda_1 = 3$ and $\lambda_2 = 1$. Repeating the process for a second iteration gives:
$A_2 = \frac{1}{41} \begin{pmatrix} 122  & 9 \\ 9  & 42 \end{pmatrix} \approx \begin{pmatrix} 2.9756  & 0.2195 \\ 0.2195  & 1.0244 \end{pmatrix}$

After just two steps, the diagonal entries have converged significantly closer to the eigenvalues, and the off-diagonal entries have shrunk further. This example demonstrates the essential behavior of the algorithm: the iterates $A_k$ tend toward a form where the mass is concentrated on the diagonal (or block-diagonal), revealing the eigenvalues.

The practical computation of the QR factorization is a critical component. While the Gram-Schmidt process used in the example is instructive, it is known to be numerically unstable. In practice, QR factorizations are computed using more robust methods, such as a sequence of **Householder reflectors** or **Givens rotations**. For instance, a Householder reflector can be constructed to zero out all subdiagonal entries in a column of the matrix at once. For an $n \times n$ matrix, a sequence of $n-1$ Householder transformations can reduce it to upper triangular form .

A simple but important property of the algorithm concerns scaling. If the algorithm is applied to a scaled matrix $\alpha A$ (with $\alpha > 0$), the iterates are simply scaled versions of the original sequence: $(\alpha A)_k = \alpha A_k$. This follows from the uniqueness of the QR factorization (with a convention, e.g., positive diagonal on $R_k$), where if $A_k = Q_k R_k$, then $(\alpha A_k) = Q_k (\alpha R_k)$ is the corresponding factorization. This implies that measures of convergence relative to the [matrix norm](@entry_id:145006) are [scale-invariant](@entry_id:178566), whereas absolute measures are not .

### Convergence: The "Why" and the "What"

The empirical observation that the QR algorithm converges to a triangular form that reveals eigenvalues begs two fundamental questions: What is the precise form of the limit matrix, and what is the underlying mechanism that drives this convergence?

#### The Convergence Target: The Schur Form

For any square matrix $A \in \mathbb{C}^{n \times n}$, the **Schur Decomposition Theorem** states that there exists a [unitary matrix](@entry_id:138978) $U$ and an upper triangular matrix $T$ such that $A = U T U^\ast$. The diagonal entries of $T$ are precisely the eigenvalues of $A$. The QR algorithm is, in essence, an iterative procedure for constructing this decomposition.

When working with real matrices in real arithmetic, we may encounter [complex conjugate](@entry_id:174888) pairs of eigenvalues. To avoid complex arithmetic, we use the **Real Schur Decomposition**. For any real matrix $A \in \mathbb{R}^{n \times n}$, there exists an [orthogonal matrix](@entry_id:137889) $Q$ and a block upper triangular matrix $T$ (also called a quasi-[triangular matrix](@entry_id:636278)) such that $A = Q T Q^\top$. The diagonal blocks of $T$ are either $1 \times 1$ blocks corresponding to real eigenvalues of $A$, or $2 \times 2$ blocks whose eigenvalues are a [complex conjugate pair](@entry_id:150139) of eigenvalues of $A$ . The un-shifted QR algorithm, when applied to a real matrix, converges toward this real Schur form.

#### The Convergence Mechanism: Power Iteration in Disguise

The convergence of the QR algorithm is elegantly explained by its deep connection to the **power method** and its generalization, **simultaneous iteration** (also known as orthogonal iteration) .

Let us define the accumulated [orthogonal matrix](@entry_id:137889) after $k$ steps as $\widehat{Q}_k = Q_0 Q_1 \cdots Q_{k-1}$. The iterate $A_k$ is then given by $A_k = \widehat{Q}_k^\ast A \widehat{Q}_k$. The key insight comes from examining the QR factorization of the $k$-th power of $A$:
$A^1 = A = Q_0 R_0 = \widehat{Q}_1 R_0$
$A^2 = A \cdot A = (Q_0 R_0)(Q_0 R_0) = Q_0 (R_0 Q_0) R_0 = Q_0 A_1 R_0 = Q_0 (Q_1 R_1) R_0 = (Q_0 Q_1)(R_1 R_0) = \widehat{Q}_2 (R_1 R_0)$

By induction, one can show that the QR factorization of the $k$-th power of $A$ is:
$A^k = \widehat{Q}_k \widehat{R}_k$, where $\widehat{R}_k = R_{k-1} \cdots R_1 R_0$.

This reveals that the columns of $\widehat{Q}_k$ form an [orthonormal basis](@entry_id:147779) for the space spanned by the columns of $A^k$. This is precisely the procedure of simultaneous iteration starting with the [standard basis vectors](@entry_id:152417) (the columns of the identity matrix). The behavior of simultaneous iteration is well understood. If we repeatedly apply $A$ to a set of vectors, the components corresponding to eigenvalues of larger modulus are amplified more rapidly. Specifically, if the eigenvalues of $A$ have strictly separated moduli, $| \lambda_1 | > | \lambda_2 | > \dots > | \lambda_n | > 0$, then the subspace spanned by the first $j$ columns of $\widehat{Q}_k$ will converge to the dominant [invariant subspace](@entry_id:137024) spanned by the first $j$ eigenvectors of $A$.

Because $\widehat{Q}_k$ converges to a matrix that orders the [invariant subspaces](@entry_id:152829) of $A$ by the magnitude of their associated eigenvalues, the matrix $A_k = \widehat{Q}_k^\ast A \widehat{Q}_k$ is driven toward an upper triangular (Schur) form whose diagonal entries are the eigenvalues sorted in decreasing order of modulus . This provides the profound "why" behind the algorithm's observed behavior.

### Quantitative Analysis of Convergence

With the mechanism understood, we can quantify the speed of convergence and analyze the important special case of [symmetric matrices](@entry_id:156259).

#### Rate of Convergence

The connection to [power iteration](@entry_id:141327) allows for a precise characterization of the algorithm's convergence rate. For an unreduced upper Hessenberg matrix, the decay of the subdiagonal entries can be analyzed directly. Let $b_{i+1,i}^{(k)}$ be the $(i+1,i)$-th entry of $A_k$. From the relations $A_k = Q_k R_k$ and $A_{k+1} = R_k Q_k$, one can derive the recurrence:

$b_{i+1,i}^{(k+1)} = b_{i+1,i}^{(k)} \frac{(R_k)_{i+1,i+1}}{(R_k)_{i,i}}$

As $k \to \infty$, the matrix $A_k$ converges to the upper triangular Schur form $T$. Consequently, its QR factors also converge: $Q_k \to I$ (up to signs) and $R_k \to T$. The diagonal entries of $R_k$ thus converge to the eigenvalues of $A$: $|(R_k)_{j,j}| \to |\lambda_j|$. Taking the limit of the recurrence ratio gives the asymptotic [linear convergence](@entry_id:163614) factor :

$\lim_{k \to \infty} \frac{|b_{i+1,i}^{(k+1)}|}{|b_{i+1,i}^{(k)}|} = \frac{|\lambda_{i+1}|}{|\lambda_i|}$

This crucial result shows that the subdiagonal entry $b_{i+1,i}^{(k)}$ converges to zero geometrically with a rate determined by the ratio of the moduli of the adjacent eigenvalues in the sorted list. Convergence is rapid when eigenvalues are well-separated in modulus, but it can be extremely slow if $|\lambda_{i+1}| \approx |\lambda_i|$.

#### Convergence for Symmetric Matrices

A particularly important and well-behaved case is when the initial matrix $A$ is real and symmetric. By the Spectral Theorem, a [symmetric matrix](@entry_id:143130) is always orthogonally diagonalizable. Its real Schur form is a [diagonal matrix](@entry_id:637782) $\Lambda$ containing the real eigenvalues.

Therefore, for a [symmetric matrix](@entry_id:143130) with distinct eigenvalues, the un-shifted QR algorithm generates a sequence $A_k$ that converges to a [diagonal matrix](@entry_id:637782). Furthermore, the accumulated [orthogonal matrix](@entry_id:137889) $\widehat{Q}_k = Q_0 Q_1 \cdots Q_{k-1}$ converges to the [orthogonal matrix](@entry_id:137889) $Q$ whose columns are the orthonormal eigenvectors of $A$ . This makes the QR algorithm a powerful (though, in its un-shifted form, slow) method for computing the complete eigensystem of a [symmetric matrix](@entry_id:143130).

### Limitations and Pathologies of the Un-shifted Algorithm

The elegant convergence theory of the un-shifted QR algorithm rests on the critical assumption that eigenvalue moduli are strictly separated. When this condition is violated, or when the matrix is pathologically non-normal, the algorithm's performance degrades or it may fail to converge to the desired form. These limitations are the primary motivation for developing the more robust shifted QR algorithms used in practice.

#### The Problem of Equal Moduli

The convergence rate $|\lambda_{i+1}/\lambda_i|$ indicates that if $|\lambda_i| = |\lambda_{i+1}|$, the convergence factor is $1$, and the corresponding subdiagonal entry $b_{i+1,i}^{(k)}$ will not decay to zero. This occurs, for example, with a real matrix having a [complex conjugate pair](@entry_id:150139) of eigenvalues $\lambda, \bar{\lambda}$ (since $|\lambda|=|\bar{\lambda}|$) or real eigenvalues of opposite sign but equal magnitude, such as $\lambda$ and $-\lambda$.

In such cases, the QR iteration fails to isolate the individual eigenvalues. Instead, it converges to a block upper triangular form where a $2 \times 2$ diagonal block corresponds to the eigenvalues with equal moduli. For instance, if a $4 \times 4$ matrix has eigenvalues $\{2, -2, 0.5, 0.25\}$, the moduli are $\{2, 2, 0.5, 0.25\}$. Since $|\lambda_1|=|\lambda_2|$, the subdiagonal entry $b_{2,1}^{(k)}$ will not converge to zero. However, since $|\lambda_2| > |\lambda_3|$, the entry $b_{3,2}^{(k)}$ will decay, [decoupling](@entry_id:160890) the matrix into a $2 \times 2$ block and a lower $2 \times 2$ block. The algorithm effectively stalls, unable to triangularize the leading $2 \times 2$ block corresponding to the eigenvalues $\{2, -2\}$ .

#### The Challenge of Non-Normal Matrices

A matrix $A$ is **non-normal** if it does not commute with its [conjugate transpose](@entry_id:147909) ($AA^\ast \neq A^\ast A$). Such matrices can have highly non-[orthogonal eigenvectors](@entry_id:155522). While the un-shifted QR algorithm will still asymptotically converge to a Schur form (given eigenvalue modulus separation), the path to convergence can be deceptive.

For highly [non-normal matrices](@entry_id:137153), the off-diagonal entries of the iterates $A_k$ can exhibit **transient growth**, increasing for a number of iterations before the eventual asymptotic decay takes over. This behavior is rooted in the same properties that cause powers of a [non-normal matrix](@entry_id:175080), $\|A^k\|$, to grow temporarily even if its [spectral radius](@entry_id:138984) is less than 1. Since the QR algorithm is equivalent to orthogonalizing the columns of $A^k$, this transient amplification in the [power method](@entry_id:148021) translates directly into the behavior of the QR iterates . This phenomenon is not an artifact of [finite-precision arithmetic](@entry_id:637673); it is an intrinsic property of the matrix and the algorithm. Importantly, the degree of [non-normality](@entry_id:752585) is preserved by the initial reduction of a matrix to Hessenberg form, meaning that this transient behavior persists in practical implementations .

### A Deeper Connection: The QR Algorithm and Krylov Subspaces

For general matrices, the QR algorithm is almost always applied to a matrix that has first been reduced to upper Hessenberg form by an orthogonal similarity. This initial reduction does not change the eigenvalues and greatly reduces the cost of each QR step. On Hessenberg matrices, the QR algorithm exhibits an even deeper connection to another major class of methods in [numerical linear algebra](@entry_id:144418): Krylov subspace methods.

For an upper Hessenberg matrix $A$ and the starting vector $v = e_1 = [1, 0, \dots, 0]^\top$, the subspace spanned by the first $m$ columns of the matrix $\widehat{Q}_k$ from the QR algorithm is identical to the $m$-th Krylov subspace $\mathcal{K}_m(A, e_1) = \operatorname{span}\{e_1, Ae_1, \dots, A^{m-1}e_1\}$. This surprising equivalence is a consequence of the so-called **Implicit Q Theorem**. It implies that the nested subspaces generated by the QR iteration are precisely the Krylov subspaces generated by $A$ and $e_1$ . This relationship is fundamental to the design and analysis of modern implicit QR algorithms, which perform the iteration without ever explicitly forming the $Q_k$ and $R_k$ matrices.