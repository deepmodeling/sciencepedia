## Introduction
Determining the eigenvalues of a matrix is a cornerstone of [applied mathematics](@entry_id:170283), with far-reaching implications for stability analysis, algorithm design, and physical modeling. However, calculating eigenvalues directly can be computationally intensive, if not impossible, for large systems. This article addresses this challenge by introducing the powerful concept of [eigenvalue localization](@entry_id:162719)—a set of techniques for estimating the location of eigenvalues in the complex plane quickly and efficiently. We begin in "Principles and Mechanisms" by deriving the celebrated Gershgorin Circle Theorem from first principles and exploring its refinements. Subsequently, "Applications and Interdisciplinary Connections" demonstrates the theorem's immense practical value, from ensuring the stability of engineering systems to analyzing the convergence of algorithms in data science. Finally, "Hands-On Practices" will allow you to solidify your understanding through guided computational exercises. By the end, you will have mastered a fundamental tool for analyzing matrices and the systems they represent.

## Principles and Mechanisms
The determination of a matrix's eigenvalues is a central problem in linear algebra, with profound implications across science and engineering. While direct computation of eigenvalues can be intensive, it is often sufficient, and far more efficient, to determine the approximate location of the eigenvalues in the complex plane. This chapter explores the principles and mechanisms of [eigenvalue localization](@entry_id:162719), focusing on one of the most elegant and useful tools available: the Gershgorin Circle Theorem. We will derive the theorem from first principles, explore its nuances and extensions, and demonstrate its power and limitations through a series of illustrative applications.

### The Gershgorin Circle Theorem: A Fundamental Bound
The **Gershgorin Circle Theorem**, published by Semyon Aranovich Gershgorin in 1931, provides a remarkably simple method for constraining the eigenvalues of any square matrix. The theorem states that every eigenvalue of a matrix lies within the union of a set of specific disks in the complex plane.

Let $A = (a_{ij})$ be an $n \times n$ matrix with entries in $\mathbb{C}$. For each row $i = 1, \dots, n$, we define the **Gershgorin disk** $G_i$ as a [closed disk](@entry_id:148403) in the complex plane centered at the diagonal entry $a_{ii}$ with radius $R_i$, where $R_i$ is the sum of the absolute values of the off-diagonal entries in that row.

Formally, the $i$-th Gershgorin disk is the set:
$G_i = \{ z \in \mathbb{C} \,:\, |z - a_{ii}| \leq R_i \}$, where $R_i = \sum_{j \neq i} |a_{ij}|$.

The theorem asserts that the spectrum of $A$, denoted $\sigma(A)$, is contained within the union of these $n$ disks:
$\sigma(A) \subseteq \bigcup_{i=1}^n G_i$.

The proof of this theorem is both elementary and insightful. Let $\lambda$ be an eigenvalue of $A$ with a corresponding eigenvector $x \neq 0$. The eigenvalue equation is $Ax = \lambda x$, which can be written for each component $i$ as:
$\sum_{j=1}^n a_{ij}x_j = \lambda x_i$.

We can separate the diagonal term from the sum:
$a_{ii}x_i + \sum_{j \neq i} a_{ij}x_j = \lambda x_i$.

Rearranging the terms gives:
$(\lambda - a_{ii})x_i = \sum_{j \neq i} a_{ij}x_j$.

Let $k$ be an index such that $|x_k|$ is the largest component of the eigenvector $x$ in absolute value. Since $x$ is an eigenvector, it is non-zero, so $|x_k| > 0$. We can write the equation for the $k$-th row:
$(\lambda - a_{kk})x_k = \sum_{j \neq k} a_{kj}x_j$.

Taking the absolute value of both sides and applying the triangle inequality, we get:
$|\lambda - a_{kk}| |x_k| = \left| \sum_{j \neq k} a_{kj}x_j \right| \leq \sum_{j \neq k} |a_{kj}| |x_j|$.

By our choice of $k$, we know that $|x_j| \leq |x_k|$ for all $j$. Therefore, we can bound the sum:
$|\lambda - a_{kk}| |x_k| \leq \sum_{j \neq k} |a_{kj}| |x_k| = |x_k| \sum_{j \neq k} |a_{kj}|$.

Since $|x_k| > 0$, we can divide both sides by $|x_k|$ to obtain:
$|\lambda - a_{kk}| \leq \sum_{j \neq k} |a_{kj}| = R_k$.

This inequality shows that the eigenvalue $\lambda$ must be in the $k$-th Gershgorin disk, $G_k$. Since every eigenvalue must have a corresponding eigenvector, every eigenvalue must belong to at least one of the Gershgorin disks. This completes the proof.

A direct consequence of this theorem is an upper bound for the **spectral radius** $\rho(A)$, which is the maximum absolute value of the eigenvalues. Any point $z$ within a disk $G_i$ satisfies $|z| \leq |a_{ii}| + R_i$. Therefore, for any eigenvalue $\lambda$:
$\rho(A) = \max_{\lambda \in \sigma(A)} |\lambda| \leq \max_{z \in \bigcup G_i} |z| = \max_{1 \le i \le n} (|a_{ii}| + R_i)$.

To illustrate, consider the matrix:
$A = \begin{pmatrix} 5  1  -1  0 \\ 2  -4  0  1 \\ 0  3  6  -2 \\ -1  0  1  2 \end{pmatrix}$.

The Gershgorin disks are:
- $G_1$: center $5$, radius $R_1 = |1| + |-1| + |0| = 2$.
- $G_2$: center $-4$, radius $R_2 = |2| + |0| + |1| = 3$.
- $G_3$: center $6$, radius $R_3 = |0| + |3| + |-2| = 5$.
- $G_4$: center $2$, radius $R_4 = |-1| + |0| + |1| = 2$.

The union of these four disks, $G_1 \cup G_2 \cup G_3 \cup G_4$, contains all eigenvalues of $A$. An upper bound on the spectral radius is given by $\max\{|5|+2, |-4|+3, |6|+5, |2|+2\} = \max\{7, 7, 11, 4\} = 11$. Thus, we can immediately conclude that $\rho(A) \leq 11$ without computing a single eigenvalue. [@problem_id:3249200]

### Refinements and Extended Interpretations
The basic theorem can be extended to provide more detailed information.

#### The Second Gershgorin Theorem: Disjoint Disks
A more powerful statement, often called the second part of the theorem, addresses situations where the disks are disjoint. It states that if a union of $k$ Gershgorin disks is disjoint from the union of the remaining $n-k$ disks, then the first union contains exactly $k$ eigenvalues of the matrix (counted with their algebraic multiplicities).

A particularly useful case is when all disks are pairwise disjoint. In this scenario, each disk is guaranteed to contain exactly one eigenvalue. This transforms the theorem from a collective bound into a set of individual localizations.

Consider the matrix:
$B = \begin{pmatrix} 0  1  0 \\ 1  10  0 \\ 1  1  25 \end{pmatrix}$.

Its Gershgorin disks are:
- $G_1$: center $0$, radius $R_1 = |1| + |0| = 1$.
- $G_2$: center $10$, radius $R_2 = |1| + |0| = 1$.
- $G_3$: center $25$, radius $R_3 = |1| + |1| = 2$.

The distance between the centers of $G_1$ and $G_2$ is $10$, which is greater than the sum of their radii, $1+1=2$. Similarly, the distances between the centers of $(G_1, G_3)$ and $(G_2, G_3)$ are $25$ and $15$, respectively, both far exceeding the sums of the corresponding radii. The three disks are pairwise disjoint. Therefore, we can conclude not only where the eigenvalues are, but how many are in each region. There is exactly one eigenvalue $\lambda_1 \in G_1$, one eigenvalue $\lambda_2 \in G_2$, and one eigenvalue $\lambda_3 \in G_3$. This provides individual [error bounds](@entry_id:139888) for approximating the eigenvalues by the diagonal entries:
$|\lambda_1 - 0| \le 1$, $|\lambda_2 - 10| \le 1$, and $|\lambda_3 - 25| \le 2$. [@problem_id:3249200]

#### Row Disks versus Column Disks
Since the eigenvalues of a matrix $A$ are the same as the eigenvalues of its transpose $A^\mathsf{T}$, the Gershgorin theorem can also be applied to $A^\mathsf{T}$. The disks for $A^\mathsf{T}$ are centered at the same diagonal entries $a_{ii}$, but their radii are determined by the sums of [absolute values](@entry_id:197463) of off-diagonal entries in the *columns* of the original matrix $A$. Let $S_j = \sum_{i \neq j} |a_{ij}|$ be the column-based radius.

An eigenvalue $\lambda$ must lie in the union of the row disks, and it must also lie in the union of the column disks. Therefore, all eigenvalues must lie in the **intersection** of these two regions:
$\sigma(A) \subseteq \left(\bigcup_{i=1}^n G_i^{\text{row}}\right) \cap \left(\bigcup_{j=1}^n G_j^{\text{col}}\right)$.

In some cases, one set of disks provides a much tighter bound than the other. Consider the matrix:
$A(t) = \begin{pmatrix} -2  t  t \\ 0  1  0 \\ 0  0  4 \end{pmatrix}$, where $t$ is a real parameter.

The eigenvalues are exactly the diagonal entries: $-2, 1, 4$.
The row-based disks are:
- $G_1^{\text{row}}$: center $-2$, radius $2|t|$.
- $G_2^{\text{row}}$: center $1$, radius $0$ (the point $\{1\}$).
- $G_3^{\text{row}}$: center $4$, radius $0$ (the point $\{4\}$).

If $t$ is large, for instance $t=2$, the first disk is $|z+2| \le 4$. The union of disks is a large region that contains all three eigenvalues, but it fails to isolate them.

Now, let's examine the column-based disks:
- $G_1^{\text{col}}$: center $-2$, radius $0$ (the point $\{-2\}$).
- $G_2^{\text{col}}$: center $1$, radius $|t|$.
- $G_3^{\text{col}}$: center $4$, radius $|t|$.

For any value of $t$, the column-based analysis immediately isolates the eigenvalue at $-2$ with perfect accuracy. For $t \ge 3/2$, the row-based disk $G_1^{\text{row}}$ overlaps with $G_2^{\text{row}}$, providing a poor localization, whereas the column-based disk $G_1^{\text{col}}$ remains a single point, providing an exact location. This demonstrates the practical importance of always considering both row and column formulations. [@problem_id:3249268]

### Applications to Structured Matrices and Numerical Methods
The true power of the Gershgorin theorem is revealed when it is applied to matrices with specific structures, yielding deep insights with minimal effort.

#### Symmetric and Positive Definite Matrices
For a real symmetric matrix ($A = A^\mathsf{T}$), it is a well-known fact that all eigenvalues are real. This means the eigenvalues must lie in the intersection of the Gershgorin disks and the real axis. This intersection is a union of real intervals:
$\sigma(A) \subseteq \bigcup_{i=1}^n [a_{ii} - R_i, a_{ii} + R_i]$.

This provides a powerful and easily computable test for [positive definiteness](@entry_id:178536). A [symmetric matrix](@entry_id:143130) is **[positive definite](@entry_id:149459)** if and only if all its eigenvalues are strictly positive. From the Gershgorin intervals, if the leftmost point of every interval is greater than zero, then all eigenvalues must be positive. This gives a [sufficient condition](@entry_id:276242):
If $a_{ii} - R_i > 0$ for all $i=1, \dots, n$, then $A$ is [positive definite](@entry_id:149459).
This condition is known as **[strict diagonal dominance](@entry_id:154277)**. For a symmetric matrix, if it is strictly diagonally dominant with positive diagonal entries, the Gershgorin theorem guarantees it is [positive definite](@entry_id:149459). This allows us to verify [positive definiteness](@entry_id:178536), a key requirement for methods like Cholesky factorization, by simple inspection of the matrix entries. [@problem_id:3249215]

#### Skew-Symmetric Matrices
For a real [skew-symmetric matrix](@entry_id:155998) ($A^\mathsf{T} = -A$), all diagonal entries $a_{ii}$ must be zero. Consequently, all Gershgorin disks are centered at the origin of the complex plane. The theorem then provides a simple bound on the [spectral radius](@entry_id:138984): $\rho(A) \le \max_i R_i$.

It is a separate algebraic fact that the eigenvalues of a real [skew-symmetric matrix](@entry_id:155998) are purely imaginary. The Gershgorin theorem itself does *not* prove this; the disks are two-dimensional regions and contain many points with non-zero real parts. The theorem's role is to provide a bound on the magnitude of these purely imaginary eigenvalues. This is a crucial lesson in distinguishing what a tool implies versus what is known from other properties. For a [skew-symmetric matrix](@entry_id:155998), we combine the algebraic knowledge that eigenvalues have the form $\lambda = ik$ for $k \in \mathbb{R}$ with the Gershgorin bound to conclude that $|k| \le \max_i R_i$. [@problem_id:3249227]

#### Stochastic Matrices
A **row-stochastic** matrix is a real matrix with non-negative entries where each row sums to 1. For such a matrix $A=(a_{ij})$, we have $a_{ij} \ge 0$ and $\sum_j a_{ij} = 1$. The diagonal entry $a_{ii}$ is therefore in $[0,1]$. The Gershgorin radius for the $i$-th row is $R_i = \sum_{j \neq i} |a_{ij}| = \sum_{j \neq i} a_{ij}$. From the row-sum property, this is simply $1 - a_{ii}$.
So, the $i$-th Gershgorin disk is centered at $a_{ii}$ and has radius $1 - a_{ii}$. The rightmost point of this disk is at $a_{ii} + (1 - a_{ii}) = 1$. This means every Gershgorin disk is contained within the [unit disk](@entry_id:172324) $|z| \le 1$ and is tangent to the point $z=1$. Consequently, all eigenvalues of a [stochastic matrix](@entry_id:269622) must satisfy $|\lambda| \le 1$. Furthermore, since all disks touch the point $z=1$, it is plausible that $1$ is an eigenvalue, a fact that is indeed true for all [row-stochastic matrices](@entry_id:266181). [@problem_id:3249358]

#### Connection to Iterative Methods and System Dynamics
The localization of eigenvalues is critical for analyzing the stability and convergence of dynamic systems and [iterative algorithms](@entry_id:160288). A key result in [matrix analysis](@entry_id:204325) states that the sequence of [matrix powers](@entry_id:264766) $A^k$ converges to the zero matrix as $k \to \infty$ if and only if the [spectral radius](@entry_id:138984) $\rho(A)  1$.

The Gershgorin theorem provides a simple [sufficient condition](@entry_id:276242) for this convergence. If all Gershgorin disks lie strictly inside the unit circle $\{z \in \mathbb{C} : |z|  1\}$, this means that for every row $i$, the point on the disk furthest from the origin is still inside the unit circle. This distance is $|a_{ii}|+R_i$. So, if $|a_{ii}| + \sum_{j \neq i} |a_{ij}|  1$ for all $i$, then the union of the disks is contained in the unit circle. This implies $\rho(A)  1$, and thus guarantees that $\lim_{k \to \infty} A^k = 0$. This condition is equivalent to stating that the matrix [infinity-norm](@entry_id:637586), $\|A\|_\infty = \max_i \sum_j |a_{ij}|$, is less than 1. [@problem_id:3249339]

As a concrete example from [scientific computing](@entry_id:143987), consider the matrix arising from the [finite difference discretization](@entry_id:749376) of the 1D Laplacian operator, which is a tridiagonal matrix with $2$ on the diagonal and $-1$ on the sub- and super-diagonals. For an $N \times N$ matrix of this type, all disks are centered at $2$. The first and last rows have a radius of $|-1|=1$, while the interior rows have a radius of $|-1| + |-1| = 2$. For $N \ge 3$, the union of the disks is the region $|z-2| \le 2$. Since the matrix is symmetric, the eigenvalues are real, so they must lie in the interval $[0, 4]$. This simple analysis provides an immediate and tight upper bound of $4$ for the largest eigenvalue, which is critical for analyzing the [stability of numerical methods](@entry_id:165924) for solving heat and wave equations. [@problem_id:3249329]

### Limitations and Advanced Techniques
While powerful, the Gershgorin theorem has limitations and can sometimes provide overly conservative (loose) bounds. Understanding these limitations opens the door to more advanced localization techniques.

#### The Pessimism of Absolute Values
The primary source of looseness in the Gershgorin bounds is the use of the triangle inequality, which leads to summing the [absolute values](@entry_id:197463) of off-diagonal entries to form the radius. This process is completely blind to the sign or phase of the matrix entries and cannot account for potential cancellations.

Consider the rank-1 matrix $A(M) = uv^\mathsf{T}$ with $u = M[1, 1, 1, 1]^\mathsf{T}$ and $v = [1, -1, 1, -1]^\mathsf{T}$ for $M > 0$. The resulting matrix has rows like $[M, -M, M, -M]$. The Gershgorin radii are large; for example, the radius of the first-row disk (centered at $M$) is $|-M|+|M|+|-M| = 3M$. This results in a large region of the complex plane, specifically the union of the disks $|z-M| \le 3M$ and $|z+M| \le 3M$. However, the true eigenvalues of this matrix are all exactly zero. The matrix is nilpotent ($A(M)^2 = 0$) because the [vector product](@entry_id:156672) $v^\mathsf{T}u = M-M+M-M = 0$. The Gershgorin theorem gives a misleadingly large region because it cannot see the perfect cancellation among the off-diagonal entries. [@problem_id:3249319]

#### Improving Bounds with Diagonal Similarity Scaling
A powerful method for tightening Gershgorin bounds is through **diagonal similarity scaling**. A similarity transformation of a matrix $A$ by a [non-singular matrix](@entry_id:171829) $P$ results in a new matrix $B = P^{-1}AP$ that has the exact same eigenvalues as $A$. If we choose $P$ to be a [diagonal matrix](@entry_id:637782), $D = \text{diag}(d_1, \dots, d_n)$ with $d_i > 0$, the transformed matrix is $B = D^{-1}AD$. Its entries are $b_{ij} = d_i^{-1} a_{ij} d_j$.

The Gershgorin disks of $B$ are different from those of $A$. Their centers are the same ($b_{ii} = a_{ii}$), but the radii change:
$R_i(B) = \sum_{j \neq i} |b_{ij}| = \sum_{j \neq i} |d_i^{-1} a_{ij} d_j| = d_i^{-1} \sum_{j \neq i} |a_{ij}| d_j$.

By carefully choosing the scaling factors $d_i$, we can often find a matrix $B$ whose Gershgorin disks are much smaller than those of the original matrix $A$, yielding a tighter localization for the same set of eigenvalues. This technique is especially effective for matrices with highly unbalanced entries. For instance, by choosing $D$ to "balance" the magnitudes of corresponding off-diagonal entries (e.g., to make $|b_{ij}| \approx |b_{ji}|$), one can significantly shrink the union of the Gershgorin disks. [@problem_id:3249296]

#### Beyond Circles: Brauer's Ovals of Cassini
The Gershgorin theorem is just one of many eigenvalue inclusion results. A notable refinement is **Brauer's Theorem**, which states that all eigenvalues of $A$ are contained in the union of $\binom{n}{2}$ sets called the **Ovals of Cassini**. For each pair of distinct indices $(i, j)$, the corresponding oval is defined as:
$K_{ij} = \{ z \in \mathbb{C} \,:\, |z - a_{ii}| |z - a_{jj}| \leq R_i R_j \}$.

The spectrum is contained in the union $\bigcup_{1 \le i  j \le n} K_{ij}$. This can sometimes provide a tighter bound than the Gershgorin disks.