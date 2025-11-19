## Introduction
Eigenvalue problems are foundational to [computational engineering](@entry_id:178146), providing critical insights into system behaviors like vibrational frequencies, structural stability, and data variance. However, standard [iterative solvers](@entry_id:136910) such as the power method are designed to find only a single eigenpair—typically the one with the largest magnitude eigenvalue. This raises a fundamental question: how do we efficiently compute multiple, or even all, eigenpairs of a system? Simply re-running the algorithm is futile, as it will converge to the same solution repeatedly. The answer lies in a powerful class of methods known as **[deflation techniques](@entry_id:169164)**.

This article provides a comprehensive exploration of deflation, the systematic process of modifying a matrix to remove a known eigenpair, thereby allowing an iterative method to discover the next one. We will navigate the theoretical underpinnings, practical challenges, and broad applications of these essential numerical tools.

The first chapter, **Principles and Mechanisms**, lays the groundwork by introducing core deflation algorithms for both symmetric and [non-symmetric matrices](@entry_id:153254), including Hotelling's method. It confronts the significant [numerical stability](@entry_id:146550) issues that arise with multiple and [clustered eigenvalues](@entry_id:747399) and presents the Schur decomposition as a unifying theoretical framework. Following this, **Applications and Interdisciplinary Connections** demonstrates the indispensable role of deflation in deciphering complex phenomena across science and engineering, from identifying degenerate energy states in quantum mechanics to extracting features in machine learning. Finally, **Hands-On Practices** will challenge you to apply these concepts to understand their limitations and nuances, such as their failure on [defective matrices](@entry_id:194492) and the superior stability of certain methods.

Let's begin our journey by examining the fundamental principles and mechanisms that make deflation possible.

## Principles and Mechanisms

Iterative methods for solving eigenvalue problems, such as the [power iteration](@entry_id:141327) or the QR algorithm, typically converge to one eigenpair or a single invariant subspace at a time. To compute multiple distinct eigenpairs, a mechanism is needed to prevent the algorithm from repeatedly converging to the same solution. This mechanism is known as **deflation**. In essence, deflation modifies the matrix after an eigenpair has been found, effectively removing it from the spectrum so that the [iterative method](@entry_id:147741) can converge to another. This chapter explores the fundamental principles of various [deflation techniques](@entry_id:169164), their mechanisms of action, and the significant [numerical stability](@entry_id:146550) challenges they present, especially in the context of multiple, clustered, or [defective eigenvalues](@entry_id:177573).

### Deflation for Symmetric Matrices: Hotelling's Method

The conceptually simplest and most foundational deflation technique applies to real symmetric matrices. For a symmetric matrix $A \in \mathbb{R}^{n \times n}$, the [spectral theorem](@entry_id:136620) guarantees a full set of real eigenvalues and a corresponding basis of orthonormal eigenvectors. Suppose we have computed the dominant eigenpair $(\lambda_1, v_1)$, where $v_1$ is a unit vector. The goal is to construct a new matrix, $A_2$, whose eigenvalues are $\{0, \lambda_2, \lambda_3, \dots, \lambda_n\}$.

This can be accomplished using **Hotelling's deflation** (also known as Wielandt-Hotelling deflation). The deflated matrix $A_2$ is constructed from the original matrix $A_1 = A$ via a [rank-one update](@entry_id:137543):

$$A_2 = A_1 - \lambda_1 v_1 v_1^{\top}$$

where $v_1 v_1^{\top}$ is the [outer product](@entry_id:201262) of the eigenvector with itself. This method is elegant because it preserves the symmetry of the matrix, as both $A_1$ and the [rank-one update](@entry_id:137543) matrix $v_1 v_1^{\top}$ are symmetric.

The mechanism of this deflation is straightforward to verify. First, consider the action of $A_2$ on the known eigenvector $v_1$:
$$A_2 v_1 = (A_1 - \lambda_1 v_1 v_1^{\top}) v_1 = A_1 v_1 - \lambda_1 v_1 (v_1^{\top} v_1)$$
Since $v_1$ is a [unit vector](@entry_id:150575), $v_1^{\top} v_1 = 1$. The equation simplifies to:
$$A_2 v_1 = \lambda_1 v_1 - \lambda_1 v_1 = 0$$
Thus, $v_1$ is an eigenvector of the deflated matrix $A_2$ with its eigenvalue transformed to $0$.

Now, consider any other eigenvector $v_j$ of $A_1$ (with $j \neq 1$). Because eigenvectors of a symmetric matrix are orthogonal, we have $v_1^{\top} v_j = 0$. The action of $A_2$ on $v_j$ is:
$$A_2 v_j = (A_1 - \lambda_1 v_1 v_1^{\top}) v_j = A_1 v_j - \lambda_1 v_1 (v_1^{\top} v_j) = \lambda_j v_j - \lambda_1 v_1 (0) = \lambda_j v_j$$
This shows that all other eigenpairs $(\lambda_j, v_j)$ of the original matrix remain eigenpairs of the deflated matrix $A_2$. An iterative method like [power iteration](@entry_id:141327), when applied to $A_2$, will now converge to the next dominant eigenpair, $(\lambda_2, v_2)$. This process can be repeated to find a sequence of eigenpairs [@problem_id:2383493].

In practice, [floating-point arithmetic](@entry_id:146236) introduces small errors. After several deflation steps, the accumulated errors can cause the nominally [symmetric matrix](@entry_id:143130) to lose its symmetry. A common and effective remedy is to explicitly re-symmetrize the matrix after each deflation:
$$A_{k+1}^{\text{sym}} = \frac{A_{k+1} + A_{k+1}^{\top}}{2}$$
This simple step helps to mitigate the propagation of numerical errors and maintain the stability of the overall process [@problem_id:2383493].

### Numerical Challenges with Multiple and Clustered Eigenvalues

The elegant simplicity of Hotelling's deflation is challenged when a matrix has multiple (degenerate) or tightly [clustered eigenvalues](@entry_id:747399). In these scenarios, the numerical stability of sequential deflation becomes a primary concern.

#### Loss of Orthogonality

In exact arithmetic, the eigenvectors computed sequentially through deflation would be perfectly orthogonal. However, in [finite-precision arithmetic](@entry_id:637673), each computed eigenvector $\hat{v}_k$ contains small errors. When the matrix is deflated using this imperfect vector, the errors are propagated into the next stage of the computation. This leads to a progressive **[loss of orthogonality](@entry_id:751493)**: the newly computed vector $\hat{v}_{k+1}$ will not be perfectly orthogonal to the previously computed vectors $\hat{v}_1, \dots, \hat{v}_k$.

This degradation of orthogonality is particularly severe when eigenvalues are clustered or identical. In such cases, the corresponding eigenvectors are not uniquely defined; any vector in the [invariant subspace](@entry_id:137024) is a valid eigenvector. Small numerical perturbations can cause the [iterative eigensolver](@entry_id:750888) to return a vector that has a small, non-zero component in the direction of previously found vectors. This error accumulates with each deflation step. Consequently, the order in which eigenvectors from a single invariant subspace are found can affect the final numerical accuracy of the computed basis [@problem_id:2383490].

A numerical experiment can vividly demonstrate this phenomenon. By applying ten successive deflation steps to matrices with different spectral properties, we can track the orthogonality error $E_k = \| V_k^{\top} V_k - I_k \|_F$, where $V_k = [\hat{v}_1, \dots, \hat{v}_k]$. For a matrix with well-separated eigenvalues, this error remains small, on the order of machine precision. For a matrix with [clustered eigenvalues](@entry_id:747399), the error grows noticeably. For a matrix with exact multiple eigenvalues, the error grows rapidly, indicating a significant [loss of orthogonality](@entry_id:751493) among the computed vectors [@problem_id:2383491]. This implies that a simple sequential deflation may yield a basis for the [invariant subspace](@entry_id:137024) that is far from orthonormal, posing problems for subsequent analyses.

#### Sensitivity to Perturbations

The stability of deflation is also sensitive to the nature of the errors in the computed eigenvectors. Consider an eigenvalue $\lambda_{\star}$ with [multiplicity](@entry_id:136466) greater than one, and let its corresponding [invariant subspace](@entry_id:137024) be $\mathcal{S}$. Suppose we have computed an approximate eigenvector $\hat{v}$ to be used for deflation.

A crucial insight is that the effect of the error in $\hat{v}$ depends on whether the error component lies inside or outside the invariant subspace $\mathcal{S}$ [@problem_id:2383547].
- If the perturbation is **in-subspace**, meaning $\hat{v}$ is simply a different linear combination of the true basis vectors for $\mathcal{S}$, then $\hat{v}$ is still an exact eigenvector. Deflating with $\hat{v}$ is equivalent to choosing a different [orthonormal basis](@entry_id:147779) for $\mathcal{S}$. The remaining eigenvalues of the matrix are perfectly preserved (in exact arithmetic).
- If the perturbation is **out-of-subspace**, meaning $\hat{v}$ has components orthogonal to $\mathcal{S}$, then $\hat{v}$ is no longer an exact eigenvector. Deflating with such a vector introduces errors into the deflated matrix, which in turn perturbs the entire remaining spectrum. The magnitude of this spectral error grows with the magnitude of the out-of-subspace perturbation.

This distinction is fundamental to understanding the behavior of deflation algorithms for matrices with [repeated eigenvalues](@entry_id:154579).

#### Block Deflation

To address the stability issues associated with clustered or multiple eigenvalues, it is often more robust to use **[block deflation](@entry_id:178634)**. Instead of deflating one eigenvector at a time, this approach deflates the entire [invariant subspace](@entry_id:137024) associated with a cluster of eigenvalues at once.

Suppose we have computed a set of linearly independent vectors $V = [v_1, \dots, v_m]$ that form an approximate basis for an $m$-dimensional invariant subspace. Crucially, these vectors may not be orthogonal due to computational errors. A naive sequential deflation, $A - \lambda \sum_{i=1}^m v_i v_i^{\top}$, is incorrect because the term $\sum v_i v_i^{\top}$ is not a projector unless the vectors are orthonormal.

The correct approach is to construct the orthogonal projector onto the subspace spanned by the columns of $V$. This projector is given by:
$$P_V = V (V^{\top} V)^{-1} V^{\top}$$
This formula holds even if the columns of $V$ are not orthogonal (though they must be [linearly independent](@entry_id:148207) for $V^{\top} V$ to be invertible). The block-deflated matrix is then:
$$A_{\text{blk}} = A - \lambda P_V$$
This method correctly removes the contribution of the entire approximate subspace $\operatorname{span}(V)$, making it numerically superior to sequential rank-one deflation when the basis vectors are not perfectly orthogonal [@problem_id:2383512]. However, this method has its own pitfall: if the vectors in $V$ are nearly collinear, the Gram matrix $V^{\top} V$ becomes ill-conditioned, and its inversion can introduce large [numerical errors](@entry_id:635587).

### Deflation in Non-Symmetric Systems

Deflation for [non-symmetric matrices](@entry_id:153254) is more complex because the eigenvectors do not, in general, form an [orthogonal basis](@entry_id:264024). A non-symmetric matrix $A$ has a set of **right eigenvectors** ($Av_i = \lambda_i v_i$) and a set of **left eigenvectors** ($w_i^{\top}A = \lambda_i w_i^{\top}$). For distinct eigenvalues, these sets form a **biorthogonal system**, meaning $w_i^{\top} v_j = 0$ for $i \neq j$.

Applying the symmetric Hotelling's formula naively to a non-[symmetric matrix](@entry_id:143130) fails to preserve the rest of the spectrum. If we form $\widetilde{A} = A - \lambda_1 v_1 v_1^{\top}$, the action on another eigenvector $v_j$ is:
$$\widetilde{A} v_j = A v_j - \lambda_1 v_1 (v_1^{\top} v_j) = \lambda_j v_j - \lambda_1 (v_1^{\top} v_j) v_1$$
Since $v_1^{\top} v_j$ is generally not zero for a non-[symmetric matrix](@entry_id:143130), the second term does not vanish. The vector $v_j$ is perturbed in the direction of $v_1$, and $(\lambda_j, v_j)$ is no longer an eigenpair of $\widetilde{A}$ [@problem_id:2383516].

The correct rank-one deflation for [non-symmetric matrices](@entry_id:153254) must utilize both the [left and right eigenvectors](@entry_id:173562). The deflated matrix is given by:
$$\widetilde{A} = A - \frac{\lambda_1}{w_1^{\top} v_1} v_1 w_1^{\top}$$
The validity of this formula hinges on the [biorthogonality](@entry_id:746831) property. For any $j \neq 1$:
$$\widetilde{A} v_j = A v_j - \frac{\lambda_1}{w_1^{\top} v_1} v_1 (w_1^{\top} v_j) = \lambda_j v_j - \frac{\lambda_1}{w_1^{\top} v_1} v_1 (0) = \lambda_j v_j$$
The other eigenpairs are preserved. The stability of this procedure, however, depends critically on the scalar denominator $w_1^{\top} v_1$. If the [left and right eigenvectors](@entry_id:173562) $w_1$ and $v_1$ are nearly orthogonal, this value is close to zero, and the deflation update can become numerically unstable due to division by a small number. The quantity $s_1 = |w_1^{\top} v_1|$ (assuming normalized vectors) is a measure of the conditioning of the eigenvalue $\lambda_1$. A value of $s_1$ close to zero indicates an ill-conditioned eigenvalue and portends instability in the deflation process [@problem_id:2383540].

### A Unifying Perspective: The Schur Decomposition

The concept of deflation is deeply connected to a cornerstone of [matrix theory](@entry_id:184978): the **Schur decomposition**. The Schur decomposition states that for any square matrix $A \in \mathbb{C}^{n \times n}$, there exists a [unitary matrix](@entry_id:138978) $Q$ and an [upper triangular matrix](@entry_id:173038) $U$ such that $A = Q U Q^H$. The columns of $Q$ are known as Schur vectors, and they form an [orthonormal basis](@entry_id:147779).

This decomposition reveals that for any $j$, the subspace $\mathcal{S}_j = \operatorname{span}\{q_1, \dots, q_j\}$ is an **[invariant subspace](@entry_id:137024)** of $A$. That is, for any $v \in \mathcal{S}_j$, we have $Av \in \mathcal{S}_j$. Deflation can be viewed as a constructive, step-by-step procedure for building the Schur decomposition.

When an iterative algorithm finds an eigenvector (or more generally, an [invariant subspace](@entry_id:137024)), it has effectively found the first Schur vector $q_1$ (or the first few columns of $Q$). The deflation step, which transforms $A$ into a block upper triangular form $\begin{pmatrix} \lambda_1  \dots \\ 0  A' \end{pmatrix}$ via a unitary [similarity transformation](@entry_id:152935), is precisely the first step in constructing the Schur form. The algorithm then proceeds recursively on the smaller subproblem $A'$, which corresponds to the unreduced trailing block of the final upper triangular matrix $U$ [@problem_id:2383555].

This perspective is particularly powerful for non-Hermitian matrices. While eigenvectors may be non-orthogonal and ill-conditioned, the basis of Schur vectors is always orthonormal. Practical, numerically stable eigenvalue algorithms (like the QR algorithm) are designed to compute the Schur form. They implicitly "lock" Schur vectors rather than eigenvectors to maintain [orthonormality](@entry_id:267887) and stability throughout the computation. Thus, deflation is not merely an ad-hoc trick but a fundamental component of a process that incrementally reveals the Schur decomposition of a matrix [@problem_id:2383555].

### Advanced Topic: Deflation for Defective Matrices

The final layer of complexity arises with **[defective matrices](@entry_id:194492)**, which do not have a full basis of eigenvectors. Instead, their structure is described by Jordan blocks and chains of **[generalized eigenvectors](@entry_id:152349)**, which satisfy:
$$(A - \lambda I) v_1 = 0, \quad (A - \lambda I) v_2 = v_1, \quad \dots, \quad (A - \lambda I) v_k = v_{k-1}$$
Can deflation be used to find this chain of vectors?

Classical orthogonal deflation methods, such as $B = P A P$ where $P = I - v_1 v_1^{\top}$, are fundamentally unsuited for this task. Such a method is designed to find eigenvectors, which are defined by the relation $Av = \lambda v$. After finding the true eigenvector $v_1$, the algorithm would search for another vector $x$ such that the residual $\|Ax - \lambda x\|$ is small. However, the next vector in the chain, $v_2$, is not an eigenvector; its residual is $\|A v_2 - \lambda v_2\| = \|v_1\| = 1$. An algorithm based on finding vectors with small eigen-residuals will correctly reject $v_2$ and any subsequent [generalized eigenvectors](@entry_id:152349). Therefore, classical orthogonal deflation will find only the true eigenvectors (one for each Jordan block) and fail to uncover the rest of the chain [@problem_id:2383495].

To compute [generalized eigenvectors](@entry_id:152349), one must directly solve the defining system of linear equations. To find $v_2$, we must solve the [singular system](@entry_id:140614) $(A - \lambda I) x = v_1$. According to the Fredholm alternative, this system has a solution if and only if the right-hand side, $v_1$, is orthogonal to the [left null space](@entry_id:152242) of $(A - \lambda I)$. For a Jordan chain, this condition is satisfied.

However, the solution is not unique, as any multiple of $v_1$ can be added to a particular solution. To obtain a unique $v_2$, a side condition must be imposed. There are two common approaches:
1.  **Pseudoinverse Solution:** One can solve the system in a least-squares sense to find the unique minimal-norm solution. This is given by $v_2 = (A - \lambda I)^{+} v_1$, where $(\cdot)^{+}$ denotes the Moore-Penrose [pseudoinverse](@entry_id:140762). This process can be repeated to find the entire chain [@problem_id:2383495].
2.  **Bordered System:** A more general technique involves augmenting the [singular system](@entry_id:140614) with an additional constraint equation, forming a larger, non-[singular system](@entry_id:140614) known as a **[bordered system](@entry_id:177056)**. For example, by using the left [generalized eigenvector chain](@entry_id:192049), one can construct a constraint that uniquely specifies the solution. This represents a more advanced form of deflation or continuation specifically designed for navigating the structure of Jordan blocks [@problem_id:2383505].

In summary, finding [generalized eigenvectors](@entry_id:152349) requires moving beyond standard [deflation techniques](@entry_id:169164) and employing methods that directly address the structure of singular linear systems inherent in the definition of a Jordan chain.