## Introduction
As datasets grow in complexity and dimensionality, tensor decompositions have emerged as an indispensable tool for multi-way data analysis, revealing the latent structures hidden within. The Canonical Polyadic (CP) decomposition, which models a tensor as a sum of rank-one components, is one of the most fundamental and interpretable of these models. However, fitting the CP model to data presents a challenging [non-convex optimization](@entry_id:634987) problem. The workhorse algorithm for this task, valued for its simplicity and robustness, is Alternating Least Squares (ALS). This article provides a comprehensive guide to CP-ALS, bridging the gap between its elegant mathematical theory and its powerful, nuanced application in the real world.

This guide is structured to build your expertise progressively. The first chapter, **Principles and Mechanisms**, lays the theoretical groundwork. It deconstructs the CP model, including its essential uniqueness properties and the subtle complexities of [tensor rank](@entry_id:266558). From there, we will derive the ALS update rules step-by-step and investigate the convergence properties and numerical pathologies, such as degeneracy, that govern its performance.

Building on this foundation, the second chapter, **Applications and Interdisciplinary Connections**, explores the algorithm's versatility. We will examine how the standard ALS framework is extended with constraints and regularization to incorporate domain knowledge, adapted to handle incomplete or complex-valued data, and leveraged as an engine for scientific discovery in fields from neuroscience to data mining.

Finally, **Hands-On Practices** will ground your theoretical knowledge in practical skill. Through a series of targeted problems, you will move from understanding the model's structure to analyzing the numerical stability and computational cost of the algorithm, preparing you to implement and apply CP-ALS effectively.

## Principles and Mechanisms

The Alternating Least Squares (ALS) algorithm is the most widely employed method for computing the Canonical Polyadic (CP) decomposition. Its prevalence stems from its conceptual simplicity and robustness. The algorithm iteratively refines the factor matrices by solving a series of linear [least-squares](@entry_id:173916) subproblems, a task for which efficient and stable numerical methods are abundant. This chapter delineates the fundamental principles of the CP model, derives the core mechanics of the ALS algorithm, and explores the theoretical properties and practical pathologies that govern its performance.

### The Canonical Polyadic (CP) Decomposition Model

The CP decomposition expresses a tensor as a sum of rank-one tensors. For a third-order tensor $\mathcal{X} \in \mathbb{R}^{I \times J \times K}$, its rank-$R$ CP model is given by:

$$
\mathcal{X} \approx \sum_{r=1}^{R} a_r \circ b_r \circ c_r
$$

where $\circ$ denotes the vector outer product, such that $(\boldsymbol{a}_r \circ \boldsymbol{b}_r \circ \boldsymbol{c}_r)_{ijk} = (a_r)_i (b_r)_j (c_r)_k$. The vectors $\{a_r\}_{r=1}^R$, $\{b_r\}_{r=1}^R$, and $\{c_r\}_{r=1}^R$ are collected as the columns of the **factor matrices** $A \in \mathbb{R}^{I \times R}$, $B \in \mathbb{R}^{J \times R}$, and $C \in \mathbb{R}^{K \times R}$, respectively. In element-wise form, the model is written as:

$$
\mathcal{X}_{ijk} \approx \sum_{r=1}^{R} A_{ir} B_{jr} C_{kr}
$$

A critical feature of the CP model is its inherent non-uniqueness, which manifests in two primary forms: permutation and scaling indeterminacies. Understanding these is essential for interpreting the results of a CP decomposition.

#### Permutation and Scaling Indeterminacies

The structure of the CP model gives rise to certain ambiguities in the factor matrices that do not alter the reconstructed tensor. These are not flaws but intrinsic properties of the model.

First, because the summation is commutative, the order of the $R$ rank-one components can be rearranged without changing the final sum. This is known as **permutation indeterminacy**. If we apply the same [permutation matrix](@entry_id:136841) $P \in \mathbb{R}^{R \times R}$ to the columns of all three factor matrices, yielding new factors $(AP, BP, CP)$, the resulting tensor is identical. The triplet of factor vectors $(a_r, b_r, c_r)$ corresponding to the $r$-th component is simply moved to a new position in the sum, but the sum itself remains unchanged .

Second, for any single rank-one component $a_r \circ b_r \circ c_r$, we can scale the constituent vectors by arbitrary non-zero scalars $\alpha_r, \beta_r, \gamma_r$ as long as their product is unity, i.e., $\alpha_r \beta_r \gamma_r = 1$. The resulting [rank-one tensor](@entry_id:202127) is $(\alpha_r a_r) \circ (\beta_r b_r) \circ (\gamma_r c_r) = (\alpha_r \beta_r \gamma_r) (a_r \circ b_r \circ c_r) = a_r \circ b_r \circ c_r$. This is the **scaling indeterminacy**. This can be expressed in matrix form: for any three [diagonal matrices](@entry_id:149228) $D_A, D_B, D_C \in \mathbb{R}^{R \times R}$ satisfying $D_A D_B D_C = I$, the factor matrices $(A D_A, B D_B, C D_C)$ produce the same tensor as $(A, B, C)$ .

This scaling ambiguity implies that the norms of the factor columns are arbitrary. In practice, this can lead to numerical issues where some factor columns grow very large while others shrink toward zero during optimization. To mitigate this, it is standard practice to enforce a normalization, such as constraining the columns of some or all factor matrices to have unit norm. The scaling is then absorbed into an explicit weight vector $\lambda \in \mathbb{R}^R$, e.g., $\mathcal{X} \approx \sum_{r=1}^R \lambda_r (\tilde{a}_r \circ \tilde{b}_r \circ \tilde{c}_r)$ where $\|\tilde{a}_r\|_2 = \|\tilde{b}_r\|_2 = \|\tilde{c}_r\|_2 = 1$. This re-[parameterization](@entry_id:265163) does not change the tensor being modeled and is a crucial step for improving the practical convergence of algorithms like ALS .

### The Distinctive Nature of Tensor Rank

A central concept in tensor decompositions is the notion of rank. However, unlike in the matrix case, [tensor rank](@entry_id:266558) is a more complex and multifaceted idea.

The **CP rank** of a tensor $\mathcal{X}$, denoted $\text{rank}_{CP}(\mathcal{X})$, is the smallest integer $R$ for which an exact CP decomposition exists. This is the tensor equivalent of [matrix rank](@entry_id:153017). However, a key distinction arises when we consider the ranks of the tensor's matricizations (or unfoldings). The **Tucker ranks** (or multilinear ranks) of a third-order tensor are the matrix ranks of its unfoldings: $(r_1, r_2, r_3) = (\text{rank}(X_{(1)}), \text{rank}(X_{(2)}), \text{rank}(X_{(3)}))$.

A fundamental relationship is that the CP rank is bounded below by the maximum Tucker rank:

$$
\text{rank}_{CP}(\mathcal{X}) \ge \max(r_1, r_2, r_3)
$$

This inequality arises because the mode-$n$ unfolding of a rank-$R$ CP model, $X_{(n)} = A^{(n)} (\odot_{m \ne n} A^{(m)})^T$, has a rank of at most $R$. One might intuitively expect equality to hold, but this is not generally true for tensors of order three or higher. There exist tensors for which the CP rank is strictly greater than the rank of any unfolding . For example, a tensor $\mathcal{X}^{(1)} \in \mathbb{R}^{3 \times 2 \times 2}$ can have Tucker ranks $(3, 2, 2)$, which immediately implies its CP rank must be at least $3$. Conversely, a tensor $\mathcal{X}^{(2)} \in \mathbb{R}^{2 \times 2 \times 2}$ can have Tucker ranks $(2, 2, 1)$, yet its CP rank can be $2$, not $1$. This illustrates that low rank in one unfolding does not necessarily imply a low CP rank for the tensor itself .

This distinction is not merely a theoretical curiosity. It has profound practical implications. The set of tensors with CP rank at most $R$ is not a closed set for $R > 1$. This means a sequence of rank-$R$ tensors can converge to a limit tensor whose CP rank is actually greater than $R$. This property is at the heart of many numerical difficulties encountered when fitting CP models, as we will explore later.

### The Alternating Least Squares (ALS) Algorithm

The goal of CP decomposition is to find the factor matrices that best approximate a given data tensor $\mathcal{X}$. This is typically formulated as a nonlinear least-squares problem:

$$
\min_{A, B, C} \left\| \mathcal{X} - \sum_{r=1}^{R} a_r \circ b_r \circ c_r \right\|_F^2
$$

Simultaneously optimizing for all factor matrices is a difficult non-convex problem. The Alternating Least Squares (ALS) algorithm circumvents this by adopting a **[block coordinate descent](@entry_id:636917)** strategy. It optimizes for one factor matrix at a time, keeping the others fixed. When $B$ and $C$ are fixed, the objective function becomes a convex quadratic function of $A$, which corresponds to a standard linear [least-squares problem](@entry_id:164198). The algorithm cycles through updates for $A$, $B$, and $C$ until convergence.

#### Derivation of the ALS Update Rules

To derive the update rule for factor matrix $A$, we fix $B$ and $C$. The key is to express the optimization problem in matrix form. This is achieved by matricizing, or unfolding, the tensor. The mode-1 unfolding of the CP model is given by a convenient matrix product:

$$
\left(\sum_{r=1}^{R} a_r \circ b_r \circ c_r\right)_{(1)} = A (C \odot B)^T
$$

Here, $\odot$ denotes the **Khatri-Rao product**, which is a column-wise Kronecker product. For two matrices with the same number of columns, say $B \in \mathbb{R}^{J \times R}$ and $C \in \mathbb{R}^{K \times R}$, their Khatri-Rao product $B \odot C$ is a matrix in $\mathbb{R}^{JK \times R}$ whose $r$-th column is the Kronecker product of the $r$-th columns of $B$ and $C$, i.e., $(B \odot C)_{:,r} = b_r \otimes c_r$ . Note that the order matters: the standard expression for the mode-1 unfolding uses $C \odot B$.

With this identity, the subproblem for $A$ becomes a [standard matrix](@entry_id:151240) [least-squares problem](@entry_id:164198):

$$
\min_{A} \| X_{(1)} - A (C \odot B)^T \|_F^2
$$

The solution is characterized by the **normal equations**, obtained by setting the gradient with respect to $A$ to zero. This yields:

$$
A \left( (C \odot B)^T (C \odot B) \right) = X_{(1)} (C \odot B)
$$

The term on the right, $X_{(1)} (C \odot B)$, is a crucial computational kernel known as the **Matricized-Tensor Times Khatri-Rao Product (MTTKRP)**. For a dense tensor of size $I \times J \times K$, this contraction is the most computationally expensive part of the ALS sweep, with a cost of $O(IJKR)$ . The term on the left, $(C \odot B)^T (C \odot B)$, can be simplified using a fundamental property of the Khatri-Rao product: it is equivalent to the element-wise or **Hadamard product** ($*$) of the Gram matrices of the constituent factors :

$$
(C \odot B)^T (C \odot B) = (C^T C) * (B^T B)
$$

This identity follows from the property $(u_1 \otimes v_1)^T (u_2 \otimes v_2) = (u_1^T u_2)(v_1^T v_2)$.

Assuming the matrix $(C^T C) * (B^T B)$ is invertible, we can write the closed-form update for $A$ as:

$$
A \leftarrow X_{(1)} (C \odot B) \left( (C^T C) * (B^T B) \right)^{-1}
$$

The updates for $B$ and $C$ are derived by cyclic permutation of the indices and factors  :

$$
B \leftarrow X_{(2)} (C \odot A) \left( (C^T C) * (A^T A) \right)^{-1}
$$
$$
C \leftarrow X_{(3)} (B \odot A) \left( (B^T B) * (A^T A) \right)^{-1}
$$

In summary, a full ALS sweep consists of computing the MTTKRP and solving a small $R \times R$ linear system for each mode. The bulk of the computation is spent on the MTTKRP, which involves the full data tensor, while the remaining operations (forming Gram matrices, Hadamard products, and solving the system) are typically much cheaper as their cost scales with $R$, which is usually much smaller than $I, J, K$ .

### Properties and Pathologies of CP-ALS

While the mechanics of ALS are straightforward, its behavior is governed by a rich set of theoretical properties and potential numerical pitfalls.

#### Uniqueness of the CP Decomposition

A key motivation for using CP decomposition is that, unlike many other matrix and tensor factorizations, it can yield essentially unique factors under mild conditions. **Essential uniqueness** means the factor matrices are unique up to the inherent permutation and scaling ambiguities. A celebrated result by Joseph Kruskal provides a [sufficient condition](@entry_id:276242) for uniqueness.

The condition is based on the **Kruskal rank** of the factor matrices. The Kruskal [rank of a matrix](@entry_id:155507) $M$, denoted $k_M$, is the largest integer $k$ such that *any* set of $k$ columns of $M$ is [linearly independent](@entry_id:148207). **Kruskal's uniqueness theorem** states that if the sum of the Kruskal ranks of the factor matrices is sufficiently large relative to the CP rank $R$, the decomposition is essentially unique. For a third-order tensor:

$$
k_A + k_B + k_C \ge 2R + 2
$$

For example, consider a rank-4 decomposition with specific factor matrices $A, B, C$. By systematically checking the [linear independence](@entry_id:153759) of all subsets of their columns, one can compute their Kruskal ranks, say $k_A=4, k_B=3, k_C=3$. In this case, the sum is $4+3+3=10$. The condition requires this to be at least $2R+2 = 2(4)+2=10$. Since $10 \ge 10$, the condition is met, and the decomposition is essentially unique .

#### Convergence and Numerical Stability

As an instance of Block Coordinate Descent, the convergence properties of ALS are well-understood. The sequence of [objective function](@entry_id:267263) values is guaranteed to be non-increasing. For the iterates themselves to converge to a [stationary point](@entry_id:164360) (a point where the gradient of the objective is zero), two main conditions are generally required :
1.  **Bounded Iterates**: The sequence of factor matrices must remain in a compact set. As discussed, the scaling ambiguity can lead to divergent factor norms. Applying normalization at each step ensures the iterates remain bounded.
2.  **Unique Subproblem Solutions**: Each [least-squares](@entry_id:173916) subproblem must have a unique solution. This is guaranteed if the matrix to be inverted, e.g., $(C^T C) * (B^T B)$, is nonsingular. This is equivalent to the Khatri-Rao product $C \odot B$ having full column rank.

The [numerical stability](@entry_id:146550) of each update step is determined by the **condition number** of this [normal equations](@entry_id:142238) matrix. A large condition number implies that small perturbations in the right-hand side (the MTTKRP) can lead to large errors in the computed factor matrix. The conditioning is highly sensitive to collinearity in the factor matrices. If columns in $B$ and $C$ become nearly collinear, the Gram matrices $B^T B$ and $C^T C$ will have off-diagonal entries close to 1. The Hadamard product preserves this structure, leading to a nearly-singular [normal matrix](@entry_id:185943) and an unstable update . For instance, if two columns $b_r, b_s$ are nearly parallel ($b_r^T b_s \approx 1$) and two columns $c_r, c_s$ are also nearly parallel ($c_r^T c_s \approx 1$), the $(r,s)$ entry of the [normal matrix](@entry_id:185943) will be approximately $1$, making it ill-conditioned .

#### Degeneracy and Swamps

The most notorious pathology of CP-ALS is the phenomenon of **degeneracy**, often leading to "swamps" where the algorithm's convergence becomes exceedingly slow. This issue is rooted in the fact that the set of tensors of CP rank at most $R$ is not closed. This allows a sequence of rank-$R$ tensors to converge to a tensor of rank greater than $R$.

A classic example demonstrates this behavior. It is possible to construct a one-parameter family of rank-2 tensors, $X(t)$, that converges to a specific rank-3 tensor, $T$, as the parameter $t \to 0^+$. In this construction, the factor vectors of the two rank-one components of $X(t)$ become perfectly collinear in the limit, while their associated scaling weights diverge to infinity in a way that their sum remains finite. Specifically, the model takes the form $\frac{1}{t} (\cdots) - \frac{1}{t} (\cdots)$ .

When an ALS algorithm attempts to fit a rank-2 model to such a rank-3 tensor $T$, it may enter a "swamp" region of the objective landscape. The algorithm tries to replicate the degenerate sequence by driving two of its factor components toward collinearity while their norms grow. This causes the [normal equations](@entry_id:142238) matrix $(C^T C) * (B^T B)$ to become progressively more ill-conditioned, as its columns become nearly linearly dependent. Consequently, the ALS updates become minuscule, and the [objective function](@entry_id:267263) value decreases at an agonizingly slow rate, creating a long plateau. This behavior is not a failure of the ALS algorithm itself but a consequence of attempting to fit a low-rank model to data that is pathologically close to the boundary of the set of rank-$R$ tensors. It is the algebraic manifestation of the non-closed nature of the CP model .