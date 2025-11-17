## Introduction
The challenge of reconstructing a high-dimensional signal from a small number of measurements is a fundamental [inverse problem](@entry_id:634767) that appears throughout science and engineering. Such [underdetermined linear systems](@entry_id:756304), modeled as $y = Ax$ where there are far fewer measurements than unknown parameters, admit infinite solutions. However, the principle of sparsity—the assumption that the true signal has very few non-zero entries—provides a powerful constraint that makes the problem tractable. While finding the "sparsest" solution is a computationally intractable, NP-hard combinatorial problem, [greedy algorithms](@entry_id:260925) offer an efficient and intuitive path to an accurate answer. This article delves into one of the most foundational and widely used greedy methods: Orthogonal Matching Pursuit (OMP).

Across the following chapters, you will gain a comprehensive understanding of this powerful technique. In **Principles and Mechanisms**, we will dissect the OMP algorithm step-by-step, exploring its iterative selection and projection process, the theoretical guarantees that ensure its success, and the critical practical considerations for a robust implementation. Next, in **Applications and Interdisciplinary Connections**, we will journey through a diverse range of fields—from geophysical tomography and [data assimilation](@entry_id:153547) to image processing and machine learning—to witness how the core ideas of OMP are adapted and applied to solve complex, real-world problems. Finally, the **Hands-On Practices** section provides an opportunity to solidify your knowledge by working through concrete examples that highlight the algorithm's mechanics and theoretical boundaries. We begin by examining the fundamental principles that make greedy [sparse recovery](@entry_id:199430) possible.

## Principles and Mechanisms

In the context of underdetermined [linear inverse problems](@entry_id:751313), where the number of measurements $m$ is less than the number of unknown parameters $n$, the system $y = Ax$ admits an infinite number of solutions. The principle of sparsity provides a powerful regularization framework, asserting that the true [state vector](@entry_id:154607) $x$ has very few non-zero entries. This assumption fundamentally transforms the problem from an ill-posed linear algebraic one into a combinatorial search for the correct subset of active parameters.

### The Combinatorial Nature of Sparse Recovery

The core of the sparse recovery problem is to identify the locations of the non-zero entries in the vector $x$. This set of locations is known as the **support** of the vector, formally defined as:
$$
\operatorname{supp}(x) = \{ j \in \{1, 2, \dots, n\} \mid x_j \neq 0 \}
$$
A vector is said to be **$k$-sparse** if the size, or cardinality, of its support is at most $k$, i.e., $|\operatorname{supp}(x)| \le k$.

Identifying this unknown support is a fundamentally **combinatorial task**. If we knew the support $S = \operatorname{supp}(x)$, we could reduce the problem to solving $y = A_S x_S$, where $A_S$ is the submatrix of $A$ containing only the columns indexed by $S$, and $x_S$ is the vector of non-zero coefficients. Since $|S|=k$ is typically much smaller than $m$, this reduced system is often overdetermined and can be solved uniquely and stably using standard [least-squares](@entry_id:173916) methods. The challenge lies in the fact that the true support $S$ is unknown. For a given sparsity level $k$, there are $\binom{n}{k}$ possible support sets. An exhaustive search through all these possibilities to find the one that best explains the data is computationally intractable for any non-trivial problem size, as this problem is known to be NP-hard [@problem_id:3387212] [@problem_id:3387226]. This intractability motivates the development of efficient algorithms that can find the true support, or a good approximation thereof, without a combinatorial search. Greedy algorithms, such as Orthogonal Matching Pursuit, provide one such powerful heuristic approach.

### The Orthogonal Matching Pursuit (OMP) Algorithm

Orthogonal Matching Pursuit (OMP) is a canonical [greedy algorithm](@entry_id:263215) that iteratively builds an estimate of the support set. Instead of testing all possible supports, OMP makes a locally optimal choice at each step, adding one index at a time to its estimate of the true support. The complete procedure can be broken down into a sequence of fundamental steps [@problem_id:3387214].

#### The OMP Iteration

The algorithm proceeds as follows:

1.  **Initialization**: Begin with an iteration counter $t=0$, an empty support set $S^{(0)} = \emptyset$, a zero solution estimate $x^{(0)} = 0$, and an initial residual $r^{(0)}$ equal to the measurement vector itself: $r^{(0)} = y$.

2.  **Greedy Selection**: At each iteration $t=1, 2, \dots$, identify the column of the dictionary $A$ that is most correlated with the current residual $r^{(t-1)}$. This is achieved by finding the index $j^{(t)}$ that maximizes the absolute value of the inner product:
    $$
    j^{(t)} = \operatorname{argmax}_{j \in \{1, \dots, n\}} |\langle a_j, r^{(t-1)} \rangle|
    $$

3.  **Support Update**: Add the newly identified index to the support set:
    $$
    S^{(t)} = S^{(t-1)} \cup \{j^{(t)}\}
    $$

4.  **Orthogonal Projection**: This is the defining "orthogonal" step of OMP. Compute a new solution estimate $x^{(t)}$ by finding the coefficients that best fit the original data $y$ using only the atoms in the current support set $S^{(t)}$. This is a classical [least-squares problem](@entry_id:164198):
    $$
    x^{(t)} = \operatorname{argmin}_{w \text{ s.t. } \operatorname{supp}(w) \subseteq S^{(t)}} \|y - Aw\|_2
    $$
    The solution involves projecting $y$ onto the subspace spanned by the columns of $A_{S^{(t)}}$. The non-zero entries of $x^{(t)}$, denoted $x_{S^{(t)}}^{(t)}$, are given by $x_{S^{(t)}}^{(t)} = (A_{S^{(t)}}^\top A_{S^{(t)}})^{-1} A_{S^{(t)}}^\top y$.

5.  **Residual Update**: Update the residual to reflect the portion of the data unexplained by the new estimate:
    $$
    r^{(t)} = y - Ax^{(t)} = y - A_{S^{(t)}}x_{S^{(t)}}^{(t)}
    $$
    A crucial property of this step is that the new residual $r^{(t)}$ is, by construction of the [least-squares solution](@entry_id:152054), orthogonal to the subspace spanned by the columns in $S^{(t)}$. That is, $\langle a_j, r^{(t)} \rangle = 0$ for all $j \in S^{(t)}$. This ensures that the algorithm does not select the same atom twice and continues to seek out new directions to explain the remaining part of the signal.

6.  **Stopping**: The iterative process continues until a stopping criterion is met. This will be discussed in detail later.

#### The Necessity of Column Normalization

The greedy selection step, which is the heart of the algorithm, relies on the inner product $\langle a_j, r \rangle$ to measure the "match" between an atom $a_j$ and the residual $r$. For this comparison to be meaningful, the dictionary atoms must be normalized. Standard practice is to enforce unit $\ell_2$-norm for all columns: $\|a_j\|_2 = 1$ for all $j$.

The reason for this becomes clear from the geometric interpretation of the inner product: $\langle a_j, r \rangle = \|a_j\|_2 \|r\|_2 \cos(\theta_j)$, where $\theta_j$ is the angle between $a_j$ and $r$. The selection rule maximizes $|\langle a_j, r \rangle|$. If the norms $\|a_j\|_2$ are not equal, this score confounds two different properties: the directional alignment, captured by $|\cos(\theta_j)|$, and the atom's intrinsic scale, $\|a_j\|_2$. An atom with a very large norm could be selected even if it is poorly aligned with the residual, simply because its large norm inflates the inner product. By enforcing $\|a_j\|_2 = 1$, the selection criterion simplifies to maximizing $\|r\|_2 |\cos(\theta_j)|$, which, for a fixed residual $r$, is equivalent to maximizing $|\cos(\theta_j)|$. This ensures the algorithm selects the atom that is most geometrically aligned with the residual, which is the intended behavior [@problem_id:3387265].

Consider a simple scenario with a residual $r = (1, 0)^{\top}$ and two atoms, $a_1 = (1, 0)^{\top}$ and $a_2 = (60, 80)^{\top}$. Here, $a_1$ is perfectly aligned with $r$, while $a_2$ is not. However, the unnormalized selection scores are $| \langle r, a_1 \rangle | = 1$ and $| \langle r, a_2 \rangle | = 60$. An unnormalized OMP would incorrectly select the poorly aligned but high-magnitude atom $a_2$. Normalizing $a_2$ gives $a_2' = (0.6, 0.8)^{\top}$, and the score becomes $|\langle r, a_2' \rangle| = 0.6$, which is less than the score for $a_1$. Normalization restores a [scale-invariant](@entry_id:178566) and geometrically meaningful selection.

It is a common error to believe that the subsequent [least-squares](@entry_id:173916) projection step can compensate for a biased selection. It cannot. OMP is a greedy algorithm, and its choices are irrevocable. If a suboptimal atom is added to the support set due to scaling bias, the algorithm is committed to that choice, and the final solution will likely be suboptimal [@problem_id:3387265]. Furthermore, it is important to note that column normalization is complementary to, not a substitute for, [data whitening](@entry_id:636289). In [data assimilation](@entry_id:153547) problems with heterogeneous noise covariance $R$, one typically pre-processes the data via whitening ($y' = R^{-1/2}y$, $A' = R^{-1/2}A$). This step ensures the noise is isotropic in the measurement space, but it does not guarantee that the columns of the new dictionary $A'$ are normalized. Thus, one should first whiten the data and then normalize the columns of the resulting dictionary $A'$ [@problem_id:3387265].

### Guarantees for Exact Recovery

While OMP is a heuristic, it is possible to provide formal guarantees that it will perfectly recover the true $k$-sparse signal $x^\star$ in the noiseless case ($y = Ax^\star$). These guarantees depend on certain structural properties of the dictionary $A$.

First, it is important to distinguish between the conditions that ensure a $k$-sparse solution is **unique** and the (stricter) conditions that ensure OMP can **find** it. If two different $k$-sparse vectors, $x_1$ and $x_2$, produce the same measurement $y$, then $A(x_1 - x_2) = 0$. The difference vector $h = x_1 - x_2$ is in the [null space](@entry_id:151476) of $A$ and is at most $2k$-sparse. Therefore, a unique $k$-sparse solution exists if and only if the [null space](@entry_id:151476) of $A$ contains no non-zero vectors with sparsity $2k$ or less. This leads to the **spark condition**: a $k$-sparse solution is unique if $\operatorname{spark}(A) > 2k$, where $\operatorname{spark}(A)$ is the smallest number of linearly dependent columns in $A$ [@problem_id:3387207]. Even if a unique solution exists by this criterion, OMP might fail to find it if the dictionary's structure is misleading.

#### Mutual Coherence

A simple, intuitive measure of a dictionary's structure is its **[mutual coherence](@entry_id:188177)**, $\mu(A)$. For a dictionary with unit-norm columns, it is defined as the largest absolute inner product between any two distinct columns:
$$
\mu(A) = \max_{i \neq j} |\langle a_i, a_j \rangle|
$$
The [mutual coherence](@entry_id:188177) ranges from $0$ (for an orthogonal set of columns) to $1$. It quantifies the "worst-case" similarity between any two atoms. A low coherence means the atoms are well-distinguished, which is ideal for sparse recovery.

The success of OMP's first step depends on the correlation with a correct atom, $| \langle a_i, y \rangle |$ for $i \in \operatorname{supp}(x^\star)$, being larger than any [spurious correlation](@entry_id:145249), $| \langle a_j, y \rangle |$ for $j \notin \operatorname{supp}(x^\star)$. We can bound these quantities using $\mu(A)$. For a "spurious" atom $j \notin \operatorname{supp}(x^\star)$, the correlation is bounded by the interference from all true atoms:
$$
|\langle a_j, y \rangle| = \left| \sum_{i \in \operatorname{supp}(x^\star)} x_i^\star \langle a_j, a_i \rangle \right| \le \sum_{i \in \operatorname{supp}(x^\star)} |x_i^\star| |\langle a_j, a_i \rangle| \le \mu(A) \|x^\star\|_1
$$
For a "correct" atom $i \in \operatorname{supp}(x^\star)$, the correlation can be lower-bounded by considering the contribution from $x_i^\star$ itself and subtracting the worst-case interference from other correct atoms:
$$
|\langle a_i, y \rangle| \ge |x_i^\star| - \left| \sum_{l \in \operatorname{supp}(x^\star), l \neq i} x_l^\star \langle a_i, a_l \rangle \right| \ge |x_i^\star| - \mu(A) \sum_{l \in \operatorname{supp}(x^\star), l \neq i} |x_l^\star|
$$
[@problem_id:3387222]. These bounds show that if $\mu(A)$ is small enough, the signal from a true coefficient will dominate the interference. A well-known [sufficient condition](@entry_id:276242) derived from this logic is that if the non-zero entries of $x^\star$ have equal magnitude, OMP is guaranteed to select a correct atom in the first step if $\mu(A)  1/(2k-1)$ [@problem_id:3387222]. A more general condition, which guarantees exact recovery of *any* $k$-sparse signal in $k$ steps, is:
$$
k  \frac{1}{2}\left(1 + \frac{1}{\mu(A)}\right)
$$
This condition is quite strict and often not met in practice, motivating the search for weaker conditions [@problem_id:3387207].

#### The Restricted Isometry Property (RIP)

A more powerful and less restrictive framework for analyzing [sparse recovery algorithms](@entry_id:189308) is the **Restricted Isometry Property (RIP)**. A matrix $A$ is said to satisfy the RIP of order $k$ if there exists a small constant $\delta_k \in [0, 1)$, called the restricted isometry constant, such that for all $k$-sparse vectors $v$:
$$
(1 - \delta_k) \|v\|_2^2 \le \|Av\|_2^2 \le (1 + \delta_k) \|v\|_2^2
$$
Geometrically, this means that any submatrix $A_S$ formed by $k$ or fewer columns of $A$ acts almost like an isometry: it nearly preserves the lengths of vectors. By the [polarization identity](@entry_id:271819), this also implies that it nearly preserves angles. In essence, RIP ensures that any small subset of columns is "nearly orthogonal," preventing sparse vectors from being mapped near the origin or being mapped to the same point [@problem_id:3387235].

The RIP provides a sufficient condition for the success of OMP that is generally weaker than coherence-based conditions. It has been shown that if the dictionary $A$ satisfies the RIP with a constant $\delta_{k+1}$ small enough, OMP is guaranteed to recover any $k$-sparse signal in $k$ steps. A well-known condition is:
$$
\delta_{k+1}  \frac{1}{\sqrt{k} + 1}
$$
The use of the constant $\delta_{k+1}$ (rather than $\delta_k$) is crucial because the analysis of each OMP step involves comparing the residual's correlation with the remaining correct atoms against its correlation with a single incorrect atom, a process that involves subspaces spanned by up to $k+1$ atoms [@problem_id:3387235].

### Practical Implementation and Extensions

Beyond the core theory, several practical aspects are critical for a successful implementation of OMP.

#### Numerical Stability of the Least-Squares Subproblem

At each iteration, OMP must solve the least-squares problem $\min_w \|A_S w - y\|_2$. A common textbook approach is to form and solve the **normal equations**:
$$
(A_S^\top A_S) w = A_S^\top y
$$
While mathematically sound, this method can be numerically unstable in [finite-precision arithmetic](@entry_id:637673). The reason lies in its effect on the problem's condition number. The $2$-norm condition number of the matrix $A_S^\top A_S$ is the square of the condition number of $A_S$ itself: $\kappa_2(A_S^\top A_S) = \kappa_2(A_S)^2$. If the columns of $A_S$ are nearly linearly dependent, $A_S$ will be ill-conditioned (large $\kappa_2(A_S)$), and forming the product $A_S^\top A_S$ will square this large number, potentially leading to catastrophic loss of precision and an inaccurate solution for $w$ [@problem_id:3387264].

A numerically robust alternative is to solve the least-squares problem using an orthogonal-triangular (**QR**) decomposition of $A_S$. By computing $A_S = QR$, where $Q$ has orthonormal columns and $R$ is upper triangular, the least-squares problem is transformed into solving the well-conditioned triangular system:
$$
Rw = Q^\top y
$$
This system can be solved efficiently and stably via [back substitution](@entry_id:138571). This approach works with the condition number $\kappa_2(R) = \kappa_2(A_S)$, completely avoiding the squaring effect of the [normal equations](@entry_id:142238). For robust computation of the QR factorization itself, methods like Householder reflections are preferred over the unstable classical Gram-Schmidt algorithm. In cases of severe ill-conditioning, QR factorization with [column pivoting](@entry_id:636812) can provide additional stability [@problem_id:3387264].

#### Stopping Criteria

A crucial practical question is when to terminate the OMP iterations. The choice of stopping criterion depends on the available prior knowledge, particularly about the signal's sparsity and the noise level in the data $y = Ax^\star + \varepsilon$.

1.  **Known Sparsity**: If the sparsity level $k$ of the true signal is known, the simplest and most common criterion is to run the algorithm for exactly $k$ iterations. This enforces the prior knowledge directly on the solution.

2.  **Residual Norm Threshold**: When $k$ is unknown or the data is noisy, we must avoid overfitting the noise. The **[discrepancy principle](@entry_id:748492)** provides a statistically sound stopping point. Once OMP has identified the true signal support, the remaining residual is essentially just projected noise. For i.i.d. Gaussian noise $\varepsilon \sim \mathcal{N}(0, \sigma^2 I)$, the squared norm of this projected noise, $\|r^{(t)}\|_2^2$, will be on the order of $(m-t)\sigma^2$. Therefore, a reliable [stopping rule](@entry_id:755483) is to terminate when the [residual norm](@entry_id:136782) falls below a threshold calibrated to the noise level, i.e., stop when $\|r^{(t)}\|_2 \le \tau$, where $\tau$ is chosen based on $\sigma$, $m$, and $t$.

3.  **Correlation Threshold**: An alternative statistical criterion is to examine the greedy selection score itself. At each step, we select the atom with the maximum correlation $\gamma^{(t)} = \max_j |\langle a_j, r^{(t)} \rangle|$. If the residual contains no more signal and is purely noise, this maximum correlation will be small. We can set a threshold and stop when $\gamma^{(t)}$ falls below it. This is a [multiple hypothesis testing](@entry_id:171420) problem: we are testing if any of the remaining atoms are significantly correlated with the residual. A statistically sound threshold must account for taking the maximum over many atoms and can be derived from [extreme value theory](@entry_id:140083) or by using a Bonferroni correction, often leading to a threshold on the order of $\sigma\sqrt{2\log n}$ [@problem_id:3387241].

#### Application to Compressible Signals

The framework of sparse recovery extends beyond signals that are strictly sparse to a broader class known as **[compressible signals](@entry_id:747592)**. These are signals whose coefficients, when sorted by magnitude, decay rapidly. Such signals are not strictly sparse but can be well-approximated by a sparse vector.

For [compressible signals](@entry_id:747592), OMP provides a powerful approximation guarantee. While it may not recover the full signal perfectly, its greedy nature of selecting the most correlated atom at each step tends to prioritize identifying the coefficients with the largest magnitudes first, especially when the dictionary has low coherence. After $k$ iterations, OMP produces a $k$-sparse approximation whose error is bounded by a constant factor of the error of the *best possible* $k$-term approximation. This near-optimal performance makes OMP a valuable tool not only for exact recovery of [sparse signals](@entry_id:755125) but also for the efficient approximation of [compressible signals](@entry_id:747592), a common scenario in [data assimilation](@entry_id:153547) and many other fields [@problem_id:3387217].

In conclusion, Orthogonal Matching Pursuit offers a computationally efficient and conceptually intuitive greedy approach to the NP-hard problem of [sparse recovery](@entry_id:199430). Its mechanism, based on iterative correlation and orthogonal projection, is backed by robust theoretical guarantees under well-defined conditions on the dictionary, such as low [mutual coherence](@entry_id:188177) or the Restricted Isometry Property. Proper practical implementation requires careful attention to numerical stability and the use of statistically-grounded stopping criteria, enabling its successful application to a wide range of inverse problems involving both sparse and [compressible signals](@entry_id:747592).