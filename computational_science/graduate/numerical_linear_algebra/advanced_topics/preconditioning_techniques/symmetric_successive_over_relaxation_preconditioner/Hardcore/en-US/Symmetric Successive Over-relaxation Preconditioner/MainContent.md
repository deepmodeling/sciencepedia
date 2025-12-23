## Introduction
Solving large, sparse [systems of linear equations](@entry_id:148943) is a fundamental challenge across science and engineering, frequently arising from the [discretization of partial differential equations](@entry_id:748527). For [symmetric positive definite](@entry_id:139466) (SPD) systems, the Conjugate Gradient (CG) method is a powerful iterative solver, but its performance degrades significantly for [ill-conditioned problems](@entry_id:137067). This creates a critical need for preconditioning—a technique to transform the original system into one that is easier to solve. This article focuses on a classical yet powerful technique to address this gap: the Symmetric Successive Over-Relaxation (SSOR) [preconditioner](@entry_id:137537).

This article provides a comprehensive exploration of the SSOR method, guiding you from its theoretical underpinnings to its practical application.
First, we will delve into the **Principles and Mechanisms** of the SSOR [preconditioner](@entry_id:137537). You will learn how it is constructed from the SOR [iterative method](@entry_id:147741), prove its essential properties of symmetry and [positive definiteness](@entry_id:178536), and analyze how it improves system conditioning.
Next, we will explore its **Applications and Interdisciplinary Connections**, demonstrating its effectiveness in solving PDEs common in fluid dynamics and geophysics, and uncovering its deep ties to advanced solver paradigms like multigrid and [domain decomposition methods](@entry_id:165176).
Finally, you will transition from theory to practice in the **Hands-On Practices** section, which presents targeted exercises to implement, test, and optimize the SSOR preconditioner, solidifying your understanding of this versatile numerical tool.

## Principles and Mechanisms

The effectiveness of iterative methods like the Conjugate Gradient algorithm hinges on the spectral properties of the system matrix. For matrices that are ill-conditioned, [preconditioning](@entry_id:141204) is a vital strategy to transform the original problem into a more tractable one. The core idea is to find a **preconditioner**, an auxiliary matrix $M$ that approximates the system matrix $A$, such that the preconditioned system has a more favorable [eigenvalue distribution](@entry_id:194746). A successful [preconditioner](@entry_id:137537) for a [symmetric positive definite](@entry_id:139466) (SPD) system $Ax = b$ should itself be SPD, and it should transform the system such that the eigenvalues of the preconditioned operator, typically $M^{-1}A$, are clustered tightly around $1$ . This clustering reduces the spectral condition number, thereby accelerating convergence.

This chapter delves into the principles and mechanisms of one of the classical preconditioners derived from iterative methods: the Symmetric Successive Over-Relaxation (SSOR) preconditioner. We will construct it from first principles, analyze its fundamental properties, explore its performance, and investigate its behavior from multiple theoretical perspectives.

### Constructing the SSOR Preconditioner

The SSOR [preconditioner](@entry_id:137537) is born from the Successive Over-Relaxation (SOR) stationary iterative method. An iterative method can be repurposed as a [preconditioning](@entry_id:141204) step by defining the action of the [preconditioner](@entry_id:137537)'s inverse, $M^{-1}$, on a vector (typically the residual, $r$) as one full iteration of the method applied to the system $Az=r$ with an initial guess of zero.

Let $A$ be an SPD matrix, which admits the splitting $A = D - L - U$, where $D$ is the diagonal part of $A$, $-L$ is the strictly lower triangular part, and $-U$ is the strictly upper triangular part. Since $A$ is symmetric, we have $U = L^{\top}$. The forward SOR sweep to update an iterate $x^k$ is given by:
$$ (D - \omega L) x^{k+1/2} = \omega b + ((1-\omega)D + \omega U) x^k $$
where $\omega \in (0, 2)$ is the [relaxation parameter](@entry_id:139937). The SSOR method symmetrizes this process by following the forward sweep with a backward sweep, where the roles of $L$ and $U$ are interchanged:
$$ (D - \omega U) x^{k+1} = \omega b + ((1-\omega)D + \omega L) x^{k+1/2} $$
To derive the [preconditioner](@entry_id:137537), we consider one full SSOR sweep as the operator that maps the residual $r^k = b - Ax^k$ to the update $\delta^k = x^{k+1} - x^k$. The action of the preconditioner inverse is thus $M_{\mathrm{SSOR}}^{-1}r^k = \delta^k$. This procedure can be derived systematically by composing the two sweeps algebraically  .

An equivalent and more direct way to derive the preconditioner matrix $M$ is to consider the action $z = M^{-1}r$ as the result of applying one full SSOR iteration to the system $Az=r$ starting from an initial guess $z_0 = 0$.

1.  **Forward Sweep:** An intermediate vector $z_{1/2}$ is computed using the forward SOR formula for the system $Az=r$ with $z_0=0$:
    $$ (D - \omega L) z_{1/2} = \omega r + ((1-\omega)D + \omega U)z_0 \implies (D - \omega L) z_{1/2} = \omega r $$
    Thus, $z_{1/2} = \omega (D - \omega L)^{-1} r$.

2.  **Backward Sweep:** The final vector $z$ is computed from $z_{1/2}$ using the backward SOR formula:
    $$ (D - \omega U) z = \omega r + ((1-\omega)D + \omega L) z_{1/2} $$
    Substituting the expression for $z_{1/2}$:
    $$ (D - \omega U) z = \omega r + ((1-\omega)D + \omega L) \omega (D - \omega L)^{-1} r $$
    $$ (D - \omega U) z = \omega \left[ I + ((1-\omega)D + \omega L) (D - \omega L)^{-1} \right] r $$
    To simplify the term in the brackets, we combine the matrices over a common denominator:
    $$ I + ((1-\omega)D + \omega L) (D - \omega L)^{-1} = \left[ (D - \omega L) + ((1-\omega)D + \omega L) \right] (D - \omega L)^{-1} $$
    $$ = (D - \omega L + D - \omega D + \omega L) (D - \omega L)^{-1} = (2-\omega)D (D - \omega L)^{-1} $$
    Substituting this back, we find the action of $M_{\mathrm{SSOR}}^{-1}$:
    $$ (D - \omega U) z = \omega (2-\omega)D (D - \omega L)^{-1} r $$
    $$ z = \omega (2-\omega) (D - \omega U)^{-1} D (D - \omega L)^{-1} r $$
    We have now found the inverse of the SSOR [preconditioner](@entry_id:137537), $M_{\mathrm{SSOR}}^{-1}$. To obtain the [preconditioner](@entry_id:137537) $M_{\mathrm{SSOR}}$ itself, we invert this expression:
    $$ M_{\mathrm{SSOR}}(\omega) = \left( \omega (2-\omega) (D - \omega U)^{-1} D (D - \omega L)^{-1} \right)^{-1} $$
    Using the property $(XYZ)^{-1} = Z^{-1}Y^{-1}X^{-1}$, this yields the standard formula for the **Symmetric Successive Over-Relaxation (SSOR) preconditioner**:
    $$ M_{\mathrm{SSOR}}(\omega) = \frac{1}{\omega(2-\omega)} (D - \omega L) D^{-1} (D - \omega U) $$
    Since $A$ is symmetric, $U = L^\top$, and the expression can be written as:
    $$ M_{\mathrm{SSOR}}(\omega) = \frac{1}{\omega(2-\omega)} (D - \omega L) D^{-1} (D - \omega L^\top) $$

A particularly important special case arises when $\omega = 1$. In this scenario, the SOR method reduces to the Gauss-Seidel method, and the SSOR preconditioner becomes the **Symmetric Gauss-Seidel (SGS) [preconditioner](@entry_id:137537)** :
$$ M_{\mathrm{SGS}} = M_{\mathrm{SSOR}}(1) = (D - L) D^{-1} (D - U) $$
The action of the SGS [preconditioner](@entry_id:137537) inverse, $z = M_{\mathrm{SGS}}^{-1}r$, can be interpreted as performing one forward Gauss-Seidel sweep on the system $A\tilde{z} = r$ (to get an intermediate result), followed by one backward Gauss-Seidel sweep.

### Fundamental Properties of the SSOR Preconditioner

For a [preconditioner](@entry_id:137537) to be used with the Conjugate Gradient method on an SPD system, it must also be symmetric and [positive definite](@entry_id:149459). The SSOR preconditioner, by its construction, satisfies these [critical properties](@entry_id:260687).

#### Symmetry and Positive Definiteness

Let us verify that $M_{\mathrm{SSOR}}(\omega)$ is SPD for any SPD matrix $A$ and any $\omega \in (0,2)$  . The scaling factor $\frac{1}{\omega(2-\omega)}$ is positive for $\omega \in (0,2)$, so we need only check the matrix part.

-   **Symmetry**: We take the transpose of the matrix part, using $U=L^\top$ and $D=D^\top$:
    $$ \left( (D - \omega L) D^{-1} (D - \omega U) \right)^\top = (D - \omega U)^\top (D^{-1})^\top (D - \omega L)^\top $$
    $$ = (D^\top - \omega U^\top) (D^\top)^{-1} (D^\top - \omega L^\top) = (D - \omega L) D^{-1} (D - \omega U) $$
    The matrix is identical to its transpose, hence it is symmetric.

-   **Positive Definiteness**: To show positive definiteness, we examine the quadratic form $x^\top M_{\mathrm{SSOR}}(\omega) x$ for a non-zero vector $x$.
    $$ x^\top M_{\mathrm{SSOR}}(\omega) x = \frac{1}{\omega(2-\omega)} x^\top (D - \omega L) D^{-1} (D - \omega L^\top) x $$
    Let $y = (D - \omega L^\top) x$. The expression becomes $\frac{1}{\omega(2-\omega)} y^\top D^{-1} y$. Since $A$ is SPD, its diagonal entries are positive, making $D$ and its inverse $D^{-1}$ SPD. Thus, $y^\top D^{-1} y > 0$ as long as $y \neq 0$. The matrix $(D - \omega L^\top)$ is lower triangular with positive diagonal entries, so it is invertible. This ensures that if $x \neq 0$, then $y = (D - \omega L^\top) x \neq 0$. Consequently, $x^\top M_{\mathrm{SSOR}}(\omega) x > 0$ for all non-zero $x$.

This proof holds for any ordering of the variables, as a reordering simply permutes $A$ to another SPD matrix $A' = PAP^\top$, and the argument applies equally to $A'$. Thus, the SSOR preconditioner is SPD regardless of ordering .

#### Cholesky-like Factorization

The structure of the SSOR preconditioner lends itself to a powerful interpretation. Since $D$ is a diagonal matrix with positive entries, its square root $D^{1/2}$ and inverse square root $D^{-1/2}$ are well-defined real [diagonal matrices](@entry_id:149228). We can rewrite the SSOR formula by splitting the $D^{-1}$ term :
$$ M_{\mathrm{SSOR}}(\omega) = \frac{1}{\omega(2-\omega)} (D - \omega L) D^{-1/2}D^{-1/2} (D - \omega L^\top) $$
Grouping the terms, we get $M_{\mathrm{SSOR}}(\omega) = B B^\top$, where $B$ is the [lower triangular matrix](@entry_id:201877)
$$ B = \frac{1}{\sqrt{\omega(2-\omega)}}(D - \omega L)D^{-1/2} $$
This shows that $M_{\mathrm{SSOR}}(\omega)$ has a Cholesky-like factorization. This form is not merely a theoretical curiosity; it is central to the practical application of the preconditioner. In PCG, one needs to solve systems of the form $Mz = r$. Using the factorization $M=BB^\top$, this is done efficiently via two triangular solves: first solve $By=r$ for $y$ ([forward substitution](@entry_id:139277)), then solve $B^\top z = y$ for $z$ ([backward substitution](@entry_id:168868)).

#### Preconditioned Operators

When applying [preconditioning](@entry_id:141204), one can use left, right, or split (symmetric) preconditioning.
- **Left Preconditioning:** Solve $M^{-1} A x = M^{-1} b$. The operator is $M^{-1}A$.
- **Right Preconditioning:** Solve $A M^{-1} y = b$, with $x = M^{-1}y$. The operator is $AM^{-1}$.
- **Split Preconditioning:** Solve $M^{-1/2} A M^{-1/2} y = M^{-1/2}b$, with $x=M^{-1/2}y$. The operator is $M^{-1/2} A M^{-1/2}$.

A fundamental result from linear algebra states that for any [invertible matrices](@entry_id:149769) $X$ and $Y$, the products $XY$ and $YX$ have the same eigenvalues. Therefore, the left-preconditioned operator $M^{-1}A$ and the right-preconditioned operator $AM^{-1}$ are spectrally equivalent. Furthermore, the operator $M^{-1}A$ is similar to the split-preconditioned operator $M^{-1/2}AM^{-1/2}$, since $M^{-1}A = M^{-1/2}(M^{-1/2}AM^{-1/2})M^{1/2}$. Because similarity transformations preserve eigenvalues, all three operators share the same spectrum .

The split form is theoretically crucial: since $A$ and $M$ are SPD, the operator $M^{-1/2} A M^{-1/2}$ is also SPD. This guarantees that its eigenvalues are real and positive, and it is this [symmetric operator](@entry_id:275833) to which the standard convergence theory of the Conjugate Gradient method applies.

### Performance and Optimization

The performance of the SSOR [preconditioner](@entry_id:137537) is determined by how well it clusters the eigenvalues of the preconditioned operator around 1. This, in turn, depends heavily on the choice of the [relaxation parameter](@entry_id:139937) $\omega$.

#### A Concrete Example

To make these concepts tangible, consider the simple $2 \times 2$ SPD matrix corresponding to the 1D discrete Laplacian: $A = \begin{pmatrix} 2  & -1 \\ -1  & 2 \end{pmatrix}$. The eigenvalues of $A$ are $1$ and $3$, giving a condition number of $\kappa(A) = 3$. Let's apply SSOR [preconditioning](@entry_id:141204) with $\omega=1$ (i.e., SGS). As shown in , the preconditioner is $M = \begin{pmatrix} 2  & -1 \\ -1  & 5/2 \end{pmatrix}$.

The left-preconditioned operator is $M^{-1}A = \begin{pmatrix} 1  & -1/8 \\ 0  & 3/4 \end{pmatrix}$. Since this matrix is triangular, its eigenvalues are simply its diagonal entries: $\lambda_1 = 1$ and $\lambda_2 = 3/4$. The condition number of the preconditioned operator is $\kappa(M^{-1}A) = \frac{\lambda_{\max}}{\lambda_{\min}} = \frac{1}{3/4} = \frac{4}{3} \approx 1.333$. Preconditioning has successfully reduced the condition number from $3$ to $4/3$, which will accelerate the convergence of the CG method.

#### Optimizing the Relaxation Parameter $\omega$

The previous example used $\omega=1$, but is this the best choice? Finding the optimal $\omega$ is a critical task. It is crucial to distinguish the goal here from that of optimizing SOR as a stand-alone iterative method .
- When using **SOR as a solver**, the goal is to minimize the [spectral radius](@entry_id:138984) of the non-symmetric SOR iteration matrix, $\rho(T_{\mathrm{SOR}}(\omega))$.
- When using **SSOR as a preconditioner for CG**, the goal is to minimize the condition number of the (symmetrizable) preconditioned matrix, $\kappa(M_{\mathrm{SSOR}}(\omega)^{-1}A)$.

These are two distinct optimization problems, and they generally lead to different optimal values of $\omega$. One cannot assume that the best $\omega$ for SOR iteration is also the best for SSOR preconditioning.

The ideal optimization, minimizing $\kappa(M^{-1}A)$, can be complex. A practical surrogate is to choose $\omega$ to make $M^{-1/2}AM^{-1/2}$ as close to the identity matrix $I$ as possible. One way to measure this is to minimize the Frobenius norm of the difference, which corresponds to minimizing the sum of the squared deviations of the eigenvalues from 1: $\min_{\omega} \sum_i (\lambda_i - 1)^2$ .

For certain model problems, an analytical expression for an optimal or near-optimal $\omega$ can be found. For the matrix $A_n$ arising from the 1D [finite difference discretization](@entry_id:749376) of the Laplacian, it can be shown that minimizing a classical bound on $\kappa(M_\omega^{-1} A_n)$ is achieved by choosing $\omega$ that minimizes the spectral radius of the corresponding SOR iteration matrix . This optimal value, $\omega_\star$, is related to the [spectral radius](@entry_id:138984) of the Jacobi [iteration matrix](@entry_id:637346), $\rho_J = \rho(D^{-1}(L+U))$, by the well-known formula:
$$ \omega_\star = \frac{2}{1 + \sqrt{1 - \rho_J^2}} $$
For the $n \times n$ matrix $A_n$, the Jacobi [spectral radius](@entry_id:138984) is $\rho_J = \cos(\frac{\pi}{n+1})$. This leads to the optimal [relaxation parameter](@entry_id:139937) for this model problem:
$$ \omega_\star = \frac{2}{1 + \sin(\frac{\pi}{n+1})} $$
This result provides valuable theoretical guidance for choosing $\omega$ in practice for problems with a similar structure.

### Advanced Perspectives

#### Dependence on Ordering

Unlike the Jacobi [preconditioner](@entry_id:137537), the SSOR preconditioner is fundamentally **dependent on the ordering** of the variables. An ordering of the vertices in the matrix's adjacency graph, $G(A)$, defines which entries fall into the lower triangular part $L$ and which fall into the upper triangular part $U$. Changing the [vertex ordering](@entry_id:261753) via a permutation matrix $P$ leads to a new matrix $A' = PAP^\top$ with a new splitting $A' = D' - L' - U'$. The resulting SSOR [preconditioner](@entry_id:137537) $M'$ will, in general, be different from the permuted original preconditioner $PMP^\top$. Consequently, the spectrum of the preconditioned operator $M'^{-1}A'$ is generally different from that of $M^{-1}A$ .

This dependence is both a challenge and an opportunity. It means there is no single "SSOR preconditioner" for a given matrix $A$, but rather a family of them, one for each possible ordering. This motivates the use of reordering algorithms, such as Reverse Cuthill-McKee (RCM) or Approximate Minimum Degree (AMD), to find an ordering that improves the [preconditioner](@entry_id:137537)'s effectiveness. However, these are [heuristics](@entry_id:261307), and they are not guaranteed to improve performance in all cases .

#### SSOR as a Smoother: A Fourier Perspective

A deeper insight into the mechanism of SSOR can be gained through Fourier analysis, especially for matrices arising from PDE discretizations on regular grids. For the 1D Poisson problem, the SSOR [preconditioner](@entry_id:137537) can be viewed as an "energy-norm filter" .

In this context, the eigenvectors of the Laplacian operator are discrete sine functions, representing different frequencies. Applying the SSOR preconditioner scales these modes non-uniformly. Analysis shows that SSOR acts as a **smoother**: it is highly effective at damping high-frequency (oscillatory) error components but is much less effective on low-frequency (smooth) error components. The eigenvalues of the preconditioned operator corresponding to high-frequency modes are clustered near 1, while those for low-frequency modes are further away.

This property explains why SSOR is an excellent choice for a smoother within a [multigrid method](@entry_id:142195). The high-frequency errors are efficiently eliminated by a few SSOR sweeps on the fine grid. The remaining smooth error can then be effectively approximated and solved on a coarser grid, where it appears more oscillatory. The combination of SSOR [smoothing and coarse-grid correction](@entry_id:754981) is the engine that drives the remarkable efficiency of [multigrid solvers](@entry_id:752283).