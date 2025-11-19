## Introduction
The eigenvalue problem is a cornerstone of computational science and engineering, providing fundamental insights into physical systems, [data structures](@entry_id:262134), and dynamical processes. However, when the matrix in question is massive—with dimensions in the millions or billions—direct methods of [diagonalization](@entry_id:147016) become computationally impossible. This presents a significant challenge: how can we extract crucial spectral information from such enormous systems? The Lanczos iteration for symmetric matrices emerges as a remarkably elegant and efficient answer. It is a powerful iterative method that avoids the need to store or factorize the large matrix, relying only on the relatively inexpensive operation of [matrix-vector multiplication](@entry_id:140544).

This article offers a deep dive into the Lanczos iteration, designed for graduate students and researchers in [numerical linear algebra](@entry_id:144418) and related computational fields. We will unravel the algorithm from its theoretical foundations to its widespread practical applications. The journey is structured into three distinct parts.
-   In **Principles and Mechanisms**, we will deconstruct the core [three-term recurrence](@entry_id:755957), revealing its geometric interpretation as an [orthogonalization](@entry_id:149208) process. We will explore its formalization as a projection onto Krylov subspaces, analyze the critical issue of orthogonality loss in finite precision, and uncover its profound connection to orthogonal polynomials and Gaussian quadrature.
-   Next, **Applications and Interdisciplinary Connections** will showcase the algorithm's impact across diverse fields. We will see how it is used to find ground states in quantum mechanics, enable [large-scale data analysis](@entry_id:165572) in machine learning, and solve [inverse problems](@entry_id:143129), while also exploring powerful extensions like the [shift-and-invert](@entry_id:141092) strategy for targeting [interior eigenvalues](@entry_id:750739).
-   Finally, **Hands-On Practices** will provide curated problems to bridge theory and implementation, challenging you to apply the concepts and confront the numerical realities of the algorithm.

By navigating these chapters, you will gain a robust understanding of not only how the Lanczos iteration works but also why it is a fundamental and indispensable tool in modern [scientific computing](@entry_id:143987).

## Principles and Mechanisms

The Lanczos iteration is a remarkably efficient and elegant algorithm for finding extremal eigenvalues of large, sparse, symmetric matrices. Its power stems from a direct and profound connection between [matrix-vector multiplication](@entry_id:140544), orthogonal projections, and the classical theory of [orthogonal polynomials](@entry_id:146918). In this chapter, we will deconstruct the algorithm from its foundational [recurrence relation](@entry_id:141039), explore its properties as a [projection method](@entry_id:144836), and uncover its deep theoretical underpinnings.

### The Core Recurrence: A Geometric Perspective

The Lanczos algorithm for a real [symmetric matrix](@entry_id:143130) $A \in \mathbb{R}^{n \times n}$ begins with a chosen starting vector $q_1 \in \mathbb{R}^n$ of unit norm, so that $\|q_1\|_2 = 1$. It then iteratively generates a sequence of [orthonormal vectors](@entry_id:152061) $q_2, q_3, \dots$ and scalar coefficients $\alpha_j$ and $\beta_{j+1}$. The entire process is governed by a concise [three-term recurrence relation](@entry_id:176845). At step $j$, the algorithm computes a new vector $q_{j+1}$ via the relation:

$\beta_{j+1} q_{j+1} = A q_j - \alpha_j q_j - \beta_j q_{j-1}$

Here, we adopt the conventions that $\beta_1 = 0$ and $q_0$ is the [zero vector](@entry_id:156189). At first glance, this equation may appear abstract. However, its geometric interpretation reveals the algorithm's core mechanism: it is a highly specialized and efficient form of the Gram-Schmidt [orthogonalization](@entry_id:149208) process [@problem_id:1371183].

To see this, let the unnormalized vector on the right-hand side be denoted by $r_j = A q_j - \alpha_j q_j - \beta_j q_{j-1}$. The equation then becomes $\beta_{j+1} q_{j+1} = r_j$. This reveals that the new vector $q_{j+1}$ is simply the normalized version of $r_j$, with $\beta_{j+1} = \|r_j\|_2$ serving as the normalization constant.

The construction of $r_j$ is the heart of the process. It begins with the vector $Aq_j$—the result of applying the [matrix transformation](@entry_id:151622) $A$ to the most recent basis vector $q_j$. The terms $-\alpha_j q_j$ and $-\beta_j q_{j-1}$ are then subtracted. This is the signature of an [orthogonalization](@entry_id:149208) procedure, where we remove the components of $Aq_j$ that lie along the directions of the two previously constructed basis vectors.

We determine the coefficient $\alpha_j$ by enforcing the orthogonality of the basis. Since the set $\{q_1, q_2, \dots, q_{j+1}\}$ is constructed to be orthonormal, the unnormalized vector $r_j$ must be orthogonal to $q_j$.

Let's enforce this condition, $q_j^\top r_j = 0$:
$q_j^\top (A q_j - \alpha_j q_j - \beta_j q_{j-1}) = q_j^\top A q_j - \alpha_j (q_j^\top q_j) - \beta_j (q_j^\top q_{j-1}) = 0$

By the [orthonormality](@entry_id:267887) of the basis up to step $j$, we have $q_j^\top q_j = 1$ and $q_j^\top q_{j-1} = 0$. The equation simplifies to $q_j^\top A q_j - \alpha_j = 0$, which gives us the formula for $\alpha_j$:

$\alpha_j = q_j^\top A q_j$

Geometrically, $\alpha_j$ is the [scalar projection](@entry_id:148823) of $Aq_j$ onto the unit vector $q_j$. Thus, the term $\alpha_j q_j$ is precisely the [vector projection](@entry_id:147046) of $Aq_j$ onto $q_j$.

A remarkable property of the Lanczos algorithm for symmetric matrices, which we will prove shortly, is that the vector $r_j$ is automatically orthogonal to all previous vectors $q_i$ for $i  j-1$. The process only requires explicit [orthogonalization](@entry_id:149208) against the two most recent vectors, $q_j$ and $q_{j-1}$. This "short-term" recurrence is the source of the algorithm's exceptional efficiency compared to a full Gram-Schmidt process, which would require orthogonalizing against all $j$ previous vectors.

The structure can be summarized in the following algorithm (using $v_j$ for the vectors):
1.  Choose a starting vector $b$. Set $v_0 = 0$, $\beta_1 = 0$, and $v_1 = b / \|b\|_2$.
2.  For $j = 1, 2, \dots, m$:
    a. Compute $w_j = A v_j$.
    b. Compute the diagonal coefficient: $\alpha_j = v_j^\top w_j$.
    c. Compute the unnormalized residual: $r_j = w_j - \alpha_j v_j - \beta_j v_{j-1}$.
    d. Compute the off-diagonal coefficient: $\beta_{j+1} = \|r_j\|_2$.
    e. If $\beta_{j+1} = 0$, stop (this is a "breakdown" condition we will discuss later).
    f. Compute the next Lanczos vector: $v_{j+1} = r_j / \beta_{j+1}$.

To make this concrete, let's perform the first two steps for the matrix $A = \begin{pmatrix} 2  1  1 \\ 1  3  1 \\ 1  1  4 \end{pmatrix}$ with starting vector $b = \begin{pmatrix} 1 \\ 1 \\ 0 \end{pmatrix}$ [@problem_id:2184085].
First, we normalize $b$: $\|b\|_2 = \sqrt{1^2 + 1^2 + 0^2} = \sqrt{2}$. So, $q_1 = \frac{1}{\sqrt{2}} \begin{pmatrix} 1 \\ 1 \\ 0 \end{pmatrix}$.

**Step 1 ($j=1$):**
-   $Aq_1 = \frac{1}{\sqrt{2}} \begin{pmatrix} 2  1  1 \\ 1  3  1 \\ 1  1  4 \end{pmatrix} \begin{pmatrix} 1 \\ 1 \\ 0 \end{pmatrix} = \frac{1}{\sqrt{2}} \begin{pmatrix} 3 \\ 4 \\ 2 \end{pmatrix}$.
-   $\alpha_1 = q_1^\top (Aq_1) = \frac{1}{\sqrt{2}} \begin{pmatrix} 1  1  0 \end{pmatrix} \frac{1}{\sqrt{2}} \begin{pmatrix} 3 \\ 4 \\ 2 \end{pmatrix} = \frac{1}{2} (3+4) = \frac{7}{2}$.
-   With $\beta_1=0$, $r_1 = Aq_1 - \alpha_1 q_1 = \frac{1}{\sqrt{2}} \begin{pmatrix} 3 \\ 4 \\ 2 \end{pmatrix} - \frac{7}{2} \frac{1}{\sqrt{2}} \begin{pmatrix} 1 \\ 1 \\ 0 \end{pmatrix} = \frac{1}{2\sqrt{2}} \begin{pmatrix} -1 \\ 1 \\ 4 \end{pmatrix}$.
-   $\beta_2 = \|r_1\|_2 = \frac{1}{2\sqrt{2}} \sqrt{(-1)^2 + 1^2 + 4^2} = \frac{\sqrt{18}}{2\sqrt{2}} = \frac{3\sqrt{2}}{2\sqrt{2}} = \frac{3}{2}$.
-   $q_2 = \frac{r_1}{\beta_2} = \frac{1}{3\sqrt{2}} \begin{pmatrix} -1 \\ 1 \\ 4 \end{pmatrix}$.

**Step 2 ($j=2$):**
-   $Aq_2 = \frac{1}{3\sqrt{2}} \begin{pmatrix} 2  1  1 \\ 1  3  1 \\ 1  1  4 \end{pmatrix} \begin{pmatrix} -1 \\ 1 \\ 4 \end{pmatrix} = \frac{1}{3\sqrt{2}} \begin{pmatrix} 3 \\ 6 \\ 16 \end{pmatrix}$.
-   $\alpha_2 = q_2^\top (Aq_2) = \frac{1}{3\sqrt{2}} \begin{pmatrix} -1  1  4 \end{pmatrix} \frac{1}{3\sqrt{2}} \begin{pmatrix} 3 \\ 6 \\ 16 \end{pmatrix} = \frac{1}{18} (-3 + 6 + 64) = \frac{67}{18}$.

After two steps, we have generated the coefficients $\alpha_1 = \frac{7}{2}$, $\beta_2 = \frac{3}{2}$, and $\alpha_2 = \frac{67}{18}$. We have also constructed the first two [orthonormal vectors](@entry_id:152061), $q_1$ and $q_2$.

### The Lanczos Decomposition and the Krylov Subspace

The vectors generated by the Lanczos process, $\{q_1, q_2, \dots, q_k\}$, form an [orthonormal basis](@entry_id:147779) for a special subspace known as the **Krylov subspace**. For a matrix $A$ and a vector $q_1$, the $k$-th Krylov subspace, denoted $\mathcal{K}_k(A, q_1)$, is defined as:

$\mathcal{K}_k(A, q_1) = \operatorname{span}\{q_1, A q_1, A^2 q_1, \dots, A^{k-1} q_1\}$

The Lanczos algorithm can be viewed as an efficient way to construct an orthonormal basis for this subspace. The set of recurrences for $j=1, \dots, k$ can be compactly written in matrix form. Let $Q_k = [q_1, q_2, \dots, q_k]$ be the $n \times k$ matrix whose columns are the Lanczos vectors. The [recurrence relations](@entry_id:276612) combine to give:

$A Q_k = Q_k T_k + \beta_{k+1} q_{k+1} e_k^\top$

where $e_k$ is the $k$-th standard [basis vector](@entry_id:199546) in $\mathbb{R}^k$, and $T_k$ is the $k \times k$ real [symmetric tridiagonal matrix](@entry_id:755732) whose entries are the computed coefficients:

$T_k = \begin{pmatrix}
\alpha_1  \beta_2    \\
\beta_2  \alpha_2  \beta_3   \\
  \ddots  \ddots  \ddots  \\
   \beta_{k-1}  \alpha_{k-1}  \beta_k \\
    \beta_k  \alpha_k
\end{pmatrix}$

The matrix equation $A Q_k = Q_k T_k + \beta_{k+1} q_{k+1} e_k^\top$ is known as the **Lanczos decomposition**. Since the columns of $Q_k$ are orthonormal, we have $Q_k^\top Q_k = I_k$, where $I_k$ is the $k \times k$ identity matrix. Furthermore, by construction, the next vector $q_{k+1}$ is orthogonal to all columns of $Q_k$, so $Q_k^\top q_{k+1} = 0$. If we pre-multiply the Lanczos decomposition by $Q_k^\top$, we obtain a fundamental relationship:

$Q_k^\top A Q_k = Q_k^\top (Q_k T_k + \beta_{k+1} q_{k+1} e_k^\top) = (Q_k^\top Q_k) T_k + \beta_{k+1} (Q_k^\top q_{k+1}) e_k^\top = I_k T_k + 0$

This yields the crucial result:

$T_k = Q_k^\top A Q_k$

This equation states that the small, tridiagonal matrix $T_k$ is the orthogonal projection of the large matrix $A$ onto the Krylov subspace $\mathcal{K}_k(A, q_1)$. This projection is the essence of why the Lanczos method works for approximating eigenvalues: the eigenvalues of the small, easy-to-handle matrix $T_k$ will provide excellent approximations to the eigenvalues of the large, computationally expensive matrix $A$.

### Orthogonality: Theory and Practice

The [orthonormality](@entry_id:267887) of the Lanczos vectors is the bedrock upon which the entire theory rests. Its maintenance, or lack thereof, is the single most important practical consideration.

#### Orthogonality in Exact Arithmetic

The most remarkable feature of the Lanczos algorithm is that for a symmetric matrix $A$, the [three-term recurrence](@entry_id:755957) is sufficient to guarantee orthogonality among all generated vectors. This is not obvious from the construction, which only explicitly orthogonalizes $Aq_j$ against $q_j$ and $q_{j-1}$. The key lies in the symmetry of $A$.

We can prove by induction that the set $\{q_1, \dots, q_k\}$ is orthonormal for all $k$ [@problem_id:3557360]. Assume we have an [orthonormal set](@entry_id:271094) $\{q_1, \dots, q_j\}$. We construct the next vector $q_{j+1}$ from the residual $r_j = A q_j - \alpha_j q_j - \beta_j q_{j-1}$. We must show that $r_j$ is orthogonal to $q_i$ for all $i \le j$.

-   For $i=j$: $q_j^\top r_j = q_j^\top A q_j - \alpha_j (q_j^\top q_j) - \beta_j (q_j^\top q_{j-1})$. By the definition of $\alpha_j$ and [orthonormality](@entry_id:267887), this is $\alpha_j - \alpha_j(1) - \beta_j(0) = 0$.
-   For $i=j-1$: $q_{j-1}^\top r_j = q_{j-1}^\top A q_j - \alpha_j (q_{j-1}^\top q_j) - \beta_j (q_{j-1}^\top q_{j-1}) = q_{j-1}^\top A q_j - \beta_j$. Using the symmetry of $A$, we have $q_{j-1}^\top A q_j = (A q_{j-1})^\top q_j$. From the recurrence for step $j-1$, we have $A q_{j-1} = \beta_{j-1} q_{j-2} + \alpha_{j-1} q_{j-1} + \beta_j q_j$. Taking the inner product with $q_j$ gives $(A q_{j-1})^\top q_j = \beta_j$. So, $q_{j-1}^\top r_j = \beta_j - \beta_j = 0$.
-   For $i  j-1$: $q_i^\top r_j = q_i^\top A q_j - \alpha_j (q_i^\top q_j) - \beta_j (q_i^\top q_{j-1}) = q_i^\top A q_j$. By symmetry, $q_i^\top A q_j = (A q_i)^\top q_j$. The recurrence for step $i$ shows that $Aq_i$ is a linear combination of $q_{i-1}, q_i,$ and $q_{i+1}$. Since $i  j-1$, we have $i+1  j$. Therefore, $Aq_i$ lies in $\operatorname{span}\{q_{i-1}, q_i, q_{i+1}\}$, which is orthogonal to $q_j$ by the [inductive hypothesis](@entry_id:139767). Thus, $(Aq_i)^\top q_j = 0$, and the proof is complete.

This proof highlights that the tridiagonal structure of $T_k$ is a direct consequence of the symmetry of $A$. For a general non-[symmetric matrix](@entry_id:143130), this "short-term" recurrence fails, and a full [orthogonalization](@entry_id:149208) (Arnoldi iteration) is required, resulting in a dense upper-Hessenberg matrix.

#### Loss of Orthogonality in Finite Precision

The elegant theory of exact arithmetic quickly collides with the reality of floating-point computation. In practice, the computed Lanczos vectors $\hat{q}_k$ are not perfectly orthogonal. While local orthogonality (e.g., $\hat{q}_k^\top \hat{q}_{k-1}$) is well-preserved by the explicit subtraction in the recurrence, global orthogonality (e.g., $\hat{q}_k^\top \hat{q}_1$) degrades over iterations [@problem_id:3557360].

This **[loss of orthogonality](@entry_id:751493)** is not a slow, gentle drift. It occurs catastrophically as soon as an eigenvalue of the tridiagonal matrix $T_k$ (a "Ritz value") converges to an eigenvalue of the original matrix $A$. The analysis by C. C. Paige shows that the supposedly small rounding errors in the vector updates accumulate in a structured way. The computed recurrence effectively behaves as if there were small additional terms:
$A \hat{q}_i \approx \hat{\beta}_{i-1} \hat{q}_{i-1} + \hat{\alpha}_i \hat{q}_i + \hat{\beta}_i \hat{q}_{i+1} + \sum_{j \lt i-1} \varepsilon_{ij} \hat{q}_j$
These small terms $\varepsilon_{ij}$ reintroduce components of distant (and supposedly orthogonal) vectors, destroying global orthogonality.

This practical failure has significant implications. For one, it means the standard Lanczos algorithm is not **backward stable** in the simplest sense. A [backward stable algorithm](@entry_id:633945) would produce computed results that are the *exact* results for a slightly perturbed problem. A model where the computed $\hat{T}_k$ and $\hat{Q}_k$ are the exact Lanczos outputs for a nearby matrix $A+E$ would require $\hat{Q}_k$ to be perfectly orthogonal, which it is not [@problem_id:3557423]. To achieve this kind of stability and maintain orthogonality, one must introduce **[reorthogonalization](@entry_id:754248)**, explicitly re-orthogonalizing each new vector $\hat{q}_{k+1}$ against all previous vectors. This adds computational cost but restores numerical stability. For many applications, however, the "ghost" eigenvalues that appear due to [loss of orthogonality](@entry_id:751493) can be managed, and the unmodified algorithm remains highly effective.

### The Rayleigh-Ritz Procedure: Approximating Eigenvalues

The primary application of the Lanczos algorithm is to approximate the eigenvalues and eigenvectors of $A$. This is achieved by applying the **Rayleigh-Ritz procedure** to the Krylov subspace $\mathcal{K}_k(A, q_1)$. The procedure seeks the best approximations of eigenpairs within this subspace.

An approximate eigenpair, known as a **Ritz pair** $(\theta, u)$, is defined by a scalar **Ritz value** $\theta$ and a non-zero **Ritz vector** $u \in \mathcal{K}_k(A, q_1)$. The pair is determined by the **Galerkin condition**, which requires the residual $Au - \theta u$ to be orthogonal to the subspace $\mathcal{K}_k(A, q_1)$ [@problem_id:3603172].
$Q_k^\top (A u - \theta u) = 0$

Since $u \in \mathcal{K}_k(A, q_1)$, it can be written as a linear combination of the Lanczos basis vectors: $u = Q_k y$ for some coefficient vector $y \in \mathbb{R}^k$. Substituting this into the Galerkin condition:
$Q_k^\top (A Q_k y - \theta Q_k y) = 0$
$(Q_k^\top A Q_k) y - \theta (Q_k^\top Q_k) y = 0$
$T_k y - \theta I_k y = 0 \implies T_k y = \theta y$

This provides a profound result: the Ritz values $\theta$ are simply the eigenvalues of the tridiagonal matrix $T_k$, and the coefficients of the Ritz vectors $u$ in the Lanczos basis are the corresponding eigenvectors of $T_k$ [@problem_id:2406055]. Finding the eigenvalues of the small matrix $T_k$ is computationally trivial compared to diagonalizing the original matrix $A$.

A crucial tool for assessing the quality of a Ritz pair is the norm of its residual, $\|Au - \theta u\|_2$. A small [residual norm](@entry_id:136782) indicates that the Ritz pair is close to being an exact eigenpair of $A$. Using the Lanczos decomposition, we can derive a remarkably simple and inexpensive formula for this norm [@problem_id:3603172] [@problem_id:2406055].
$Au - \theta u = A(Q_k y) - \theta(Q_k y) = (AQ_k)y - \theta u$
$= (Q_k T_k + \beta_{k+1} q_{k+1} e_k^\top)y - \theta u$
$= Q_k(T_k y) + \beta_{k+1} (e_k^\top y) q_{k+1} - \theta u$
Since $T_k y = \theta y$ and $u = Q_k y$, this simplifies to:
$Au - \theta u = \theta (Q_k y) + \beta_{k+1} (e_k^\top y) q_{k+1} - \theta u = \beta_{k+1} (e_k^\top y) q_{k+1}$

The [residual vector](@entry_id:165091) is a scalar multiple of the next Lanczos vector $q_{k+1}$. Taking the norm, and noting that $\|q_{k+1}\|_2 = 1$ and $\beta_{k+1} \ge 0$, we get:
$\|Au - \theta u\|_2 = \beta_{k+1} |y_k|$
where $y_k = e_k^\top y$ is the last component of the eigenvector $y$ of $T_k$. This formula provides a powerful, cheap stopping criterion for the iteration: if the product of the next off-diagonal element $\beta_{k+1}$ and the last component of a specific eigenvector of $T_k$ is small, the corresponding Ritz pair is a good approximation.

Finally, if the eigenvectors $\{y_j\}$ of the symmetric matrix $T_k$ are chosen to be an [orthonormal set](@entry_id:271094), the corresponding Ritz vectors $\{u_j = Q_k y_j\}$ also form an orthonormal basis for the Krylov subspace $\mathcal{K}_k(A, q_1)$ [@problem_id:2406055]. This is because $u_i^\top u_j = (Q_k y_i)^\top (Q_k y_j) = y_i^\top Q_k^\top Q_k y_j = y_i^\top I_k y_j = y_i^\top y_j = \delta_{ij}$.

### Termination and Breakdown

The Lanczos iteration terminates if at some step $k$, the off-diagonal coefficient $\beta_{k+1}$ becomes zero. This event, known as a **breakdown**, has a deep mathematical meaning.

#### Happy Breakdown in Exact Arithmetic

If $\beta_{k+1}=0$ in exact arithmetic, it means the [residual vector](@entry_id:165091) $r_k$ is zero. The Lanczos decomposition simplifies to $AQ_k = Q_k T_k$. This implies that the Krylov subspace $\mathcal{K}_k(A, q_1)$ is an **invariant subspace** of $A$; that is, for any vector $x \in \mathcal{K}_k(A, q_1)$, the vector $Ax$ also lies in $\mathcal{K}_k(A, q_1)$ [@problem_id:3557360] [@problem_id:3590638].

In this scenario, the Ritz pairs are no longer approximations; they become exact eigenpairs of $A$. The eigenvalues of $T_k$ are a subset of the eigenvalues of $A$. This is why such an event is often called a "happy breakdown." It signifies that the algorithm has successfully found a piece of the spectral information of $A$. The condition for an exact eigenpair, $\|Au - \theta u\|_2 = \beta_{k+1} |y_k| = 0$, is satisfied for all Ritz pairs since $\beta_{k+1}=0$ [@problem_id:2406055].

The step at which breakdown occurs is determined entirely by the choice of starting vector $q_1$. A breakdown at step $k$ occurs if and only if the **[minimal polynomial](@entry_id:153598)** of $A$ with respect to $q_1$ (the [monic polynomial](@entry_id:152311) $p$ of least degree such that $p(A)q_1=0$) has degree $k$ [@problem_id:3590638].

The spectral content of $q_1$ is key. Let $A = \sum_{i=1}^n \lambda_i u_i u_i^\top$ be the spectral decomposition of $A$. We can write $q_1 = \sum_{i=1}^n c_i u_i$. The Lanczos process can only "see" the eigen-components for which $c_i \neq 0$. If the starting vector $q_1$ happens to be orthogonal to some eigenvector $u_j$ (i.e., $c_j=0$), then the entire Krylov subspace will remain orthogonal to $u_j$, and the eigenvalue $\lambda_j$ can never be approximated by the process [@problem_id:3590641]. Conversely, if $q_1$ is an eigenvector itself, say $q_1 = u_j$, then $Aq_1 = \lambda_j q_1$. The algorithm finds $\alpha_1 = \lambda_j$ and $r_1=0$, leading to $\beta_2=0$ and immediate breakdown after one step. The matrix $T_1$ is simply $[\lambda_j]$ [@problem_id:3590641].

For a "generic" starting vector—one that has non-zero components along all eigenvectors of $A$—the minimal polynomial will have degree $n$ (assuming distinct eigenvalues), and the Lanczos process will run for $n$ steps in exact arithmetic, at which point $T_n$ will be orthogonally similar to $A$ and share its exact spectrum [@problem_id:3590638] [@problem_id:3590641].

#### Soft Breakdown in Finite Precision

In floating-point arithmetic, an exact zero $\beta_{k+1}$ is rare. Instead, one might encounter a "soft breakdown," where $\beta_{k+1}$ is numerically tiny. This can cause instability when computing the next vector $q_{k+1}$. Advanced **look-ahead Lanczos** methods are designed to handle this by effectively taking a block of steps at once, building a basis for $\mathcal{K}_{k+p}(A, q_1)$ from $\mathcal{K}_k(A, q_1)$ in a more stable manner. This leads to a [block tridiagonal matrix](@entry_id:746893) instead of a purely tridiagonal one, but preserves the underlying projection framework [@problem_id:3590638].

### Connections to Orthogonal Polynomials and Gaussian Quadrature

The deepest and most beautiful aspect of the Lanczos algorithm is its equivalence to the theory of orthogonal polynomials and Gaussian quadrature. This connection explains the algorithm's remarkable properties, including the rapid convergence of Ritz values.

Let us define a **[spectral measure](@entry_id:201693)** $d\mu$ associated with the pair $(A, q_1)$. This is a [discrete measure](@entry_id:184163) supported on the eigenvalues of $A$, defined by its action on polynomials:
$\int p(\lambda) d\mu(\lambda) = q_1^\top p(A) q_1$

If $q_1 = \sum c_i u_i$, this integral is equal to $\sum c_i^2 p(\lambda_i)$. The theory of orthogonal polynomials concerns sequences of polynomials $\{p_k(\lambda)\}$ that are orthogonal with respect to the inner product induced by this measure: $\langle p_i, p_j \rangle_\mu = \int p_i(\lambda) p_j(\lambda) d\mu(\lambda) = \delta_{ij}$.

The Lanczos algorithm is an algebraic realization of this process. The Lanczos vectors are directly related to a sequence of [orthogonal polynomials](@entry_id:146918) $\{p_k\}$ by $q_{k+1} = c_k p_k(A) q_1$, where $c_k$ is a [normalization constant](@entry_id:190182) [@problem_id:3246883]. The [three-term recurrence](@entry_id:755957) of the Lanczos algorithm is precisely the [three-term recurrence relation](@entry_id:176845) that all sequences of [orthogonal polynomials](@entry_id:146918) satisfy. The matrix $T_k$ is nothing other than the $k \times k$ **Jacobi matrix** that encodes this polynomial recurrence [@problem_id:3206397] [@problem_id:3590641].

This connection immediately links the Lanczos method to **Gaussian quadrature**, a powerful numerical integration technique. A fundamental result in this theory states that for any measure $d\mu$, the nodes of the $k$-point Gaussian [quadrature rule](@entry_id:175061)—the rule that exactly integrates all polynomials of degree up to $2k-1$—are the eigenvalues of the $k \times k$ Jacobi matrix associated with $d\mu$.

Translating this to the Lanczos context [@problem_id:3206397] [@problem_id:3590641]:
-   The Ritz values (eigenvalues of $T_k$) are the nodes of the $k$-point Gaussian quadrature rule for the [spectral measure](@entry_id:201693) $d\mu$.
-   The [quadrature weights](@entry_id:753910) $w_j$ are given by the squares of the first components of the normalized eigenvectors of $T_k$.

This explains the **moment-matching property** of the Lanczos algorithm [@problem_id:2406033]:
$q_1^\top A^j q_1 = \int \lambda^j d\mu(\lambda) \approx \sum_{i=1}^k w_i \theta_i^j$
The approximation is, in fact, an exact equality for all polynomial moments up to degree $j=2k-1$. In matrix terms, this means:
$q_1^\top A^j q_1 = e_1^\top T_k^j e_1 \quad \text{for } 0 \le j \le 2k-1$

This perspective provides profound insight into why the algorithm works so well. The Rayleigh-Ritz procedure is equivalent to approximating an integral (related to the spectrum of $A$) with an optimal quadrature rule. The extremal eigenvalues of $A$, which correspond to the endpoints of the support of the measure $d\mu$, are precisely the points that Gaussian [quadrature rules](@entry_id:753909) approximate most rapidly. This explains the observed fast convergence of the Lanczos algorithm to the extremal eigenvalues of $A$. For $k=1$, this elegant theory simplifies to a familiar result: $T_1 = [\alpha_1] = [q_1^\top A q_1]$, so the single quadrature node is the Rayleigh quotient, and its weight is 1 [@problem_id:3206397].