## Introduction
In linear algebra, a similarity transformation is a fundamental operation that simplifies the representation of a [linear map](@entry_id:201112) by changing the basis of the vector space. This process has profound implications, forming the theoretical bedrock for much of [numerical analysis](@entry_id:142637) and its application across scientific disciplines. The core significance of similarity lies in understanding which properties of a matrix remain unchanged—or invariant—under this transformation. This article addresses the crucial question of what is preserved and what is not, revealing why eigenvalues hold a special, invariant status while other properties, like singular values or matrix structure, do not.

This exploration will guide you through the essential aspects of similarity transformations across three focused chapters. The first, "Principles and Mechanisms," establishes the foundational theory, proving the invariance of the characteristic polynomial and exploring the limits of this preservation, including the conditions for similarity defined by the Jordan Normal Form. The second chapter, "Applications and Interdisciplinary Connections," demonstrates how this theoretical principle is a powerful tool in practice, underpinning numerical algorithms, physical models in quantum mechanics, and data analysis techniques. Finally, "Hands-On Practices" will provide opportunities to apply and solidify these concepts through targeted computational problems.

## Principles and Mechanisms

In the study of [linear transformations](@entry_id:149133) and their [matrix representations](@entry_id:146025), it is often advantageous to change the basis of the vector space to simplify the matrix. This leads to the concept of a [similarity transformation](@entry_id:152935), a cornerstone of both theoretical linear algebra and numerical computation. This chapter delineates the fundamental principles governing similarity transformations, focusing on which properties are preserved and which are not, and culminates in an analysis of the numerical stability of the most critical invariant: the eigenvalues.

### The Invariance of the Characteristic Polynomial

A matrix $B \in \mathbb{C}^{n \times n}$ is said to be **similar** to a matrix $A \in \mathbb{C}^{n \times n}$ if there exists an [invertible matrix](@entry_id:142051) $P \in \mathbb{C}^{n \times n}$ such that:

$$ B = P^{-1} A P $$

This transformation has a profound geometric interpretation. If $A$ represents a linear transformation $T: V \to V$ with respect to a basis $\mathcal{E}$, then $B$ represents the *same* linear transformation $T$ with respect to a new basis $\mathcal{F}$, where the columns of $P$ are the coordinate vectors of the new basis vectors of $\mathcal{F}$ expressed in the old basis $\mathcal{E}$. The matrix $P$ is thus the **[change-of-basis matrix](@entry_id:184480)**.

The most fundamental property of a [similarity transformation](@entry_id:152935) is its effect on the eigenvalues of the matrix. Remarkably, the eigenvalues remain entirely unchanged. This is not merely an incidental property but a direct consequence of the fact that the entire **[characteristic polynomial](@entry_id:150909)** is an invariant of similarity.

Let us prove this from first principles. The [characteristic polynomial](@entry_id:150909) of a matrix $M$ is defined as $p_M(\lambda) = \det(\lambda I - M)$. For the matrix $B = P^{-1}AP$, its [characteristic polynomial](@entry_id:150909) is:

$$ p_B(\lambda) = \det(\lambda I - B) = \det(\lambda I - P^{-1}AP) $$

The key insight is to express the identity matrix $I$ as $I = P^{-1}IP$. This allows us to factor the expression within the determinant:

$$ p_B(\lambda) = \det(\lambda P^{-1}IP - P^{-1}AP) = \det(P^{-1}(\lambda I - A)P) $$

Using the [multiplicative property of determinants](@entry_id:148055), $\det(XYZ) = \det(X)\det(Y)\det(Z)$, we can separate the terms:

$$ p_B(\lambda) = \det(P^{-1}) \det(\lambda I - A) \det(P) $$

Since the determinant is a scalar value, we can reorder the terms. Furthermore, for any invertible matrix, $\det(P^{-1}) = 1/\det(P)$. This leads to a cancellation:

$$ p_B(\lambda) = \det(P^{-1})\det(P) \det(\lambda I - A) = \left(\frac{1}{\det(P)}\right)\det(P) \det(\lambda I - A) = \det(\lambda I - A) = p_A(\lambda) $$

This result, $p_B(\lambda) = p_A(\lambda)$, shows that [similar matrices](@entry_id:155833) have identical characteristic polynomials . Since polynomials are identical if and only if all their corresponding coefficients are identical, this implies that all properties derived from these coefficients are also invariants. These include:
- The **spectrum** (the set of eigenvalues, which are the roots of the polynomial) and their **algebraic multiplicities**.
- The **trace** of the matrix, $\operatorname{tr}(A)$, which is related to the coefficient of the $\lambda^{n-1}$ term. We can also see this directly: $\operatorname{tr}(B) = \operatorname{tr}(P^{-1}AP) = \operatorname{tr}(APP^{-1}) = \operatorname{tr}(A)$ by the cyclic property of the trace.
- The **determinant** of the matrix, $\det(A)$, which is the product of the eigenvalues and is related to the constant term of the polynomial. This means $\det(B) = \det(P^{-1}AP) = \det(P^{-1})\det(A)\det(P) = \det(A)$ .

### The Transformation of Eigenvectors

While eigenvalues are invariant, eigenvectors are not. They transform according to the change of basis. Suppose $v$ is an eigenvector of $B$ corresponding to an eigenvalue $\lambda$. By definition:

$$ Bv = \lambda v $$

Substituting $B = P^{-1}AP$, we get:

$$ (P^{-1}AP)v = \lambda v $$

If we pre-multiply both sides by $P$, we obtain:

$$ A(Pv) = \lambda(Pv) $$

This equation is precisely the definition of an eigenvector. It shows that if $v$ is an eigenvector of $B$, then the vector $x = Pv$ is an eigenvector of $A$ corresponding to the same eigenvalue $\lambda$. Since $P$ is invertible and $v \neq 0$, it follows that $x \neq 0$.

Geometrically, this means that the [invariant subspaces](@entry_id:152829) ([eigenspaces](@entry_id:147356)) of the linear transformation are the same physical objects in the vector space. The [similarity transformation](@entry_id:152935) only changes their coordinate representation. An eigenvector $v$ of $B$ is the [coordinate vector](@entry_id:153319) of an invariant direction in the new basis $\mathcal{F}$. The vector $x=Pv$ is the [coordinate vector](@entry_id:153319) of that *same* invariant direction, but expressed in the original basis $\mathcal{E}$ .

### The Limits of Invariance: What Similarity Does Not Preserve

The preservation of eigenvalues is such a powerful property that it is tempting to assume other matrix properties are also preserved. This is a common pitfall. It is crucial to understand what is *not* invariant under general similarity transformations.

#### Matrix Structure

Special matrix structures, such as being Hermitian or skew-Hermitian, are not generally preserved under arbitrary similarity. Consider a skew-Hermitian matrix $A$, where $A^* = -A$. Let's examine the structure of $B = S^{-1}AS$:

$$ B^* = (S^{-1}AS)^* = S^*A^*(S^{-1})^* = S^*(-A)(S^{-1})^* = -S^*A(S^{-1})^* $$

For $B$ to be skew-Hermitian, we would need $B^* = -B = -S^{-1}AS$. This equality does not hold for a general invertible matrix $S$.

However, if the transformation is **unitary**, meaning $S$ is a [unitary matrix](@entry_id:138978) ($S^{-1} = S^*$), the structure is preserved. For a unitary $S$, we have $S^* = S^{-1}$ and $(S^{-1})^* = (S^*)^* = S$. Substituting these into the expression for $B^*$ gives:

$$ B^* = -S^*A(S^{-1})^* = -(S^{-1})A(S) = -S^{-1}AS = -B $$

This shows that $B$ is also skew-Hermitian. This highlights a critical distinction:
1.  The property of having a certain spectrum (e.g., purely imaginary eigenvalues for a skew-Hermitian matrix) is preserved under *any* [similarity transformation](@entry_id:152935) because eigenvalues are always preserved.
2.  The algebraic structure that gives rise to that spectrum (e.g., the skew-Hermitian property itself) is preserved only under **[unitary similarity](@entry_id:203501) transformations** . The same logic applies to Hermitian, normal, and other structurally defined matrix classes.

#### Singular Values

Another fundamental set of numbers associated with a matrix are its **singular values**, which are the square roots of the eigenvalues of $M^\mathsf{T} M$. Unlike eigenvalues, singular values are **not** preserved under similarity transformations.

To see this clearly, let's consider a concrete example . Let
$$ A = \begin{pmatrix} 1  0 \\ 0  2 \end{pmatrix}, \qquad P = \begin{pmatrix} 1  1 \\ 0  1 \end{pmatrix} $$
The matrix $A$ is diagonal, so its singular values are simply the absolute values of its diagonal entries, which are $\sigma_1(A)=2$ and $\sigma_2(A)=1$. The eigenvalues of $A$ are $1$ and $2$.

The similar matrix $B = P^{-1}AP$ is calculated as:
$$ B = \begin{pmatrix} 1  -1 \\ 0  1 \end{pmatrix} \begin{pmatrix} 1  0 \\ 0  2 \end{pmatrix} \begin{pmatrix} 1  1 \\ 0  1 \end{pmatrix} = \begin{pmatrix} 1  -1 \\ 0  2 \end{pmatrix} $$
The eigenvalues of $B$ are $1$ and $2$, as expected. To find the singular values of $B$, we examine the eigenvalues of $B^\mathsf{T} B$:
$$ B^\mathsf{T} B = \begin{pmatrix} 1  0 \\ -1  2 \end{pmatrix} \begin{pmatrix} 1  -1 \\ 0  2 \end{pmatrix} = \begin{pmatrix} 1  -1 \\ -1  5 \end{pmatrix} $$
The characteristic polynomial of $B^\mathsf{T} B$ is $\lambda^2 - 6\lambda + 4 = 0$, giving eigenvalues $3 \pm \sqrt{5}$. The singular values of $B$ are thus $\sigma_1(B) = \sqrt{3+\sqrt{5}}$ and $\sigma_2(B) = \sqrt{3-\sqrt{5}}$. These are clearly different from the singular values of $A$. This demonstrates that similarity transformations, which are changes of basis for a linear map, do not preserve the properties related to the metric structure (lengths and angles) that singular values represent.

#### Distinction from Congruence Transformations

It is essential to distinguish similarity from another common transformation, **[congruence](@entry_id:194418)**. A [congruence transformation](@entry_id:154837) takes the form $C = P^\mathsf{T} A P$ for an [invertible matrix](@entry_id:142051) $P$. While this looks similar, its purpose and properties are different. Congruence arises in the context of changing basis for [quadratic forms](@entry_id:154578) ($x^\mathsf{T} A x$).

A [congruence transformation](@entry_id:154837) does **not** preserve eigenvalues. For the [symmetric matrix](@entry_id:143130) $A = \begin{pmatrix} 3  1 \\ 1  1 \end{pmatrix}$ and the same $P = \begin{pmatrix} 2  1 \\ 0  1 \end{pmatrix}$ as before, the eigenvalues of $A$ are $2 \pm \sqrt{2}$. The congruent matrix is $C = P^\mathsf{T} A P = \begin{pmatrix} 12  8 \\ 8  6 \end{pmatrix}$, which has eigenvalues $9 \pm \sqrt{73}$. The eigenvalues have changed dramatically .

For symmetric matrices, congruence preserves the number of positive, negative, and zero eigenvalues, a result known as **Sylvester's Law of Inertia**. This property, the **inertia** of a matrix, is also preserved by similarity, but for a different reason: similarity preserves the eigenvalues themselves, and thus must preserve their signs . The confusion often arises because for an **orthogonal** matrix $P$ (where $P^{-1}=P^\mathsf{T}$), the similarity and [congruence](@entry_id:194418) transformations are identical.

### The Condition for Similarity: The Jordan Normal Form

We have established that if two matrices are similar, they must have the same [characteristic polynomial](@entry_id:150909). Is the converse true? If two matrices have the same set of eigenvalues (with the same algebraic multiplicities), are they necessarily similar?

The answer is **no**. Consider the two matrices:
$$ A = \begin{pmatrix} 2  0 \\ 0  2 \end{pmatrix} \quad \text{and} \quad B = \begin{pmatrix} 2  1 \\ 0  2 \end{pmatrix} $$
Both have the characteristic polynomial $(\lambda-2)^2$ and thus share the eigenvalue $\lambda=2$ with [algebraic multiplicity](@entry_id:154240) 2. However, they are not similar. Matrix $A$ is diagonalizable and its geometric multiplicity for $\lambda=2$ is 2. Matrix $B$ is not diagonalizable and its [geometric multiplicity](@entry_id:155584) for $\lambda=2$ is 1. Since similarity preserves [geometric multiplicity](@entry_id:155584), $A$ and $B$ cannot be similar  .

This reveals that the characteristic polynomial does not contain enough information to uniquely determine a matrix up to similarity. The missing information pertains to the structure of the generalized [eigenspaces](@entry_id:147356). This structure is completely captured by the **Jordan Normal Form (JNF)**. A [fundamental theorem of linear algebra](@entry_id:190797) states:

> Two matrices $A, B \in \mathbb{C}^{n \times n}$ are similar over $\mathbb{C}$ if and only if they have the same Jordan Normal Form, up to a permutation of the Jordan blocks.

For real matrices, the analogous canonical form is the **Real Jordan Normal Form (RJNF)**, which uses $2 \times 2$ blocks for complex conjugate eigenvalue pairs. The theorem holds true: two real matrices are similar over $\mathbb{R}$ if and only if they have the same RJNF .

A powerful special case arises when a matrix is **diagonalizable** over $\mathbb{C}$. This means its JNF is a [diagonal matrix](@entry_id:637782), with all Jordan blocks being of size $1 \times 1$. If two real matrices $A$ and $B$ are both diagonalizable over $\mathbb{C}$ and have the same eigenvalues, their JNFs must be identical (as they are just the [diagonal matrices](@entry_id:149228) of eigenvalues). Consequently, their RJNFs are also identical, and they must be similar over $\mathbb{R}$ .

### Numerical Stability and Eigenvalue Sensitivity

In the world of [finite-precision arithmetic](@entry_id:637673), we must ask a more practical question. Even if eigenvalues are mathematically invariant, how sensitive are they to small perturbations in the matrix entries, such as those introduced by measurement error or [floating-point rounding](@entry_id:749455)?

The answer is given by the **Bauer-Fike Theorem**. For a [diagonalizable matrix](@entry_id:150100) $A = P D P^{-1}$, where $D$ is the diagonal matrix of eigenvalues, the sensitivity of the eigenvalues is governed by the **condition number** of the eigenvector matrix $P$. The theorem states that for any eigenvalue $\mu$ of a perturbed matrix $A+\Delta A$, there is an eigenvalue $\lambda$ of $A$ such that:

$$ |\mu - \lambda| \le \kappa(P) \|\Delta A\| $$

where $\kappa(P) = \|P\| \|P^{-1}\|$ is the condition number of $P$ with respect to a given [operator norm](@entry_id:146227), and $\|\Delta A\|$ is the norm of the perturbation  .

This inequality is of paramount importance. It reveals that:
- If the eigenvector matrix $P$ is well-conditioned (i.e., $\kappa(P)$ is close to 1), then the eigenvalues are **well-conditioned** (insensitive to perturbations). Small relative changes in $A$ lead to small relative changes in the eigenvalues.
- If $P$ is ill-conditioned (i.e., $\kappa(P)$ is very large), the eigenvalues can be **ill-conditioned** (highly sensitive). This happens when the eigenvectors are nearly linearly dependent. In such cases, a tiny perturbation $\|\Delta A\|$ can be amplified by a large factor $\kappa(P)$, leading to a significant change in the eigenvalues.

This explains the immense importance of **[normal matrices](@entry_id:195370)** in [numerical analysis](@entry_id:142637). A matrix $A$ is normal if $A^*A = AA^*$. Normal matrices (which include Hermitian, skew-Hermitian, and [unitary matrices](@entry_id:200377)) are precisely those that are [unitarily diagonalizable](@entry_id:195045). This means their eigenvector matrix $P$ can be chosen to be a [unitary matrix](@entry_id:138978) $Q$. For the spectral [2-norm](@entry_id:636114), unitary matrices have a condition number of exactly 1: $\kappa_2(Q) = 1$. The Bauer-Fike bound then simplifies to:

$$ |\mu - \lambda| \le \|\Delta A\|_2 $$

This means the eigenvalues of a [normal matrix](@entry_id:185943) are perfectly conditioned; the perturbation in the eigenvalues is never larger than the perturbation in the matrix .

For non-diagonalizable (defective) matrices, the situation is even more precarious. At a repeated eigenvalue corresponding to a Jordan block of size $k > 1$, the eigenvalues are generally not differentiable functions of the matrix entries. A perturbation of size $\varepsilon$ can lead to a change in the eigenvalue of order $\varepsilon^{1/k}$. For small $\varepsilon$, this is a much larger change, indicating extreme [ill-conditioning](@entry_id:138674) .

In summary, while similarity transformations provide a powerful theoretical tool for simplifying matrices while preserving their spectra, the practical stability of those spectra depends critically on the conditioning of the eigenvectors. The distinction between a general similarity transform and a unitary one lies at the heart of robust numerical eigenvalue algorithms.