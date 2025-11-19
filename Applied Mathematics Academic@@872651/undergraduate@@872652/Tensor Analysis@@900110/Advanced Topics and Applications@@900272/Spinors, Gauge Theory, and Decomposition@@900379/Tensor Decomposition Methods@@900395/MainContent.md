## Introduction
As data becomes increasingly complex and multidimensional, a simple matrix is often insufficient to capture its rich structure. Tensors, or multi-way arrays, provide a natural framework for representing such data, from video sequences (height × width × time) to neurological data (voxels × time × subjects). However, simply storing this data is not enough; the central challenge lies in extracting meaningful patterns, uncovering latent relationships, and building predictive models from these vast and intricate structures. This is the knowledge gap that tensor [decomposition methods](@entry_id:634578) are designed to fill, offering a powerful toolkit for dissecting high-order data in a way that is analogous to how [matrix factorization](@entry_id:139760) analyzes two-dimensional data.

This article serves as a comprehensive guide to the foundational techniques of [tensor analysis](@entry_id:184019). In the first chapter, **"Principles and Mechanisms,"** we will delve into the mathematical underpinnings of the two cornerstone models: the CANDECOMP/PARAFAC (CP) and Tucker decompositions. You will learn how they break down tensors into simpler components and understand their key properties, such as uniqueness and rank. Next, in **"Applications and Interdisciplinary Connections,"** we will explore the remarkable impact of these methods across a wide range of fields, from uncovering brain networks in neuroscience to enabling [blind source separation](@entry_id:196724) in [chemometrics](@entry_id:154959) and regularizing complex models in machine learning. Finally, the **"Hands-On Practices"** chapter will provide a set of targeted problems to help you apply these concepts and develop a practical, working knowledge of [tensor decomposition](@entry_id:173366).

## Principles and Mechanisms

Having established the importance of tensors in representing multidimensional data, we now turn to the central task of their analysis: decomposition. Just as [matrix factorization](@entry_id:139760) methods like Singular Value Decomposition (SVD) are indispensable for understanding two-dimensional data, tensor decompositions provide a powerful framework for dissecting higher-order data structures. These methods aim to break down a complex, high-dimensional tensor into a set of simpler, more interpretable components. This process is not merely a mathematical exercise; it is fundamental to uncovering latent structures, compressing vast datasets, and extracting meaningful features from complex phenomena. In this chapter, we will explore the principles and mechanisms of the two most foundational [tensor decomposition](@entry_id:173366) models: the CANDECOMP/PARAFAC (CP) decomposition and the Tucker decomposition.

### The CANDECOMP/PARAFAC (CP) Decomposition

The CANDECOMP/PARAFAC decomposition, often abbreviated as **CP decomposition**, is conceptually one of the most direct generalizations of [matrix rank](@entry_id:153017) decomposition to [higher-order tensors](@entry_id:183859). It models a tensor as a sum of a finite number of **rank-one tensors**.

#### The Rank-One Tensor: The Fundamental Building Block

Before defining the full CP model, we must first understand its elementary component: the [rank-one tensor](@entry_id:202127). An $N$-th order tensor is said to be rank-one if it can be expressed as the **outer product** of $N$ vectors. For a third-order tensor $\mathcal{T}$, this means it can be written as:
$$
\mathcal{T} = \mathbf{u} \circ \mathbf{v} \circ \mathbf{w}
$$
where $\mathbf{u}$, $\mathbf{v}$, and $\mathbf{w}$ are vectors. The symbol $\circ$ denotes the [outer product](@entry_id:201262). In terms of individual elements, this relationship is expressed as:
$$
T_{ijk} = u_i v_j w_k
$$
This structure implies that all the information within the tensor is encoded in these three constituent vectors. For example, in materials science, an anisotropic property of a crystal might be described by a third-order [rank-one tensor](@entry_id:202127), where the characteristic vectors $\mathbf{u}$, $\mathbf{v}$, and $\mathbf{w}$ represent fundamental directions within the crystal's lattice structure [@problem_id:1542448]. Given these vectors, any element of the tensor can be computed directly.

#### The CP Model and Data Compression

The CP decomposition represents a tensor $\mathcal{T} \in \mathbb{R}^{I_1 \times I_2 \times \dots \times I_N}$ as a sum of $R$ rank-one tensors. For a third-order tensor $\mathcal{T} \in \mathbb{R}^{I \times J \times K}$, the model is:
$$
\mathcal{T} = \sum_{r=1}^{R} \mathbf{a}_r \circ \mathbf{b}_r \circ \mathbf{c}_r
$$
Here, $\mathbf{a}_r \in \mathbb{R}^{I}$, $\mathbf{b}_r \in \mathbb{R}^{J}$, and $\mathbf{c}_r \in \mathbb{R}^{K}$ are the factor vectors for the $r$-th component. It is common practice to group these vectors into **factor matrices** $A = [\mathbf{a}_1, \dots, \mathbf{a}_R] \in \mathbb{R}^{I \times R}$, $B = [\mathbf{b}_1, \dots, \mathbf{b}_R] \in \mathbb{R}^{J \times R}$, and $C = [\mathbf{c}_1, \dots, \mathbf{c}_R] \in \mathbb{R}^{K \times R}$. In this framework, the element-wise reconstruction formula for the tensor is given by [@problem_id:1542379]:
$$
T_{ijk} = \sum_{r=1}^{R} A_{ir} B_{jr} C_{kr}
$$
The smallest number $R$ for which such an exact decomposition exists is called the **CP-rank** (or simply, the rank) of the tensor $\mathcal{T}$. In practical applications, we often seek an approximation with a small rank $R$ that captures the essential structure of the data.

One of the most significant advantages of this representation is **data compression**. Consider a large tensor representing movie ratings, with dimensions for users, movies, and time slots. If the dimensions are $I=J=K=1000$, storing the full or "dense" tensor requires storing $1000^3 = 10^9$ numerical values. However, if this tensor can be well-approximated by a rank-$R=10$ CP decomposition, we only need to store the three factor matrices. The total number of elements in these matrices is $(I \times R) + (J \times R) + (K \times R) = (1000+1000+1000) \times 10 = 30,000$. The compression ratio, defined as the ratio of storage requirements, would be $10^9 / 30,000 \approx 3.33 \times 10^4$. This demonstrates a colossal reduction in memory usage, making the storage and manipulation of massive datasets feasible [@problem_id:1542426].

#### Uniqueness and Ambiguities in CP Decomposition

A remarkable and highly valuable property of the CP decomposition is its **essential uniqueness** under relatively mild conditions. Unlike matrix factorizations, which often have rotational freedom, a low-rank CP decomposition is often unique up to two inherent ambiguities: permutation and scaling of the components.

1.  **Permutation Ambiguity**: The order of the rank-one components in the summation does not affect the final tensor. We can reorder the terms in the sum, which corresponds to permuting the columns of the factor matrices $A$, $B$, and $C$ in the same way.

2.  **Scaling Ambiguity**: For any given rank-one component $\mathbf{a}_r \circ \mathbf{b}_r \circ \mathbf{c}_r$, we can scale the factor vectors by scalar multiples $\lambda_A, \lambda_B, \lambda_C$ as long as their product is one: $(\lambda_A \mathbf{a}_r) \circ (\lambda_B \mathbf{b}_r) \circ (\lambda_C \mathbf{c}_r) = (\lambda_A \lambda_B \lambda_C) (\mathbf{a}_r \circ \mathbf{b}_r \circ \mathbf{c}_r) = \mathbf{a}_r \circ \mathbf{b}_r \circ \mathbf{c}_r$. The scaling is absorbed into the vectors without changing the component.

Therefore, two CP decompositions $\{A, B, C\}$ and $\{A', B', C'\}$ are considered equivalent if $A'$, $B'$, and $C'$ can be obtained from $A$, $B$, and $C$ by applying a consistent column permutation and balancing the scaling of the corresponding vector triplets [@problem_id:1542408].

This essential uniqueness is not guaranteed. **Kruskal's condition** provides a powerful sufficient (but not necessary) condition for the uniqueness of a CP decomposition. It relates the rank $R$ of the decomposition to the **Kruskal-rank** (or k-rank) of the factor matrices. The k-[rank of a matrix](@entry_id:155507) is the maximum number $k$ such that any set of $k$ columns of that matrix is [linearly independent](@entry_id:148207). For an $N$-th order tensor with rank-$R$ CP decomposition and factor matrices $\{A^{(1)}, \dots, A^{(N)}\}$, the decomposition is unique if:
$$
\sum_{n=1}^{N} k_{A^{(n)}} \ge 2R + (N-1)
$$
For a third-order tensor ($N=3$), this simplifies to $k_A + k_B + k_C \ge 2R + 2$. If the factor matrices have linearly dependent columns, their k-ranks will be reduced, and the condition may not be met, indicating that the decomposition might not be unique [@problem_id:1542376].

#### The Challenge of Tensor Rank

While the definition of CP-rank is a natural extension of [matrix rank](@entry_id:153017), its properties are significantly more complex. For a matrix, the rank is a well-behaved quantity that can be reliably computed via SVD. For tensors of order three or higher, determining the CP-rank is an NP-hard problem.

One might attempt to diagnose [tensor rank](@entry_id:266558) by **unfolding** or **matricizing** the tensor—rearranging its elements into a matrix. For a third-order tensor $\mathcal{T} \in \mathbb{R}^{I \times J \times K}$, there are three standard unfoldings: $T_{(1)} \in \mathbb{R}^{I \times JK}$, $T_{(2)} \in \mathbb{R}^{J \times IK}$, and $T_{(3)} \in \mathbb{R}^{K \times IJ}$. It can be shown that the CP-[rank of a tensor](@entry_id:204291) is always greater than or equal to the rank of any of its unfoldings:
$$
\text{rank}_{CP}(\mathcal{T}) \ge \max(\text{rank}(T_{(1)}), \text{rank}(T_{(2)}), \text{rank}(T_{(3)}))
$$
However, unlike in the matrix case (where a tensor is just a vectorized matrix and the ranks are equal), this inequality can be strict for [higher-order tensors](@entry_id:183859). There exist tensors for which the CP-rank is strictly greater than the maximum rank of its unfoldings. For example, a specific $2 \times 2 \times 2$ tensor can be constructed where all three unfoldings have a [matrix rank](@entry_id:153017) of 2, yet the tensor's CP-rank is 3 [@problem_id:1542406]. This illustrates a fundamental departure from [matrix theory](@entry_id:184978) and underscores the intricate nature of [multilinear rank](@entry_id:195814).

### The Tucker Decomposition

While the CP model is powerful and interpretable, its strict structure can be limiting. The **Tucker decomposition** offers a more flexible and general framework, often viewed as a higher-order analogue of Principal Component Analysis (PCA).

#### A More General Model: Core Tensors and Factor Matrices

The Tucker decomposition models a tensor $\mathcal{X}$ as a dense, smaller **core tensor** $\mathcal{G}$ that is multiplied along each mode by a factor matrix. For a third-order tensor $\mathcal{X} \in \mathbb{R}^{I_1 \times I_2 \times I_3}$, the Tucker decomposition is written as:
$$
\mathcal{X} \approx \mathcal{G} \times_1 A^{(1)} \times_2 A^{(2)} \times_3 A^{(3)}
$$
Here, $A^{(n)} \in \mathbb{R}^{I_n \times R_n}$ are the **factor matrices** (often constrained to have orthonormal columns), $\mathcal{G} \in \mathbb{R}^{R_1 \times R_2 \times R_3}$ is the core tensor, and $\times_n$ denotes the **n-mode product** of a tensor by a matrix. The dimensions of the core tensor, $(R_1, R_2, R_3)$, define the **[multilinear rank](@entry_id:195814)** of the decomposition.

The element-wise reconstruction formula is:
$$
x_{i_1 i_2 i_3} = \sum_{r_1=1}^{R_1} \sum_{r_2=1}^{R_2} \sum_{r_3=1}^{R_3} g_{r_1 r_2 r_3} a^{(1)}_{i_1 r_1} a^{(2)}_{i_2 r_2} a^{(3)}_{i_3 r_3}
$$
This formula highlights the roles of the different components [@problem_id:1542413]. The factor matrices $A^{(n)}$ can be interpreted as containing the principal components or basis vectors for each mode. The core tensor $\mathcal{G}$ governs the interactions between these components. Its elements $g_{r_1 r_2 r_3}$ indicate the level of interaction between the $r_1$-th component of the first mode, the $r_2$-th component of the second mode, and the $r_3$-th component of the third mode.

#### Computation via Higher-Order Singular Value Decomposition (HOSVD)

Finding the optimal Tucker decomposition is computationally challenging. However, an excellent approximation can be obtained via a non-iterative procedure called the **Higher-Order Singular Value Decomposition (HOSVD)**. HOSVD provides a deterministic way to find the factor matrices and the core tensor.

The procedure is as follows: for each mode $n$, the factor matrix $A^{(n)}$ is chosen as the matrix whose columns are the first $R_n$ [left singular vectors](@entry_id:751233) of the mode-$n$ unfolding of the tensor, $X_{(n)}$. These singular vectors correspond to the largest singular values and represent the dominant orthonormal basis for the data in that mode [@problem_id:1542425]. Once the (orthogonal) factor matrices $\{A^{(n)}\}$ have been determined, the core tensor $\mathcal{G}$ that minimizes the [approximation error](@entry_id:138265) is computed directly by projecting the original tensor onto the space spanned by these factor matrices:
$$
\mathcal{G} = \mathcal{X} \times_1 (A^{(1)})^T \times_2 (A^{(2)})^T \times_3 (A^{(3)})^T
$$
While HOSVD does not guarantee the best possible fit for a given [multilinear rank](@entry_id:195814), it provides a very good starting point and is often used to initialize more refined [iterative algorithms](@entry_id:160288) like Higher-Order Orthogonal Iteration (HOOI).

### A Unified View: The Relationship Between CP and Tucker Decompositions

At first glance, the CP and Tucker models may seem distinct. However, the CP decomposition is, in fact, a special, constrained case of the Tucker decomposition. This connection provides a deeper understanding of both models.

Consider a rank-$R$ CP decomposition of a tensor $\mathcal{X}$. This can be expressed as a Tucker decomposition where the [multilinear rank](@entry_id:195814) is $(R, R, \dots, R)$ and the core tensor $\mathcal{G}$ is **superdiagonal**. A superdiagonal tensor is one where the only non-zero elements are those for which all indices are equal, i.e., $g_{r,r,\dots,r}$. All off-diagonal elements are constrained to be zero.

Let's demonstrate this for a third-order tensor. A CP model with weights $\lambda_r$ is:
$$
\mathcal{X} = \sum_{r=1}^{R} \lambda_r (\mathbf{a}_r \circ \mathbf{b}_r \circ \mathbf{c}_r)
$$
This is equivalent to a Tucker model $\mathcal{X} = \mathcal{G} \times_1 A \times_2 B \times_3 C$ where the factor matrices are simply $A = [\mathbf{a}_1, \dots, \mathbf{a}_R]$, etc., and the core tensor $\mathcal{G}$ is a diagonal $R \times R \times R$ tensor with $\mathcal{G}_{rrr} = \lambda_r$ and all other elements being zero [@problem_id:1542418]. The trace of this core tensor, $\sum_{r=1}^R \mathcal{G}_{rrr}$, is simply the sum of the weights of the CP components.

This reveals the fundamental difference between the two models. The Tucker decomposition is more general because its core tensor $\mathcal{G}$ can be any arbitrary dense tensor. The CP model imposes the strict constraint that $\mathcal{G}$ must be diagonal. For an $N$-th order tensor with a core of size $R \times \dots \times R$, a general Tucker model has $R^N$ parameters in its core tensor. The equivalent CP model has only $R$ parameters (the diagonal elements). The additional $R^N - R$ off-diagonal elements in the Tucker core tensor provide it with significantly more flexibility to model complex interactions between components, which is a freedom the CP model lacks [@problem_id:1542422].

This leads to a practical trade-off. The CP model's strength lies in its parsimony and the direct interpretability of its rank-one components as distinct latent factors. The Tucker model, with its greater flexibility, can often achieve a better data fit with a smaller [multilinear rank](@entry_id:195814) but at the cost of [interpretability](@entry_id:637759), as the interactions are now encoded in the dense core tensor. The choice between CP and Tucker decomposition therefore depends on the specific goals of the analysis: interpretability and simplicity versus approximation power and generality.