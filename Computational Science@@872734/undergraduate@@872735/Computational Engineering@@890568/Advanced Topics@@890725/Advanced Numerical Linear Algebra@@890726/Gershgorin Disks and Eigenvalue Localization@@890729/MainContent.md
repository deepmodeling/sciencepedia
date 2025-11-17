## Introduction
Eigenvalue problems are ubiquitous in [computational engineering](@entry_id:178146), forming the mathematical backbone for analyzing everything from [structural vibrations](@entry_id:174415) and circuit behavior to the stability of [numerical algorithms](@entry_id:752770). While computing exact eigenvalues is often the ultimate goal, it can be a computationally demanding task, especially for [large-scale systems](@entry_id:166848). In many practical scenarios, however, a precise answer is not required; instead, knowing the approximate location of eigenvalues is sufficient to make critical design and analysis decisions. What if there was a simple, low-cost way to draw a "map" in the complex plane and know with certainty that all eigenvalues reside within its borders?

This is precisely the knowledge gap addressed by the Gershgorin circle theorem, a remarkably elegant tool for [eigenvalue localization](@entry_id:162719). This article provides a comprehensive exploration of this theorem, designed for the undergraduate computational engineer. Over the next three chapters, you will gain a robust understanding of both its theory and application. The "Principles and Mechanisms" chapter will lay the groundwork, defining Gershgorin disks and exploring the core theorems that govern eigenvalue containment, counting, and [matrix invertibility](@entry_id:152978). Following that, the "Applications and Interdisciplinary Connections" chapter will demonstrate the theorem's power in practice, showing how it is used to assess system stability, bound physical quantities, and analyze complex networks. Finally, the "Hands-On Practices" section will allow you to solidify your knowledge by applying these concepts to solve concrete engineering problems.

## Principles and Mechanisms

Following the introduction to [eigenvalue problems](@entry_id:142153) in [computational engineering](@entry_id:178146), this chapter delves into the principles and mechanisms of a foundational tool for their analysis: the Gershgorin circle theorem. While finding exact eigenvalues can be computationally intensive, localizing them within specific regions of the complex plane is often sufficient for tasks such as assessing [system stability](@entry_id:148296) or designing numerical methods. The Gershgorin theorem provides an elegant and inexpensive way to establish such localizations.

### The Gershgorin Circle Theorem: A Fundamental Bound

The core idea of the theorem is to associate each diagonal element of a square matrix with a disk in the complex plane that is guaranteed to contain at least one eigenvalue.

#### Defining the Gershgorin Disks

For any square matrix $A \in \mathbb{C}^{n \times n}$ with entries $a_{ij}$, we define the **$i$-th Gershgorin disk**, denoted $\mathcal{D}_i$, as the [closed disk](@entry_id:148403) centered at the diagonal entry $a_{ii}$ with a radius $R_i$ equal to the sum of the [absolute values](@entry_id:197463) of the off-diagonal entries in that row. Formally:
$$
\mathcal{D}_i = \left\{ z \in \mathbb{C} : |z - a_{ii}| \leq R_i \right\}, \quad \text{where} \quad R_i = \sum_{j \neq i} |a_{ij}|
$$
The center of the disk is determined solely by the diagonal entry of a row, while its radius is a measure of the "weight" of the off-diagonal entries in that same row.

As a concrete example, consider the $n \times n$ matrix $J_n$ where every entry is $1$. For any row $i$, the diagonal entry is $a_{ii} = 1$. The radius is the sum of the absolute values of the $n-1$ other entries in the row, so $R_i = \sum_{j \neq i} |1| = n-1$. Consequently, all $n$ Gershgorin disks for this matrix are identical: a single disk centered at $z=1$ with radius $n-1$. The union of all disks, which we denote as the Gershgorin region $G$, is simply this one disk, $G = \{z \in \mathbb{C} : |z - 1| \leq n-1\}$. This simple construction already provides valuable information. For $n \geq 2$, the known eigenvalues of $J_n$, which are $\lambda=n$ (with [multiplicity](@entry_id:136466) 1) and $\lambda=0$ (with [multiplicity](@entry_id:136466) $n-1$), are both contained within this region, as the theorem predicts. For the eigenvalue $\lambda=0$, its distance to the center is $|0-1|=1$, which is less than or equal to the radius $n-1$ for all $n \ge 2$ [@problem_id:2396926].

#### The First Theorem: Eigenvalue Containment

The first and most fundamental part of the Gershgorin theorem states that all eigenvalues of a matrix $A$ are located within the union of all its $n$ Gershgorin disks.
$$
\sigma(A) \subseteq \bigcup_{i=1}^{n} \mathcal{D}_i
$$
where $\sigma(A)$ represents the spectrum (the set of all eigenvalues) of $A$. This theorem provides a bounded region in the complex plane where all eigenvalues must reside.

This result connects directly to the concept of [matrix norms](@entry_id:139520). The **[spectral radius](@entry_id:138984)**, $\rho(A)$, is the maximum absolute value of any eigenvalue: $\rho(A) = \max_{\lambda \in \sigma(A)} |\lambda|$. From the containment property, any eigenvalue $\lambda$ must be in some disk $\mathcal{D}_i$, so $|\lambda - a_{ii}| \le R_i$. By the triangle inequality, this implies $|\lambda| \le |a_{ii}| + R_i$. Since this holds for every eigenvalue, it must hold for the one with the largest modulus, so $\rho(A) \le \max_{i} (|a_{ii}| + R_i)$. The term on the right is precisely the definition of the **induced matrix [infinity-norm](@entry_id:637586)**, $\|A\|_{\infty} = \max_{i} \sum_{j=1}^{n} |a_{ij}|$. Thus, the Gershgorin circle theorem provides an intuitive, geometric proof for the fundamental inequality $\rho(A) \le \|A\|_{\infty}$ [@problem_id:2396951]. This bound is not always tight, but in certain important cases, it is exact. For instance, if a matrix $A$ has non-negative entries and a constant row sum $r$ (i.e., $\sum_{j=1}^{n} a_{ij} = r$ for all $i$), it can be shown that $r$ is an eigenvalue. In this case, $\|A\|_{\infty} = r$, and since $\rho(A) \ge r$, we must have $\rho(A) = \|A\|_{\infty} = r$. The Gershgorin bound is perfectly sharp here [@problem_id:2396951].

### Refining the Eigenvalue Hunt: Techniques for Tighter Bounds

The region defined by the union of Gershgorin disks can sometimes be quite large. Fortunately, there are systematic ways to refine and shrink this region, providing a more precise localization of the eigenvalues.

#### The Power of Transposition: Column Disks

A key insight is that a matrix $A$ and its transpose $A^T$ share the same set of eigenvalues, i.e., $\sigma(A) = \sigma(A^T)$. We can therefore apply the Gershgorin theorem to $A^T$. The row disks of $A^T$ correspond to the **column disks** of the original matrix $A$. The $j$-th column disk, $\mathcal{D}^{\text{col}}_{j}$, is centered at the diagonal entry $a_{jj}$ with a radius $C_j$ equal to the sum of the [absolute values](@entry_id:197463) of the off-diagonal entries in column $j$:
$$
\mathcal{D}^{\text{col}}_{j} = \left\{ z \in \mathbb{C} : |z - a_{jj}| \leq C_j \right\}, \quad \text{where} \quad C_j = \sum_{i \neq j} |a_{ij}|
$$
Since the eigenvalues must lie in the union of row disks *and* in the union of column disks, they must lie in the **intersection** of these two regions:
$$
\sigma(A) \subseteq \left( \bigcup_{i=1}^{n} \mathcal{D}^{\text{row}}_{i} \right) \cap \left( \bigcup_{j=1}^{n} \mathcal{D}^{\text{col}}_{j} \right)
$$
This intersection is always a subset of (or equal to) the original row-disk region, often providing a significantly tighter bound. For an [upper triangular matrix](@entry_id:173038), for instance, the column disk for the first column is just the point $a_{11}$, immediately pinpointing it as an eigenvalue [@problem_id:2396936].

This refinement is crucial in stability analysis. A system is stable if all its eigenvalues lie in the open left half-plane (LHP), where $\Re(z)  0$. Suppose the union of row disks lies entirely in the LHP. This might suggest stability. However, the union of column disks might intersect the right half-plane (RHP). Since the true eigenvalues are in the intersection, we cannot conclude stability from the row disks alone. A careful engineer must always consider both sets of disks before making a judgment [@problem_id:2396962].

#### Similarity Transformations: A Change of Perspective

An even more powerful refinement technique involves similarity transformations. A matrix $B$ is similar to $A$ if $B = P^{-1}AP$ for some invertible matrix $P$. A fundamental property of [similar matrices](@entry_id:155833) is that they have identical eigenvalues. This means we can apply the Gershgorin theorem to *any* matrix $B$ similar to $A$ to obtain a valid (and potentially much smaller) localization region for the eigenvalues of $A$.

A particularly effective and widely used choice is a **diagonal similarity transformation**, where $P$ is an invertible diagonal matrix, $D = \text{diag}(d_1, d_2, \dots, d_n)$ with $d_i \neq 0$. The transformed matrix is $B = D^{-1}AD$, and its entries are given by $b_{ij} = d_i^{-1} a_{ij} d_j$. Notice that the diagonal entries remain unchanged: $b_{ii} = d_i^{-1} a_{ii} d_i = a_{ii}$. The centers of the Gershgorin disks are invariant under diagonal scaling. However, the off-diagonal entries are scaled, which changes the radii:
$$
R'_i = \sum_{j \neq i} |b_{ij}| = \sum_{j \neq i} |d_i^{-1} a_{ij} d_j| = \frac{1}{|d_i|} \sum_{j \neq i} |a_{ij}| |d_j|
$$
By carefully choosing the scaling factors $d_i$, we can often significantly reduce the radii of the disks. One common strategy is to treat the scaling factors as variables and use [optimization techniques](@entry_id:635438) to find the values that minimize the total area or total sum of radii of the resulting disks, thereby "squeezing" the localization region as tightly as possible around the true eigenvalues [@problem_id:1365596].

### Advanced Insights: Structure, Disjointness, and Invertibility

The Gershgorin framework offers deeper insights when we consider the structure of the matrix and the topology of the disks.

#### Disjoint Disks and Eigenvalue Counting (Taussky's Theorem)

The second part of the Gershgorin theorem, often attributed to Olga Taussky-Todd, provides a way to count eigenvalues. It states:

*If a union of $k$ Gershgorin disks is disjoint from the union of the remaining $n-k$ disks, then the first union contains exactly $k$ eigenvalues of $A$, and the second union contains exactly $n-k$ eigenvalues (counted with algebraic multiplicity).*

This is a powerful result. For example, if we can construct a $2 \times 2$ matrix whose two Gershgorin disks do not touch, we immediately know that each disk contains exactly one eigenvalue. Two disks $\mathcal{D}_1$ and $\mathcal{D}_2$ are disjoint if the distance between their centers is greater than the sum of their radii: $|a_{11} - a_{22}| > R_1 + R_2$ [@problem_id:2396902].

This principle can be extended. For a **real matrix** ($A \in \mathbb{R}^{n \times n}$), its non-real eigenvalues must occur in [complex conjugate](@entry_id:174888) pairs. Suppose we find a set of $k$ Gershgorin disks that is disjoint from the others and is also symmetric with respect to the real axis (i.e., if $z$ is in the set, so is its conjugate $\bar{z}$). By the theorem, this region contains exactly $k$ eigenvalues. Because the matrix is real and the region is symmetric, the multiset of these $k$ eigenvalues must itself be closed under [complex conjugation](@entry_id:174690). A direct consequence is that if $k$ is odd, at least one of the eigenvalues in this region must be real [@problem_id:2396898].

#### Reducibility and Block Structures

A matrix $A$ is called **reducible** if it can be rearranged, through a simultaneous permutation of rows and columns, into a block upper triangular form. Otherwise, it is **irreducible**. This permutation is a [similarity transformation](@entry_id:152935) $P A P^T$, where $P$ is a [permutation matrix](@entry_id:136841). A key property is that the multiset of Gershgorin disks (the collection of center-radius pairs) is invariant under this reordering; the permutation merely shuffles the association of disks with row indices [@problem_id:2396970].

If a matrix is reducible, say into a block [diagonal form](@entry_id:264850) $A' = \begin{pmatrix} B_1  0 \\ 0  B_2 \end{pmatrix}$, its spectrum is simply the union of the spectra of the blocks: $\sigma(A) = \sigma(A') = \sigma(B_1) \cup \sigma(B_2)$. The Gershgorin analysis can then be performed on the blocks separately. If the union of Gershgorin disks for block $B_1$ is disjoint from the union of disks for block $B_2$, Taussky's theorem can be applied to count the number of eigenvalues contributed by each block. For a computational model with weakly coupled subsystems, this mathematical property reflects the physical separation of the system's dynamic modes [@problem_id:2396970].

#### Gershgorin Disks and Matrix Invertibility

A matrix is invertible if and only if zero is not one of its eigenvalues. The Gershgorin theorem provides a simple [sufficient condition](@entry_id:276242) for invertibility: if the origin $z=0$ does not lie in the union of any of the Gershgorin disks, the matrix is guaranteed to be invertible. This is equivalent to the condition that $0 \notin \mathcal{D}_i$ for all $i$, which means $|0 - a_{ii}| > R_i$, or:
$$
|a_{ii}| > \sum_{j \neq i} |a_{ij}| \quad \text{for all } i=1, \dots, n.
$$
A matrix satisfying this condition is called **strictly [diagonally dominant](@entry_id:748380) (SDD)**. The Levy-Desplanques theorem formally states that any [strictly diagonally dominant matrix](@entry_id:198320) is invertible.

However, this is a sufficient, not a necessary, condition. A matrix can be invertible even if one of its Gershgorin disks contains the origin. For instance, if a diagonal entry $a_{kk}$ is zero, its disk $\mathcal{D}_k$ is centered at the origin, and the simple SDD test fails. This does not mean the matrix is singular. In such cases, more powerful criteria may be needed. For example, one can show that if the matrix $A^T A$ is strictly diagonally dominant, then $A^T A$ is invertible, which in turn implies that $A$ must be invertible. This provides an alternative pathway to prove invertibility when the most direct Gershgorin test is inconclusive [@problem_id:2396905].