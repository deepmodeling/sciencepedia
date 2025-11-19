## Introduction
In an age of increasingly complex and [high-dimensional data](@entry_id:138874), traditional two-dimensional matrices are often insufficient to capture the rich, multi-way relationships inherent in scientific and engineering datasets. Tensors, or multi-way arrays, provide a natural framework for representing such data. However, their complexity presents a significant analytical challenge: how do we extract meaningful patterns and latent structure from these dense objects? Tensor decomposition provides the answer, offering a suite of powerful techniques to break down a tensor into a set of simpler, more interpretable components. This article serves as a comprehensive guide to these fundamental methods, addressing the need for a clear understanding of their mechanics and utility.

Across the following sections, you will gain a deep understanding of tensor decompositions. We will begin by exploring the foundational "Principles and Mechanisms" of the two most prominent models, the Canonical Polyadic (CP) and Tucker decompositions. Next, we will witness their power in action by examining their diverse "Applications and Interdisciplinary Connections," from signal processing and machine learning to quantum physics. Finally, you will have the opportunity to solidify your knowledge and bridge theory with practice through a series of "Hands-On Practices" designed to build your computational skills.

## Principles and Mechanisms

Having established the motivation for tensor decompositions, we now turn to the foundational principles and mechanisms that govern these powerful techniques. This chapter will deconstruct the two most prominent models, the Canonical Polyadic (CP) and Tucker decompositions, by examining their core mathematical structures, their fundamental operators, and the critical differences in their properties that guide their application in [scientific computing](@entry_id:143987) and data analysis.

### The Rank-One Tensor: The Fundamental Building Block

At the heart of [tensor decomposition](@entry_id:173366) lies the concept of the **[rank-one tensor](@entry_id:202127)**. Just as any matrix can be conceptualized in terms of rank-one matrices, any higher-order tensor can be described in terms of rank-one tensors. A [rank-one tensor](@entry_id:202127) is the simplest type of tensor beyond a scalar, formed by the **outer product** of vectors.

For a third-order tensor $\mathcal{T} \in \mathbb{R}^{I \times J \times K}$, if it is of rank one, it can be expressed as the [outer product](@entry_id:201262) of three vectors: $\mathbf{u} \in \mathbb{R}^{I}$, $\mathbf{v} \in \mathbb{R}^{J}$, and $\mathbf{w} \in \mathbb{R}^{K}$. We denote this as:
$$
\mathcal{T} = \mathbf{u} \circ \mathbf{v} \circ \mathbf{w}
$$
In this construction, each element $T_{ijk}$ of the tensor is simply the product of the corresponding elements from the constituent vectors. This component-wise definition is expressed as:
$$
T_{ijk} = u_i v_j w_k
$$
This structure implies that all the information within the tensor is encoded in these three vectors. For instance, in a materials science context, a property tensor might be constructed from characteristic vectors representing fundamental directions in a crystal lattice. Calculating tensor elements becomes a straightforward multiplication of vector components [@problem_id:1542448]. This elemental simplicity is what makes the [rank-one tensor](@entry_id:202127) the fundamental atom from which more complex tensor structures are built.

### The Canonical Polyadic (CP) Decomposition

While rank-one tensors are simple, most real-world data are far more complex. The first major decomposition model, the **Canonical Polyadic (CP) decomposition**, also known as **CANDECOMP** (Canonical Decomposition) or **PARAFAC** (Parallel Factors), proposes that any tensor can be expressed as a finite sum of rank-one tensors.

#### Decomposition as a Sum of Rank-One Tensors

The CP model represents a tensor $\mathcal{X} \in \mathbb{R}^{I \times J \times K}$ as a sum of $R$ rank-one tensors:
$$
\mathcal{X} = \sum_{r=1}^{R} \lambda_r (\mathbf{a}_r \circ \mathbf{b}_r \circ \mathbf{c}_r)
$$
Here, $\mathbf{a}_r \in \mathbb{R}^{I}$, $\mathbf{b}_r \in \mathbb{R}^{J}$, and $\mathbf{c}_r \in \mathbb{R}^{K}$ are the factor vectors for the $r$-th component, and $\lambda_r$ are scalar weights, which are often absorbed into one of the factor vectors for convenience. The vectors for each mode are typically collected as columns into **factor matrices** $\mathbf{A} \in \mathbb{R}^{I \times R}$, $\mathbf{B} \in \mathbb{R}^{J \times R}$, and $\mathbf{C} \in \mathbb{R}^{K \times R}$. The element-wise formula for reconstructing the tensor from these factor matrices is a direct extension of the rank-one case [@problem_id:1542379]:
$$
X_{ijk} = \sum_{r=1}^{R} A_{ir} B_{jr} C_{kr}
$$
In applications, each of the $R$ components can be interpreted as a latent factor or pattern that is present in the data, with the columns of $\mathbf{A}$, $\mathbf{B}$, and $\mathbf{C}$ describing how this pattern is expressed across each mode.

#### CP Rank

The central concept associated with the CP decomposition is the **[tensor rank](@entry_id:266558)** or **CP rank**. It is defined as the smallest integer $R$ such that $\mathcal{X}$ can be written exactly as a sum of $R$ rank-one tensors. This is the direct generalization of [matrix rank](@entry_id:153017) to [higher-order tensors](@entry_id:183859). However, the analogy can be deceptive, as [tensor rank](@entry_id:266558) has several properties that are surprisingly different from [matrix rank](@entry_id:153017).

It is crucial to distinguish the CP rank from other related concepts [@problem_id:3282193]. First, it is not the same as the **Tucker rank**, which we will discuss shortly. Second, unlike for matrices, the CP rank is not generally equal to the rank of the matrix unfoldings of the tensor. Third, the rank of a real-valued tensor can actually decrease if one is allowed to use complex-valued factor vectors. Finally, and most subtly, the set of tensors with a CP rank less than or equal to a given $R$ (for $R>1$) is not a topologically closed set, giving rise to the notion of **[border rank](@entry_id:201708)**.

#### Matricized Form and the Khatri-Rao Product

To work with tensor decompositions algorithmically, it is often necessary to rearrange the tensor's elements into a matrix, a process known as **[matricization](@entry_id:751739)** or **unfolding**. The mode-1 unfolding of $\mathcal{X}$, denoted $\mathbf{X}_{(1)}$, is an $I \times (JK)$ matrix where each of the $I$ rows contains the elements of a horizontal slice of the tensor.

A key algebraic tool for expressing the CP decomposition in this matricized form is the **Khatri-Rao product**, denoted by $\odot$. For two matrices with the same number of columns, say $\mathbf{C} \in \mathbb{R}^{K \times R}$ and $\mathbf{B} \in \mathbb{R}^{J \times R}$, their Khatri-Rao product $\mathbf{C} \odot \mathbf{B}$ is a $(KJ) \times R$ matrix formed by taking the Kronecker product of their corresponding columns. For instance, the $r$-th column of the product matrix is the Kronecker product of the $r$-th column of $\mathbf{C}$ and the $r$-th column of $\mathbf{B}$ [@problem_id:1542398].

Using this product, the CP decomposition can be written elegantly in terms of its unfoldings. For example, the mode-1 unfolding has the compact form:
$$
\mathbf{X}_{(1)} = \mathbf{A} (\mathbf{C} \odot \mathbf{B})^T
$$
This [matrix equation](@entry_id:204751) is the foundation for many computational algorithms for finding the CP decomposition, such as Alternating Least Squares (ALS).

### The Tucker Decomposition

The Tucker decomposition offers a more general and flexible model for tensor approximation. Instead of a strict sum of rank-one components, it represents a tensor as a multilinear transformation of a smaller, dense **core tensor**.

#### A Generalization: Core Tensors and Factor Subspaces

The Tucker decomposition expresses a tensor $\mathcal{X} \in \mathbb{R}^{I_1 \times I_2 \times I_3}$ in terms of a core tensor $\mathcal{G} \in \mathbb{R}^{R_1 \times R_2 \times R_3}$ and a set of factor matrices $\mathbf{A}^{(n)} \in \mathbb{R}^{I_n \times R_n}$ for each mode $n=1, 2, 3$. The model is written using the mode-n product, which we will define shortly:
$$
\mathcal{X} \approx \mathcal{G} \times_1 \mathbf{A}^{(1)} \times_2 \mathbf{A}^{(2)} \times_3 \mathbf{A}^{(3)}
$$
The factor matrices can be thought of as defining a principal subspace for each mode, and the core tensor $\mathcal{G}$ governs the interactions between these subspaces. The element-wise reconstruction formula is a sum over all combinations of components from the factor matrices, weighted by the elements of the core tensor [@problem_id:1542413]:
$$
X_{i_1 i_2 i_3} = \sum_{r_1=1}^{R_1} \sum_{r_2=1}^{R_2} \sum_{r_3=1}^{R_3} g_{r_1 r_2 r_3} A^{(1)}_{i_1 r_1} A^{(2)}_{i_2 r_2} A^{(3)}_{i_3 r_3}
$$

#### The Mode-n Product

The fundamental operation in the Tucker model is the **mode-n product**, denoted $\mathcal{X} \times_n \mathbf{A}$. This operation applies a [linear map](@entry_id:201112), represented by the matrix $\mathbf{A}$, to the mode-$n$ fibers of the tensor $\mathcal{X}$. A **mode-n fiber** is the vector obtained by fixing all indices except for the $n$-th index.

Formally, if $\mathcal{X} \in \mathbb{R}^{I_1 \times \dots \times I_n \times \dots \times I_N}$ and $\mathbf{A} \in \mathbb{R}^{J_n \times I_n}$, the mode-$n$ product $\mathcal{Y} = \mathcal{X} \times_n \mathbf{A}$ results in a tensor $\mathcal{Y} \in \mathbb{R}^{I_1 \times \dots \times J_n \times \dots \times I_N}$. Its elements are given by:
$$
Y_{i_1 \dots j_n \dots i_N} = \sum_{k=1}^{I_n} X_{i_1 \dots k \dots i_N} A_{j_n k}
$$
This operation exhibits several important properties, such as [associativity](@entry_id:147258) with matrix multiplication, which is key to the consistency of the Tucker model. For instance, applying two successive transformations along the same mode is equivalent to applying a single transformation with the product of the matrices: $(\mathcal{X} \times_n \mathbf{A}) \times_n \mathbf{B} = \mathcal{X} \times_n (\mathbf{B}\mathbf{A})$ [@problem_id:3282074].

#### Unfolding and Multilinear Rank

The dimensions of the core tensor, $(R_1, R_2, R_3)$, are a crucial aspect of the Tucker model and define another notion of rank known as the **[multilinear rank](@entry_id:195814)** or **Tucker rank**. The [multilinear rank](@entry_id:195814) of a tensor $\mathcal{X}$ is the tuple containing the ranks of its matrix unfoldings. Specifically, $R_n = \text{rank}(\mathbf{X}_{(n)})$. One can compute the [multilinear rank](@entry_id:195814) of a tensor by constructing each of its unfoldings and calculating their respective matrix ranks [@problem_id:1542439]. The Tucker decomposition is most effective when the [multilinear rank](@entry_id:195814) $(R_1, R_2, R_3)$ is significantly smaller than the original dimensions $(I_1, I_2, I_3)$, allowing for substantial [data compression](@entry_id:137700).

### Unification and Comparison of Models

While CP and Tucker decompositions appear structurally different, they are deeply related. Understanding this relationship, along with their contrasting properties regarding uniqueness, is essential for choosing the appropriate model for a given task.

#### Structural Relationship: CP as a Special Case of Tucker

A CP decomposition can be viewed as a constrained form of a Tucker decomposition. Consider a Tucker decomposition where the core tensor $\mathcal{G} \in \mathbb{R}^{R \times R \times R}$ is **superdiagonal**—meaning its only non-zero elements are on the main diagonal where all indices are equal ($g_{rrr} \neq 0$, and $g_{ijk} = 0$ if $i, j, k$ are not all equal). In this case, the triple summation in the Tucker reconstruction formula collapses into a single sum:
$$
X_{ijk} = \sum_{r=1}^{R} g_{rrr} A^{(1)}_{ir} A^{(2)}_{jr} A^{(3)}_{kr}
$$
This is precisely the formula for a CP decomposition, where the diagonal elements of the core, $g_{rrr}$, correspond to the weights $\lambda_r$. This insight reveals that the CP model imposes a rigid structure where the $r$-th component of each mode interacts *only* with the $r$-th component of the other modes. The Tucker model is more general, allowing for interactions between all component combinations, as described by the full core tensor $\mathcal{G}$ [@problem_id:3282237].

#### A Critical Distinction: Uniqueness and Interpretability

The most significant difference between the CP and Tucker models from a practical standpoint is their **uniqueness**.

The CP decomposition of a third-order or higher tensor is, under very mild conditions, **essentially unique**. This remarkable property, formalized by Kruskal's theorem, means that if a tensor has a CP decomposition, the factor matrices are unique up to permutation of the rank-one components and scaling/counter-scaling of the vectors within each component. This uniqueness is the reason why CP decomposition is often favored in applications where the interpretation of latent factors is paramount, such as in [chemometrics](@entry_id:154959) or psychometrics. The extracted factors are not arbitrary; they reflect an intrinsic structure of the data [@problem_id:3282077].

In stark contrast, the Tucker decomposition is subject to **rotational ambiguity**. The factor matrices $\mathbf{A}^{(n)}$ are not unique. Any invertible [change of basis](@entry_id:145142) (or rotation, if the factors are constrained to be orthogonal) applied to a factor matrix can be compensated for by applying an inverse transformation to the core tensor, yielding a different set of factors and core that reconstruct the exact same original tensor [@problem_id:3282191]. This means the individual columns of the factor matrices do not have an intrinsic meaning on their own; they merely form a [basis for a subspace](@entry_id:160685). While the subspaces themselves are unique (under certain conditions), the basis is arbitrary. Consequently, the factors from a Tucker decomposition are generally not directly interpretable without additional processing steps, such as rotating them to a "simple structure".

### A Deeper Look at Tensor Rank: The Border Rank Phenomenon

Finally, we address a profound and subtle property of the CP rank that distinguishes it from [matrix rank](@entry_id:153017). The set of tensors with a CP rank of $R$ or less is not, in general, a closed set in the standard topological sense. This means it is possible to have a sequence of tensors, all of which have rank $R$, that converges to a limit tensor with a rank greater than $R$.

This gives rise to the concept of **[border rank](@entry_id:201708)**. The border [rank of a tensor](@entry_id:204291) $\mathcal{X}$, denoted $\underline{\text{rank}}(\mathcal{X})$, is the smallest integer $R$ such that $\mathcal{X}$ can be approximated with arbitrary precision by tensors of rank $R$. By definition, $\underline{\text{rank}}(\mathcal{X}) \le \text{rank}(\mathcal{X})$. For matrices, rank and [border rank](@entry_id:201708) are always equal. For tensors, they can differ.

A classic example demonstrates this phenomenon for a $2 \times 2 \times 2$ tensor. Consider the sequence of tensors $T_\varepsilon$ defined for $\varepsilon \neq 0$:
$$
T_{\varepsilon} = \frac{(e_1 + \varepsilon e_2)^{\otimes 3} - e_1^{\otimes 3}}{\varepsilon}
$$
For any nonzero $\varepsilon$, this tensor is the sum of two rank-one tensors, so its CP rank is at most 2. However, as $\varepsilon$ approaches zero, this sequence converges to a limit tensor $T_0$:
$$
T_0 = \lim_{\varepsilon \to 0} T_{\varepsilon} = e_1 \otimes e_1 \otimes e_2 + e_1 \otimes e_2 \otimes e_1 + e_2 \otimes e_1 \otimes e_1
$$
This limit tensor can be proven to have a CP rank of exactly 3. Therefore, we have a sequence of rank-2 tensors converging to a rank-3 tensor. This shows that the [border rank](@entry_id:201708) of $T_0$ is 2, while its CP rank is 3 [@problem_id:3282089]. This "[border rank](@entry_id:201708) phenomenon" is a fundamental feature of [tensor algebra](@entry_id:161671) and has practical consequences for [optimization algorithms](@entry_id:147840), which may struggle to converge when the solution lies near the boundary of a set of lower-rank tensors.