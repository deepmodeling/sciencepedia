## Introduction
In the study of [linear systems](@entry_id:147850), a single physical process can be described by infinitely many [state-space models](@entry_id:137993). This ambiguity raises a fundamental question: which properties are artifacts of our chosen mathematical description, and which are intrinsic to the system itself? The answer lies in the theory of similarity transformations and their associated invariant properties. A [similarity transformation](@entry_id:152935) is a formal [change of coordinates](@entry_id:273139), a new lens through which to view the system's dynamics. Understanding what remains unchanged through this transformation is the key to uncovering the deep, coordinate-independent truths about a system's behavior.

This article provides a graduate-level exploration of this cornerstone of control theory. We will bridge the gap between abstract linear algebra and its profound implications for [system analysis](@entry_id:263805) and design. You will learn not only what similarity transformations are but why they are essential for defining and understanding the core properties of any linear system.

Over the next three chapters, we will embark on a comprehensive journey. First, in **Principles and Mechanisms**, we will establish the mathematical foundation of similarity transformations, identify fundamental invariants like eigenvalues, and explore how they lead to [canonical forms](@entry_id:153058) that reveal a system's structure. Next, **Applications and Interdisciplinary Connections** will demonstrate how these principles confirm the invariance of critical control properties like [controllability and observability](@entry_id:174003), and we will discover how the same ideas provide a unifying language across diverse scientific fields. Finally, **Hands-On Practices** will offer a set of curated problems to solidify your theoretical understanding and build practical skills in applying these concepts.

## Principles and Mechanisms

In the analysis of linear time-invariant (LTI) systems, the choice of state variables is not unique. Any [invertible linear transformation](@entry_id:149915) of the [state vector](@entry_id:154607) results in a different [state-space representation](@entry_id:147149) of the same underlying physical system. Understanding how system properties behave under such transformations is fundamental to both theoretical analysis and computational practice. This chapter delves into the principles and mechanisms of the most important of these transformations: the similarity transformation. We will explore which properties remain invariant, how these invariants lead to [canonical forms](@entry_id:153058) that reveal the system's intrinsic structure, and what the practical implications are for [control system design](@entry_id:262002) and analysis.

### The Similarity Transformation: A Change of State Coordinates

Consider a [state-space model](@entry_id:273798) described by $\dot{x} = Ax$, where $x \in \mathbb{C}^n$ is the state vector and $A \in \mathbb{C}^{n \times n}$ is the state matrix. A **[change of basis](@entry_id:145142)**, or a change of state coordinates, is defined by an [invertible matrix](@entry_id:142051) $T \in \mathbb{C}^{n \times n}$ through the relation $x = Tz$. Differentiating this expression gives $\dot{x} = T\dot{z}$. Substituting these into the state equation yields:

$T\dot{z} = A(Tz)$

Since $T$ is invertible, we can multiply by $T^{-1}$ from the left to obtain the dynamics in the new coordinates:

$\dot{z} = (T^{-1}AT)z$

The new state matrix, let us call it $B$, is related to the original matrix $A$ by the transformation $B = T^{-1}AT$. This is known as a **similarity transformation**. Two matrices $A$ and $B$ are said to be **similar** if such an [invertible matrix](@entry_id:142051) $T$ exists. This transformation is the mathematical embodiment of viewing the same [linear operator](@entry_id:136520) (the system dynamics) in a different basis. Consequently, any property that describes the intrinsic dynamics of the system, independent of the choice of coordinates, must be an invariant of the similarity transformation.

### Fundamental Invariants of Similarity

The most fundamental properties of a linear system are its modes of behavior, which are captured by the eigenvalues of the state matrix. A key result is that eigenvalues are indeed preserved under similarity. This can be demonstrated by examining the **characteristic polynomial**, $p_A(\lambda) = \det(A - \lambda I)$. For a similar matrix $B = T^{-1}AT$, its characteristic polynomial is:

$p_B(\lambda) = \det(B - \lambda I) = \det(T^{-1}AT - \lambda T^{-1}IT) = \det(T^{-1}(A - \lambda I)T)$

Using the multiplicative property of the determinant, $\det(XYZ) = \det(X)\det(Y)\det(Z)$, and the fact that $\det(T^{-1}) = 1/\det(T)$, we find:

$p_B(\lambda) = \det(T^{-1})\det(A - \lambda I)\det(T) = \det(A - \lambda I) = p_A(\lambda)$

Since the characteristic polynomials are identical, their roots must also be identical. Therefore, [similar matrices](@entry_id:155833) have the same multiset of **eigenvalues**, including their **algebraic multiplicities**. This is a cornerstone result in [linear systems theory](@entry_id:172825) [@problem_id:2905091] [@problem_id:2744717].

From the invariance of eigenvalues, the invariance of two other important quantities follows directly: the **determinant** (the product of the eigenvalues) and the **trace** (the sum of the eigenvalues). These properties are thus preserved under any change of state coordinates [@problem_id:2744730].

It is equally important to recognize what is *not* invariant. While the eigenvalues are preserved, the corresponding **eigenvectors** are not. If $v$ is an eigenvector of $A$ for an eigenvalue $\lambda$ (i.e., $Av = \lambda v$), the corresponding eigenvector of $B=T^{-1}AT$ is found by left-multiplying by $T^{-1}$: $T^{-1}Av = \lambda T^{-1}v$. Substituting $A=TBT^{-1}$ gives $(T^{-1}T)B(T^{-1}v) = \lambda(T^{-1}v)$, which simplifies to $B(T^{-1}v) = \lambda(T^{-1}v)$. This shows that the corresponding eigenvector of $B$ is $w = T^{-1}v$. The eigenvector is transformed by the inverse of the basis-change matrix [@problem_id:2905091].

A more general and powerful invariant is the rank of any polynomial function of the matrix. For any polynomial $p(s)$, the matrix $p(B)$ is similar to $p(A)$:

$p(B) = p(T^{-1}AT) = \sum c_k (T^{-1}AT)^k = \sum c_k (T^{-1}A^k T) = T^{-1}(\sum c_k A^k)T = T^{-1}p(A)T$

Since rank is preserved by similarity, it follows that $\operatorname{rank}(p(A)) = \operatorname{rank}(p(B))$ for any polynomial $p$. This has profound implications, as it guarantees the invariance of the **[minimal polynomial](@entry_id:153598)** and the dimensions of generalized eigenspaces [@problem_id:2744730] [@problem_id:2744717].

### Canonical Forms and the Classification of Linear Systems

The purpose of a change of coordinates is often to transform the state matrix into a "simpler" or **canonical form** that reveals the system's structure.

#### Diagonalization: The Ideal Case

The simplest possible form for a matrix is diagonal. A matrix $A$ is **diagonalizable** if it is similar to a diagonal matrix $\Lambda$. This occurs if and only if there exists a basis for the entire state space $\mathbb{C}^n$ consisting of eigenvectors of $A$. If such a basis of eigenvectors $\{v_1, \dots, v_n\}$ exists, we can construct the [similarity transformation](@entry_id:152935) matrix $T$ by using these eigenvectors as its columns: $T = [v_1 \ v_2 \ \cdots \ v_n]$. The action of $A$ on $T$ is then:

$AT = A[v_1 \ \cdots \ v_n] = [Av_1 \ \cdots \ Av_n] = [\lambda_1 v_1 \ \cdots \ \lambda_n v_n] = [v_1 \ \cdots \ v_n] \begin{pmatrix} \lambda_1   \\  \ddots  \\    \lambda_n \end{pmatrix} = T\Lambda$

Since the eigenvectors form a basis, $T$ is invertible, and we can write $T^{-1}AT = \Lambda$. A [sufficient condition](@entry_id:276242) for [diagonalizability](@entry_id:748379) is that the matrix has $n$ distinct eigenvalues, as eigenvectors corresponding to distinct eigenvalues are always linearly independent, guaranteeing that $T$ is invertible [@problem_id:2744705].

This leads to a simple classification for diagonalizable systems: two diagonalizable matrices $A$ and $B$ are similar if and only if they have the same [characteristic polynomial](@entry_id:150909) (i.e., the same multiset of eigenvalues). If they do, they are both similar to the same [diagonal matrix](@entry_id:637782) $\Lambda$ (up to permutation of entries), and therefore are similar to each other [@problem_id:2744721].

#### The Jordan Canonical Form: The General Theory

Not all matrices are diagonalizable. A matrix may have [repeated eigenvalues](@entry_id:154579) where the number of linearly independent eigenvectors associated with an eigenvalue (its [geometric multiplicity](@entry_id:155584)) is less than its [algebraic multiplicity](@entry_id:154240). Such a matrix is called **defective**.

For any square matrix over the complex numbers $\mathbb{C}$, there is still a canonical form it can be reduced to: the **Jordan Canonical Form (JCF)**. The fundamental theorem of Jordan decomposition states that any matrix $A \in \mathbb{C}^{n \times n}$ is similar to a [block diagonal matrix](@entry_id:150207) $J$, where each block is a **Jordan block** of the form:

$J_k(\lambda) = \begin{pmatrix} \lambda  1   \\  \lambda  \ddots  \\   \ddots  1 \\    \lambda \end{pmatrix} \in \mathbb{C}^{k \times k}$

The JCF of a matrix is unique up to the permutation of its Jordan blocks. This means the multiset of eigenvalues, and for each eigenvalue, the number and sizes of its associated Jordan blocks, form a complete set of invariants for similarity. Therefore, two matrices $A, B \in \mathbb{C}^{n \times n}$ are similar if and only if they have the same Jordan Canonical Form (up to reordering the blocks) [@problem_id:2744731] [@problem_id:2744718]. This provides a definitive "fingerprint" for the equivalence class of a matrix under similarity.

This also reveals why simpler invariants are insufficient for a general classification. For example, the matrices $A = \operatorname{diag}(J_2(0), J_2(0))$ and $B = \operatorname{diag}(J_2(0), J_1(0), J_1(0))$ both have the [characteristic polynomial](@entry_id:150909) $s^4$ and the [minimal polynomial](@entry_id:153598) $s^2$. However, their Jordan structures are different (partitions $2+2$ vs. $2+1+1$ of the algebraic multiplicity 4), so they are not similar. This demonstrates that the full specification of the Jordan block sizes for each eigenvalue is necessary to uniquely determine the similarity class [@problem_id:2744718].

### Invariant Subspaces and Block Decomposition

The block structure of [canonical forms](@entry_id:153058) is deeply connected to the concept of [invariant subspaces](@entry_id:152829). A subspace $\mathcal{V} \subseteq \mathbb{C}^n$ is said to be an **A-[invariant subspace](@entry_id:137024)** if for every vector $v \in \mathcal{V}$, its image $Av$ is also in $\mathcal{V}$.

The existence of an A-[invariant subspace](@entry_id:137024) allows for a structural simplification of the matrix $A$. If we choose a basis for $\mathbb{C}^n$ where the first $k$ vectors form a basis for a $k$-dimensional A-invariant subspace $\mathcal{V}$, the matrix of the operator $A$ in this new basis will be block upper-triangular.

To see this, let $\{v_1, \dots, v_k\}$ be a basis for $\mathcal{V}$, and complete it to a basis $\{v_1, \dots, v_n\}$ for $\mathbb{C}^n$. Form the similarity transformation matrix $T = [v_1 \ \cdots \ v_n]$. The transformed matrix is $B = T^{-1}AT$. The $j$-th column of $B$ contains the coordinates of $Av_j$ in the new basis. For $j \le k$, since $v_j \in \mathcal{V}$ and $\mathcal{V}$ is A-invariant, $Av_j$ must also be in $\mathcal{V}$. This means $Av_j$ can be written as a [linear combination](@entry_id:155091) of only the first $k$ basis vectors. Consequently, its [coordinate vector](@entry_id:153319) will have zeros in positions $k+1$ through $n$. This forces the structure of $B$ to be:

$B = \begin{pmatrix} B_{11}   B_{12} \\ 0   B_{22} \end{pmatrix}$

where $B_{11} \in \mathbb{C}^{k \times k}$ is the matrix representation of the operator $A$ restricted to the invariant subspace $\mathcal{V}$. This block decomposition is a powerful tool for analyzing complex systems by breaking them into smaller, interacting subsystems [@problem_id:2744734].

### Numerical Stability and Orthogonal Transformations

While the Jordan form provides a complete theoretical classification, it is notoriously sensitive to perturbations and thus numerically unstable. This makes it unsuitable for most practical computations.

#### The Fragility of the Jordan Form

The problem lies in the basis of eigenvectors (and [generalized eigenvectors](@entry_id:152349)) used to form the transformation matrix $P$ for the JCF. As a matrix approaches being defective, the eigenvalues get closer, and the corresponding eigenvectors can become nearly linearly dependent. This causes the [transformation matrix](@entry_id:151616) $P$ to become **ill-conditioned**, meaning its condition number $\kappa(P) = \|P\|\|P^{-1}\|$ is very large.

Consider the classic example $A_\varepsilon = \begin{bmatrix} \lambda  1 \\ \varepsilon  \lambda \end{bmatrix}$ for $\varepsilon  0$. Its eigenvalues are $\lambda \pm \sqrt{\varepsilon}$, and a corresponding eigenvector matrix is $V_\varepsilon = \begin{bmatrix} 1  1 \\ \sqrt{\varepsilon}  -\sqrt{\varepsilon} \end{bmatrix}$. As $\varepsilon \to 0^+$, the eigenvalues coalesce and the matrix becomes defective. The [2-norm](@entry_id:636114) condition number of $V_\varepsilon$ can be computed as $\kappa_2(V_\varepsilon) = \varepsilon^{-1/2}$, which grows without bound as $\varepsilon \to 0^+$. Any computation involving $V_\varepsilon$ or its inverse will amplify numerical errors by a factor proportional to $\kappa_2(V_\varepsilon)$, rendering [modal analysis](@entry_id:163921) unreliable [@problem_id:2744736]. The Jordan structure itself is a [discontinuous function](@entry_id:143848) of matrix entries; an infinitesimal perturbation can change it dramatically (e.g., from a single $2 \times 2$ block to two $1 \times 1$ blocks), which is the source of this numerical fragility.

#### Unitary Similarity and the Schur Decomposition

To overcome this instability, we use transformations that are guaranteed to be well-conditioned. The ideal choice is a **unitary transformation** (or **orthogonal** in the real case), where the [transformation matrix](@entry_id:151616) $Q$ satisfies $Q^*Q=I$ (or $Q^\top Q=I$). Such matrices are perfectly conditioned, with $\kappa_2(Q)=1$, and do not amplify [numerical errors](@entry_id:635587).

The **Schur Decomposition Theorem** states that any matrix $A \in \mathbb{C}^{n \times n}$ is unitarily similar to an [upper-triangular matrix](@entry_id:150931) $T$, i.e., $A = QTQ^*$ where $Q$ is unitary and $T$ is upper-triangular. The diagonal entries of $T$ are the eigenvalues of $A$. For real matrices, the **real Schur form** is a [quasi-upper-triangular matrix](@entry_id:753962), with $1 \times 1$ blocks for real eigenvalues and $2 \times 2$ blocks for [complex conjugate](@entry_id:174888) pairs on its diagonal. The Schur form provides a numerically stable way to compute and represent [invariant subspaces](@entry_id:152829). The leading $k$ columns of $Q$ span an invariant subspace corresponding to the leading $k$ eigenvalues on the diagonal of $T$ [@problem_id:2744741] [@problem_id:2744736].

The distinction between general and [unitary similarity](@entry_id:203501) also affects which properties are invariant. While eigenvalues are always invariant, other properties are preserved only by the more restrictive unitary transformations. For instance, the **singular values** of a matrix and its **Frobenius norm** $\|A\|_F = \sqrt{\operatorname{tr}(A^*A)}$ are invariant under [unitary similarity](@entry_id:203501) but can change under a general similarity transformation. Likewise, the property of being **normal** ($A^*A = AA^*$) is preserved by [unitary similarity](@entry_id:203501) but not by general similarity [@problem_id:2744730].

### System-Theoretic Implications: Duality and Structural Properties

The concept of similarity invariance is central to many fundamental ideas in control theory. Structural properties like **[controllability](@entry_id:148402)** and **[observability](@entry_id:152062)** describe the intrinsic capabilities of a system and must therefore be invariant under any change of state coordinates. This can be formally shown by examining the [controllability matrix](@entry_id:271824) $\mathcal{C}(A,B) = [B \ AB \ \cdots \ A^{n-1}B]$. Under a similarity transformation, it transforms as $\mathcal{C}(T^{-1}AT, T^{-1}B) = T^{-1}\mathcal{C}(A,B)$. Since $T$ is invertible, the rank of the [controllability matrix](@entry_id:271824) is preserved, and thus controllability itself is a similarity invariant [@problem_id:2744740].

A powerful concept that connects system properties is the **principle of duality**. This principle states that the pair $(A,B)$ is controllable if and only if the dual pair $(A^\top, C^\top)$, where $C$ is interpreted as $B^\top$, is observable. This duality is profound and extends to nearly all structural aspects of a system:
-   **PBH Test:** The Popov-Belevitch-Hautus (PBH) test states that $(A,B)$ is controllable if and only if $\operatorname{rank}[\lambda I - A \ \ B] = n$ for all $\lambda \in \mathbb{C}$. The corresponding observability test for $(A^\top, B^\top)$ is that $\operatorname{rank}\begin{bmatrix} \lambda I - A^\top \\ B^\top \end{bmatrix} = n$. The two test matrices are transposes of each other, so their ranks are always equal, beautifully reflecting the duality at a matrix level.
-   **Structural Indices:** The set of [controllability](@entry_id:148402) indices for $(A,B)$ is identical to the set of observability indices for the dual pair $(A^\top, B^\top)$.
-   **Transmission Zeros:** The [transmission zeros](@entry_id:175186) of a system $(A,B,C,D)$, which represent frequencies where signal transmission is blocked, are identical to those of its dual system $(A^\top, C^\top, B^\top, D^\top)$. This is because the transfer function of the dual system is the transpose of the original system's transfer function, $G_d(s) = G(s)^\top$ [@problem_id:2744740].

### A Note on Other Transformations: The Case of Congruence

Finally, it is instructive to contrast similarity with another important [matrix transformation](@entry_id:151622), **congruence**, defined as $B = T^\top A T$ for an [invertible matrix](@entry_id:142051) $T$. While similar in form, congruence arises in a different context: the change of variables for [quadratic forms](@entry_id:154578), $x \mapsto x^\top A x$.

Because the context is different, the invariants are different. A [congruence transformation](@entry_id:154837) does not, in general, preserve eigenvalues, the characteristic polynomial, or the trace. For example, for $A=I$ and $T=\operatorname{diag}(2,1)$, the congruent matrix is $B=T^\top I T = \operatorname{diag}(4,1)$, which has different eigenvalues from $A$. The key invariant for the [congruence](@entry_id:194418) of real symmetric matrices is given by **Sylvester's Law of Inertia**, which states that the **inertia**—the number of positive, negative, and zero eigenvalues—is preserved [@problem_id:2744717].

The two transformations merge in one important special case: when the [transformation matrix](@entry_id:151616) $T$ is orthogonal. In this case, $T^\top = T^{-1}$, so the [congruence](@entry_id:194418) $T^\top A T$ is also a similarity $T^{-1} A T$. Consequently, for orthogonal transformations, both the [spectral invariants](@entry_id:200177) of similarity and the inertial invariants of congruence are preserved [@problem_id:2744717].