## Introduction
Solving large [systems of linear equations](@entry_id:148943), often expressed as $Ax=b$, is a cornerstone of computational science and engineering. While direct methods like Gaussian elimination are effective for smaller systems, they become computationally infeasible for the massive, sparse matrices that arise from discretizing [partial differential equations](@entry_id:143134) or modeling [complex networks](@entry_id:261695). Stationary [iterative methods](@entry_id:139472) provide a powerful alternative, generating a sequence of approximate solutions that converge toward the exact solution. This approach avoids the high cost of direct factorization, making it suitable for large-scale problems. This article addresses the fundamental question of how to construct these iterative schemes and rigorously analyze their convergence. It provides a comprehensive exploration of these foundational techniques. The journey begins in the "Principles and Mechanisms" chapter, which lays out the core theory of matrix splitting, the derivation of classical methods like Jacobi and Gauss-Seidel, and the critical role of the spectral radius in determining convergence. The "Applications and Interdisciplinary Connections" chapter then demonstrates the broad utility of these methods, from solving PDEs in physics to analyzing [electrical circuits](@entry_id:267403) and stochastic processes. Finally, the "Hands-On Practices" section offers concrete exercises to solidify theoretical understanding and build practical skills in applying these essential numerical tools.

## Principles and Mechanisms

The solution of the linear system $A x = b$ is a foundational problem in computational science. While direct methods like Gaussian elimination provide an exact solution in a finite number of steps, they can be computationally prohibitive for large, sparse systems that frequently arise in the [discretization of partial differential equations](@entry_id:748527). Stationary iterative methods offer an alternative approach, constructing a sequence of approximate solutions $\{x^{k}\}$ that, under appropriate conditions, converges to the true solution $x^{\star}$. This chapter elucidates the fundamental principles governing these methods, their mechanisms of convergence, and the practical considerations that determine their efficacy.

### The General Framework of Stationary Iterative Methods

The core idea behind any stationary [iterative method](@entry_id:147741) is the concept of **matrix splitting**. We decompose the system matrix $A$ into the difference of two matrices, $A = M - N$, where $M$ is chosen to be a matrix that is easily invertible. "Easily invertible" typically means that $M$ is diagonal, triangular, or a product of such matrices, allowing the system $Mz=d$ to be solved much more efficiently than the original system $Ax=b$.

Given this splitting, we can rewrite the original equation $Ax=b$ as $(M-N)x = b$, or $Mx = Nx + b$. This algebraic rearrangement forms the basis of the iterative scheme. We replace the exact solution $x$ on each side with successive iterates, leading to the general form of a stationary iteration:

$$ M x^{k+1} = N x^k + b $$

Since $M$ is nonsingular by construction, we can solve for the next iterate $x^{k+1}$ by left-multiplying by $M^{-1}$:

$$ x^{k+1} = M^{-1}N x^k + M^{-1}b $$

This equation is in the [canonical form](@entry_id:140237) of a [fixed-point iteration](@entry_id:137769), $x^{k+1} = T x^k + c$. We can immediately identify the **iteration matrix** $T = M^{-1}N$ and the constant vector $c = M^{-1}b$. The term "stationary" refers to the fact that the matrix $T$ and vector $c$ are constant for all iterations $k$.

A crucial property of this construction is the relationship between the fixed point of the iteration and the solution to the original linear system. A fixed point $x^{\star}$ is a vector that remains unchanged by the iteration, meaning $x^{\star} = T x^{\star} + c$. By substituting the expressions for $T$ and $c$, we have $x^{\star} = (M^{-1}N)x^{\star} + M^{-1}b$. Left-multiplying by $M$ yields $Mx^{\star} = Nx^{\star} + b$, which rearranges to $(M-N)x^{\star} = b$, or simply $A x^{\star} = b$. Thus, a vector is a fixed point of the stationary iteration if and only if it is a solution to the original linear system $Ax=b$ . If $A$ is nonsingular, this fixed point is unique and corresponds to the unique solution $x^{\star} = A^{-1}b$ .

An alternative and often useful expression for the [iteration matrix](@entry_id:637346) can be derived from the splitting $A=M-N$. This implies $N = M-A$. Substituting this into the definition of $T$ gives:

$$ T = M^{-1}(M-A) = M^{-1}M - M^{-1}A = I - M^{-1}A $$

This form highlights that the iteration matrix is a perturbation of the identity matrix, a perspective that is valuable in both analysis and implementation .

### The Mechanism of Convergence: Error Propagation

The central question for any [iterative method](@entry_id:147741) is whether the sequence of approximates $\{x^{k}\}$ converges to the true solution $x^{\star}$. To answer this, we must analyze the behavior of the **error vector**, defined at each step as $e^{k} = x^{\star} - x^{k}$.

We have the iteration for the approximate solution, $x^{k+1} = T x^{k} + c$, and the [fixed-point equation](@entry_id:203270) for the true solution, $x^{\star} = T x^{\star} + c$. Subtracting the former from the latter gives a simple and powerful relationship for the propagation of error :

$$ x^{\star} - x^{k+1} = (T x^{\star} + c) - (T x^{k} + c) = T(x^{\star} - x^{k}) $$

This simplifies to the fundamental **[error propagation](@entry_id:136644) equation**:

$$ e^{k+1} = T e^{k} $$

By applying this relation recursively, we find that the error at step $k$ is related to the initial error $e^0 = x^{\star} - x^0$ by $e^{k} = T^{k}e^0$. The iteration converges to the true solution for any arbitrary starting vector $x^0$ if and only if the error vector $e^k$ vanishes as $k \to \infty$, regardless of the initial error $e^0$. This requires the matrix power $T^k$ to converge to the zero matrix as $k \to \infty$.

A cornerstone of [matrix analysis](@entry_id:204325) provides the necessary and [sufficient condition](@entry_id:276242) for this to occur: $\lim_{k \to \infty} T^k = 0$ if and only if the **[spectral radius](@entry_id:138984)** of $T$, denoted $\rho(T)$, is strictly less than 1. The [spectral radius](@entry_id:138984) is defined as the maximum modulus of the eigenvalues of the iteration matrix $T$:

$$ \rho(T) = \max \{ |\lambda| : \det(T - \lambda I) = 0 \} $$

Therefore, we arrive at the **fundamental theorem of convergence for stationary iterative methods**: the iteration converges for any initial vector $x^0$ if and only if $\rho(T)  1$  . If $\rho(T) \ge 1$, the iteration will fail to converge for at least some initial guesses .

For instance, consider a method whose [iteration matrix](@entry_id:637346) is $T = \begin{pmatrix} 0  2 \\ 0  0.4 \end{pmatrix}$. Since $T$ is upper triangular, its eigenvalues are its diagonal entries, $\lambda_1 = 0$ and $\lambda_2 = 0.4$. The spectral radius is $\rho(T) = \max\{|0|, |0.4|\} = 0.4$. Because $0.4  1$, the corresponding iterative method is guaranteed to converge .

### Classical Stationary Methods

The general framework of matrix splitting gives rise to several classical methods, each defined by a specific choice of $M$ and $N$. These methods are derived from the standard decomposition of the matrix $A$ into its diagonal, strictly lower-triangular, and strictly upper-triangular parts. We adopt the convention $A = D - L - U$, where $D$ is the diagonal of $A$, $-L$ is the strictly lower part of $A$, and $-U$ is the strictly upper part of $A$. This implies that the matrices $L$ and $U$ themselves have zero diagonals and non-negative entries if the corresponding off-diagonal entries of $A$ are negative. We assume that all diagonal entries of $A$ are non-zero, ensuring $D$ is invertible.

#### The Jacobi Method

The Jacobi method is perhaps the most straightforward iterative scheme. At each step, to find the $i$-th component of the new iterate $x_i^{k+1}$, it uses only the component values from the *previous* iterate $x^k$. This corresponds to moving all off-diagonal terms to the right-hand side of the equation $Ax=b$ and dividing by the diagonal element $a_{ii}$. In matrix form, this is equivalent to choosing the splitting $M_J = D$ and $N_J = L+U$.

The Jacobi iteration is then $Dx^{k+1} = (L+U)x^k + b$, which gives the [iteration matrix](@entry_id:637346):

$$ T_J = D^{-1}(L+U) = I - D^{-1}A $$

The affine term is $c_J = D^{-1}b$ . The key feature of the Jacobi method is that all components of $x^{k+1}$ can be computed simultaneously (or "in parallel"), as each new component $x_i^{k+1}$ depends only on the elements of $x^k$.

#### The Gauss-Seidel Method

The Gauss-Seidel (GS) method is a refinement of the Jacobi method. It aims to accelerate convergence by using the most up-to-date information available. When computing the $i$-th component $x_i^{k+1}$, it uses the newly computed values $x_1^{k+1}, \dots, x_{i-1}^{k+1}$ from the current iteration, and the old values $x_{i+1}^{k}, \dots, x_{n}^{k}$ for the components not yet updated.

This sequential update process corresponds to the splitting $A = (D-L) - U$. We choose $M_{GS} = D-L$ and $N_{GS} = U$. The matrix $M_{GS}$ is lower triangular, and since its diagonal entries are the non-zero diagonal entries of $A$, it is invertible by [forward substitution](@entry_id:139277). The Gauss-Seidel iteration is $(D-L)x^{k+1} = Ux^k + b$, and its iteration matrix is:

$$ T_{GS} = (D-L)^{-1}U $$

The update process is inherently sequential, which makes it less amenable to [parallelization](@entry_id:753104) than the Jacobi method .

#### Successive Over-Relaxation (SOR)

The SOR method can be viewed as an [extrapolation](@entry_id:175955) of the Gauss-Seidel method. It introduces a [relaxation parameter](@entry_id:139937) $\omega$ to potentially accelerate convergence. A key takeaway from the existence of methods like SOR is that for a single matrix $A$, different splittings can lead to vastly different convergence behaviors. The choice of splitting, and thus the choice of method, is not arbitrary. For example, for the [symmetric positive definite matrix](@entry_id:142181) $A = \begin{pmatrix} 2  -1 \\ -1  2 \end{pmatrix}$, the Gauss-Seidel method (which is SOR with $\omega=1$) converges, with $\rho(T_{GS}) = 0.25$. However, the SOR method for the same matrix with $\omega=2.5$ yields an [iteration matrix](@entry_id:637346) with $\rho(T_{SOR}) = 1.5$, which guarantees divergence. This demonstrates that convergence is not a property of the matrix $A$ alone, but of the interplay between $A$ and the chosen splitting $(M,N)$ .

### Conditions for Convergence

While the condition $\rho(T)  1$ is both necessary and sufficient, calculating the eigenvalues of the [iteration matrix](@entry_id:637346) $T$ can be as computationally demanding as solving the original system. Therefore, it is invaluable to have [sufficient conditions](@entry_id:269617) for convergence that depend only on the properties of the original matrix $A$.

A simple and powerful condition is **[diagonal dominance](@entry_id:143614)**. A matrix $A$ is called **strictly diagonally dominant** if for every row $i$, the absolute value of the diagonal entry is greater than the sum of the [absolute values](@entry_id:197463) of the off-diagonal entries in that row:
$$ |a_{ii}|  \sum_{j \neq i} |a_{ij}|, \quad \text{for all } i=1, \dots, n. $$
If a matrix $A$ is strictly [diagonally dominant](@entry_id:748380), then both the Jacobi and Gauss-Seidel methods are guaranteed to converge.

A more general result involves a weaker condition. A matrix is **weakly diagonally dominant** if $|a_{ii}| \ge \sum_{j \neq i} |a_{ij}|$ for all $i$. If a matrix is also **irreducible**, meaning its associated directed graph is strongly connected, and the strict inequality holds for at least one row, the matrix is called **irreducibly [diagonally dominant](@entry_id:748380)**. The Taussky-Varga theorem states that if $A$ is irreducibly [diagonally dominant](@entry_id:748380), then both Jacobi and Gauss-Seidel converge.

For example, the matrix $A = \begin{pmatrix} 2  -1  -1 \\ -1  3  -1 \\ -1  -1  3 \end{pmatrix}$ is irreducible and weakly diagonally dominant (with [strict dominance](@entry_id:137193) in rows 2 and 3), so its Jacobi iteration converges. In contrast, the related matrix $B = \begin{pmatrix} 2  -1  -1 \\ -1  2  -1 \\ -1  -1  2 \end{pmatrix}$, which is also irreducible but only weakly diagonally dominant (with no strictly dominant rows), leads to a Jacobi iteration with $\rho(T_J) = 1$, for which convergence is not guaranteed .

### Advanced Topics in Convergence Behavior

#### Residual Dynamics

While the error vector $e^k$ is the theoretical object of interest, it is not computable in practice because the true solution $x^{\star}$ is unknown. A practical, computable quantity is the **[residual vector](@entry_id:165091)**, defined as $r^k = b - A x^k$. The residual measures how well the approximate solution $x^k$ satisfies the original equation.

The error and the residual are connected by a simple [linear relationship](@entry_id:267880). Substituting $b = Ax^{\star}$ into the residual definition gives:
$$ r^k = Ax^{\star} - Ax^k = A(x^{\star} - x^k) = A e^k $$
Since $A$ is nonsingular, we can also write $e^k = A^{-1} r^k$. This means the norm of the residual, $\|r^k\|$, can serve as a proxy for the norm of the error, $\|e^k\|$.

Furthermore, the residual itself follows a stationary iterative process. Starting with $r^{k+1} = A e^{k+1}$ and using the [error propagation](@entry_id:136644) $e^{k+1} = T e^k$ and $e^k = A^{-1} r^k$, we find:
$$ r^{k+1} = A(T e^k) = A(T(A^{-1}r^k)) = (ATA^{-1})r^k $$
Thus, the residual propagates according to the matrix $S = ATA^{-1}$. This transformation relating $T$ and $S$ is a **similarity transformation**. A key property of [similar matrices](@entry_id:155833) is that they have the same eigenvalues. Therefore, $\rho(S) = \rho(T)$, and the convergence condition can be stated equivalently in terms of the [spectral radius](@entry_id:138984) of the residual propagator .

#### Transient Error Growth and Nonnormal Matrices

The criterion $\rho(T)  1$ guarantees that the error $\|e^k\|$ will eventually decay to zero. However, it does not guarantee that the error will decrease at every single step. For some methods, the error can exhibit **transient growth**, where $\|e^k\|$ temporarily increases for a few iterations before the asymptotic convergence takes over.

This behavior is intimately linked to the properties of the iteration matrix $T$. A matrix $T$ is called **normal** if it commutes with its [conjugate transpose](@entry_id:147909), $TT^* = T^*T$. For [normal matrices](@entry_id:195370), the [2-norm](@entry_id:636114) (or spectral norm) is equal to the [spectral radius](@entry_id:138984): $\|T\|_2 = \rho(T)$. In this case, the [error propagation](@entry_id:136644) $\|e^{k+1}\|_2 = \|Te^k\|_2 \le \|T\|_2 \|e^k\|_2 = \rho(T)\|e^k\|_2$. If $\rho(T)  1$, the error norm is guaranteed to decrease monotonically at every step .

However, many iteration matrices are **nonnormal**. For a nonnormal matrix, it is possible to have $\|T\|_2 > 1$ even when $\rho(T)  1$. This discrepancy is the source of transient growth. The bound $\|e^{k+1}\|_2 \le \|T\|_2 \|e^k\|_2$ no longer guarantees a decrease in error if $\|T\|_2 > 1$.

The canonical example of this phenomenon is a Jordan block, such as $T = \begin{pmatrix} \alpha  1 \\ 0  \alpha \end{pmatrix}$ with $0  \alpha  1$. Here, $\rho(T) = \alpha  1$, ensuring eventual convergence. However, $T$ is nonnormal, and its norm is $\|T\|_2 > 1$. If we start with an initial error $e^0 = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$, the next error is $e^1 = Te^0 = \begin{pmatrix} 1 \\ \alpha \end{pmatrix}$. The [error norms](@entry_id:176398) are $\|e^0\|_2 = 1$ and $\|e^1\|_2 = \sqrt{1+\alpha^2} > 1$. The error has grown.

This growth is explained by the behavior of the powers of $T$. For the Jordan block, $T^k = \begin{pmatrix} \alpha^k  k\alpha^{k-1} \\ 0  \alpha^k \end{pmatrix}$. The off-diagonal term $k\alpha^{k-1}$ can increase for small $k$ before the [exponential decay](@entry_id:136762) of $\alpha^{k-1}$ dominates the linear growth of $k$. This initial increase in the entries of $T^k$ can cause $\|T^k\|_2$ to grow before it ultimately decays to zero, enabling transient error growth . For diagonalizable matrices, this effect is governed by the condition number of the eigenvector matrix, $\kappa(V)$, which appears in the bound $\|T^k\|_2 \le \kappa(V)\rho(T)^k$. A large condition number, a hallmark of [non-normality](@entry_id:752585), allows for significant transient amplification of the error even as $\rho(T)^k$ decays .