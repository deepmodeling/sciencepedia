## Introduction
The question of how the eigenvalues of a [symmetric matrix](@entry_id:143130) respond to an additive perturbation is a cornerstone of [matrix analysis](@entry_id:204325), with deep implications across computational science and engineering. While one's initial intuition might suggest a simple additive relationship, the reality is far more subtle and elegant. Understanding this relationship is critical for analyzing the stability of physical systems, the reliability of numerical algorithms, and the robustness of data-driven models. This article tackles the knowledge gap between naive intuition and the rigorous reality of [eigenvalue perturbation](@entry_id:152032) theory for symmetric matrices.

This article is structured to build a comprehensive understanding of Weyl's inequalities. The journey begins in the **Principles and Mechanisms** chapter, where we will establish the variational foundation of eigenvalues using the Courant-Fischer min-max theorem and use this powerful geometric framework to derive Weyl's inequalities, revealing the origin of their characteristic index shifts. Following this, the **Applications and Interdisciplinary Connections** chapter will bridge theory and practice, demonstrating how these inequalities are applied to assess [numerical stability in algorithms](@entry_id:145005), guarantee robustness in optimization and control theory, and model complex phenomena in fields like [spectral graph theory](@entry_id:150398) and [computational mechanics](@entry_id:174464). Finally, the **Hands-On Practices** section will provide concrete problems to solidify your command of these concepts, guiding you from direct verification to computational exploration of the conditions for equality.

## Principles and Mechanisms

The study of how eigenvalues of a [symmetric matrix](@entry_id:143130) are affected by an additive perturbation is central to many areas of mathematics, physics, and engineering. This chapter delves into the principles and mechanisms that govern this relationship, culminating in the celebrated Weyl's inequalities. Our exploration will be grounded in the [variational characterization of eigenvalues](@entry_id:155784), which provides a powerful geometric framework for understanding their behavior.

### The Variational Foundation: Courant–Fischer Min–Max Theorem

For a real [symmetric matrix](@entry_id:143130) $A \in \mathbb{R}^{n \times n}$, the **[spectral theorem](@entry_id:136620)** guarantees that all its eigenvalues are real and that there exists an [orthonormal basis of eigenvectors](@entry_id:180262). This reality of the spectrum allows for a canonical ordering of the eigenvalues, which, by convention in this context, we take to be nonincreasing:
$$
\lambda_1(A) \ge \lambda_2(A) \ge \dots \ge \lambda_n(A)
$$

While eigenvalues are formally defined as the roots of the characteristic polynomial, this definition offers limited intuition about their behavior under matrix operations like addition. A more powerful and geometric perspective is provided by the **Rayleigh quotient**, defined for any nonzero vector $x \in \mathbb{R}^n$ as:
$$
R_A(x) = \frac{x^\top A x}{x^\top x}
$$
Because $A$ is symmetric, the scalar $x^\top A x$ is always real, and thus the Rayleigh quotient is always a real value. In fact, its range is precisely the interval between the smallest and largest eigenvalues, $[\lambda_n(A), \lambda_1(A)]$. The largest eigenvalue, $\lambda_1(A)$, is the maximum value of $R_A(x)$, and the smallest, $\lambda_n(A)$, is its minimum value.

The **Courant–Fischer min–max theorem** extends this concept to provide a variational characterization for every eigenvalue. It defines each $\lambda_k(A)$ as the result of a [constrained optimization](@entry_id:145264) of the Rayleigh quotient over subspaces of $\mathbb{R}^n$. For each $k \in \{1, \dots, n\}$, the $k$-th eigenvalue is given by :
$$
\lambda_k(A) = \max_{\substack{S \subset \mathbb{R}^n \\ \dim(S)=k}} \; \min_{\substack{x \in S \\ \|x\|_2=1}} \; x^\top A x
$$
This is the **max-min** formulation. It can be interpreted as finding the $k$-dimensional subspace $S$ that "pushes up" its minimum Rayleigh quotient as high as possible. An equivalent **min-max** formulation is:
$$
\lambda_k(A) = \min_{\substack{U \subset \mathbb{R}^n \\ \dim(U)=n-k+1}} \; \max_{\substack{x \in U \\ \|x\|_2=1}} \; x^\top A x
$$
This dual perspective will be indispensable in our proofs. This entire variational framework is the foundation upon which Weyl's inequalities are built.

### The Perturbation Problem: A Deceptively Simple Question

Consider two real [symmetric matrices](@entry_id:156259), $A$ and $B$. If we form their sum, $C = A+B$, how are the eigenvalues of $C$ related to the eigenvalues of $A$ and $B$? A natural first guess might be that the ordered eigenvalues simply add, or at least that an inequality like $\lambda_k(A+B) \le \lambda_k(A) + \lambda_k(B)$ holds for each index $k$.

However, a simple [counterexample](@entry_id:148660) reveals this intuition to be flawed. Consider the $2 \times 2$ [symmetric matrices](@entry_id:156259) :
$$
A = \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}, \qquad B = \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix}
$$
The eigenvalues are easily found. Since $A$ is diagonal, its eigenvalues are its diagonal entries: $\lambda_1(A) = 1$ and $\lambda_2(A) = -1$. The characteristic polynomial of $B$ is $\lambda^2 - 1 = 0$, so its eigenvalues are also $\lambda_1(B) = 1$ and $\lambda_2(B) = -1$.
The sum is $A+B = \begin{pmatrix} 1  1 \\ 1  -1 \end{pmatrix}$. Its [characteristic polynomial](@entry_id:150909) is $(1-\lambda)(-1-\lambda) - 1 = \lambda^2 - 2 = 0$, yielding eigenvalues $\lambda_1(A+B) = \sqrt{2}$ and $\lambda_2(A+B) = -\sqrt{2}$.

Let us test the naive inequality for the second eigenvalue, $k=2$:
$$
\lambda_2(A+B) \le \lambda_2(A) + \lambda_2(B)
$$
Substituting the computed values gives:
$$
-\sqrt{2} \le (-1) + (-1) = -2
$$
This statement is false, as $-\sqrt{2} \approx -1.414 > -2$. The gap, defined as $\Delta = \lambda_2(A+B) - (\lambda_2(A) + \lambda_2(B))$, is $\Delta = -\sqrt{2} - (-2) = 2 - \sqrt{2} > 0$, explicitly demonstrating the failure of the simple index-matched inequality. This failure motivates a deeper inquiry: a more subtle relationship must be at play, one that involves a shift in indices.

### The Main Theorem: Weyl's Inequalities

The correct relationship between the eigenvalues of $A$, $B$, and $A+B$ was discovered by Hermann Weyl. His inequalities elegantly resolve the issue of index-matching by introducing specific index shifts that arise naturally from the geometry of subspaces.

**Weyl's Inequalities.** Let $A, B \in \mathbb{R}^{n \times n}$ be symmetric matrices. Let the eigenvalues of any such matrix $M$ be ordered nonincreasingly, $\lambda_1(M) \ge \lambda_2(M) \ge \dots \ge \lambda_n(M)$. Then the following inequalities hold:

1.  For all integers $i, j$ with $1 \le i, j \le n$ and $i+j-1 \le n$:
    $$
    \lambda_{i+j-1}(A+B) \le \lambda_i(A) + \lambda_j(B)
    $$

2.  For all integers $i, j$ with $1 \le i, j \le n$ and $i+j-n \ge 1$:
    $$
    \lambda_i(A) + \lambda_j(B) \le \lambda_{i+j-n}(A+B)
    $$

The proof of these inequalities is a beautiful application of the Courant–Fischer theorem and a fundamental result from linear algebra concerning the dimension of intersecting subspaces   .

Let's sketch the proof for the first inequality. Our goal is to establish an upper bound on $\lambda_{i+j-1}(A+B)$. The min-max formulation is the natural tool:
$$
\lambda_{i+j-1}(A+B) = \min_{\substack{U \subset \mathbb{R}^n \\ \dim(U)=n-(i+j-1)+1}} \; \max_{\substack{x \in U \\ \|x\|_2=1}} \; (R_A(x) + R_B(x))
$$
The key is to construct a specific test subspace $U^*$ of the required dimension, $d = n-i-j+2$, for which we can effectively bound the Rayleigh quotient. Let $V_A$ be the subspace spanned by the eigenvectors of $A$ corresponding to eigenvalues $\lambda_i(A), \dots, \lambda_n(A)$, and let $V_B$ be the subspace for eigenvalues $\lambda_j(B), \dots, \lambda_n(B)$ of $B$.
For any $x \in V_A$, we have $R_A(x) \le \lambda_i(A)$. The dimension is $\dim(V_A) = n-i+1$.
For any $x \in V_B$, we have $R_B(x) \le \lambda_j(B)$. The dimension is $\dim(V_B) = n-j+1$.

Now consider their intersection, $U^* = V_A \cap V_B$. By the Grassmann dimension formula, $\dim(U^*) = \dim(V_A) + \dim(V_B) - \dim(V_A+V_B) \ge (n-i+1) + (n-j+1) - n = n-i-j+2$. So, the intersection has at least the dimension $d$ required by the min-max theorem. For any [unit vector](@entry_id:150575) $x$ in this intersection $U^*$, both bounds apply simultaneously:
$$
R_{A+B}(x) = R_A(x) + R_B(x) \le \lambda_i(A) + \lambda_j(B)
$$
This means that for our constructed subspace $U^*$ (or a $d$-dimensional subspace within it), the maximum Rayleigh quotient is bounded: $\max_{x \in U^*} R_{A+B}(x) \le \lambda_i(A) + \lambda_j(B)$. Since $\lambda_{i+j-1}(A+B)$ is the *minimum* of these maximums over *all* possible subspaces of dimension $d$, it must be less than or equal to the value for our specific choice. This completes the argument. The proof for the second inequality proceeds analogously using the max-min formulation.

The index shifts $i+j-1$ and $i+j-n$ are therefore not arbitrary; they are precisely the conditions dictated by the geometry of subspace intersections, ensuring a common ground where the behaviors of $A$ and $B$ can be simultaneously controlled.

### Key Corollaries and Related Principles

While the general form of Weyl's inequalities is powerful, several special cases are of immense practical importance.

#### Two-Sided Eigenvalue Bounds

Perhaps the most frequently cited consequence of Weyl's inequalities is a direct two-sided bound on the eigenvalues of the sum $A+B$ . These bounds are obtained by making extremal choices for the index $j$ in the general theorems.

-   **Upper Bound**: In the inequality $\lambda_{i+j-1}(A+B) \le \lambda_i(A) + \lambda_j(B)$, let $j=1$. The index on the left becomes $i+1-1=i$. This gives:
    $$
    \lambda_i(A+B) \le \lambda_i(A) + \lambda_1(B)
    $$
    This holds for any $i \in \{1, \dots, n\}$. Here, $\lambda_1(B)$ is the largest eigenvalue of $B$, which is also the maximum value of its Rayleigh quotient.

-   **Lower Bound**: In the inequality $\lambda_i(A) + \lambda_j(B) \le \lambda_{i+j-n}(A+B)$, let $j=n$. The index on the right becomes $i+n-n=i$. This gives:
    $$
    \lambda_i(A) + \lambda_n(B) \le \lambda_i(A+B)
    $$
    This also holds for any $i \in \{1, \dots, n\}$. Here, $\lambda_n(B)$ is the [smallest eigenvalue](@entry_id:177333) of $B$.

Combining these, we obtain the elegant two-sided inequality for each eigenvalue $\lambda_i(A+B)$:
$$
\lambda_i(A) + \lambda_n(B) \le \lambda_i(A+B) \le \lambda_i(A) + \lambda_1(B)
$$
This provides an interval of width $\lambda_1(B) - \lambda_n(B)$ that contains each perturbed eigenvalue. If we consider $B$ to be a perturbation matrix $E$, this implies that for any $i$, $|\lambda_i(A+E) - \lambda_i(A)| \le \max(|\lambda_1(E)|, |\lambda_n(E)|)$. Since for a symmetric matrix $E$, the spectral norm $\|E\|_2$ is precisely $\max(|\lambda_1(E)|, |\lambda_n(E)|)$, we arrive at the absolute perturbation bound:
$$
|\lambda_i(A+E) - \lambda_i(A)| \le \|E\|_2
$$
This per-eigenvalue bound is a remarkably strong result, showing that the eigenvalues of a [symmetric matrix](@entry_id:143130) are perfectly conditioned with respect to symmetric perturbations.

#### Cauchy's Interlacing Theorem

A related but distinct principle is **Cauchy's interlacing theorem**. It describes the relationship between the eigenvalues of a [symmetric matrix](@entry_id:143130) $A \in \mathbb{R}^{n \times n}$ and those of any [principal submatrix](@entry_id:201119). Let $A_m$ be a [principal submatrix](@entry_id:201119) of $A$ obtained by deleting $n-m$ rows and the corresponding columns. If $\lambda_1(A) \ge \dots \ge \lambda_n(A)$ and $\mu_1 \ge \dots \ge \mu_m$ are the ordered eigenvalues of $A$ and $A_m$ respectively, then they interlace:
$$
\lambda_k(A) \ge \mu_k \ge \lambda_{k+n-m}(A) \quad \text{for } k=1, \dots, m.
$$
In the common case where we remove a single row and column ($m=n-1$), the inequalities become:
$$
\lambda_1(A) \ge \mu_1 \ge \lambda_2(A) \ge \mu_2 \ge \dots \ge \lambda_{n-1}(A) \ge \mu_{n-1} \ge \lambda_n(A)
$$
This can be proven elegantly using the Courant-Fischer theorem. For instance, to show $\mu_k \le \lambda_k(A)$, we note that $\mathbb{R}^m$ (the space on which $A_m$ acts) can be viewed as a subspace of $\mathbb{R}^n$. The max-min characterization $\lambda_k(A) = \max_{\dim(S)=k} \min_{x \in S} R_A(x)$ involves maximizing over all $k$-dimensional subspaces. Since the set of $k$-dimensional subspaces of $\mathbb{R}^m$ is a subset of all $k$-dimensional subspaces of $\mathbb{R}^n$, the maximum over the larger set must be at least as great, implying $\lambda_k(A) \ge \mu_k$.

### Context and Comparisons

The power of Weyl's inequalities is best appreciated when contrasted with other eigenvalue bounding techniques.

#### Weyl's Inequalities vs. Gershgorin's Circle Theorem

Gershgorin's theorem provides bounds by constructing discs in the complex plane centered at the diagonal entries of a matrix. While general and easy to apply, it is a "local" method that considers only the sum of absolute values of off-diagonal entries in each row, ignoring the matrix's algebraic structure. Weyl's inequalities, by contrast, are "global" and leverage the full structure of the perturbation through the Rayleigh quotient.

Consider a case study with $n=10$, where $T$ is a [tridiagonal matrix](@entry_id:138829) with zeros on the diagonal and ones on the first off-diagonals, and the perturbation is a dense, [rank-one matrix](@entry_id:199014) $E = -3 \mathbf{1}\mathbf{1}^\top$ . The matrix $M=T+E$ has a diagonal of $-3$. Each row of $E$ has entries equal to $-3$, so the Gershgorin radii are large (e.g., $R_1 = |1-3| + \sum_{j=3}^{10}|-3| = 2 + 8 \times 3 = 26$), giving a loose upper bound for $\lambda_1(M)$ of $-3+26=23$.
Weyl's inequality, $\lambda_1(M) \le \lambda_1(T) + \lambda_1(E)$, sees the situation very differently. The perturbation $E$ is negative semidefinite, so its largest eigenvalue is $\lambda_1(E) = 0$. The Weyl bound is simply $\lambda_1(M) \le \lambda_1(T) = 2\cos(\pi/11) \approx 1.96$. The Weyl bound is substantially tighter because the variational approach recognizes that the perturbation, despite its large entries, is structured in a way that cannot increase any eigenvalue.

#### Weyl's Inequalities vs. The Bauer–Fike Theorem

For a general (non-symmetric) [diagonalizable matrix](@entry_id:150100) $A = V \Lambda V^{-1}$, the **Bauer–Fike theorem** states that for any perturbation $E$, every eigenvalue of $A+E$ lies within a distance of $\kappa_2(V) \|E\|_2$ from some eigenvalue of $A$, where $\kappa_2(V) = \|V\|_2 \|V^{-1}\|_2$ is the condition number of the eigenvector matrix. When $A$ is symmetric, its eigenvector matrix can be chosen to be orthogonal, making $\kappa_2(V)=1$. In this case, Bauer-Fike gives a result that looks similar to the Weyl corollary. However, there are crucial differences :
1.  **Pairing:** Weyl's inequality guarantees a per-index bound: the $k$-th new eigenvalue is close to the $k$-th old eigenvalue. Bauer–Fike only guarantees that each new eigenvalue is close to *some* old eigenvalue, without preserving the ordering.
2.  **Conditioning:** For [non-symmetric matrices](@entry_id:153254), the [eigenvector basis](@entry_id:163721) can be nearly linearly dependent, making $\kappa_2(V)$ arbitrarily large. This can lead to extreme sensitivity of eigenvalues, a phenomenon that the Bauer-Fike bound correctly captures but which Weyl's inequalities, restricted to the symmetric case, do not encounter.

#### Weyl's Inequalities vs. Cauchy's Interlacing Theorem

While both are powerful results for symmetric matrices, they apply in different contexts. Weyl's inequalities relate $\lambda(A+B)$ to $\lambda(A)$ and $\lambda(B)$. Cauchy's theorem relates $\lambda(A)$ to $\lambda(A_m)$ where $A_m$ is a [principal submatrix](@entry_id:201119). One can frame the latter as a special perturbation problem where $B$ is a matrix chosen such that $A+B$ is block diagonal. In some cases, the structural specificity of interlacing can provide tighter bounds. For the matrix $A = \begin{pmatrix} 2  1  1 \\ 1  2  1 \\ 1  1  -1 \end{pmatrix}$ and its leading $2 \times 2$ submatrix $A_{11}$, interlacing gives $\mu_2 \le \lambda_2(A)$, which evaluates to $1 \le 1$. A Weyl-type bound derived by treating the problem as a perturbation gives $\mu_2 \le 3$ . The interlacing bound is tighter because it is tailored to the specific structure of forming a [principal submatrix](@entry_id:201119).

### Scope and Tightness

The entire framework of Weyl's inequalities rests on the properties of symmetric (or Hermitian) matrices. The min-max proof fails for general [non-symmetric matrices](@entry_id:153254) because their eigenvalues may be complex (prohibiting a simple ordering) and, more fundamentally, their eigenvalues are not characterized by extremal values of the (now complex-valued) Rayleigh quotient . The correct analogy for general matrices involves singular values, which are themselves the square roots of the eigenvalues of the Hermitian matrix $A^*A$ and thus do admit a min-max characterization and satisfy Weyl-type inequalities.

Finally, it is instructive to ask when the bounds in Weyl's inequalities are met exactly. Consider the two-sided bound $\lambda_k(A) + \lambda_n(B) \le \lambda_k(A+B) \le \lambda_k(A) + \lambda_1(B)$. The tightness is determined by the alignment of the perturbation $B$ with the eigenspaces of $A$.
Let $A$ be a $4 \times 4$ matrix with eigenvalues $\{7, 5, 3, 2\}$ and eigenvectors $\{e_1, e_2, e_3, e_4\}$.
- If we choose a rank-one perturbation $B = u u^\top$ where $u = e_3$, then $A$ and $B$ share the same eigenvectors. The eigenvalues of $A+B$ are simply the sums of the corresponding eigenvalues of $A$ and $B$. In this case, $\lambda_3(B)=0$, $\lambda_1(B)=1$, and we find $\lambda_3(A+B) = \lambda_3(A) + \lambda_1(B) = 3+1=4$. The upper bound is achieved .
- If we choose $u$ to be orthogonal to the subspaces relevant for the calculation of $\lambda_3(A)$, for example, by choosing $u$ in the span of $\{e_1, e_2\}$, then the perturbation may have no effect on $\lambda_3$. If $u = \frac{1}{\sqrt{2}}(e_1+e_2)$, we can show that $\lambda_3(A+B) = \lambda_3(A) = 3$. This corresponds to achieving the lower bound if we view the perturbation as $B - \lambda_n(B)I + \lambda_n(B)I$, where the first term is positive semidefinite .
These examples show that the effect of a perturbation is not just about its "size" (norm), but critically, about its geometric orientation relative to the structure of the original matrix. Weyl's inequalities, derived from the variational principle, beautifully encapsulate this geometric interplay.