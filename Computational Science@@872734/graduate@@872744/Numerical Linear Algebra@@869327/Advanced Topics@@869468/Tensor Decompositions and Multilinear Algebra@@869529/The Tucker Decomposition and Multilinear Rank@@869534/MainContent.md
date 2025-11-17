## Introduction
In an era defined by vast, multidimensional datasets, the ability to extract meaningful structure from complex data arrays is paramount. Tensor decompositions offer a powerful mathematical framework for this task, extending linear algebra's [matrix factorization](@entry_id:139760) techniques to higher-order data. Among these methods, the Tucker decomposition stands out as one of the most flexible and widely used models for compressing and interpreting multiway information. This article addresses the fundamental challenge of representing large tensors in a compact and understandable form by exploring the Tucker model in depth.

Across the following chapters, you will gain a comprehensive understanding of this essential technique. The journey begins with **"Principles and Mechanisms,"** where we will formally define the Tucker decomposition, introduce the crucial concept of [multilinear rank](@entry_id:195814), and detail the HOSVD algorithm used for its computation. Next, in **"Applications and Interdisciplinary Connections,"** we will bridge theory and practice by exploring how the model is used for data compression, [feature extraction](@entry_id:164394), and in cutting-edge fields like [medical imaging](@entry_id:269649). Finally, **"Hands-On Practices"** will offer a series of targeted problems to solidify your grasp of the core concepts, from calculating [multilinear rank](@entry_id:195814) to implementing key algorithmic steps. This structured approach will equip you with the theoretical knowledge and practical insight needed to apply the Tucker decomposition effectively.

## Principles and Mechanisms

Having introduced the foundational motivations for tensor decompositions, we now delve into the principles and mechanisms of one of the most powerful and flexible models: the Tucker decomposition. This chapter will formally define the decomposition, introduce the crucial concept of [multilinear rank](@entry_id:195814), explore the mechanics and geometric interpretation of the operations involved, and discuss the primary algorithm for its computation, the Higher-Order Singular Value Decomposition (HOSVD). We will conclude by examining the model's approximation properties and its relationship to other tensor factorization methods.

### The Tucker Decomposition: A Formal Definition

The Tucker decomposition models a given $N$-way tensor $\mathcal{X} \in \mathbb{R}^{I_1 \times I_2 \times \cdots \times I_N}$ as the product of a smaller, dense **core tensor** and a set of **factor matrices**, one for each mode. Formally, the decomposition is expressed as:

$$
\mathcal{X} \approx \mathcal{G} \times_1 U^{(1)} \times_2 U^{(2)} \cdots \times_N U^{(N)}
$$

Here, $\mathcal{G} \in \mathbb{R}^{r_1 \times r_2 \times \cdots \times r_N}$ is the core tensor, and each $U^{(n)} \in \mathbb{R}^{I_n \times r_n}$ is a factor matrix for the $n$-th mode. The tuple $(r_1, r_2, \ldots, r_N)$, where $r_n \le I_n$, defines the dimensions of the core tensor and is referred to as the **[multilinear rank](@entry_id:195814)** of the model. The operation $\times_n$ is the **mode-n product**, which is a cornerstone of [multilinear algebra](@entry_id:199321).

The mode-$n$ product of a tensor $\mathcal{A} \in \mathbb{R}^{I_1 \times \cdots \times I_N}$ with a matrix $U \in \mathbb{R}^{J \times I_n}$, denoted $\mathcal{Y} = \mathcal{A} \times_n U$, results in a new tensor $\mathcal{Y} \in \mathbb{R}^{I_1 \times \cdots \times I_{n-1} \times J \times I_{n+1} \times \cdots \times I_N}$. Conceptually, this operation transforms each mode-$n$ fiber of $\mathcal{A}$ (which are vectors of length $I_n$) by left-multiplying it with the matrix $U$. The effect is to change the dimension of the $n$-th mode from $I_n$ to $J$.

In the context of the Tucker decomposition, the expression is evaluated sequentially. Starting with the core tensor $\mathcal{G}$, the first operation $\mathcal{G} \times_1 U^{(1)}$ uses the matrix $U^{(1)} \in \mathbb{R}^{I_1 \times r_1}$ to transform the first mode of $\mathcal{G}$, changing its size from $r_1$ to $I_1$. The resulting tensor is of size $I_1 \times r_2 \times \cdots \times r_N$. The second operation then uses $U^{(2)} \in \mathbb{R}^{I_2 \times r_2}$ to transform the second mode, changing its size from $r_2$ to $I_2$. This process continues for all $N$ modes, progressively expanding the core tensor until it matches the dimensions of the original tensor $\mathcal{X}$ [@problem_id:3598156]. The power of this representation lies in its ability to capture the essential information of a large tensor $\mathcal{X}$ within a much smaller core tensor $\mathcal{G}$ and a set of factor matrices, provided the multilinear ranks $r_n$ are significantly smaller than the original dimensions $I_n$.

### Multilinear Rank and Tensor Unfolding

To understand the intrinsic dimensionality that the Tucker decomposition seeks to capture, we must introduce the concepts of **[tensor unfolding](@entry_id:755868)** (also known as [matricization](@entry_id:751739)) and **[multilinear rank](@entry_id:195814)**.

The **mode-n unfolding**, denoted $X_{(n)}$, is a process that reshapes the tensor $\mathcal{X}$ into a matrix. The matrix $X_{(n)}$ is constructed by arranging all the mode-$n$ fibers of $\mathcal{X}$ as its columns. This results in a matrix of size $I_n \times (I_1 \cdots I_{n-1} I_{n+1} \cdots I_N)$. While the ordering of the columns can vary, a standard convention is to use a [lexicographical ordering](@entry_id:143032) of the non-$n$ indices. The unfolding effectively exposes the structure of the tensor along a specific mode, making it accessible to the powerful tools of linear algebra.

The **[multilinear rank](@entry_id:195814)** of a tensor $\mathcal{X}$ is then defined as the tuple of the matrix ranks of its unfoldings:

$$
\operatorname{rank}_{\mathrm{ml}}(\mathcal{X}) = (\operatorname{rank}(X_{(1)}), \operatorname{rank}(X_{(2)}), \ldots, \operatorname{rank}(X_{(N)}))
$$

The [multilinear rank](@entry_id:195814) is not just a descriptive feature; it is an intrinsic property of the tensor that is invariant under certain transformations. Specifically, if we apply an [invertible linear transformation](@entry_id:149915) $A^{(n)} \in \mathbb{R}^{I_n \times I_n}$ to each mode of a tensor $\mathcal{X}$ to obtain a new tensor $\mathcal{Y} = \mathcal{X} \times_1 A^{(1)} \cdots \times_N A^{(N)}$, the [multilinear rank](@entry_id:195814) remains unchanged: $\operatorname{rank}_{\mathrm{ml}}(\mathcal{Y}) = \operatorname{rank}_{\mathrm{ml}}(\mathcal{X})$ [@problem_id:3598149]. This signifies that [multilinear rank](@entry_id:195814) captures a fundamental structural property, independent of the choice of basis in each mode's vector space.

Crucially, the [multilinear rank](@entry_id:195814) of a tensor dictates the minimal size of the core tensor required for an *exact* Tucker decomposition. It is a fundamental theorem that a tensor $\mathcal{X}$ with [multilinear rank](@entry_id:195814) $(r_1, \ldots, r_N)$ can be exactly represented by a Tucker decomposition with a core tensor of size $r_1 \times \cdots \times r_N$, and no smaller core tensor will suffice [@problem_id:3598149, Option F].

### The Mechanics of Multilinear Operations

A deep understanding of the Tucker decomposition requires a grasp of the interplay between mode products and unfoldings. The algebraic relationship between these operations is central to both the theory and computation of tensor decompositions.

For a mode-$n$ product $\mathcal{Y} = \mathcal{X} \times_n U$, the corresponding operation on the unfoldings is remarkably simple. The mode-$n$ unfolding of the resulting tensor, $Y_{(n)}$, is given by the matrix product of $U$ and the mode-$n$ unfolding of the original tensor, $X_{(n)}$:

$$
Y_{(n)} = U X_{(n)}
$$

Let's derive this for a concrete example [@problem_id:3598157]. Consider a third-order tensor $\mathcal{X} \in \mathbb{R}^{I_1 \times I_2 \times I_3}$ and a matrix $U \in \mathbb{R}^{J_2 \times I_2}$. The mode-2 product is $\mathcal{Y} = \mathcal{X} \times_2 U$. By definition, an element of $\mathcal{Y}$ is $(\mathcal{Y})_{i_1, j_2, i_3} = \sum_{i_2=1}^{I_2} (\mathcal{X})_{i_1, i_2, i_3} U_{j_2, i_2}$. The mode-2 unfolding $Y_{(2)}$ is a matrix of size $J_2 \times (I_1 I_3)$ where the element $(Y_{(2)})_{j_2, c}$ corresponds to $(\mathcal{Y})_{i_1, j_2, i_3}$ for some column index $c$ that depends on $i_1$ and $i_3$. Similarly, $(X_{(2)})_{i_2, c}$ corresponds to $(\mathcal{X})_{i_1, i_2, i_3}$. Substituting this into the sum, we get $(Y_{(2)})_{j_2, c} = \sum_{i_2=1}^{I_2} U_{j_2, i_2} (X_{(2)})_{i_2, c}$. This is precisely the definition of the matrix product $Y_{(2)} = U X_{(2)}$.

This property extends to the full Tucker decomposition. The mode-$n$ unfolding of the tensor $\mathcal{X} = \mathcal{G} \times_1 U^{(1)} \cdots \times_N U^{(N)}$ is given by the matrix product:
$$
X_{(n)} = U^{(n)} G_{(n)} (U^{(N)} \otimes \cdots \otimes U^{(n+1)} \otimes U^{(n-1)} \otimes \cdots \otimes U^{(1)})^T
$$
where $\otimes$ denotes the Kronecker product. This formula is the key to analyzing the properties of the decomposition and is fundamental to its computation.

### Geometric Interpretation: The Core as Coordinates

The Tucker decomposition has an elegant and insightful geometric interpretation. Let us assume the factor matrices $U^{(n)}$ have orthonormal columns. This is a common and desirable property, as it means the columns of each $U^{(n)}$ form an [orthonormal basis](@entry_id:147779) for an $r_n$-dimensional subspace of the original $I_n$-dimensional vector space for that mode. These subspaces, spanned by the columns of the factor matrices, represent the principal directions of variation of the tensor data along each mode.

Under this [orthonormality](@entry_id:267887) assumption, the core tensor $\mathcal{G}$ can be computed by projecting the original tensor $\mathcal{X}$ onto these subspaces:
$$
\mathcal{G} = \mathcal{X} \times_1 (U^{(1)})^T \times_2 (U^{(2)})^T \cdots \times_N (U^{(N)})^T
$$
A beautiful result emerges when we write out what an individual entry of the core tensor represents. Using the definition of the mode-product and the inner product of tensors (the sum of the product of their entries, also known as the Hilbert-Schmidt inner product), one can prove that [@problem_id:3598151]:
$$
g_{j_1, j_2, \ldots, j_N} = \langle \mathcal{X}, u^{(1)}_{j_1} \circ u^{(2)}_{j_2} \circ \cdots \circ u^{(N)}_{j_N} \rangle
$$
where $u^{(n)}_{j_n}$ is the $j_n$-th column of $U^{(n)}$, and $\circ$ denotes the vector outer product.

The set of rank-1 tensors $\{ u^{(1)}_{j_1} \circ \cdots \circ u^{(N)}_{j_N} \}$ forms an [orthonormal basis](@entry_id:147779) for the subspace into which $\mathcal{X}$ is projected. The identity above thus states that each entry of the core tensor, $g_{j_1, \ldots, j_N}$, is the coordinate of the tensor $\mathcal{X}$ with respect to the corresponding basis tensor. The core tensor, therefore, contains the "multilinear coordinates" of $\mathcal{X}$ in this new, data-driven basis. It describes the interactions between the different principal components of the modes.

### Data Compression and Storage Cost

One of the primary applications of the Tucker decomposition is data compression. For a large, dense tensor, the storage required can be prohibitive. The Tucker decomposition provides a compact representation, especially when the multilinear ranks $r_n$ are much smaller than the original dimensions $I_n$.

Let's analyze the storage costs [@problem_id:3598141].
- The full tensor $\mathcal{X} \in \mathbb{R}^{I_1 \times \cdots \times I_N}$ requires storing $\prod_{n=1}^N I_n$ scalar values.
- The Tucker model consists of the core tensor and the factor matrices.
    - The core tensor $\mathcal{G} \in \mathbb{R}^{r_1 \times \cdots \times r_N}$ requires $\prod_{n=1}^N r_n$ scalars.
    - The $N$ factor matrices $U^{(n)} \in \mathbb{R}^{I_n \times r_n}$ require a total of $\sum_{n=1}^N I_n r_n$ scalars.

The total storage cost for the Tucker model is thus $\prod_{n=1}^N r_n + \sum_{n=1}^N I_n r_n$.

The compression ratio is the ratio of these two costs. Consider a $3$-way tensor of size $1000 \times 1000 \times 1000$. Storing it directly requires $10^9$ values. If we can approximate it well with a [multilinear rank](@entry_id:195814) of $(10, 10, 10)$, the storage cost for the Tucker model would be $10^3 + (1000 \times 10 + 1000 \times 10 + 1000 \times 10) = 1000 + 30000 = 31000$ values. This represents a [compression factor](@entry_id:173415) of over 32,000. This dramatic reduction in storage complexity is what makes tensor methods feasible for many [large-scale data analysis](@entry_id:165572) problems.

### Computing the Decomposition: The HOSVD Algorithm

The discussion so far has assumed the existence of the factor matrices $U^{(n)}$ and the core tensor $\mathcal{G}$. The standard algorithm for computing them is the **Higher-Order Singular Value Decomposition (HOSVD)**, a generalization of the matrix SVD.

The HOSVD procedure constructs a Tucker decomposition with orthonormal factor matrices [@problem_id:3424618]. The algorithm proceeds as follows:
1.  For each mode $n \in \{1, \ldots, N\}$, compute the mode-$n$ unfolding of the input tensor, $X_{(n)}$.
2.  Compute the Singular Value Decomposition (SVD) of each unfolding matrix: $X_{(n)} = U_n \Sigma_n V_n^T$. The columns of the [orthogonal matrix](@entry_id:137889) $U_n \in \mathbb{R}^{I_n \times I_n}$ are the [left singular vectors](@entry_id:751233) of $X_{(n)}$.
3.  For a target [multilinear rank](@entry_id:195814) $(r_1, \ldots, r_N)$, construct the factor matrix $U^{(n)} \in \mathbb{R}^{I_n \times r_n}$ for each mode by taking the first $r_n$ columns of the corresponding matrix $U_n$. These columns represent an [orthonormal basis](@entry_id:147779) for the $r_n$-dimensional subspace that best captures the variance of the data along mode $n$.
4.  Once the factor matrices are determined, the core tensor $\mathcal{G}$ is computed by projecting the original tensor $\mathcal{X}$ onto the subspaces spanned by these factors: $\mathcal{G} = \mathcal{X} \times_1 (U^{(1)})^T \times_2 (U^{(2)})^T \cdots \times_N (U^{(N)})^T$.
5.  The final approximate tensor, $\hat{\mathcal{X}}$, is then given by $\hat{\mathcal{X}} = \mathcal{G} \times_1 U^{(1)} \cdots \times_N U^{(N)}$.

The HOSVD algorithm has a strong connection to Principal Component Analysis (PCA). The [left singular vectors](@entry_id:751233) of a data matrix are the eigenvectors of its Gram matrix ($X_{(n)} X_{(n)}^T$), which, for centered data, are the principal components. Therefore, Step 3 of HOSVD is equivalent to performing a PCA on each mode's unfolding and selecting the top principal components to form the basis for that mode [@problem_id:3598163]. The HOSVD can thus be viewed as a multilinear generalization of PCA.

### Approximation Quality and Optimality

While HOSVD is a powerful and intuitive algorithm, it is essential to understand the nature and quality of the approximation it provides. A key result provides an upper bound on the [approximation error](@entry_id:138265) in terms of the discarded singular values from the unfoldings [@problem_id:3424618]:

$$
\|\mathcal{X} - \hat{\mathcal{X}}\|_F^2 \le \sum_{n=1}^N \sum_{j=r_n+1} (\sigma_{j}^{(n)})^2
$$

Here, $\|\cdot\|_F$ is the Frobenius norm (square root of the sum of squared entries), and $\sigma_{j}^{(n)}$ is the $j$-th [singular value](@entry_id:171660) of the unfolding $X_{(n)}$. This bound is highly informative: it tells us that the HOSVD approximation will be accurate if, for every mode, the energy of the data is concentrated in its first few singular values. In other words, the approximation is good if every unfolding is well-approximated by a [low-rank matrix](@entry_id:635376) [@problem_id:3598163].

However, it is crucial to recognize that HOSVD does **not** generally yield the *best* possible tensor approximation for a given [multilinear rank](@entry_id:195814) $(r_1, \ldots, r_N)$. The reason is subtle but fundamental [@problem_id:3598146]:
1.  The set of all tensors with [multilinear rank](@entry_id:195814) at most $(r_1, \ldots, r_N)$ is a **nonconvex set**. Finding the closest point in a nonconvex set to a given point (our tensor $\mathcal{X}$) is a [nonconvex optimization](@entry_id:634396) problem, which is notoriously difficult and may have many local minima.
2.  The HOSVD algorithm is a **greedy, one-shot procedure**. It optimizes the basis for each mode *independently*, by minimizing the [approximation error](@entry_id:138265) for each unfolding separately. This decoupled optimization does not guarantee a minimum for the coupled, global problem of minimizing $\|\mathcal{X} - \hat{\mathcal{X}}\|_F$.

Despite this, the HOSVD approximation is not arbitrary; it is **quasi-optimal**. The error of the HOSVD approximation $\hat{\mathcal{X}}$ is guaranteed to be within a factor of the error of the true [best approximation](@entry_id:268380) $\mathcal{X}_\star$:

$$
\|\mathcal{X} - \hat{\mathcal{X}}\|_F \le \sqrt{N} \, \|\mathcal{X} - \mathcal{X}_\star\|_F
$$

This provides a valuable performance guarantee, ensuring that HOSVD is never too far from the [optimal solution](@entry_id:171456), especially for a small number of modes $N$.

### Context and Broader Implications

The Tucker decomposition is one of two primary models for [low-rank tensor](@entry_id:751518) factorization. The other is the **Canonical Polyadic (CP) decomposition**, which models a tensor as a sum of rank-1 tensors. A deep connection exists between them: the CP decomposition can be viewed as a special case of the Tucker decomposition where the core tensor $\mathcal{G}$ is **superdiagonal**—meaning its only non-zero entries are on the main diagonal where $j_1 = j_2 = \cdots = j_N$ [@problem_id:3282237]. This provides a unified framework, with Tucker being the more general model.

This generality leads to profound theoretical and practical differences [@problem_id:3598131]:
-   **Existence of Best Approximations:** The set of tensors with bounded [multilinear rank](@entry_id:195814) is a topologically **closed** set. This property guarantees that for any tensor, a best Tucker approximation always exists. In stark contrast, the set of tensors with bounded CP rank is **not closed**. This leads to pathological cases where a sequence of rank-$R$ tensors can converge to a tensor of rank greater than $R$, meaning a best rank-$R$ approximation does not exist.
-   **Rank Disparity:** For a given tensor, the [multilinear rank](@entry_id:195814) and CP rank can be vastly different. While the Tucker model offers a flexible hierarchy of ranks, the CP rank is a single number. For many tensors, especially in higher dimensions, the CP rank can be astronomically larger than the components of the [multilinear rank](@entry_id:195814). For generic tensors in $\mathbb{C}^{r \times r \times r}$, the [multilinear rank](@entry_id:195814) is $(r,r,r)$ while the CP rank grows quadratically with $r$, roughly as $r^2/3$.

In summary, the Tucker decomposition, underpinned by the concept of [multilinear rank](@entry_id:195814) and operationalized by the HOSVD algorithm, provides a robust, flexible, and theoretically sound framework for representing and compressing multidimensional data. Its well-posed nature and guaranteed existence of best approximations make it a reliable and indispensable tool in scientific computing and data analysis.