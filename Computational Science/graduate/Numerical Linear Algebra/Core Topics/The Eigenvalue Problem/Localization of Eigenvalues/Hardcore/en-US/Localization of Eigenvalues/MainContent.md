## Introduction
The eigenvalues of a matrix are fundamental quantities that reveal its deepest properties, governing everything from the stability of a bridge to the convergence rate of a machine learning algorithm. However, calculating these eigenvalues directly is computationally equivalent to finding the roots of a high-degree polynomial—a task that is often intractable for the large matrices encountered in modern science and engineering. This computational barrier creates a critical knowledge gap: How can we understand a system's behavior without knowing its exact eigenvalues?

This article addresses this challenge by exploring the powerful field of [eigenvalue localization](@entry_id:162719), which provides methods for identifying regions in the complex plane guaranteed to contain a matrix's spectrum. Instead of exact values, we seek reliable bounds, offering a practical and efficient way to analyze complex systems. Across three chapters, you will gain a thorough understanding of this essential topic. The first chapter, **Principles and Mechanisms**, delves into the cornerstone of localization—the Gershgorin circle theorem—and its elegant extensions. The second chapter, **Applications and Interdisciplinary Connections**, demonstrates how these theoretical tools are applied to solve real-world problems in engineering, [numerical analysis](@entry_id:142637), and data science. Finally, **Hands-On Practices** provides opportunities to solidify your understanding by working through concrete examples. We begin by examining the foundational principles that make [eigenvalue localization](@entry_id:162719) possible.

## Principles and Mechanisms

The determination of a matrix's eigenvalues, while fundamental to many scientific and engineering disciplines, is computationally equivalent to finding the roots of its [characteristic polynomial](@entry_id:150909). For matrices of even moderate size, this is a formidable task that generally cannot be solved by a finite sequence of arithmetic operations. Consequently, a significant branch of [numerical linear algebra](@entry_id:144418) is devoted to the **localization of eigenvalues**—the identification of regions in the complex plane that are guaranteed to contain the spectrum of a given matrix. This chapter elucidates the foundational principles and mechanisms of [eigenvalue localization](@entry_id:162719), beginning with the cornerstone result in this area: the Gershgorin circle theorem.

### The Gershgorin Circle Theorem

The Gershgorin circle theorem provides a remarkably simple yet powerful tool for estimating the location of eigenvalues using only the entries of the matrix. It consists of two principal parts.

#### Spectral Inclusion in Gershgorin Discs

The first part of the theorem establishes a set of discs in the complex plane whose union is guaranteed to contain the entire spectrum of the matrix. For a given square matrix $A \in \mathbb{C}^{n \times n}$ with entries $a_{ij}$, we define the $i$-th **Gershgorin row disc**, $D_i(A)$, as a closed disc centered at the diagonal entry $a_{ii}$ with a radius $R_i$ equal to the sum of the [absolute values](@entry_id:197463) of the off-diagonal entries in that row.

**Definition: Gershgorin Row Disc**
For a matrix $A \in \mathbb{C}^{n \times n}$, the $i$-th Gershgorin row disc is the set:
$$
D_i(A) = \{ z \in \mathbb{C} : |z - a_{ii}| \le R_i \}, \quad \text{where} \quad R_i = \sum_{j \neq i} |a_{ij}|
$$

The first part of the theorem states that every eigenvalue of $A$ must lie in at least one of these discs.

**Theorem 2.1 (Gershgorin, Part I).** The spectrum $\sigma(A)$ of a matrix $A \in \mathbb{C}^{n \times n}$ is contained within the union of its Gershgorin row discs:
$$
\sigma(A) \subseteq \bigcup_{i=1}^n D_i(A)
$$

The mechanism underlying this powerful result is surprisingly direct. Let $\lambda$ be an eigenvalue of $A$, and let $x \in \mathbb{C}^n$ be a corresponding non-zero eigenvector, such that $Ax = \lambda x$. This matrix equation can be written as a [system of linear equations](@entry_id:140416). For the $i$-th row, we have:
$$
\sum_{j=1}^n a_{ij} x_j = \lambda x_i
$$
Isolating the diagonal term gives:
$$
(\lambda - a_{ii}) x_i = \sum_{j \neq i} a_{ij} x_j
$$
Since the eigenvector $x$ is non-zero, at least one of its components must be non-zero. Let $k$ be an index for which the component $x_k$ has the maximum absolute value, i.e., $|x_k| \ge |x_j|$ for all $j=1, \dots, n$. As $x \ne 0$, we know $|x_k| > 0$. Writing the equation above for this specific index $k$:
$$
(\lambda - a_{kk}) x_k = \sum_{j \neq k} a_{kj} x_j
$$
Taking the absolute value of both sides and applying the [triangle inequality](@entry_id:143750), we find:
$$
|\lambda - a_{kk}| |x_k| = \left| \sum_{j \neq k} a_{kj} x_j \right| \le \sum_{j \neq k} |a_{kj}| |x_j|
$$
By our choice of $k$, we know that $|x_j| \le |x_k|$ for all $j$. Substituting this into the inequality yields:
$$
|\lambda - a_{kk}| |x_k| \le \sum_{j \neq k} |a_{kj}| |x_k| = \left( \sum_{j \neq k} |a_{kj}| \right) |x_k|
$$
Since $|x_k| > 0$, we can divide by it to obtain the final result:
$$
|\lambda - a_{kk}| \le \sum_{j \neq k} |a_{kj}| = R_k
$$
This inequality demonstrates that the eigenvalue $\lambda$ must reside in the $k$-th Gershgorin disc, $D_k(A)$. Because this logic applies to any eigenvalue, the entire spectrum must lie within the union of all such discs, proving the theorem .

#### The Multiplicity Refinement

The second, more refined part of the Gershgorin theorem provides information about the distribution of eigenvalues among the discs.

**Theorem 2.2 (Gershgorin, Part II).** If a union of $k$ Gershgorin discs forms a connected component that is disjoint from the other $n-k$ discs, then this component contains exactly $k$ eigenvalues of $A$, counted with algebraic multiplicity.

The underlying mechanism for this result is a **homotopy argument**. Consider a family of matrices $A(t) = D + t O$ for $t \in [0, 1]$, where $D$ is the diagonal part of $A$ and $O$ is its off-diagonal part.
-   At $t=0$, we have $A(0) = D$, a [diagonal matrix](@entry_id:637782) whose eigenvalues are simply its diagonal entries, $\{a_{11}, a_{22}, \dots, a_{nn}\}$.
-   At $t=1$, we recover our original matrix, $A(1) = A$.

The eigenvalues of a matrix are continuous functions of its entries. Therefore, as $t$ varies from $0$ to $1$, each eigenvalue of $A(t)$ traces a [continuous path](@entry_id:156599) in the complex plane, starting at a diagonal entry $a_{ii}$ and ending at an eigenvalue of $A$.

For any $t \in [0,1]$, the Gershgorin radii of $A(t)$ are $R_i(t) = \sum_{j \neq i} |t a_{ij}| = t R_i(A)$. These discs are nested: $D_i(A(t)) \subseteq D_i(A(1))$ for all $t \in [0,1]$. Now, suppose a set of $k$ discs of $A$ (at $t=1$) forms a connected component $\mathcal{U}$ that is disjoint from the other $n-k$ discs. Because of the nested property, the corresponding $k$ discs of $A(t)$ will also form a component that is disjoint from the others for all $t$. The $k$ eigenvalue paths that start at the centers of the discs in $\mathcal{U}$ cannot cross into the other disjoint components due to continuity. They are "trapped" within $\mathcal{U}$. Consequently, at $t=1$, the component $\mathcal{U}$ must contain precisely those $k$ eigenvalues .

A direct corollary is that if all $n$ discs are mutually disjoint, then each disc contains exactly one eigenvalue.

### Applying and Interpreting the Theorem

To solidify these principles, consider two illustrative cases.

First, take the matrix from a block-diagonal system :
$$
A = \begin{pmatrix}
0.31  & 0.06  & -0.05  & 0.004  & -0.003 \\
0.02  & -0.18  & 0.08  & -0.005  & 0.004 \\
-0.03  & 0.07  & 0.27  & 0.006  & -0.004 \\
0.003  & -0.004  & 0.005  & 10.8  & 0.09 \\
-0.004  & 0.003  & -0.005  & 0.08  & 11.2
\end{pmatrix}
$$
The Gershgorin discs are:
-   $D_1$: center $0.31$, radius $R_1 = 0.117$. Real interval: $[0.193, 0.427]$.
-   $D_2$: center $-0.18$, radius $R_2 = 0.109$. Real interval: $[-0.289, -0.071]$.
-   $D_3$: center $0.27$, radius $R_3 = 0.110$. Real interval: $[0.160, 0.380]$.
-   $D_4$: center $10.8$, radius $R_4 = 0.102$. Real interval: $[10.698, 10.902]$.
-   $D_5$: center $11.2$, radius $R_5 = 0.092$. Real interval: $[11.108, 11.292]$.

Let's examine the union of these discs. The first three discs, $D_1, D_2, D_3$, are all located near the origin. The maximum real part of any point in their union is $0.427$. The last two discs, $D_4, D_5$, are located far to the right. The minimum real part of any point in their union is $10.698$. Since $0.427  10.698$, the set $\mathcal{U}_1 = D_1 \cup D_2 \cup D_3$ is disjoint from the set $\mathcal{U}_2 = D_4 \cup D_5$.
$\mathcal{U}_1$ is a connected component formed by $k=3$ discs. By Theorem 2.2, it must contain exactly $3$ eigenvalues. $\mathcal{U}_2$ is a connected component formed by $2$ discs and must contain the remaining $2$ eigenvalues. Thus, we conclude that the eigenvalue counts for these two regions are 3 and 2, respectively.

Second, consider a matrix where the off-diagonal terms are large enough to cause significant overlap :
$$
A = \begin{pmatrix}
0  \tfrac{5}{3}  \tfrac{5}{3}  \tfrac{5}{3} \\
\tfrac{5}{3}  4  \tfrac{5}{3}  \tfrac{5}{3} \\
\tfrac{5}{3}  \tfrac{5}{3}  8  \tfrac{5}{3} \\
\tfrac{5}{3}  \tfrac{5}{3}  \tfrac{5}{3}  12
\end{pmatrix}
$$
All rows have the same off-diagonal sum of absolute values, giving a uniform radius of $R_i = 3 \times \frac{5}{3} = 5$ for all discs. The discs are $D_1: |z| \le 5$, $D_2: |z-4| \le 5$, $D_3: |z-8| \le 5$, and $D_4: |z-12| \le 5$.
$D_1$ intersects $D_2$, whose union intersects $D_3$, and so on. All four discs merge to form a single connected component. In this case, Theorem 2.2 still applies: this one component, formed from $k=4$ discs, must contain all $4$ eigenvalues of the matrix. While correct, this localization is less precise than in the previous example.

### Refinements and Extensions

The basic Gershgorin theorem is the starting point for a variety of more sophisticated localization techniques.

#### Row Discs versus Column Discs

The spectrum of a matrix $A$ is identical to the spectrum of its transpose, $A^T$. We can therefore apply the Gershgorin theorem to $A^T$ to obtain another valid inclusion region for the eigenvalues of $A$. The rows of $A^T$ are the columns of $A$. This leads to the definition of **Gershgorin column discs**.

**Definition: Gershgorin Column Disc**
For a matrix $A \in \mathbb{C}^{n \times n}$, the $j$-th Gershgorin column disc is the set:
$$
D_j^{(col)}(A) = \{ z \in \mathbb{C} : |z - a_{jj}| \le C_j \}, \quad \text{where} \quad C_j = \sum_{i \neq j} |a_{ij}|
$$

Since the spectrum $\sigma(A)$ must lie in the union of row discs *and* in the union of column discs, it must lie in their **intersection**. This often provides a tighter bound.
$$
\sigma(A) \subseteq \left( \bigcup_{i=1}^n D_i(A) \right) \cap \left( \bigcup_{j=1}^n D_j^{(col)}(A) \right)
$$
It is crucial to note that the row-disc union and column-disc union are not generally the same set . The choice between them can matter significantly, especially when off-diagonal magnitudes are anisotropically distributed. For instance, consider the matrix :
$$
A(t) = \begin{pmatrix} 0  t  t \\ 0  1  0 \\ 0  0  2 \end{pmatrix}
$$
Its eigenvalues are clearly $0, 1, 2$.
-   **Row discs:** $D_1(A)$ has center $0$ and radius $2|t|$. $D_2(A)$ and $D_3(A)$ are the points $\{1\}$ and $\{2\}$. The localization for the eigenvalue at $0$ is $|z| \le 2|t|$, which is loose for large $|t|$.
-   **Column discs:** $D_1^{(col)}(A)$ is the point $\{0\}$. $D_2^{(col)}(A)$ has center $1$ and radius $|t|$. $D_3^{(col)}(A)$ has center $2$ and radius $|t|$. For $|t| > 1/2$, these three discs are disjoint, precisely isolating each eigenvalue.
In this case, the column-based analysis is far superior because the off-diagonal mass is concentrated in a single row but distributed among multiple columns.

#### Improving Localization with Diagonal Similarity

A more powerful refinement comes from the observation that eigenvalues are invariant under similarity transformations. For any non-singular [diagonal matrix](@entry_id:637782) $S = \text{diag}(s_1, \dots, s_n)$, the matrix $B = S^{-1}AS$ has the same eigenvalues as $A$. The entries of $B$ are $b_{ij} = s_i^{-1} a_{ij} s_j$. The diagonal entries $b_{ii} = a_{ii}$ are unchanged, so the centers of the Gershgorin discs are preserved. However, the radii change:
$$
R_i(B) = \sum_{j \neq i} |b_{ij}| = \sum_{j \neq i} |s_i^{-1} a_{ij} s_j| = \frac{1}{|s_i|} \sum_{j \neq i} |a_{ij}| |s_j|
$$
By carefully choosing the scaling factors $s_i$, we can often shrink the Gershgorin discs. Since $\sigma(A) = \sigma(B) \subseteq \bigcup_i D_i(B)$ for *any* choice of $S$, the eigenvalues must lie in the intersection of all such unions:
$$
\sigma(A) \subseteq \bigcap_{S \text{ diagonal}} \left( \bigcup_{i=1}^n D_i(S^{-1}AS) \right)
$$
This intersection defines a tighter inclusion region, sometimes called the "minimal Gershgorin set".

As a practical example of this "balancing" procedure, consider the matrix from :
$$
A = \begin{pmatrix} 5  2 \\ 18  -3 \end{pmatrix}
$$
Its Gershgorin discs are $D_1: |z-5| \le 2$ and $D_2: |z+3| \le 18$. The union is dominated by the large second disc.
Let's find a [scaling matrix](@entry_id:188350) $S = \text{diag}(d_1, 1)$ with $d_1>0$. The transformed matrix is $B = \text{diag}(d_1^{-1}, 1) A \text{diag}(d_1, 1)$, which computes to:
$$
B = \begin{pmatrix} 5  2/d_1 \\ 18d_1  -3 \end{pmatrix}
$$
The new radii are $R_1(B) = 2/d_1$ and $R_2(B) = 18d_1$. To minimize the size of the union, we aim to reduce the largest radius. A common strategy is to balance the radii, setting $R_1(B) = R_2(B)$, which implies $2/d_1 = 18d_1$, or $d_1^2 = 1/9$, so $d_1=1/3$. With this scaling, the radii become $R_1(B) = R_2(B) = 6$. The new inclusion region, $\{z: |z-5|\le 6\} \cup \{z: |z+3|\le 6\}$, is significantly smaller than the original one. The largest radius has been reduced from $18$ to $6$.

#### The Block Gershgorin Theorem

The principles of the Gershgorin theorem can be extended from scalar entries to [block matrices](@entry_id:746887). This is particularly useful in the analysis of discretized partial differential equations and [large-scale systems](@entry_id:166848). For a [block matrix](@entry_id:148435) $A = [A_{ij}]_{i,j=1}^n$ where each $A_{ij} \in \mathbb{C}^{m \times m}$, we can define analogous inclusion sets. The role of the absolute value is replaced by a [matrix norm](@entry_id:145006), and the distance to a scalar center $a_{ii}$ is replaced by a measure involving the inverse of $A_{ii} - zI$.

**Theorem 2.3 (Block Gershgorin).** Let $A=[A_{ij}]$ be a [block matrix](@entry_id:148435). An eigenvalue $\lambda$ of $A$ must satisfy one of the following conditions for at least one block index $k$:
1.  $\lambda$ is an eigenvalue of the diagonal block $A_{kk}$.
2.  $1 \le \|(A_{kk} - \lambda I)^{-1}\| \sum_{j \neq k} \|A_{kj}\|$.

This theorem's contrapositive form is often more practical: if $z$ is not an eigenvalue of any $A_{ii}$ and $\|(A_{ii} - zI)^{-1}\| \sum_{j \neq i} \|A_{ij}\|  1$ for all $i$, then $z$ is not an eigenvalue of $A$. If the diagonal blocks $A_{ii}$ are **normal**, this simplifies beautifully. For a [normal matrix](@entry_id:185943) $M$, $\|(M-zI)^{-1}\| = 1/\text{dist}(z, \sigma(M))$, where $\text{dist}(z, S)$ is the minimum distance from point $z$ to the set $S$. This yields the inclusion:
$$
\sigma(A) \subseteq \bigcup_{i=1}^n \left\{ z \in \mathbb{C} : \text{dist}(z, \sigma(A_{ii})) \le \sum_{j \neq i} \|A_{ij}\| \right\}
$$
Each set in this union is an "inflated" version of the spectrum of a diagonal block. Furthermore, a [separation principle](@entry_id:176134) analogous to Theorem 2.2 holds: if these inflated spectral sets form disjoint connected components, the number of eigenvalues in each component is the sum of the dimensions of the corresponding diagonal blocks . This theorem is instrumental in analyzing the [convergence of iterative methods](@entry_id:139832) like the block Jacobi iteration.

### Beyond Gershgorin: Other Localization Methods

While powerful, Gershgorin's theorem is not the only tool for [eigenvalue localization](@entry_id:162719). One important alternative is the theorem of Brauer, which gives inclusion sets based on pairs of rows.

**Theorem 2.4 (Brauer's Ovals of Cassini).** The spectrum $\sigma(A)$ is contained in the union of $\binom{n}{2}$ sets, known as the ovals of Cassini:
$$
\sigma(A) \subseteq \bigcup_{i \neq j} K_{ij}, \quad \text{where} \quad K_{ij} = \{ z \in \mathbb{C} : |z - a_{ii}| |z - a_{jj}| \le R_i R_j \}
$$
An oval of Cassini $K_{ij}$ is a single oval-shaped region if the centers $a_{ii}, a_{jj}$ are close relative to the radii $R_i, R_j$, and it consists of two disjoint egg-shaped regions if the centers are far apart.

This theorem can sometimes provide a dramatically tighter bound than Gershgorin's. Consider a matrix with one row having very large off-diagonal entries and others having very small ones . For example, with $\rho=1000$ and $\varepsilon = 5 \times 10^{-4}$:
$$
A = \begin{pmatrix} 0  1000  1000 \\ 5 \times 10^{-4}  100  0 \\ 5 \times 10^{-4}  0  -100 \end{pmatrix}
$$
The Gershgorin disc for the first row is huge: $D_1: |z| \le 2000$. The other two are tiny: $D_2: |z-100| \le \varepsilon$ and $D_3: |z+100| \le \varepsilon$. The union is essentially the large disc centered at the origin.
Brauer's theorem, however, considers products of radii. The oval $K_{23}$ is defined by $|z-100||z+100| \le \varepsilon^2$, which confines eigenvalues to two tiny regions very close to $\pm 100$. The ovals $K_{12}$ and $K_{13}$ are defined by $|z||z\mp 100| \le (2\rho)\varepsilon = 1$. This also provides a much stronger constraint than the Gershgorin disc $D_1$. In this case, the upper bound on the real part of any eigenvalue provided by Brauer's theorem is approximately $100$, whereas the Gershgorin bound is $2000$. The gap between the two bounds, $\Delta = U_G - U_B$, is approximately $1.900 \times 10^3$, demonstrating the potential advantage of considering alternative localization results.

### Sensitivity, Non-Normality, and the Limits of Localization

Localization theorems provide guarantees about the spectrum of a fixed, exact matrix. A critical question in [numerical analysis](@entry_id:142637) is how these locations behave under small perturbations to the matrix.

The Gershgorin regions themselves are stable in a predictable way. A perturbation $\Delta A$ applied to $A$ results in a perturbed matrix $A + \Delta A$. The new Gershgorin discs $D_i(A+\Delta A)$ are contained in an expanded version of the original discs. It can be shown that :
$$
D_i(A+\Delta A) \subseteq \{ z \in \mathbb{C} : |z - a_{ii}| \le R_i(A) + \|\Delta A\|_{\infty} \}
$$
This shows that the Gershgorin region for the perturbed matrix is contained in an inflation of the original region, where the inflation factor is the [infinity norm](@entry_id:268861) of the perturbation.

However, the stability of the Gershgorin *region* does not guarantee the stability of the *eigenvalues themselves*. The true sensitivity of eigenvalues is captured by the **Bauer-Fike theorem**.

**Theorem 2.5 (Bauer-Fike).** If $A$ is diagonalizable with $A=V\Lambda V^{-1}$, then for any eigenvalue $\lambda'$ of a perturbed matrix $A+\Delta A$, there exists an eigenvalue $\lambda$ of $A$ such that:
$$
|\lambda' - \lambda| \le \kappa(V) \|\Delta A\|
$$
Here, $\kappa(V) = \|V\| \|V^{-1}\|$ is the **condition number** of the eigenvector matrix $V$, and $\|\cdot\|$ is any [induced matrix norm](@entry_id:145756).

This theorem reveals that the sensitivity of eigenvalues is governed by the condition number of the eigenvector matrix.
-   If $A$ is **normal** ($A^*A=AA^*$), it is [unitarily diagonalizable](@entry_id:195045), meaning we can choose $V$ to be unitary. For the spectral [2-norm](@entry_id:636114), this gives $\kappa_2(V)=1$. The bound simplifies to $|\lambda' - \lambda| \le \|\Delta A\|_2$, indicating that eigenvalues of [normal matrices](@entry_id:195370) are perfectly well-conditioned .
-   If $A$ is **non-normal**, $\kappa(V)$ can be very large. In this case, small perturbations to $A$ can cause large changes in the eigenvalues, a phenomenon that Gershgorin's theorem does not capture.

This leads to an apparent discrepancy. Consider the nearly [defective matrix](@entry_id:153580) from :
$$
A = \begin{pmatrix} -\alpha  1 \\ \varepsilon  -\alpha \end{pmatrix}, \quad \text{with } \alpha > 1 \text{ and } 0  \varepsilon \ll 1
$$
Its Gershgorin discs are $|z+\alpha| \le 1$ and $|z+\alpha| \le \varepsilon$. The union is $|z+\alpha| \le 1$. Since $\alpha > 1$, the rightmost point of this region is $-\alpha+1  0$. The Gershgorin localization suggests stability, as all eigenvalues are bounded away from the imaginary axis in the left half-plane.
However, the eigenvalues are $\lambda_{\pm} = -\alpha \pm \sqrt{\varepsilon}$. The [eigenvalue condition number](@entry_id:176727) for $\lambda_+ = -\alpha + \sqrt{\varepsilon}$ can be computed as:
$$
\kappa(\lambda_+) = \frac{1+\varepsilon}{2\sqrt{\varepsilon}}
$$
As $\varepsilon \to 0$, this condition number approaches infinity. This indicates extreme sensitivity: a tiny perturbation to the matrix could send the eigenvalue $\lambda_+$ close to the imaginary axis, potentially destabilizing the system.

There is no contradiction here. The Gershgorin theorem correctly locates the eigenvalues of the *exact* matrix $A$. The large condition number warns us that this location is not robust. For [non-normal matrices](@entry_id:137153), the spectrum alone can be a misleading indicator of the matrix's behavior under perturbation. This sensitivity is more accurately described by the concept of **[pseudospectra](@entry_id:753850)**, which are sets of complex numbers that are "almost" eigenvalues. The Gershgorin theorem is a powerful first step in spectral analysis, but for [non-normal matrices](@entry_id:137153), it is only part of a much larger and more subtle story.