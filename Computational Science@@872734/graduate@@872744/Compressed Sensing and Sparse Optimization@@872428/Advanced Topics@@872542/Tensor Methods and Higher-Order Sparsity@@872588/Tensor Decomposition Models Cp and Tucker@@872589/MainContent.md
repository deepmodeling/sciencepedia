## Introduction
In an era of increasingly complex and high-dimensional data, tensors—or multi-dimensional arrays—have emerged as the natural representation for information across fields ranging from signal processing to data science. However, extracting meaningful structure and latent patterns from these massive datasets presents a significant challenge. Tensor decomposition provides a powerful suite of tools to address this problem, breaking down a complex tensor into simpler, more interpretable components. This article focuses on two of the most foundational and widely used models: the Canonical Polyadic (CP) and Tucker decompositions. It aims to bridge the gap between their abstract mathematical definitions and their practical application by exploring their distinct properties, strengths, and weaknesses.

This article is structured into three comprehensive chapters. The first chapter, **"Principles and Mechanisms,"** delves into the mathematical foundations of the CP and Tucker models, defining their structure, analyzing their [parameterization](@entry_id:265163) and indeterminacies, and contrasting their core concepts of rank. The second chapter, **"Applications and Interdisciplinary Connections,"** showcases how these models are applied to solve real-world problems in areas like [compressed sensing](@entry_id:150278), [medical imaging](@entry_id:269649), and communications engineering. Finally, **"Hands-On Practices"** provides a set of targeted exercises to solidify understanding of key theoretical and algorithmic concepts, such as uniqueness conditions and [model complexity](@entry_id:145563). By progressing through these sections, the reader will gain a robust understanding of both the theory and practice of [tensor decomposition](@entry_id:173366).

## Principles and Mechanisms

This chapter delves into the foundational principles and mechanisms of two of the most prominent [tensor decomposition](@entry_id:173366) models: the Canonical Polyadic (CP) decomposition and the Tucker decomposition. We will begin by establishing the essential mathematical machinery for manipulating tensors—[matricization](@entry_id:751739) and [vectorization](@entry_id:193244). Subsequently, we will explore each decomposition model in detail, defining their structures, inherent ambiguities, and parametric complexities. A comparative analysis will highlight their distinct structural assumptions and analytical properties. Finally, we will examine critical algorithmic and theoretical issues, including computational methods, conditions for uniqueness, and the challenges of [ill-posedness](@entry_id:635673) in tensor approximation.

### Foundational Concepts: Reshaping Tensors

While tensors are inherently multi-dimensional arrays, many of their most important properties and computations are revealed by re-organizing their elements into two-dimensional matrices or one-dimensional vectors. These operations, known as [matricization](@entry_id:751739) (or unfolding) and [vectorization](@entry_id:193244), form the bedrock of [tensor algebra](@entry_id:161671) and algorithms.

A tensor is composed of one-dimensional arrays called **fibers**. For an order-$N$ tensor $\mathcal{X} \in \mathbb{R}^{I_1 \times \cdots \times I_N}$, a **mode-$n$ fiber** is a vector obtained by fixing all indices except the $n$-th index, $i_n$. For instance, the vector $\mathcal{X}(i_1, \ldots, i_{n-1}, :, i_{n+1}, \ldots, i_N)$ is a mode-$n$ fiber of length $I_n$.

The **mode-$n$ unfolding**, denoted $\mathbf{X}_{(n)}$, is a matrix that arranges all the mode-$n$ fibers of the tensor as its columns. The index $i_n$ maps to the row of this matrix, so $\mathbf{X}_{(n)}$ has $I_n$ rows. The remaining $N-1$ indices identify which fiber is being placed in which column. The total number of mode-$n$ fibers is $\prod_{k \neq n} I_k$, so the dimensions of the unfolding are $\mathbf{X}_{(n)} \in \mathbb{R}^{I_n \times \prod_{k \neq n} I_k}$. A consistent ordering convention is crucial. Adopting a column-major (lexicographical) ordering where lower mode indices vary fastest, the mapping from a tensor element $\mathcal{X}(i_1, \ldots, i_N)$ to a matrix entry $(r,c)$ in $\mathbf{X}_{(n)}$ is as follows [@problem_id:3485656]:
- The row index is simply the mode-$n$ index: $r = i_n$.
- The column index $c$ is the linearized index of the remaining $(N-1)$ indices $(i_1, \ldots, i_{n-1}, i_{n+1}, \ldots, i_N)$. If we re-order these indices by their mode number (e.g., $i_1, i_2, \ldots$ excluding $i_n$), the column index $c$ is given by:
$$ c = 1 + \sum_{u=1}^{N-1} (i_{p(u)} - 1) \prod_{v=1}^{u-1} I_{p(v)} $$
where $p: \{1, \ldots, N-1\} \to \{1, \ldots, N\} \setminus \{n\}$ is an index mapping that preserves the ascending order of the modes.

In contrast, **[vectorization](@entry_id:193244)**, denoted $\mathrm{vec}(\mathcal{X})$, flattens the entire tensor into a single column vector of length $\prod_{k=1}^N I_k$. Following the same column-major convention, the linear index $\ell$ corresponding to the element $\mathcal{X}(i_1, \ldots, i_N)$ is given by [@problem_id:3485656]:
$$ \ell = 1 + \sum_{k=1}^N (i_k - 1) \prod_{m=1}^{k-1} I_m $$
Conceptually, $\mathbf{X}_{(n)}$ is a reorganization that preserves and isolates the structure along a specific mode, making it the primary tool for mode-wise analysis and operations. Vectorization, on the other hand, discards all explicit multi-modal structure in favor of a monolithic vector representation, which is useful in different algebraic contexts. Note that $\mathrm{vec}(\mathbf{X}_{(n)})$ is generally a permutation of $\mathrm{vec}(\mathcal{X})$, but they are not identical unless $n=1$ (under our chosen convention).

### The Canonical Polyadic (CP) Decomposition

The Canonical Polyadic (CP) decomposition, also known as CANDECOMP or PARAFAC, provides one of the most fundamental and intuitive models for tensor structure. It expresses a tensor as a sum of a finite number of rank-one tensors.

#### Definition and CP Rank

A [rank-one tensor](@entry_id:202127) is the outer product of vectors. For a third-order tensor, this is $\mathbf{a} \circ \mathbf{b} \circ \mathbf{c}$, where $\circ$ denotes the vector outer product. The CP decomposition of a tensor $\mathcal{X} \in \mathbb{R}^{I \times J \times K}$ is given by:
$$ \mathcal{X} = \sum_{r=1}^R \mathbf{a}_r \circ \mathbf{b}_r \circ \mathbf{c}_r $$
where $\mathbf{a}_r \in \mathbb{R}^I$, $\mathbf{b}_r \in \mathbb{R}^J$, and $\mathbf{c}_r \in \mathbb{R}^K$. This can be compactly represented using factor matrices $A = [\mathbf{a}_1, \ldots, \mathbf{a}_R] \in \mathbb{R}^{I \times R}$, $B = [\mathbf{b}_1, \ldots, \mathbf{b}_R] \in \mathbb{R}^{J \times R}$, and $C = [\mathbf{c}_1, \ldots, \mathbf{c}_R] \in \mathbb{R}^{K \times R}$, often denoted as $\mathcal{X} = \llbracket A, B, C \rrbracket$.

The **CP rank** of a tensor $\mathcal{X}$, denoted $\mathrm{rank}(\mathcal{X})$, is the minimum number of rank-one components $R$ required to represent $\mathcal{X}$ *exactly* [@problem_id:3485653]. Unlike [matrix rank](@entry_id:153017), computing the CP rank is an NP-hard problem in general, and it can depend on whether the decomposition is over real or complex numbers.

#### Fundamental Indeterminacies

The CP representation has two inherent ambiguities: permutation and scaling.
1.  **Permutation Indeterminacy**: The order of the rank-one terms in the summation is arbitrary. Swapping the $r$-th and $s$-th components does not change the resulting tensor. This can be expressed as a simultaneous permutation of the columns of the factor matrices. For any $R \times R$ [permutation matrix](@entry_id:136841) $\Pi$, the decomposition $\llbracket A\Pi, B\Pi, C\Pi \rrbracket$ yields the same tensor as $\llbracket A, B, C \rrbracket$.

2.  **Scaling Indeterminacy**: For any rank-one component $\mathbf{a}_r \circ \mathbf{b}_r \circ \mathbf{c}_r$, we can scale the constituent vectors by non-zero scalars $\alpha_r, \beta_r, \gamma_r$ as long as their product is one: $(\alpha_r \mathbf{a}_r) \circ (\beta_r \mathbf{b}_r) \circ (\gamma_r \mathbf{c}_r) = (\alpha_r \beta_r \gamma_r) (\mathbf{a}_r \circ \mathbf{b}_r \circ \mathbf{c}_r)$. For the component to remain unchanged, we must have $\alpha_r \beta_r \gamma_r = 1$. This can be done independently for each of the $R$ components. Using diagonal scaling matrices $D_1 = \mathrm{diag}(\alpha_1, \ldots, \alpha_R)$, $D_2 = \mathrm{diag}(\beta_1, \ldots, \beta_R)$, and $D_3 = \mathrm{diag}(\gamma_1, \ldots, \gamma_R)$, the decomposition $\llbracket AD_1, BD_2, CD_3 \rrbracket$ is equivalent to $\llbracket A, B, C \rrbracket$ provided that the [element-wise product](@entry_id:185965) of the scaling vectors is the all-ones vector: $\boldsymbol{\alpha} \odot \boldsymbol{\beta} \odot \boldsymbol{\gamma} = \mathbf{1}_R$ [@problem_id:3485653].

For example, for a rank-3 decomposition, scaling vectors such as $\boldsymbol{\alpha}=(2, \frac{1}{3}, -4)$, $\boldsymbol{\beta}=(\frac{1}{2}, 6, \frac{1}{8})$, and $\boldsymbol{\gamma}=(1, \frac{1}{2}, -2)$ constitute a valid transformation, since for each component $r=1,2,3$, the product $\alpha_r \beta_r \gamma_r = 1$.

#### Degrees of Freedom

Understanding these indeterminacies is key to counting the number of free parameters, or **degrees of freedom (DoF)**, of a CP model. The DoF is the dimension of the parameter space after accounting for continuous [reparameterization](@entry_id:270587) symmetries.
1.  The initial number of parameters is the total number of elements in the factor matrices: $N_{params} = IR + JR + KR = R(I+J+K)$.
2.  The continuous scaling indeterminacy introduces redundancy. For each of the $R$ components, we have three scaling factors ($\alpha_r, \beta_r, \gamma_r$) constrained by one equation ($\alpha_r \beta_r \gamma_r = 1$). This leaves two free parameters for each component, leading to a total redundancy of dimension $2R$.
3.  The permutation indeterminacy corresponds to a [discrete symmetry](@entry_id:146994) group ($S_R$), which has dimension 0. Discrete symmetries identify a finite number of points as equivalent but do not create a continuous family of equivalent parameterizations, and thus do not reduce the local dimension of the parameter manifold.

Therefore, the degrees of freedom for a rank-$R$ CP model of an $I \times J \times K$ tensor are [@problem_id:3485670]:
$$ \mathrm{DoF} = N_{params} - N_{redundancy} = R(I+J+K) - 2R = R(I+J+K-2) $$

### The Tucker Decomposition

The Tucker decomposition offers a different perspective on tensor structure, viewing it as a compressed core tensor transformed by factor matrices in each mode. It can be seen as a form of higher-order Principal Component Analysis (PCA).

#### Definition and Multilinear Rank

The Tucker decomposition of a tensor $\mathcal{X} \in \mathbb{R}^{I_1 \times \cdots \times I_N}$ is given by:
$$ \mathcal{X} = \mathcal{G} \times_1 U_1 \times_2 U_2 \cdots \times_N U_N $$
Here, $\mathcal{G} \in \mathbb{R}^{R_1 \times \cdots \times R_N}$ is the **core tensor**, which captures the interactions between the components, and $U_n \in \mathbb{R}^{I_n \times R_n}$ are the **factor matrices**, which represent the principal subspaces for each mode. The operation $\times_n$ denotes the mode-$n$ product of a tensor with a matrix.

The size of the core tensor, $(R_1, \ldots, R_N)$, is known as the **[multilinear rank](@entry_id:195814)** of the decomposition. The [multilinear rank](@entry_id:195814) of the tensor $\mathcal{X}$ itself is the tuple of the ranks of its mode-$n$ unfoldings: $(\mathrm{rank}(\mathbf{X}_{(1)}), \ldots, \mathrm{rank}(\mathbf{X}_{(N)}))$. The Tucker decomposition seeks to find factor matrices $U_n$ such that the data tensor $\mathcal{X}$ is well-approximated by a projection onto the low-dimensional subspaces spanned by their columns.

#### Fundamental Indeterminacies

The indeterminacies of the Tucker model are fundamentally different from those of the CP model and depend critically on the constraints imposed.

-   **Unrestricted Case**: If the core $\mathcal{G}$ and factors $U_n$ are unrestricted, there is a significant ambiguity. For any set of [invertible matrices](@entry_id:149769) $Q_n \in \mathbb{R}^{R_n \times R_n}$, we can define new factors $\tilde{U}_n = U_n Q_n$ and a new core $\tilde{\mathcal{G}} = \mathcal{G} \times_1 Q_1^{-1} \times_2 Q_2^{-1} \cdots \times_N Q_N^{-1}$. This new decomposition $(\tilde{\mathcal{G}}, \{\tilde{U}_n\})$ represents the exact same tensor $\mathcal{X}$. This ambiguity encompasses scaling, rotation, reflection, and shear transformations of the latent component bases [@problem_id:3485669].

-   **Orthonormal Case**: To reduce this ambiguity, it is common practice to constrain the factor matrices to have orthonormal columns, i.e., $U_n^\top U_n = I$. This forces the factors to represent [orthogonal projection](@entry_id:144168) bases. Under this constraint, the transformation matrices $Q_n$ must themselves be orthogonal ($Q_n^\top Q_n = I$). This eliminates scaling and shear ambiguities but preserves rotational and reflectional freedom. To fully resolve this remaining continuous ambiguity, one must impose a canonical structure on the core tensor $\mathcal{G}$, for instance by requiring its slices to be orthogonal and ordered by norm, as is done in the Higher-Order Singular Value Decomposition (HOSVD). This reduces the ambiguity to a [discrete set](@entry_id:146023) of signed permutations [@problem_id:3485669].

#### Degrees of Freedom

For the common case of an orthonormal Tucker model, we can precisely count the degrees of freedom.
1.  The core tensor $\mathcal{G} \in \mathbb{R}^{r_1 \times r_2 \times r_3}$ is unconstrained, so it contributes $r_1 r_2 r_3$ free parameters.
2.  Each factor matrix $U_n \in \mathbb{R}^{I_n \times r_n}$ with orthonormal columns belongs to a **Stiefel manifold**, $\mathrm{St}(I_n, r_n)$. The dimension of this manifold represents its degrees of freedom. An unconstrained $I_n \times r_n$ matrix has $I_n r_n$ parameters. The constraint $U_n^\top U_n = I$ imposes a set of equations on these parameters. Since $U_n^\top U_n$ is a symmetric $r_n \times r_n$ matrix, this corresponds to $\frac{r_n(r_n+1)}{2}$ independent scalar constraints. Thus, the degrees of freedom for each factor matrix are $\mathrm{DoF}(U_n) = I_n r_n - \frac{r_n(r_n+1)}{2}$.

The total degrees of freedom for the orthonormal Tucker model of an $I_1 \times I_2 \times I_3$ tensor are [@problem_id:3485662]:
$$ \mathrm{DoF} = r_1 r_2 r_3 + \sum_{n=1}^3 \left( I_n r_n - \frac{r_n(r_n+1)}{2} \right) $$
For instance, for a $50 \times 40 \times 30$ tensor with [multilinear rank](@entry_id:195814) $(5, 4, 3)$, the total degrees of freedom would be $(5 \cdot 4 \cdot 3) + (50 \cdot 5 - \frac{5 \cdot 6}{2}) + (40 \cdot 4 - \frac{4 \cdot 5}{2}) + (30 \cdot 3 - \frac{3 \cdot 4}{2}) = 60 + 235 + 150 + 84 = 529$.

### Contrasting CP and Tucker: Rank and Structure

While both models decompose a tensor into simpler parts, their structural assumptions are distinct, leading to profound differences in their properties and applications.

#### CP Rank vs. Multilinear Rank

A crucial distinction lies in the concepts of rank. For any tensor $\mathcal{X}$, the CP rank is bounded below by the maximum of its multilinear ranks: $\mathrm{rank}(\mathcal{X}) \geq \max_n(\mathrm{rank}(\mathbf{X}_{(n)}))$. However, the CP rank can be significantly larger than the multilinear ranks.

A classic example illustrates this gap. Consider the $2 \times 2 \times 2$ tensor $\mathcal{T}$ constructed as the sum of three rank-one components whose factor vectors in each mode span the full two-dimensional space. For example, the tensor whose frontal slices are the identity matrix and the standard [symplectic matrix](@entry_id:142706) can be constructed this way. Such a tensor has [multilinear rank](@entry_id:195814) $(2,2,2)$, as its unfoldings will have rank 2. However, its CP rank is 3. This can be proven by examining the [matrix pencil](@entry_id:751760) of its frontal slices, $\mathbf{S}_1 - t\mathbf{S}_2$. The determinant of this pencil is $1+t^2$. For a $2 \times 2 \times 2$ tensor, a CP rank of 2 is possible only if this determinant has real roots for $t$. Since $1+t^2=0$ has no real solutions, the CP rank over the real numbers cannot be 2. Since it is demonstrably not rank 1, and is constructed from 3 components, its CP rank must be 3 [@problem_id:3485666]. This example reveals that the CP model can require more components to capture interactions that are efficiently represented within the Tucker core.

#### Structural Priors and Convex Surrogates

The structural differences between CP and Tucker models are mirrored in the convex optimization frameworks used for tensor completion and denoising.
-   The **CP [atomic norm](@entry_id:746563)**, $\|\mathcal{X}\|_{\mathcal{A}}$, is the natural convex surrogate for CP rank. It is defined as the gauge of the convex hull of unit-norm rank-one tensors. It promotes solutions that are sparse combinations of rank-one "atoms."
-   The **overlapped trace norm**, $\sum_n \|\mathbf{X}_{(n)}\|_\ast$, where $\|\cdot\|_\ast$ is the matrix [nuclear norm](@entry_id:195543) (sum of singular values), is the convex surrogate for the sum of multilinear ranks. It promotes solutions whose unfoldings are low-rank, which is characteristic of the Tucker model.

These two norms favor different tensor structures. Consider the "diagonal" tensor $\mathcal{X} = \mathbf{e}_1 \otimes \mathbf{e}_1 \otimes \mathbf{e}_1 + \mathbf{e}_2 \otimes \mathbf{e}_2 \otimes \mathbf{e}_2$.
-   Its CP [atomic norm](@entry_id:746563) is small, $\|\mathcal{X}\|_{\mathcal{A}} = 2$, because it is constructed from just two unit-norm rank-one components. It is "simple" from a CP perspective.
-   However, its [multilinear rank](@entry_id:195814) is $(2,2,2)$, the maximum possible for a $2 \times 2 \times 2$ tensor. Its unfoldings are all rank-2 matrices, leading to a large overlapped trace norm of $\sum_n \|\mathbf{X}_{(n)}\|_\ast = 2+2+2 = 6$. It is "complex" from a Tucker perspective.
The ratio of these norms, $\rho=3$ in this case, quantifies the gap between the two structural models for this type of tensor [@problem_id:3485673]. Tensors with low CP rank but high [multilinear rank](@entry_id:195814) are common when the factor vectors across components are nearly orthogonal.

### Algorithmic and Theoretical Considerations

The practical application and theoretical understanding of tensor decompositions involve several critical issues, from computational algorithms to the conditions ensuring a unique solution.

#### Alternating Least Squares (ALS) for CP Decomposition

The most common algorithm for computing the CP decomposition is **Alternating Least Squares (ALS)**. It seeks to minimize the squared Frobenius norm of the residual, $\| \mathcal{X} - \llbracket A, B, C \rrbracket \|_F^2$, by cyclically optimizing one factor matrix while keeping the others fixed.

When fixing $B$ and $C$, the objective function becomes a linear [least-squares problem](@entry_id:164198) in $A$. This can be seen most clearly by matricizing the problem. Using the mode-1 unfolding, the objective is equivalent to minimizing $\| \mathbf{X}_{(1)} - A(C \odot B)^\top \|_F^2$, where $\odot$ is the **Khatri-Rao product** (the column-wise Kronecker product). The solution is given by the normal equations:
$$ A = \mathbf{X}_{(1)} (C \odot B) \left( (C \odot B)^\top (C \odot B) \right)^{-1} $$
The term $\mathbf{X}_{(1)} (C \odot B)$ is a computationally crucial quantity known as the **Matricized Tensor Times Khatri-Rao Product (MTTKRP)**. The matrix to be inverted has a remarkably elegant structure. It can be proven that [@problem_id:3485665]:
$$ (C \odot B)^\top (C \odot B) = (C^\top C) * (B^\top B) $$
where $*$ denotes the element-wise **Hadamard product**. This identity, which relies on the fact that the Hadamard product is commutative, allows the computationally expensive inverse to be replaced by the inverse of a Hadamard product of smaller Gram matrices, forming the basis of efficient ALS implementations. The updates for $B$ and $C$ follow by symmetry.

#### Identifiability and Uniqueness of CP Decomposition

A key advantage of the CP decomposition is its potential for uniqueness, a property not generally shared by matrix factorizations. Under relatively mild conditions, the factor matrices are uniquely determined up to the inherent permutation and scaling ambiguities. The foundational result is **Kruskal's theorem**, which provides a sufficient condition for uniqueness based on the **Kruskal rank** (or k-rank) of the factor matrices. The k-[rank of a matrix](@entry_id:155507) is the maximum number $k$ such that any $k$ columns are linearly independent. For a third-order rank-$R$ decomposition $\llbracket A, B, C \rrbracket$, uniqueness is guaranteed if:
$$ k_A + k_B + k_C \geq 2R + 2 $$

When this condition is not met, the decomposition may not be unique. A classic case of non-uniqueness arises when a factor matrix has collinear columns, which lowers its k-rank and can cause the condition to fail. For example, consider a rank-$R$ decomposition where two columns in the third factor matrix are identical, $\mathbf{c}_1 = \mathbf{c}_2$. This implies $k_C=1$. Even if $k_A$ and $k_B$ are high, the sum may easily fall below $2R+2$, thus violating the condition. In such cases of failure, this scenario admits an entire family of alternative factorizations that produce the same tensor. A transformation of the form $\mathbf{a}'_1 = \mathbf{a}_1 + t \mathbf{a}_2$ and $\mathbf{b}'_2 = \mathbf{b}_2 - t \mathbf{b}_1$ (with $\mathbf{b}'_1=\mathbf{b}_1, \mathbf{a}'_2=\mathbf{a}_2$) creates cross-terms that cancel out precisely because they share the same factor vector $\mathbf{c}$ in the third mode [@problem_id:3485686]. This demonstrates a specific mechanism through which uniqueness can fail.

#### Ill-Posedness and Degeneracy in CP Approximation

While the CP decomposition of a tensor of a given rank is often unique, the problem of finding the *best [low-rank approximation](@entry_id:142998)* is notoriously ill-posed. The set of tensors with CP rank at most $R$ (for $R>1$) is not a [closed set](@entry_id:136446). This means that a sequence of rank-$R$ tensors can converge to a limit tensor that has a rank greater than $R$.

This phenomenon can lead to **degeneracy** or **swamping** in [approximation algorithms](@entry_id:139835). It is possible to construct a sequence of rank-2 tensors, $\mathcal{X}(t)$, that converge to a rank-3 tensor $\mathcal{T}$ as a parameter $t \to 0$. In a typical construction, the factor weights diverge (e.g., scale as $1/t$), but their contributions almost perfectly cancel, leaving a finite residual that vanishes as $t \to 0$. The [objective function](@entry_id:267263) $\|\mathcal{T} - \mathcal{X}(t)\|_F^2$ decreases towards zero, yet the norms of the factor components diverge to infinity [@problem_id:3485668].

This behavior causes severe practical problems for algorithms like ALS. As the approximation approaches degeneracy, the factor vectors in each mode become nearly collinear. This leads to the Gram matrices in the ALS [normal equations](@entry_id:142238), such as $(C^\top C) * (B^\top B)$, becoming nearly singular. The [ill-conditioning](@entry_id:138674) of these linear subproblems results in extremely slow convergence and long "plateaus" where the objective function makes negligible progress. This [ill-posedness](@entry_id:635673) is a defining challenge of the CP model and a key difference from the Tucker model, whose [best approximation problem](@entry_id:139798) is well-posed.