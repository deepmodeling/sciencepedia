## Introduction
Eigenvalue problems are fundamental to modern science and engineering, modeling everything from the vibrational modes of a bridge to the energy levels of a quantum system. For large-scale problems, direct computation is infeasible, necessitating the use of [iterative algorithms](@entry_id:160288). The practical efficiency of these methods hinges on a powerful concept: **deflation**. This is the process of systematically removing known parts of a solution from a problem, thereby reducing its complexity and size, and allowing computational resources to be focused on what remains unknown. This article addresses the critical role of deflation, a technique that transforms intractable computations into manageable ones.

This article provides a comprehensive exploration of deflation, structured to build a deep understanding from first principles to practical application.
- The first section, **Principles and Mechanisms**, will uncover the mathematical foundation of deflation rooted in [invariant subspaces](@entry_id:152829) and the Schur decomposition. It will also explore the justifications for its use in [finite-precision arithmetic](@entry_id:637673) and detail its implementation in core eigenvalue algorithms.
- The second section, **Applications and Interdisciplinary Connections**, will showcase the far-reaching impact of deflation, demonstrating its use in accelerating core numerical methods and enabling discoveries in fields like data science, [computational physics](@entry_id:146048), and engineering.
- Finally, **Hands-On Practices** will offer a set of targeted problems designed to solidify the theoretical concepts through practical implementation and analysis.

By journeying through these sections, you will gain a thorough understanding of how deflation works, why it is stable, and where it is applied, revealing it as an indispensable tool in the computational scientist's arsenal.

## Principles and Mechanisms

The computation of [eigenvalues and eigenvectors](@entry_id:138808) is a cornerstone of numerical linear algebra. For matrices of even moderate size, direct methods based on the [characteristic polynomial](@entry_id:150909) are numerically unstable and computationally infeasible. Instead, practical algorithms are iterative, progressively refining approximations to eigenpairs. A crucial concept that underpins the efficiency and success of these [iterative methods](@entry_id:139472) is **deflation**. In essence, deflation is a collection of techniques for simplifying an eigenvalue problem once a portion of its solution—such as one or more eigenpairs, or more generally, an [invariant subspace](@entry_id:137024)—has been found. This chapter elucidates the fundamental principles of deflation and explores its mechanical implementation in several of the most important eigenvalue algorithms.

### The Fundamental Principle: Invariant Subspaces and Decoupling

The core principle of deflation is the algebraic [decoupling](@entry_id:160890) of a problem into smaller, independent subproblems. This decoupling is made possible by the identification of an **[invariant subspace](@entry_id:137024)**. A subspace $\mathcal{U} \subset \mathbb{C}^{n}$ is said to be an **[invariant subspace](@entry_id:137024)** of a matrix $A \in \mathbb{C}^{n \times n}$ if for every vector $u \in \mathcal{U}$, the vector $Au$ is also in $\mathcal{U}$; that is, $A\mathcal{U} \subseteq \mathcal{U}$.

Suppose we have identified a $k$-dimensional $A$-[invariant subspace](@entry_id:137024) $\mathcal{U}$. We can construct a unitary matrix $Q \in \mathbb{C}^{n \times n}$ whose first $k$ columns, which we denote as a block $Q_1$, form an orthonormal basis for $\mathcal{U}$. The remaining $n-k$ columns, denoted $Q_2$, form an [orthonormal basis](@entry_id:147779) for the orthogonal complement $\mathcal{U}^{\perp}$. We can write $Q = [Q_1, Q_2]$. Performing a unitary similarity transformation on $A$ using this basis reveals a special structure:

$$
Q^{*} A Q = \begin{pmatrix} Q_1^{*} A Q_1 & Q_1^{*} A Q_2 \\ Q_2^{*} A Q_1 & Q_2^{*} A Q_2 \end{pmatrix}
$$

Because the [column space](@entry_id:150809) of $Q_1$ is $\mathcal{U}$ and $\mathcal{U}$ is $A$-invariant, $A Q_1$ can be written as a [linear combination](@entry_id:155091) of the columns of $Q_1$. This means there exists a matrix $B \in \mathbb{C}^{k \times k}$ such that $A Q_1 = Q_1 B$. The lower-left block of the transformed matrix then becomes:

$$
Q_2^{*} A Q_1 = Q_2^{*} (Q_1 B) = (Q_2^{*} Q_1) B = 0 \cdot B = 0
$$

The [zero matrix](@entry_id:155836) appears because the columns of $Q_2$ are orthogonal to the columns of $Q_1$. Consequently, the transformed matrix is block upper triangular:

$$
Q^{*} A Q = \begin{pmatrix} B & C \\ 0 & D \end{pmatrix}
$$

where $B = Q_1^{*} A Q_1$, $C = Q_1^{*} A Q_2$, and $D = Q_2^{*} A Q_2$. Since a similarity transformation preserves eigenvalues, the spectrum of $A$, denoted $\sigma(A)$, is the same as the spectrum of $Q^{*}AQ$. The eigenvalues of a block triangular matrix are the union of the eigenvalues of its diagonal blocks. Therefore, $\sigma(A) = \sigma(B) \cup \sigma(D)$. The $k$ eigenvalues of $B$ are the eigenvalues of $A$ associated with the invariant subspace $\mathcal{U}$. The remaining $n-k$ eigenvalues of $A$ are precisely the eigenvalues of the smaller $(n-k) \times (n-k)$ matrix $D$. The problem has been **deflated**: once the eigenproblem for $B$ is considered solved, we only need to solve the smaller eigenproblem for $D$ . The simplest case is when we find a single eigenvector $v$ corresponding to an eigenvalue $\lambda$. Here, $\mathcal{U} = \mathrm{span}\{v\}$ is a one-dimensional [invariant subspace](@entry_id:137024), and the deflation procedure yields a $1 \times 1$ block $[\lambda]$ and an $(n-1) \times (n-1)$ deflated problem .

This process of progressive deflation is deeply connected to the **Schur Decomposition**. The Schur theorem states that any square matrix $A \in \mathbb{C}^{n \times n}$ can be factorized as $A = QUQ^{*}$, where $Q$ is a [unitary matrix](@entry_id:138978) and $U$ is an [upper triangular matrix](@entry_id:173038). The columns of $Q$, called **Schur vectors**, form an orthonormal basis, and the diagonal entries of $U$ are the eigenvalues of $A$. The equation $AQ = QU$ reveals that for any $j \in \{1, \dots, n\}$, the subspace spanned by the first $j$ Schur vectors, $\mathrm{span}\{q_1, \dots, q_j\}$, is an [invariant subspace](@entry_id:137024) of $A$. Eigenvalue algorithms that use deflation can be viewed as methods that constructively build the Schur decomposition. At each step, the algorithm finds an approximate eigenvector or a low-dimensional invariant subspace, "locks" its [orthonormal basis](@entry_id:147779) vectors (which become the next columns of $Q$), and continues the search in the [orthogonal complement](@entry_id:151540). This corresponds to revealing the matrix $U$ block by block . For general non-Hermitian matrices, whose eigenvectors may be non-orthogonal and lead to [numerical instability](@entry_id:137058), this focus on finding [orthonormal bases](@entry_id:753010) for [invariant subspaces](@entry_id:152829) (i.e., Schur vectors) is essential for robust computation .

### Justifications for Deflation in Finite Precision

The principle of deflation relies on having an exact [invariant subspace](@entry_id:137024). In practice, [iterative algorithms](@entry_id:160288) produce approximations, known as **Ritz vectors**, which lie in some search subspace (e.g., a Krylov subspace). We must therefore ask: when is an approximate invariant subspace "good enough" to be deflated? The answer comes from two perspectives: [perturbation theory](@entry_id:138766) and [backward error analysis](@entry_id:136880).

#### A Perturbation Theory Perspective: Residuals and Spectral Gaps

Let $(\theta, v)$ be an approximate eigenpair, called a **Ritz pair**, where $v$ is a [unit vector](@entry_id:150575). The quality of this approximation is typically measured by the norm of the **residual** vector, $r = Av - \theta v$. A small residual suggests that $(\theta, v)$ is close to a true eigenpair $(\lambda, u)$. The celebrated Davis-Kahan theorem and its variants provide a quantitative link. For a [symmetric matrix](@entry_id:143130) $A$, the angle between the Ritz vector $v$ and the true invariant subspace $\mathcal{U}$ associated with a set of "wanted" eigenvalues is bounded by the [residual norm](@entry_id:136782), provided there is a sufficient gap between the Ritz value $\theta$ and the "unwanted" eigenvalues.

More precisely, let $\Lambda_{\mathrm{wanted}}$ be a set of target eigenvalues and $\mathcal{U}$ be the [invariant subspace](@entry_id:137024) they span. Let $\Lambda_{\mathrm{unwanted}}$ be the set of all other eigenvalues. The [spectral gap](@entry_id:144877) is defined as $\mathrm{gap}(\theta, \Lambda_{\mathrm{unwanted}}) = \min_{\lambda \in \Lambda_{\mathrm{unwanted}}} |\lambda - \theta|$. One can derive a bound of the form:

$$
\sin(\angle(v, \mathcal{U})) \le \frac{\|r\|_2}{\mathrm{gap}(\theta, \Lambda_{\mathrm{unwanted}})}
$$

Here, $\angle(v, \mathcal{U})$ is the principal angle between the vector $v$ and the subspace $\mathcal{U}$ . This inequality is profound: it guarantees that if the [residual norm](@entry_id:136782) $\|r\|_2$ is small relative to the [spectral gap](@entry_id:144877), the Ritz vector $v$ is closely aligned with the true [invariant subspace](@entry_id:137024). This provides a rigorous justification for using the residual as a deflation criterion. An algorithm can declare a Ritz vector "converged" and proceed with deflation when its [residual norm](@entry_id:136782) drops below a certain tolerance, giving confidence that the locked-in direction is not spurious. For a desired angular accuracy $\alpha$, we can deflate when $\|r\|_2 \le \sin(\alpha) \cdot \mathrm{gap}(\theta, \Lambda_{\mathrm{unwanted}})$ .

#### A Backward Error Perspective

An alternative justification regards deflation as a form of controlled [numerical error](@entry_id:147272). Many algorithms, such as the QR algorithm, iteratively transform a matrix $H$ into a form where an off-diagonal entry becomes negligibly small. For instance, in an upper Hessenberg matrix, a subdiagonal entry $h_{i+1,i}$ may approach zero. The act of deflation consists of setting this small entry to zero, $h_{i+1,i} := 0$.

This modification can be interpreted as introducing a perturbation $\Delta H$ to the matrix, where $\Delta H$ has only one non-zero entry, $(\Delta H)_{i+1,i} = -h_{i+1,i}$. The Frobenius norm of this perturbation is simply $\|\Delta H\|_F = |h_{i+1,i}|$. The core idea of **[backward stability](@entry_id:140758)** is to ensure that any error introduced by the algorithm is no larger than the inherent uncertainty from representing the initial problem in finite precision. If the perturbation $\Delta H$ is small enough, the eigenvalues of the modified (split) matrix are the exact eigenvalues of a matrix $H+\Delta H$ that is very close to the original $H$.

A common deflation criterion is to commit to deflation if the size of the necessary perturbation is on the order of the machine's [unit roundoff](@entry_id:756332) $u$. A simple criterion is to require $\|\Delta H\|_F \le u \|H\|_F$, which translates to deflating if $|h_{i+1,i}| \le u \|H\|_F$ . This ensures that the act of splitting the matrix introduces a backward error that is comparable in magnitude to the roundoff errors made in a single step of the algorithm.

### Mechanisms of Deflation in Key Algorithms

While the principle of decoupling is universal, its implementation varies significantly across different classes of eigenvalue algorithms.

#### The QR Algorithm

The QR algorithm is the workhorse for dense [eigenvalue problems](@entry_id:142153). It is typically preceded by a reduction to upper Hessenberg form (or tridiagonal form for symmetric matrices), which is preserved by the QR iterations. A step of the shifted QR algorithm is given by $H - \mu I = QR$ followed by $H_{\text{new}} = RQ + \mu I = Q^{*}HQ$.

The choice of the shift $\mu$ is the engine of convergence. When $\mu$ is chosen to be a good approximation of an eigenvalue of $H$, the matrix $H - \mu I$ becomes nearly singular. The QR factorization inherits this property, causing an entry on the diagonal of $R$ (typically the last one, $r_{nn}$) to become very small. This small value, in turn, causes a subdiagonal entry in the subsequent iterate $H_{\text{new}}$ (typically $h_{n,n-1}$) to become very small. The "bulge-chasing" procedure in the implicit QR algorithm is a computationally efficient way to perform this similarity transformation, effectively propagating the information from the shift down the diagonal to attenuate a subdiagonal entry .

Once a subdiagonal entry $h_{i+1,i}$ becomes sufficiently small, deflation is triggered. While the global criterion $|h_{i+1,i}| \le u \|H\|_F$ is valid, a more robust and widely used local criterion is:

$$
|h_{i+1,i}| \le c \cdot u \cdot (|h_{i,i}| + |h_{i+1,i+1}|)
$$

where $c$ is a small constant. This criterion compares the coupling term $h_{i+1,i}$ to a local scale defined by its neighboring diagonal elements. If the criterion is met, $h_{i+1,i}$ is set to zero. This splits the Hessenberg matrix into two smaller, independent Hessenberg subproblems, and the algorithm proceeds on each block separately  .

#### Krylov Subspace Methods

For large, sparse matrices, methods that transform the matrix directly are not feasible. Instead, Krylov subspace methods like the Arnoldi (for non-Hermitian) or Lanczos (for symmetric) algorithms project the large matrix onto a small Krylov subspace $\mathcal{K}_m(A, v_1) = \mathrm{span}\{v_1, Av_1, \dots, A^{m-1}v_1\}$, and solve the smaller projected eigenproblem.

When a Ritz pair $(\theta, x)$ from the subspace is deemed converged (i.e., its residual $\|Ax - \theta x\|$ is small), it is **locked**. Locking involves explicitly storing the converged Ritz vector(s) in an [orthonormal set](@entry_id:271094) $Q$ and ensuring that all subsequent search vectors for the Krylov subspace are orthogonal to $\mathrm{span}(Q)$. This prevents the algorithm from rediscovering the same eigenpairs and focuses its computational effort on the yet-unconverged part of the spectrum.

Mathematically, if we have locked $k$ vectors in $Q$ that span an approximate [invariant subspace](@entry_id:137024) such that $AQ \approx Q\Theta$, and we continue the Arnoldi iteration in the orthogonal complement, building a basis $V_m$, the combined process is described by an augmented Arnoldi relation:

$$
A[Q, V_m] = [Q, V_{m+1}] \begin{pmatrix} \Theta & Q^{*}AV_m \\ 0 & \bar{H}_m \end{pmatrix}
$$

Here, $\bar{H}_m$ is the $(m+1) \times m$ Hessenberg matrix from the new Arnoldi run. The zero in the lower-left block explicitly shows the deflation: the dynamics of the new search vectors in $V_m$ are governed by $\bar{H}_m$ and are decoupled from the locked subspace $\mathrm{span}(Q)$ .

#### Symmetric Tridiagonal Divide-and-Conquer

The [divide-and-conquer algorithm](@entry_id:748615) is a remarkably fast method for the symmetric tridiagonal eigenproblem. It operates by splitting the matrix $T$ into two smaller tridiagonal subproblems, solving them recursively, and then merging the results. The merge step relies on the insight that the original matrix can be expressed as a [block-diagonal matrix](@entry_id:145530) (formed from the subproblems) plus a simple [rank-one update](@entry_id:137543): $T = \mathrm{diag}(T_1, T_2) + \rho u u^{\top}$.

After a change of basis using the eigenvectors of the subproblems, the problem becomes finding the eigenvalues of $D + \rho z z^{\top}$, where $D$ is diagonal (containing the eigenvalues of the subproblems) and $z$ is a vector derived from the rank-one term. The eigenvalues $\lambda$ of this matrix are the roots of the **[secular equation](@entry_id:265849)**:

$$
f(\lambda) = 1 + \rho \sum_{i=1}^{n} \frac{z_i^2}{d_i - \lambda} = 0
$$

Deflation is a critical component of this algorithm's efficiency. If a component $z_k$ of the coupling vector is zero or numerically negligible, the $k$-th term vanishes from the [secular equation](@entry_id:265849). This directly implies that $\lambda = d_k$ is an eigenvalue of the merged matrix, and its corresponding eigenvector can be easily constructed. This eigenpair can be deflated from the problem, and the algorithm proceeds to find the roots of a smaller [secular equation](@entry_id:265849) . This happens, for example, when an eigenvector of one of the sub-problems happens to have a zero entry at the split point . A safe numerical deflation test will accept $d_k$ as an eigenvalue if $|z_k|$ is below a tolerance relative to $\|z\|_2$, provided $d_k$ is well-separated from other diagonal entries .

### Distinctions and Advanced Topics

It is important to distinguish deflation from two other common techniques used in iterative eigenvalue solvers: spectral shifting and restarting .
- **Spectral Shifting** transforms the operator to $A_s = A - \mu I$. This shifts the eigenvalues by $-\mu$ but preserves the eigenvectors. It is used to accelerate convergence towards eigenvalues near the shift $\mu$, but it does not reduce the problem size.
- **Restarting**, used in Krylov methods, is a procedure to manage memory by truncating the basis of the search subspace and starting a new one with a more promising initial vector. It does not alter the underlying matrix $A$ or its spectrum.
- **Deflation**, in contrast, explicitly removes known eigen-components from the problem, thereby reducing its [effective dimension](@entry_id:146824).

Deflation is a powerful but delicate tool. In cases of tightly **[clustered eigenvalues](@entry_id:747399)**, the choice of basis for the approximate invariant subspace becomes critical. Locking vectors one-by-one can be less stable than locking an entire block of vectors that span the clustered subspace simultaneously, as sequential deflation can amplify errors . For **[defective eigenvalues](@entry_id:177573)**, where [geometric multiplicity](@entry_id:155584) is less than algebraic multiplicity, the [invariant subspace](@entry_id:137024) contains [generalized eigenvectors](@entry_id:152349). Finding a stable basis for such a subspace is a significant challenge. Specialized methods, such as solving a homogeneous **Sylvester equation** of the form $AX - XJ = 0$ (where $J$ is a Jordan block), can be used to compute such a basis. However, these methods are highly sensitive to perturbations of $A$ that may break the defective structure and split the eigenvalue, making the Sylvester equation non-singular and its solution non-trivial to obtain numerically . These advanced cases highlight that while the principle of deflation is simple, its robust and stable implementation is a sophisticated art at the heart of modern [numerical linear algebra](@entry_id:144418).