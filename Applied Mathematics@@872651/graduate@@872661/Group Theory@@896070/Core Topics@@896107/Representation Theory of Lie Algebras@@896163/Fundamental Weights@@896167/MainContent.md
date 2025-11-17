## Introduction
In the study of symmetries that govern the laws of mathematics and physics, semi-simple Lie algebras provide a foundational framework. While the root system offers a complete structural blueprint of these algebras, its basis of [simple roots](@entry_id:197415) is not always the most practical for analyzing their representations. This creates a gap between the abstract algebraic structure and its concrete manifestation in [vector spaces](@entry_id:136837), which is crucial for physical applications. This article introduces the concept of **fundamental weights**, the elementary building blocks of representation theory, which bridge this gap. By working in the basis of fundamental weights, the intricate world of representations becomes organized and computationally accessible.

This article will guide you through the theory and application of fundamental weights across three comprehensive chapters. In **Principles and Mechanisms**, you will learn the formal definition of fundamental weights, their duality relationship with roots, and the essential algebraic machinery that connects them. Following this, **Applications and Interdisciplinary Connections** will demonstrate how these concepts are used to characterize representations, decompose tensor products, and build sophisticated models in theoretical physics, from Grand Unified Theories to Conformal Field Theory. Finally, **Hands-On Practices** will offer a selection of problems to solidify your computational skills and deepen your conceptual understanding of this vital topic.

## Principles and Mechanisms

In the study of semi-simple Lie algebras, the root system provides a complete blueprint of the algebra's structure. The basis of [simple roots](@entry_id:197415), $\{\alpha_i\}$, is fundamental to constructing this system. However, for the theory of representations, it is often more convenient to work with a different, albeit related, basis in the dual space of the Cartan subalgebra, $\mathfrak{h}^*$. This is the basis of **fundamental weights**, $\{\omega_i\}$, which can be seen as the elementary building blocks from which all irreducible representations are constructed. This chapter will elucidate the definition, properties, and principal applications of these essential objects.

### The Definition of Fundamental Weights

While the [simple roots](@entry_id:197415) $\{\alpha_i\}$ form a basis for $\mathfrak{h}^*$, they are not orthonormal. Their geometric relationship is captured by the inner product $(\cdot, \cdot)$ derived from the Killing form, and more abstractly by the Cartan matrix. To work effectively with representations, we introduce a basis that is "dual" to the [simple roots](@entry_id:197415) in a specific sense.

For each [simple root](@entry_id:635422) $\alpha_j$, we first define its corresponding **simple coroot**, $\alpha_j^\vee$, as:
$$
\alpha_j^\vee = \frac{2\alpha_j}{(\alpha_j, \alpha_j)}
$$
The set of simple [coroots](@entry_id:193338), $\{\alpha_j^\vee\}$, also forms a basis for $\mathfrak{h}^*$. The fundamental weights, $\{\omega_i\}$, are then defined as the basis dual to the simple [coroots](@entry_id:193338) with respect to the inner product.

**Definition:** For a simple Lie algebra of rank $n$, the set of **fundamental weights** $\{\omega_i\}_{i=1}^n$ is the basis of $\mathfrak{h}^*$ satisfying the duality relation:
$$
(\omega_i, \alpha_j^\vee) = \delta_{ij}
$$
where $\delta_{ij}$ is the Kronecker delta. Substituting the definition of the simple coroot, this defining property is most commonly expressed as:
$$
\frac{2(\omega_i, \alpha_j)}{(\alpha_j, \alpha_j)} = \delta_{ij}
$$
This equation is the cornerstone of the theory of fundamental weights. It implies that the $i$-th fundamental weight, $\omega_i$, is orthogonal to all [simple roots](@entry_id:197415) $\alpha_j$ for $j \neq i$, in the sense of the bilinear form appearing in the definition. The value of the expression $\frac{2(\lambda, \alpha_j)}{(\alpha_j, \alpha_j)}$ for any weight $\lambda$ gives the $j$-th **Dynkin label** of that weight. The definition thus states that the $i$-th fundamental weight $\omega_i$ is the unique weight whose Dynkin labels are $(0, \dots, 1, \dots, 0)$, with the '1' appearing in the $i$-th position.

### The Interplay of Bases: From Roots to Weights and Back

Since both the [simple roots](@entry_id:197415) $\{\alpha_i\}$ and the fundamental weights $\{\omega_i\}$ are bases for the same vector space $\mathfrak{h}^*$, they must be expressible as linear combinations of one another. The matrices governing this change of basis are of central importance and are directly related to the Cartan matrix $A$, whose entries are $A_{ij} = \frac{2(\alpha_i, \alpha_j)}{(\alpha_j, \alpha_j)}$.

Let us first consider expressing a [simple root](@entry_id:635422) in the basis of fundamental weights. We can write $\alpha_j = \sum_{k=1}^n c_{jk} \omega_k$ for some coefficients $c_{jk}$. To find these coefficients, we can take the inner product with a simple coroot $\alpha_i^\vee$:
$$
(\alpha_j, \alpha_i^\vee) = \left( \sum_{k=1}^n c_{jk} \omega_k, \alpha_i^\vee \right) = \sum_{k=1}^n c_{jk} (\omega_k, \alpha_i^\vee) = \sum_{k=1}^n c_{jk} \delta_{ki} = c_{ji}
$$
By definition, the left-hand side is precisely the Cartan matrix entry $A_{ji}$. This yields the remarkably simple relation:
$$
\alpha_j = \sum_{i=1}^n A_{ji} \omega_i
$$
This shows that the coefficients for expanding a [simple root](@entry_id:635422) $\alpha_j$ in the weight basis are given by the $j$-th row of the Cartan matrix. For example, for the Lie algebra $\mathfrak{sp}(6)$ (type $C_3$), the Cartan matrix is $A = \begin{pmatrix} 2 & -1 & 0 \\ -1 & 2 & -1 \\ 0 & -2 & 2 \end{pmatrix}$. The expansion for the second [simple root](@entry_id:635422) $\alpha_2$ is immediately read from the second row: $\alpha_2 = -1 \cdot \omega_1 + 2 \cdot \omega_2 - 1 \cdot \omega_3$. This principle can be extended by linearity to express any element of the root lattice, such as a positive root $\beta = \sum_i n_i \alpha_i$, in the fundamental weight basis.

The inverse transformation, expressing fundamental weights in terms of [simple roots](@entry_id:197415), is equally important. Let us write $\omega_i = \sum_{k=1}^n C_{ik} \alpha_k$. Using the defining relation of the weights:
$$
\delta_{ij} = \frac{2(\omega_i, \alpha_j)}{(\alpha_j, \alpha_j)} = \frac{2}{(\alpha_j, \alpha_j)} \left( \sum_{k=1}^n C_{ik} \alpha_k, \alpha_j \right) = \sum_{k=1}^n C_{ik} \frac{2(\alpha_k, \alpha_j)}{(\alpha_j, \alpha_j)} = \sum_{k=1}^n C_{ik} A_{kj}
$$
In matrix notation, this is simply the identity matrix $I = C A^T$. Thus, the matrix of coefficients $C$ is the inverse of the transpose of the Cartan matrix, $C = (A^T)^{-1}$. This leads to the expansion:
$$
\omega_i = \sum_{k=1}^n ((A^T)^{-1})_{ik} \alpha_k
$$
This formula is computationally powerful, though it requires inverting the Cartan matrix. For the same $C_3$ algebra, one can compute the inverse of the Cartan matrix to be $A^{-1} = \begin{pmatrix} 1 & 1 & 1/2 \\ 1 & 2 & 1 \\ 1 & 2 & 3/2 \end{pmatrix}$. As $A$ is not symmetric, we need $(A^T)^{-1} = (A^{-1})^T = \begin{pmatrix} 1 & 1 & 1 \\ 1 & 2 & 2 \\ 1/2 & 1 & 3/2 \end{pmatrix}$. The expansion of the second fundamental weight $\omega_2$ can then be read from the second row of $(A^T)^{-1}$, yielding $\omega_2 = 1 \cdot \alpha_1 + 2 \cdot \alpha_2 + 2 \cdot \alpha_3$.

### Geometric Properties of Fundamental Weights

The fundamental weights, as vectors in $\mathfrak{h}^*$, have lengths and relative angles determined by the inner product. Computing these geometric quantities provides deeper insight into the structure of the [weight space](@entry_id:195741).

A concrete way to perform these calculations is to realize the root system within a Euclidean space $\mathbb{R}^n$ with a standard [orthonormal basis](@entry_id:147779) $\{e_i\}$. One can write down explicit vector expressions for the [simple roots](@entry_id:197415) in this basis and then solve for the fundamental weights using their defining relation. For example, for the Lie algebra $B_3 \cong \mathfrak{so}(7)$, the [simple roots](@entry_id:197415) can be given as $\alpha_1 = e_1 - e_2$, $\alpha_2 = e_2 - e_3$, and $\alpha_3 = e_3$. By systematically applying the conditions $(\omega_i, \alpha_j) = \delta_{ij} \frac{(\alpha_j, \alpha_j)}{2}$, one can solve for the fundamental weights in this basis. This procedure yields $\omega_1 = e_1$ and $\omega_2 = e_1 + e_2$. The inner product is then straightforward: $(\omega_1, \omega_2) = (e_1, e_1 + e_2) = (e_1, e_1) + (e_1, e_2) = 1 + 0 = 1$. This method can be generalized to any rank $n$, as demonstrated in calculating the squared norms of weights for the $B_n$ series.

While this approach is intuitive, a more elegant and powerful method exists that bypasses the need for an explicit orthonormal basis. We can derive a general formula for the inner product of two fundamental weights. Starting from $\omega_i = \sum_k ((A^T)^{-1})_{ik} \alpha_k$:
$$
(\omega_i, \omega_j) = \left( \sum_k ((A^T)^{-1})_{ik} \alpha_k, \omega_j \right) = \sum_k ((A^T)^{-1})_{ik} (\alpha_k, \omega_j)
$$
Using the defining relation $(\omega_j, \alpha_k) = \delta_{jk} \frac{(\alpha_k, \alpha_k)}{2}$, we get:
$$
(\omega_i, \omega_j) = \sum_k ((A^T)^{-1})_{ik} \delta_{kj} \frac{(\alpha_k, \alpha_k)}{2} = ((A^T)^{-1})_{ij} \frac{(\alpha_j, \alpha_j)}{2}
$$
For a **simply-laced** algebra (types A, D, E), all roots have the same length and the Cartan matrix is symmetric. By normalizing this squared length to 2, i.e., $(\alpha_j, \alpha_j) = 2$ for all $j$, the formula simplifies dramatically:
$$
(\omega_i, \omega_j) = (A^{-1})_{ij} \quad \text{(for simply-laced algebras with } (\alpha_k, \alpha_k)=2)
$$
This remarkable result states that the Gram matrix of the fundamental weights in the inner product is precisely the inverse of the Cartan matrix. This allows for the direct computation of all norms and angles between fundamental weights once $A^{-1}$ is known. For instance, in the case of $D_4$, one can compute the angle between the spinor weights $\omega_3$ and $\omega_4$ by simply calculating $A^{-1}$ and reading off the entries $(A^{-1})_{33}$, $(A^{-1})_{44}$, and $(A^{-1})_{34}$ to use in the cosine formula.

### Lattices, the Quotient Group, and the Center

The [simple roots](@entry_id:197415) and fundamental weights each generate a lattice in $\mathfrak{h}^*$.

**Definition:**
- The **root lattice**, denoted $Q$ or $\Lambda_R$, is the set of all integer linear combinations of the [simple roots](@entry_id:197415): $Q = \left\{ \sum_{i=1}^n c_i \alpha_i \mid c_i \in \mathbb{Z} \right\}$.
- The **[weight lattice](@entry_id:195778)**, denoted $P$, is the set of all integer [linear combinations](@entry_id:154743) of the fundamental weights: $P = \left\{ \sum_{i=1}^n k_i \omega_i \mid k_i \in \mathbb{Z} \right\}$. Any vector $\lambda \in P$ is called an integral weight.

From the expansion $\omega_i = \sum_k ((A^T)^{-1})_{ik} \alpha_k$, we see that since the entries of $(A^T)^{-1}$ are not always integers, the fundamental weights are not always in the root lattice. However, every [simple root](@entry_id:635422) can be written as an integer combination of fundamental weights (since the Cartan matrix $A$ has integer entries), which implies that the root lattice is a sublattice of the [weight lattice](@entry_id:195778): $Q \subseteq P$.

The structure of the finite abelian [quotient group](@entry_id:142790) $P/Q$ is of profound importance. It is isomorphic to the center of the simply connected compact Lie group corresponding to the Lie algebra. The [order of an element](@entry_id:145276) $[\lambda] \in P/Q$ is the smallest positive integer $k$ such that $k\lambda \in Q$.

To find the order of a fundamental weight $[\omega_i]$ in $P/Q$, we examine its expansion in the [simple root](@entry_id:635422) basis, $\omega_i = \sum_j ((A^T)^{-1})_{ij} \alpha_j$. The coefficients $((A^T)^{-1})_{ij}$ are rational numbers. The order of $[\omega_i]$ is the smallest positive integer $k$ that, when multiplied by $\omega_i$, clears all denominators in its coefficients, resulting in an element of the root lattice $Q$. For the Lie algebra $D_5$, expressing $\omega_1$ in the [simple root](@entry_id:635422) basis reveals coefficients of $1/2$, so its order is 2.

In some cases, it can be more intuitive to work in an explicit [orthonormal basis](@entry_id:147779). For $D_5$, the spinor weight $\omega_5$ can be written as $\frac{1}{2}(\epsilon_1 + \epsilon_2 + \epsilon_3 + \epsilon_4 + \epsilon_5)$. To determine the smallest integer $k$ such that $k\omega_5$ is in the root lattice, one must find the smallest $k$ for which $k\omega_5$ can be written as $\sum c_i \alpha_i$ for integers $c_i$. This leads to a system of linear equations whose solution shows that $k=4$ is the minimal integer. This confirms that the order of the spinor weight $[\omega_5]$ in $P/Q$ for $D_5$ is 4.

### Application in Representation Theory

The ultimate utility of fundamental weights lies in their role as the building blocks of representation theory. An irreducible finite-dimensional representation of a simple Lie algebra is uniquely characterized by its **highest weight**, $\lambda$. A weight is a highest weight if and only if it is a **dominant integral weight**, which means it can be written as a non-negative integer combination of the fundamental weights:
$$
\lambda = \sum_{i=1}^n k_i \omega_i, \quad k_i \in \mathbb{Z}_{\ge 0}
$$
The integers $k_i$ are precisely the Dynkin labels of the [highest weight](@entry_id:202808). The representation with [highest weight](@entry_id:202808) $\lambda$ is denoted $V(\lambda)$.

An important operation on representations is the **contragredient** or [dual representation](@entry_id:146263), $V^*$. If $V(\lambda)$ is irreducible, then so is its dual. The [highest weight](@entry_id:202808) of the [dual representation](@entry_id:146263), $\lambda^*$, is related to the lowest weight of the original representation. The lowest weight of $V(\lambda)$ is given by $w_0(\lambda)$, where $w_0$ is the unique longest element of the Weyl group $W$. The highest weight of the contragredient is then given by the simple formula:
$$
\lambda^* = -w_0(\lambda)
$$
The action of $w_0$ on the fundamental weights is given by $w_0(\omega_i) = -\omega_{\sigma(i)}$ for some permutation $\sigma$ of the indices $\{1, \dots, n\}$, which corresponds to a symmetry of the Dynkin diagram. For the Lie algebra series $A_n$, this action is particularly simple: $w_0(\omega_i) = -\omega_{n+1-i}$.

This provides a straightforward algorithm for finding the [highest weight](@entry_id:202808) of a [dual representation](@entry_id:146263). For example, consider the Lie algebra $A_4$ and the [irreducible representation](@entry_id:142733) $V(\lambda)$ with highest weight $\lambda = \omega_1 + 2\omega_3$. To find the highest weight $\lambda^*$ of the contragredient representation, we compute:
$$
\lambda^* = -w_0(\omega_1 + 2\omega_3) = -w_0(\omega_1) - 2w_0(\omega_3)
$$
Using the formula for $A_4$ (where $n=4$), we have $w_0(\omega_1) = -\omega_{5-1} = -\omega_4$ and $w_0(\omega_3) = -\omega_{5-3} = -\omega_2$. Substituting these in, we find:
$$
\lambda^* = -(-\omega_4) - 2(-\omega_2) = 2\omega_2 + \omega_4
$$
Thus, the dual of the representation $V(\omega_1 + 2\omega_3)$ is $V(2\omega_2 + \omega_4)$. This demonstrates how the concepts of fundamental weights and Weyl group symmetries combine to provide powerful and elegant results in the theory of representations.