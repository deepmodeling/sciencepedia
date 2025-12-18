## Introduction
In an era of increasingly complex and [high-dimensional data](@entry_id:138874), traditional matrix-based methods often fall short. Multi-way data, or tensors, are now ubiquitous, appearing in fields from signal processing to machine learning. The CANDECOMP/PARAFAC (CP) decomposition has emerged as a fundamental tool for analyzing such data, offering a powerful way to break down intricate structures into a parsimonious sum of interpretable components. However, the transition from two-way matrices to multi-way tensors introduces significant theoretical complexities; concepts like rank, uniqueness, and numerical stability behave in ways that can be counter-intuitive. This article aims to demystify these core concepts, providing a rigorous yet accessible guide to the theory and application of the CP model.

This exploration is structured into three distinct parts. The first chapter, "Principles and Mechanisms," lays the theoretical groundwork, formally defining the CP decomposition and delving into the subtle yet crucial notions of [tensor rank](@entry_id:266558), the conditions for uniqueness established by Kruskal's theorem, and pathological behaviors like degeneracy and [border rank](@entry_id:201708). The second chapter, "Applications and Interdisciplinary Connections," bridges theory and practice by showcasing how the CP model is used to solve real-world problems in [chemometrics](@entry_id:154959), signal processing, and machine learning, demonstrating the practical value of its unique properties. Finally, the "Hands-On Practices" chapter provides a set of guided problems designed to solidify your understanding of [tensor rank](@entry_id:266558), uniqueness, and the challenges of [low-rank approximation](@entry_id:142998), translating abstract theory into tangible computational skills.

## Principles and Mechanisms

The CANDECOMP/PARAFAC (CP) decomposition is a cornerstone of [multilinear algebra](@entry_id:199321), providing a powerful model for analyzing multi-way data. It represents a tensor as a sum of a minimal number of rank-1 components. This chapter delves into the foundational principles and mechanisms governing this decomposition, exploring the rich and often subtle concepts of [tensor rank](@entry_id:266558), uniqueness, and the challenging behaviors that can arise in practice.

### The CANDECOMP/PARAFAC (CP) Decomposition

At its core, the CP decomposition expresses an $N$-way tensor as a [linear combination](@entry_id:155091) of simpler, rank-1 tensors.

#### Definition and Element-wise Form

An order-$N$ tensor $\mathcal{X} \in \mathbb{R}^{I_1 \times \cdots \times I_N}$ is said to have a **Canonical Polyadic (CP) decomposition** of length $R$ if it can be expressed as a sum of $R$ rank-1 tensors. A **rank-1 tensor** is the outer product of $N$ vectors, denoted $a^{(1)} \otimes \cdots \otimes a^{(N)}$, where each vector $a^{(n)} \in \mathbb{R}^{I_n}$. The decomposition is thus written as:
$$
\mathcal{X} = \sum_{r=1}^{R} a_r^{(1)} \otimes a_r^{(2)} \otimes \cdots \otimes a_r^{(N)}
$$
The vectors $a_r^{(n)}$ are collected as columns into **factor matrices** $A^{(n)} = [a_1^{(n)} \ \cdots \ a_R^{(n)}] \in \mathbb{R}^{I_n \times R}$.

To understand this structure at the most fundamental level, we can derive the expression for an individual element of the tensor $\mathcal{X}$. By the definition of the [outer product](@entry_id:201262), the $(i_1, \dots, i_N)$-th element of a single rank-1 tensor $a_r^{(1)} \otimes \cdots \otimes a_r^{(N)}$ is the product of the corresponding elements of its constituent vectors: $\prod_{n=1}^{N} (a_r^{(n)})_{i_n}$. Since tensor addition is element-wise, the corresponding element of $\mathcal{X}$ is the sum over all $R$ rank-1 terms . This gives the fundamental element-wise equation for the CP model:
$$
(\mathcal{X})_{i_1, \dots, i_N} = \sum_{r=1}^{R} \prod_{n=1}^{N} (a_r^{(n)})_{i_n}
$$
Recognizing that $(a_r^{(n)})_{i_n}$ is the entry in the $i_n$-th row and $r$-th column of the factor matrix $A^{(n)}$, we can write this as:
$$
(\mathcal{X})_{i_1, \dots, i_N} = \sum_{r=1}^{R} \prod_{n=1}^{N} (A^{(n)})_{i_n, r}
$$

#### Matricized Form and the Khatri-Rao Product

While the element-wise form is definitionally primary, much of the theory and computational practice for tensors relies on **[matricization](@entry_id:751739)**, or the unfolding of a tensor into a matrix. The **mode-$n$ unfolding**, denoted $X_{(n)}$, is a matrix of size $I_n \times (\prod_{k \neq n} I_k)$ whose columns are the mode-$n$ fibers of $\mathcal{X}$. A mode-$n$ fiber is a vector obtained by fixing all indices except the $n$-th one.

The matricized form of the CP decomposition reveals a deep connection to a special matrix product. To express this, we must first define the **Khatri-Rao product**, denoted by $\odot$. For two matrices $A \in \mathbb{R}^{I \times R}$ and $B \in \mathbb{R}^{J \times R}$ with the same number of columns, their Khatri-Rao product $A \odot B$ is a matrix of size $(IJ) \times R$ formed by the column-wise Kronecker products of their columns:
$$
(A \odot B)_{:, r} = A_{:, r} \otimes B_{:, r}
$$
This operation is associative. By substituting the element-wise CP formula into the definition of the mode-$n$ unfolding, a crucial identity emerges. The mode-$n$ unfolding of $\mathcal{X}$ can be written in a compact matrix form involving its factor matrices :
$$
X_{(n)} = A^{(n)} \left( A^{(N)} \odot \cdots \odot A^{(n+1)} \odot A^{(n-1)} \odot \cdots \odot A^{(1)} \right)^{\top}
$$
This identity is central to the popular Alternating Least Squares (ALS) algorithm for computing the CP decomposition and provides the algebraic foundation for analyzing the properties of the model. The specific ordering of the factor matrices within the Khatri-Rao product depends on the convention used for ordering the columns of the unfolding. The order given here corresponds to a standard [lexicographical ordering](@entry_id:143032) of the indices $(i_N, \dots, i_{n+1}, i_{n-1}, \dots, i_1)$ with the first index varying fastest.

### The Notion of Tensor Rank

Unlike matrices, tensors are associated with several different notions of rank. Disambiguating these concepts is essential for a correct understanding of tensor decompositions.

#### CP Rank

The most fundamental notion is the **CP rank**, often referred to simply as **[tensor rank](@entry_id:266558)**. It is defined as the smallest integer $R$ for which a CP decomposition of a tensor $\mathcal{X}$ exists. We denote it by $\operatorname{rank}_{CP}(\mathcal{X})$. Finding the rank of a general tensor is an NP-hard problem, and many of its mathematical properties are subjects of ongoing research.

#### Multilinear Rank

A different and computationally more tractable concept is the **[multilinear rank](@entry_id:195814)**. The [multilinear rank](@entry_id:195814) of an order-$N$ tensor $\mathcal{X}$ is the $N$-tuple $(r_1, r_2, \dots, r_N)$, where each component $r_n$ is the rank of the corresponding mode-$n$ unfolding:
$$
r_n = \operatorname{rank}(X_{(n)})
$$
The [multilinear rank](@entry_id:195814) corresponds to the dimensions of the core tensor in the **Tucker decomposition**, another fundamental tensor model that represents a tensor $\mathcal{X}$ as a multilinear product of a core tensor $\mathcal{G} \in \mathbb{R}^{r_1 \times \cdots \times r_N}$ and orthogonal factor matrices $U^{(n)} \in \mathbb{R}^{I_n \times r_n}$. The integers $r_n$ are the smallest possible dimensions for such an exact representation .

#### The Relationship Between Ranks

The CP rank and [multilinear rank](@entry_id:195814) are related, but they are not equivalent. A rank-1 tensor provides the simplest case: a non-zero tensor $\mathcal{X}$ has CP rank 1 if and only if its [multilinear rank](@entry_id:195814) is $(1, 1, \dots, 1)$ . That is, $\operatorname{rank}_{CP}(\mathcal{X}) = 1 \iff \operatorname{rank}(X_{(n)}) = 1$ for all $n \in \{1, \dots, N\}$.

However, this simple correspondence breaks down for higher ranks. One might hypothesize that if the rank of at least one unfolding is 1, the tensor's CP rank might also be 1. This is not true. Consider a hypothetical third-order tensor $\mathcal{X} = a_1 \otimes b \otimes c_1 + a_2 \otimes b \otimes c_2$, where $\{a_1, a_2\}$ and $\{c_1, c_2\}$ are linearly independent sets of vectors, and $b$ is a non-[zero vector](@entry_id:156189) .
- The mode-1 unfolding $X_{(1)}$ has a column space spanned by $\{a_1, a_2\}$, so its rank is 2.
- The mode-3 unfolding $X_{(3)}$ has a [column space](@entry_id:150809) spanned by $\{c_1, c_2\}$, so its rank is 2.
- However, every mode-2 fiber of this tensor is a scalar multiple of the vector $b$. Consequently, the mode-2 unfolding $X_{(2)}$ has a [column space](@entry_id:150809) spanned only by $b$, and its rank is 1.
The [multilinear rank](@entry_id:195814) of this tensor is $(2, 1, 2)$. Since not all components are 1, its CP rank is greater than 1. This example definitively shows that having a rank-1 unfolding in one mode does not imply the tensor has CP rank 1.

In the general case, the ranks are related by a set of important inequalities. For any tensor $\mathcal{X}$ with CP rank $R$ and [multilinear rank](@entry_id:195814) $(r_1, \dots, r_N)$, we have the lower bound:
$$
R \ge \max_{1 \le n \le N} r_n
$$
This inequality holds because the column space of the unfolding $X_{(n)}$ is contained within the span of the columns of the factor matrix $A^{(n)}$, whose dimension cannot exceed $R$ . While this bound is fundamental, it can be very loose. There are cases where the CP rank is strictly greater than the rank of any of its unfoldings. A well-known result from algebraic geometry shows that a generic $3 \times 3 \times 3$ tensor over the complex numbers has a maximal unfolding rank of 3, but its CP rank is 5 . This gap highlights the inherent complexity of [tensor rank](@entry_id:266558) compared to [matrix rank](@entry_id:153017).

An upper bound, though often not tight, is given by the product of the multilinear ranks, $R \le \prod_{n=1}^N r_n$ . This follows from representing the tensor in its minimal Tucker form and then expressing the core tensor as a sum of its elements.

### Uniqueness of the CP Decomposition

One of the most compelling features of the CP decomposition, and a primary reason for its widespread use in signal processing, [chemometrics](@entry_id:154959), and neuroscience, is its **uniqueness** under mild conditions. Unlike matrix factorizations such as PCA or SVD, which have rotational ambiguities, the CP decomposition can often recover the underlying components of a signal uniquely, up to trivial scaling and permutation ambiguities.

**Essential uniqueness** refers to the fact that if a tensor $\mathcal{X}$ has a unique rank-$R$ CP decomposition, then any two such decompositions, say with factor matrices $(A, B, C)$ and $(\tilde{A}, \tilde{B}, \tilde{C})$, are related by a permutation of their columns and a scaling of the vectors within each component. That is, there exists a [permutation matrix](@entry_id:136841) $P$ and diagonal scaling matrices $D_A, D_B, D_C$ with $D_A D_B D_C = I$ such that $\tilde{A} = A P D_A$, $\tilde{B} = B P D_B$, and $\tilde{C} = C P D_C$.

#### Kruskal's Theorem

The foundational result on the uniqueness of the CP decomposition is Kruskal's theorem. It provides a sufficient condition for uniqueness based on a property of the factor matrices called the **k-rank**. The k-[rank of a matrix](@entry_id:155507) $A$, denoted $k(A)$, is the largest integer $k$ such that every subset of $k$ columns of $A$ is linearly independent . Note that $k(A) \le \operatorname{rank}(A)$.

For a third-order tensor $\mathcal{X}$ with a rank-$R$ CP decomposition defined by factor matrices $A, B, C$, Kruskal's theorem states that the decomposition is essentially unique if:
$$
k(A) + k(B) + k(C) \ge 2R + 2
$$
For example, consider a tensor $\mathcal{X} \in \mathbb{R}^{3 \times 3 \times 2}$ constructed from two components ($R=2$) with factor matrices $A, B, C$ whose columns are pairwise linearly independent. In this case, the k-rank of each factor matrix is 2. The sum of the k-ranks is $k(A) + k(B) + k(C) = 2 + 2 + 2 = 6$. The condition requires this sum to be at least $2R+2 = 2(2)+2=6$. Since $6 \ge 6$, the condition is satisfied, and the rank-2 decomposition of this tensor is guaranteed to be essentially unique .

#### Uniqueness and Its Distinction from Matrix Factorization

The stringent uniqueness property of CP decomposition marks a profound departure from [matrix factorization](@entry_id:139760). This can be understood by examining the ambiguity in [low-rank matrix approximation](@entry_id:751514) . Suppose we have a matrix $X_{(1)}$ of rank $R$ that we factorize as $X_{(1)} = \hat{A} M^\top$, where $\hat{A}$ and $M$ both have $R$ columns. This factorization is never unique. For any [invertible matrix](@entry_id:142051) $Q \in \mathbb{R}^{R \times R}$, the pair $(\hat{A}Q, M Q^{-\top})$ provides an equally valid factorization:
$$
(\hat{A}Q)(M Q^{-\top})^\top = (\hat{A}Q)(Q^{-1}M^\top) = \hat{A} M^\top = X_{(1)}
$$
The set of all such [invertible matrices](@entry_id:149769) $Q$ forms the [general linear group](@entry_id:141275) $\mathrm{GL}(R)$, a continuous group with dimension $R^2$.

Now, consider the case where $X_{(1)}$ is the unfolding of a tensor with a unique CP decomposition, so $X_{(1)} = A (C \odot B)^\top$. The [matrix factorization](@entry_id:139760) finds factors $\hat{A} = AQ$ and $M = (C \odot B) Q^{-\top}$. The crucial insight is that for a general invertible matrix $Q$, the new matrix $M$ will no longer have the structure of a Khatri-Rao product. Its columns will be [linear combinations](@entry_id:154743) of the columns of $C \odot B$, and these mixed columns generally cannot be represented as single Kronecker products of vectors. The component-wise structure of modes $B$ and $C$ is lost.

The CP model's structure is only preserved if $Q$ belongs to the much smaller group of scaled permutation matrices. The continuous part of this group is the set of invertible [diagonal matrices](@entry_id:149228), which has dimension $R$. The "loss of identifiability" when moving from a tensor model to a simple [matrix factorization](@entry_id:139760) of an unfolding can be quantified by the difference in the dimensions of the ambiguity groups: $\dim(\mathrm{GL}(R)) - \dim(\text{Diagonal matrices}) = R^2 - R$. This highlights the powerful structural constraint imposed by the tensor model, which is the very source of its uniqueness.

### Pathological Behavior: Degeneracy and Border Rank

Despite its power, the CP model exhibits some challenging behaviors. The most notable is the phenomenon of **degeneracy**, which is tied to the concept of **[border rank](@entry_id:201708)**.

#### Rank, Border Rank, and Non-Closed Sets

Let $S_R$ be the set of all tensors with CP rank at most $R$. One might intuitively assume that this set is topologically closed; that is, if a sequence of tensors $\{ \mathcal{X}_k \}_{k=1}^\infty$ with each $\mathcal{X}_k \in S_R$ converges to a limit $\mathcal{X}$, then $\mathcal{X}$ must also be in $S_R$. This is not always true. The set $S_R$ is not always closed.

This fact gives rise to the definition of **[border rank](@entry_id:201708)**. The border [rank of a tensor](@entry_id:204291) $\mathcal{X}$, denoted $\operatorname{brank}(\mathcal{X})$, is the smallest integer $R$ such that $\mathcal{X}$ is a limit point of a sequence of tensors of rank at most $R$. By definition, we always have $\operatorname{brank}(\mathcal{X}) \le \operatorname{rank}_{CP}(\mathcal{X})$. When this inequality is strict, i.e., $\operatorname{brank}(\mathcal{X})  \operatorname{rank}_{CP}(\mathcal{X})$, we encounter significant theoretical and computational issues.

#### The Mechanism of Degeneracy

The mechanism that allows a sequence of rank-$R$ tensors to converge to a tensor of rank greater than $R$ is known as **degeneracy**. A sequence of CP factorizations $\{(A^{(k)}, B^{(k)}, C^{(k)})\}$ is called degenerate if the reconstructed tensors $\mathcal{X}^{(k)}$ converge to a finite limit $\mathcal{X}$, but at least one of the factor matrices has norms that diverge to infinity . This divergence cannot be resolved by the standard scaling ambiguity of the CP model. In essence, two or more of the rank-1 components in the sum become nearly linearly dependent and grow infinitely large, but in opposing directions, such that their sum cancels to produce a finite, well-behaved contribution to the limit tensor.

A classic example can be constructed to illustrate this . Consider the sequence of rank-2 tensors for $\varepsilon > 0$:
$$
\mathcal{X}_{\varepsilon} = \frac{1}{\varepsilon} \left( (e_1 + \varepsilon e_2) \otimes (e_1 + \varepsilon e_2) \otimes (e_1 + \varepsilon e_2) - e_1 \otimes e_1 \otimes e_1 \right)
$$
As $\varepsilon \to 0$, expanding the outer product reveals that the terms proportional to $1/\varepsilon$ cancel, and the limit is:
$$
\lim_{\varepsilon \to 0} \mathcal{X}_{\varepsilon} = e_2 \otimes e_1 \otimes e_1 + e_1 \otimes e_2 \otimes e_1 + e_1 \otimes e_1 \otimes e_2 = \mathcal{X}
$$
The limit tensor $\mathcal{X}$ can be proven to have CP rank 3. Yet, it is the limit of a sequence of tensors of rank at most 2. Therefore, for this tensor $\mathcal{X}$, we have $\operatorname{brank}(\mathcal{X}) = 2$ while $\operatorname{rank}_{CP}(\mathcal{X}) = 3$. The norms of the factors in the construction of $\mathcal{X}_\varepsilon$ diverge as $1/\varepsilon$, demonstrating the mechanism of degeneracy.

#### Consequences of Degeneracy

The existence of tensors whose rank exceeds their [border rank](@entry_id:201708) has profound consequences. Firstly, it means the problem of finding the best rank-$R$ approximation to a tensor may not have a solution . If a tensor $\mathcal{X}$ has $\operatorname{brank}(\mathcalX) = R$ but $\operatorname{rank}_{CP}(\mathcal{X}) > R$, then the infimum of the [approximation error](@entry_id:138265) is zero:
$$
\inf \{ \|\mathcal{X} - \mathcal{Y}\|_F : \operatorname{rank}_{CP}(\mathcal{Y}) \le R \} = 0
$$
However, since $\mathcal{X}$ itself does not have rank $R$, this [infimum](@entry_id:140118) is never attained. There is no "best" rank-$R$ approximation . Secondly, this phenomenon poses a major challenge for computational algorithms like ALS. When trying to fit a rank-$R$ model to data that is close to a degenerate tensor, the algorithm may exhibit extreme [ill-conditioning](@entry_id:138674), with factor norms diverging as it attempts to reach an unattainable solution.

### Field Dependence and Typical Ranks

A final, often surprising, property of [tensor rank](@entry_id:266558) is its dependence on the underlying field, i.e., whether we are working with real numbers ($\mathbb{R}$) or complex numbers ($\mathbb{C}$).

#### Typical Ranks

Over an [algebraically closed field](@entry_id:151401) like $\mathbb{C}$, there is usually a single **generic rank**, which is the rank that holds for all tensors except for those on a lower-dimensional subvariety. This is the unique **typical rank**. Over $\mathbb{R}$, which is not algebraically closed, the situation can be more complex. We define a typical rank as any rank $r$ for which the set of tensors of rank $r$ contains a non-empty open set in the Euclidean topology. Over $\mathbb{R}$, there can be more than one typical rank .

#### The 2x2x2 Case

The space of $2 \times 2 \times 2$ tensors provides a canonical illustration of this field dependence.
Over the complex numbers $\mathbb{C}$, the generic rank is 2. A generic $\mathcal{X} \in \mathbb{C}^{2 \times 2 \times 2}$ has $\operatorname{rank}_{CP}(\mathcal{X}) = 2$.
Over the real numbers $\mathbb{R}$, the behavior is governed by a polynomial in the tensor entries known as the **Cayley hyperdeterminant**, $\operatorname{Det}(\mathcal{X})$. This polynomial divides the space $\mathbb{R}^{2 \times 2 \times 2}$ into regions with different ranks:
-   If $\operatorname{Det}(\mathcal{X}) > 0$, the tensor has real rank 2. This region is a non-empty open set.
-   If $\operatorname{Det}(\mathcal{X})  0$, the tensor has real rank 3. This region is also a non-empty open set.
-   If $\operatorname{Det}(\mathcal{X}) = 0$, the tensor lies on the boundary and has [border rank](@entry_id:201708) 2 (or less).

Because both rank 2 and rank 3 occur on open sets of positive volume in the space of real $2 \times 2 \times 2$ tensors, we say that this space has two typical ranks: 2 and 3. This striking difference between the real and complex cases underscores the intricate geometry of tensor spaces and serves as a caution that results proven over one field may not necessarily hold over another.