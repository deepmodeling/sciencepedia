## Introduction
In the landscape of numerical linear algebra, the Eigenvalue Decomposition (EVD) and the Singular Value Decomposition (SVD) stand as twin pillars of [matrix factorization](@entry_id:139760). The EVD reveals the intrinsic dynamics of a linear transformation through its invariant directions, while the SVD provides a robust geometric breakdown of how a matrix maps vectors from one space to another. While both offer powerful insights, the precise nature of their relationship is nuanced and often misunderstood, particularly for the vast class of [non-normal matrices](@entry_id:137153) where their properties diverge significantly. This gap in understanding can lead to misinterpreted results and suboptimal algorithmic choices in scientific computing.

This article illuminates this crucial connection across three comprehensive chapters. The first chapter, **"Principles and Mechanisms,"** establishes the core algebraic link through Gram matrices, explores their parallel geometric interpretations, and defines the critical role of matrix normality in their alignment. The second chapter, **"Applications and Interdisciplinary Connections,"** demonstrates the practical consequences of their differences in fields from data science and control theory to network analysis, highlighting why the choice between an SVD or EVD-based approach is a critical design decision. Finally, **"Hands-On Practices"** offers a series of guided problems to solidify the theoretical concepts and build intuition for their application in challenging scenarios.

## Principles and Mechanisms

The Eigenvalue Decomposition (EVD) and the Singular Value Decomposition (SVD) are two of the most fundamental and powerful matrix factorizations in linear algebra. While the EVD reveals the intrinsic behavior of a [linear transformation](@entry_id:143080) in terms of its invariant directions, the SVD provides a more general and robust analysis of the transformation's geometric action on vector spaces. This chapter delves into the profound and multifaceted relationship between these two decompositions, exploring their algebraic connections, geometric interpretations, and the critical role of matrix normality in dictating their alignment or divergence.

### The Foundational Bridge: Gram Matrices and the SVD

The most direct algebraic connection between the EVD and the SVD is established through the **Gram matrices** associated with a matrix $A \in \mathbb{C}^{m \times n}$. These are the matrices $A^{\ast}A$ and $AA^{\ast}$. The matrix $A^{\ast}A \in \mathbb{C}^{n \times n}$ operates on the domain space of $A$, while $AA^{\ast} \in \mathbb{C}^{m \times m}$ operates on its [codomain](@entry_id:139336). Both matrices are inherently **Hermitian positive semidefinite**. A matrix $M$ is Hermitian if $M = M^{\ast}$, and it is positive semidefinite if $x^{\ast}Mx \ge 0$ for all vectors $x$. The [hermiticity](@entry_id:141899) is clear: $(A^{\ast}A)^{\ast} = A^{\ast}(A^{\ast})^{\ast} = A^{\ast}A$. The [positive semidefiniteness](@entry_id:147720) follows from $x^{\ast}(A^{\ast}A)x = (Ax)^{\ast}(Ax) = \|Ax\|_{2}^{2} \ge 0$.

Because $A^{\ast}A$ and $AA^{\ast}$ are Hermitian, they are [unitarily diagonalizable](@entry_id:195045) according to the Spectral Theorem. Their EVDs provide the bridge to the SVD of $A$. Let the SVD of $A$ be $A = U\Sigma V^{\ast}$, where $U \in \mathbb{C}^{m \times m}$ and $V \in \mathbb{C}^{n \times n}$ are unitary, and $\Sigma \in \mathbb{R}^{m \times n}$ is a rectangular diagonal matrix with non-negative real entries $\sigma_i$, the singular values.

Let us substitute this factorization into the Gram matrices:
$$A^{\ast}A = (U\Sigma V^{\ast})^{\ast}(U\Sigma V^{\ast}) = V\Sigma^{\ast}U^{\ast}U\Sigma V^{\ast}$$
Since $U$ is unitary, $U^{\ast}U=I_m$. The expression simplifies to:
$$A^{\ast}A = V(\Sigma^{\ast}\Sigma)V^{\ast}$$
Similarly, for the other Gram matrix:
$$AA^{\ast} = (U\Sigma V^{\ast})(U\Sigma V^{\ast})^{\ast} = U\Sigma V^{\ast}V\Sigma^{\ast}U^{\ast}$$
Since $V$ is unitary, $V^{\ast}V=I_n$. This simplifies to:
$$AA^{\ast} = U(\Sigma\Sigma^{\ast})U^{\ast}$$

These two equations are, in fact, the eigenvalue decompositions of $A^{\ast}A$ and $AA^{\ast}$. They reveal a profound set of relationships:

1.  The columns of $V$ (the **[right singular vectors](@entry_id:754365)** of $A$) are the orthonormal eigenvectors of $A^{\ast}A$.
2.  The columns of $U$ (the **[left singular vectors](@entry_id:751233)** of $A$) are the orthonormal eigenvectors of $AA^{\ast}$.
3.  The diagonal entries of both $\Sigma^{\ast}\Sigma$ (an $n \times n$ matrix) and $\Sigma\Sigma^{\ast}$ (an $m \times m$ matrix) are the squares of the singular values of $A$, $\sigma_i^2$. The non-zero eigenvalues of $A^{\ast}A$ and $AA^{\ast}$ are identical and equal to the squares of the non-zero singular values of $A$.

This demonstrates that the SVD of $A$ can be constructed from the EVDs of its associated Gram matrices. This principle is foundational to both the theory and computation of the SVD, and it forms the basis of applications such as Principal Component Analysis (PCA), which analyzes the EVD of the covariance matrix $X^{\ast}X$ to understand the structure of the data matrix $X$ .

### Variational Principles and Geometric Interpretations

The algebraic link via Gram matrices finds a parallel in [variational principles](@entry_id:198028), which characterize eigenvalues and singular values as solutions to [optimization problems](@entry_id:142739). This perspective offers a powerful geometric intuition for their distinct roles.

For a Hermitian matrix $H \in \mathbb{C}^{n \times n}$, its eigenvalues can be characterized by the **Rayleigh quotient**, $\mathcal{R}_H(x) = \frac{x^{\ast}Hx}{x^{\ast}x}$. The stationary points of $\mathcal{R}_H(x)$ on the unit sphere are precisely the eigenvectors of $H$, and the stationary values are the corresponding eigenvalues. In particular, the maximum and minimum values of the Rayleigh quotient are the largest and smallest eigenvalues of $H$. This frames eigenvalues as extremal values of the [quadratic form](@entry_id:153497) $x^{\ast}Hx$.

The singular values of a general matrix $A \in \mathbb{C}^{m \times n}$ have a different, but related, variational characterization. The largest singular value, $\sigma_{\max}$, which is also the spectral norm $\|A\|_2$, is the solution to the optimization problem:
$$\sigma_{\max}(A) = \max_{x \in \mathbb{C}^n, \|x\|_2=1} \|Ax\|_2$$
Squaring this expression, we get:
$$\sigma_{\max}(A)^2 = \max_{\|x\|_2=1} \|Ax\|_2^2 = \max_{\|x\|_2=1} (Ax)^{\ast}(Ax) = \max_{\|x\|_2=1} \frac{x^{\ast}A^{\ast}Ax}{x^{\ast}x}$$
This final expression is exactly the Rayleigh quotient for the Hermitian matrix $A^{\ast}A$. Therefore, the maximum value is the largest eigenvalue of $A^{\ast}A$, which we already know is $\sigma_{\max}^2$. The vector $x$ that achieves this maximum is the eigenvector of $A^{\ast}A$ corresponding to this largest eigenvalue, which is by definition the right [singular vector](@entry_id:180970) $v_1$ of $A$ .

This leads to a crucial geometric distinction between the two decompositions :

-   **Eigenvalue Decomposition (EVD):** For a square matrix $A$, the EVD identifies **invariant directions**. An eigenvector $v$ is a vector whose direction is unchanged by the transformation $A$; it is merely scaled by the eigenvalue $\lambda$ (i.e., $Av = \lambda v$).

-   **Singular Value Decomposition (SVD):** For any matrix $A$, the SVD identifies a pair of [orthonormal bases](@entry_id:753010), $\{v_i\}$ for the domain and $\{u_i\}$ for the codomain, such that $A$ maps each $v_i$ to a scaled version of its counterpart $u_i$ (i.e., $Av_i = \sigma_i u_i$). The [right singular vectors](@entry_id:754365) $\{v_i\}$ represent the principal axes of the ellipsoid formed by mapping the unit sphere in the domain. The singular values $\sigma_i$ are the lengths of the semiaxes of this image [ellipsoid](@entry_id:165811), and the [left singular vectors](@entry_id:751233) $\{u_i\}$ are the directions of these semiaxes. The SVD thus reveals the fundamental geometry of the linear map by finding input directions that are mapped to orthogonal output directions.

### Coincidence and Divergence: The Role of Normality

The relationship between the EVD and SVD hinges critically on whether a matrix is **normal**. A square matrix $A$ is defined as normal if it commutes with its conjugate transpose: $A^{\ast}A = AA^{\ast}$.

#### The Normal Case: An Elegant Alignment

The **Spectral Theorem** states that a matrix is normal if and only if it is [unitarily diagonalizable](@entry_id:195045), meaning it admits an EVD of the form $A = U\Lambda U^{\ast}$, where $U$ is unitary and $\Lambda$ is a diagonal matrix of eigenvalues $\lambda_i$.

For a [normal matrix](@entry_id:185943), the singular values are simply the absolute values of the eigenvalues: $\sigma_i = |\lambda_i|$. This can be seen by substituting the EVD into the expression for $A^{\ast}A$:
$$A^{\ast}A = (U\Lambda U^{\ast})^{\ast}(U\Lambda U^{\ast}) = U\Lambda^{\ast}U^{\ast}U\Lambda U^{\ast} = U\Lambda^{\ast}\Lambda U^{\ast} = U|\Lambda|^2 U^{\ast}$$
This is the EVD of $A^{\ast}A$. Its eigenvalues are $|\lambda_i|^2$, and thus the singular values of $A$ are $\sigma_i = \sqrt{|\lambda_i|^2} = |\lambda_i|$. In this case, the left and [right singular vectors](@entry_id:754365) are related to the eigenvectors through simple phase factors .

This alignment becomes even more direct for specific classes of [normal matrices](@entry_id:195370):

-   **Hermitian Matrices:** If $A$ is Hermitian ($A=A^{\ast}$), its eigenvalues $\lambda_i$ are real. The singular values are $\sigma_i = |\lambda_i|$. The SVD can be constructed directly from the EVD, $A = Q\Lambda Q^{\ast}$. To ensure the singular values are non-negative, we can write $\Lambda = R\Sigma$, where $\Sigma = |\Lambda|$ and $R$ is a diagonal matrix with entries $\operatorname{sgn}(\lambda_i)$. Then $A = Q(R\Sigma)Q^{\ast} = (QR)\Sigma Q^{\ast}$. This gives an SVD with $U=QR$ and $V=Q$. The matrix $R$ is a simple reflector that "corrects" for the negative eigenvalues .

-   **Hermitian Positive Semidefinite (HPS) Matrices:** If $A$ is HPS, its eigenvalues are non-negative, $\lambda_i \ge 0$. In this case, $\sigma_i = |\lambda_i| = \lambda_i$. The EVD, $A = Q\Lambda Q^{\ast}$, is already a valid SVD, with $U=V=Q$ and $\Sigma = \Lambda$. This represents the perfect coincidence of the two decompositions. A criterion to test if an arbitrary matrix $A$ is HPS can be derived directly from its SVD factors $U, \Sigma, V$. The matrix is HPS if and only if its left and [right singular vectors](@entry_id:754365) corresponding to positive singular values are identical, a condition expressible as $\Sigma(U-V)^{\ast}=0$ .

#### The Non-Normal Case: Inevitable Divergence

For [non-normal matrices](@entry_id:137153) ($A^{\ast}A \neq AA^{\ast}$), the elegant relationship between eigenvalues and singular values breaks down completely.

First, a [non-normal matrix](@entry_id:175080) may not be diagonalizable at all. A matrix is diagonalizable if and only if it has a complete set of linearly independent eigenvectors. Some [non-normal matrices](@entry_id:137153), termed **defective**, lack this property. A classic example is the [shear matrix](@entry_id:180719)
$$
A = \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix}
$$
which has only one linearly independent eigenvector despite being a $2 \times 2$ matrix . For such matrices, an EVD of the form $A = X\Lambda X^{-1}$ does not exist.

In stark contrast, an SVD exists for *every* matrix, regardless of normality or squareness. This is because the Gram matrices $A^{\ast}A$ and $AA^{\ast}$ are always Hermitian and thus always admit a complete [orthonormal set](@entry_id:271094) of eigenvectors, from which the SVD can be constructed. This universal existence makes the SVD a more robust and generally applicable tool than the EVD.

For [non-normal matrices](@entry_id:137153), the singular values are not equal to the eigenvalue moduli. The [non-normality](@entry_id:752585) introduces a "gap" between them. For instance, consider the matrix
$$
A(t) = \begin{pmatrix} 1 & t \\ 0 & 0 \end{pmatrix}
$$
for $t \neq 0$ . Its eigenvalues are $1$ and $0$, so its spectral radius is $\rho(A(t)) = 1$. However, its singular values are $\sqrt{1+t^2}$ and $0$. The largest [singular value](@entry_id:171660) (spectral norm) is $\|A(t)\|_2 = \sqrt{1+t^2}$. The difference $\|A(t)\|_2 - \rho(A(t)) = \sqrt{1+t^2} - 1$ is a direct measure of the matrix's [non-normality](@entry_id:752585).

This gap can be arbitrarily large. For the matrix
$$
A_{\alpha} = \begin{pmatrix} 0 & 1 \\ 0 & \alpha \end{pmatrix}
$$
with $\alpha > 0$ , the [spectral radius](@entry_id:138984) is $\rho(A_{\alpha}) = \alpha$, while the [spectral norm](@entry_id:143091) is $\|A_{\alpha}\|_2 = \sqrt{1+\alpha^2}$. The ratio $R(\alpha) = \frac{\|A_{\alpha}\|_2}{\rho(A_{\alpha})} = \frac{\sqrt{1+\alpha^2}}{\alpha}$ approaches infinity as $\alpha \to 0^+$. This discrepancy is crucial in fields like control theory and dynamical systems, where the [spectral radius](@entry_id:138984) governs long-term [asymptotic stability](@entry_id:149743), but the [spectral norm](@entry_id:143091) governs short-term transient amplification, a phenomenon only captured by the SVD.

### Advanced Connections and Frameworks

The relationship between EVD and SVD can also be understood through more abstract frameworks and powerful inequalities.

#### The Augmented Matrix Method

A particularly elegant construction unifies the SVD of $A \in \mathbb{C}^{m \times n}$ with the EVD of a larger, Hermitian matrix. Consider the augmented [block matrix](@entry_id:148435):
$$
B = \begin{pmatrix} 0 & A \\ A^{\ast} & 0 \end{pmatrix} \in \mathbb{C}^{(m+n) \times (m+n)}
$$
This matrix $B$ is Hermitian by construction. Its [eigenvalue equation](@entry_id:272921) $Bx=\lambda x$, with $x = \begin{pmatrix} u \\ v \end{pmatrix}$, expands to the coupled system $Av = \lambda u$ and $A^{\ast}u = \lambda v$. Decoupling these equations yields $A^{\ast}Av = \lambda^2 v$ and $AA^{\ast}u = \lambda^2 u$. This reveals that:
- The non-zero eigenvalues of $B$ are precisely $\pm \sigma_i$, where $\sigma_i$ are the positive singular values of $A$.
- The corresponding eigenvectors of $B$ are formed by combining the singular vectors of $A$. Specifically, for each singular triplet $(\sigma_i, u_i, v_i)$ of $A$, the matrix $B$ has an eigenpair $(\sigma_i, \begin{pmatrix} u_i \\ v_i \end{pmatrix})$ and $(-\sigma_i, \begin{pmatrix} u_i \\ -v_i \end{pmatrix})$.

This construction demonstrates that the SVD of any matrix $A$ is mathematically equivalent to the EVD of a related Hermitian matrix of larger dimension . This provides a powerful theoretical tool and an alternative route for SVD computation.

#### Majorization and Trace Inequalities

The divergence between singular values and eigenvalue moduli for [non-normal matrices](@entry_id:137153) can be formalized by the concept of **[majorization](@entry_id:147350)**. For two vectors $x, y \in \mathbb{R}^n$ with entries sorted in descending order, $x$ is said to majorize $y$ (written $y \prec x$) if $\sum_{i=1}^k y_i \le \sum_{i=1}^k x_i$ for $k=1, \dots, n-1$, and $\sum_{i=1}^n y_i = \sum_{i=1}^n x_i$.

A celebrated result by Hermann Weyl states that for any square matrix $A$, the vector of its absolute eigenvalues is majorized by the vector of its singular values:
$$(|\lambda_1|, |\lambda_2|, \dots, |\lambda_n|) \prec (\sigma_1, \sigma_2, \dots, \sigma_n)$$
(Here, the sum equality for $k=n$ does not hold in general). This implies the inequalities $\sum_{i=1}^k |\lambda_i| \le \sum_{i=1}^k \sigma_i$ for all $k=1, \dots, n$. This inequality is a sharp expression of the principle that singular values are more "dispersed" than eigenvalue moduli. The [supremum](@entry_id:140512) of a sum of the largest eigenvalue moduli, such as $\sup(|\lambda_1|+|\lambda_2|)$, is therefore bounded by the sum of the corresponding singular values, $\sigma_1+\sigma_2$, with equality being attained for a [normal matrix](@entry_id:185943) .

This theme extends to trace inequalities. The famous **von Neumann Trace Inequality** provides an upper bound for the [trace of a matrix product](@entry_id:150319) in terms of singular values:
$$|\operatorname{tr}(A^{\ast}B)| \le \sum_{i=1}^n \sigma_i(A)\sigma_i(B)$$
The supremum, $\sum \sigma_i(A)\sigma_i(B)$, is achieved when the [singular vectors](@entry_id:143538) of $A$ and $B$ are perfectly aligned, for instance, when $A$ and $B$ are [diagonal matrices](@entry_id:149228) with their entries (the singular values) sorted in the same order . This result highlights how the SVD provides the natural basis for analyzing matrix inner products and norms.