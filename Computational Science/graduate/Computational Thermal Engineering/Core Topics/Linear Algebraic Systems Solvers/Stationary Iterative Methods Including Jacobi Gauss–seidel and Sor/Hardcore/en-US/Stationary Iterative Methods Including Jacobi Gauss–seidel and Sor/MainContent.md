## Introduction
In [computational engineering](@entry_id:178146), the [discretization of partial differential equations](@entry_id:748527) that model physical phenomena like heat transfer and fluid flow invariably leads to large, sparse [systems of linear equations](@entry_id:148943). While [direct solvers](@entry_id:152789) are effective for small problems, their computational cost and memory demands become prohibitive for the high-fidelity simulations required in [modern analysis](@entry_id:146248). This challenge necessitates the use of [iterative methods](@entry_id:139472), which offer a more scalable and efficient path to a solution. This article provides a comprehensive exploration of [stationary iterative methods](@entry_id:144014)—the foundational class of such techniques.

The following chapters will guide you from theory to practice. The **Principles and Mechanisms** chapter lays the theoretical groundwork, detailing matrix splitting, convergence theory, and the mechanics of the Jacobi, Gauss-Seidel, and Successive Over-Relaxation (SOR) methods. Next, the **Applications and Interdisciplinary Connections** chapter demonstrates how these methods are applied to solve real-world engineering problems, from heat conduction to fluid dynamics, and explores their surprising relevance in fields like machine learning and image processing. Finally, the **Hands-On Practices** section provides concrete exercises to solidify your understanding and build practical implementation skills. We begin by establishing the fundamental principles that govern all [stationary iterative methods](@entry_id:144014).

## Principles and Mechanisms

The [discretization of partial differential equations](@entry_id:748527) governing thermal and fluid systems frequently results in large, sparse systems of linear algebraic equations of the form $A x = b$. While direct methods like Gaussian elimination are effective for small systems, their computational cost and memory requirements become prohibitive for the large-scale problems common in [computational engineering](@entry_id:178146). This necessitates the use of iterative methods, which generate a sequence of approximate solutions $\{x^k\}$ that converges to the true solution $x^*$. This chapter introduces the foundational class of **[stationary iterative methods](@entry_id:144014)**, detailing their theoretical underpinnings and the mechanisms of the most common variants: the Jacobi, Gauss-Seidel, and Successive Over-Relaxation methods.

### The General Framework of Stationary Iterative Methods

The core principle of a stationary iterative method is to rearrange the system $A x = b$ into an equivalent fixed-point problem of the form $x = g(x)$, which then suggests an iterative scheme $x^{k+1} = g(x^k)$. This transformation is systematically achieved through a **matrix splitting**.

#### Matrix Splitting and the Iteration Matrix

We begin by splitting the [coefficient matrix](@entry_id:151473) $A$ into two matrices, $A = M - N$, where $M$ is a nonsingular matrix chosen to be easily invertible. The choice of $M$ is the defining feature of a particular stationary method. Substituting this split into the original system gives:

$(M - N) x = b$

This can be rearranged to isolate a term with $M$:

$M x = N x + b$

This equation naturally suggests a [fixed-point iteration](@entry_id:137769). By evaluating the left-hand side at the new iteration level, $k+1$, and the right-hand side at the current level, $k$, we obtain the general form of a stationary iterative method :

$M x^{k+1} = N x^k + b$

Since $M$ is nonsingular, we can solve for the next iterate $x^{k+1}$:

$x^{k+1} = M^{-1} N x^k + M^{-1} b$

This equation is in the [canonical form](@entry_id:140237) $x^{k+1} = B x^k + c$, where the matrix $B = M^{-1} N$ is called the **[iteration matrix](@entry_id:637346)** and the vector $c = M^{-1} b$ is a constant vector associated with the iteration. The method is termed "stationary" because the matrix $B$ and vector $c$ do not change from one iteration to the next.

The convergence of such a method is determined entirely by the properties of its [iteration matrix](@entry_id:637346) $B$. An iterative method is convergent for any initial guess $x^0$ if and only if the **spectral radius** of the [iteration matrix](@entry_id:637346) is strictly less than one :

$\rho(B) = \max_{i} |\lambda_i|  1$

where $\{\lambda_i\}$ are the eigenvalues of $B$. The smaller the spectral radius, the faster the asymptotic [rate of convergence](@entry_id:146534).

#### Equivalence with Preconditioned Richardson Iteration

An alternative perspective on stationary methods arises from the idea of **[residual correction](@entry_id:754267)**. The residual at step $k$ is defined as $r^k = b - A x^k$. The iteration can be viewed as updating the current solution $x^k$ with a correction term that is related to the residual. The **preconditioned Richardson iteration** formalizes this as :

$x^{k+1} = x^k + M^{-1} r^k = x^k + M^{-1}(b - A x^k)$

Here, $M^{-1}$ acts as a preconditioner that approximates the action of $A^{-1}$. Rearranging this equation reveals its connection to the matrix-splitting framework:

$x^{k+1} = (I - M^{-1}A) x^k + M^{-1} b$

Comparing this to the form $x^{k+1} = M^{-1}N x^k + M^{-1}b$, we see that the iteration matrices are identical if we identify $M^{-1}N = I - M^{-1}A$. Multiplying by $M$ from the left gives $N = M - A$. Thus, the preconditioned Richardson iteration is algebraically equivalent to the matrix splitting scheme $A = M - (M - A)$. This provides a powerful dual perspective: a stationary method can be seen either as arising from a matrix split or as a preconditioned [residual correction](@entry_id:754267).

A **weighted** or relaxed version of the Richardson iteration is often used  :

$x^{k+1} = x^k + \omega M^{-1}(b - A x^k) = (I - \omega M^{-1}A) x^k + \omega M^{-1} b$

Here, $\omega$ is a **[relaxation parameter](@entry_id:139937)** used to control the step size and potentially accelerate convergence. The corresponding [iteration matrix](@entry_id:637346) is $B(\omega) = I - \omega M^{-1} A$.

### Classical Point-Wise Methods

The general framework gives rise to specific, widely used methods through particular choices of the splitting matrix $M$. These choices are typically based on a [canonical decomposition](@entry_id:634116) of the matrix $A$ into its diagonal ($D$), strictly lower triangular ($-L$), and strictly upper triangular ($-U$) parts, such that $A = D - L - U$. Note the convention that $L$ and $U$ represent the negated strictly triangular parts of $A$ and thus have non-negative entries for typical discretization matrices.

#### The Jacobi Method

The Jacobi method is the simplest iterative scheme. It is defined by choosing the splitting matrix $M$ to be the diagonal part of $A$, i.e., $M_J = D$. This choice is computationally attractive because the inverse of a diagonal matrix is trivial to compute.

- **Splitting:** $M_J = D$, $N_J = L + U$.
- **Iteration Matrix:** $B_J = M_J^{-1} N_J = D^{-1}(L+U)$.
- **Update Formula:** $D x^{k+1} = (L+U) x^k + b$.

In component form, the update for the $i$-th unknown is:

$x_i^{k+1} = \frac{1}{a_{ii}} \left( b_i - \sum_{j \ne i} a_{ij} x_j^k \right)$

This formula reveals the mechanism of the Jacobi method: to compute the new value for $x_i^{k+1}$, it uses exclusively the values of all other components from the *previous* iteration, $x^k$. This means all components can be updated simultaneously (in parallel), but it also means the information from newly computed components within the same iteration is not utilized immediately.

For example, consider the 1D steady heat conduction problem on a bar, discretized with three interior nodes. This yields a linear system with the matrix $A = \begin{pmatrix} 2  -1  0 \\ -1  2  -1 \\ 0  -1  2 \end{pmatrix}$. The Jacobi [iteration matrix](@entry_id:637346) is $B_J = D^{-1}(L+U) = \begin{pmatrix} 0  1/2  0 \\ 1/2  0  1/2 \\ 0  1/2  0 \end{pmatrix}$. The eigenvalues of this matrix can be computed as $\{0, 1/\sqrt{2}, -1/\sqrt{2}\}$, giving a spectral radius of $\rho(B_J) = 1/\sqrt{2} \approx 0.707107$. Since $\rho(B_J)  1$, the Jacobi method is guaranteed to converge for this problem .

#### The Gauss-Seidel Method

The Gauss-Seidel (GS) method improves upon the Jacobi method by using the most up-to-date information available. It is defined by choosing the splitting matrix $M$ to be the lower triangular part of $A$, including the diagonal.

- **Splitting:** $M_{GS} = D - L$, $N_{GS} = U$.
- **Iteration Matrix:** $B_{GS} = M_{GS}^{-1} N_{GS} = (D-L)^{-1}U$.
- **Update Formula:** $(D-L) x^{k+1} = U x^k + b$.

In component form, the update for the $i$-th unknown is:

$x_i^{k+1} = \frac{1}{a_{ii}} \left( b_i - \sum_{j  i} a_{ij} x_j^{k+1} - \sum_{j > i} a_{ij} x_j^k \right)$

The key difference from Jacobi is apparent here: when computing $x_i^{k+1}$, the Gauss-Seidel method uses the newly computed values $x_j^{k+1}$ for all $j  i$ from the *current* iteration. This sequential, information-rich update is the reason Gauss-Seidel typically converges faster than Jacobi for problems arising from PDE discretizations.

For a simple 2D finite element problem resulting in the matrix $K = \begin{pmatrix} 2  -1 \\ -1  2 \end{pmatrix}$, the Gauss-Seidel [iteration matrix](@entry_id:637346) is $B_{GS} = (D-L)^{-1}U = \begin{pmatrix} 0  1/2 \\ 0  1/4 \end{pmatrix}$. The eigenvalues are $\{0, 1/4\}$, so the spectral radius is $\rho(B_{GS}) = 1/4$. This value is less than the corresponding Jacobi spectral radius of $\rho(B_J)=1/2$ for this matrix, illustrating the typical performance gain .

#### The Successive Over-Relaxation (SOR) Method

The Successive Over-Relaxation (SOR) method can be viewed as an extrapolated version of Gauss-Seidel. It takes the GS update and pushes it a bit further in the same direction, controlled by a [relaxation parameter](@entry_id:139937) $\omega$.

- **Splitting:** $M_{SOR} = \frac{1}{\omega}(D - \omega L)$, $N_{SOR} = \frac{1}{\omega}((1-\omega)D + \omega U)$.
- **Iteration Matrix:** $B_{SOR}(\omega) = M_{SOR}^{-1} N_{SOR} = (D - \omega L)^{-1}((1-\omega)D + \omega U)$.
- **Update Formula:** $(D - \omega L)x^{k+1} = ((1-\omega)D + \omega U)x^k + \omega b$.

The parameter $\omega$ is crucial. For convergence of SOR on a [symmetric positive-definite](@entry_id:145886) (SPD) matrix, $\omega$ must be in the range $(0, 2)$.
- If $\omega = 1$, SOR reduces to the Gauss-Seidel method.
- If $\omega \in (0, 1)$, the method is called **[under-relaxation](@entry_id:756302)**, which can help stabilize convergence for some problems.
- If $\omega \in (1, 2)$, the method is called **over-relaxation**, which can significantly accelerate convergence for many problems arising from PDEs. Finding the optimal $\omega_{opt}$ that minimizes $\rho(B_{SOR})$ is a key challenge in using SOR effectively.

### Convergence Theory and Analysis

The convergence of stationary methods is intimately linked to the properties of the [system matrix](@entry_id:172230) $A$, which in turn are inherited from the underlying physical problem and the discretization method.

#### The Role of Diagonal Dominance

A sufficient (but not necessary) condition for the convergence of both Jacobi and Gauss-Seidel methods is that the matrix $A$ be **strictly [diagonally dominant](@entry_id:748380)**. A matrix is strictly [diagonally dominant](@entry_id:748380) by rows if for every row $i$, the magnitude of the diagonal element is greater than the sum of the magnitudes of the off-diagonal elements in that row:

$|a_{ii}| > \sum_{j \ne i} |a_{ij}|$

Discretizations of elliptic PDEs, such as the steady heat equation, often lead to matrices with this property. However, it is important to be precise. Consider the 1D conduction equation with variable conductivity, $-(k(x)u'(x))' = f(x)$. A standard second-order finite difference/volume discretization on interior nodes yields matrix entries $a_{i,i} = k_{i-1/2} + k_{i+1/2}$, $a_{i,i-1} = -k_{i-1/2}$, and $a_{i,i+1} = -k_{i+1/2}$. For these interior rows, the diagonal dominance margin is exactly zero: $|a_{i,i}| = |a_{i,i-1}| + |a_{i,i+1}|$. Such rows are only **weakly [diagonally dominant](@entry_id:748380)**. Strict [diagonal dominance](@entry_id:143614) is often only achieved in rows corresponding to nodes adjacent to a Dirichlet boundary, where a boundary term is moved to the right-hand side, effectively removing an off-diagonal entry from the sum .

A powerful tool for visualizing and bounding the eigenvalues of a matrix is the **Gershgorin Circle Theorem**. It states that every eigenvalue of a matrix $A$ lies within at least one of the Gershgorin discs $\mathcal{D}_i$ in the complex plane, where each disc is centered at a diagonal entry $a_{ii}$ and has a radius $R_i = \sum_{j \ne i} |a_{ij}|$. For a discrete Laplacian matrix from a 2D problem, the diagonal entries are 4 and off-diagonal entries are -1. For an interior node with four neighbors, the radius is $R_i = 4$, so the Gershgorin disc is a real interval $[4-4, 4+4] = [0, 8]$. For a corner node with two neighbors, the radius is $R_i=2$, yielding the interval $[2, 6]$. The union of all such discs, $[0, 8]$, provides an upper bound on the largest eigenvalue of the matrix . The fact that the interval for interior nodes touches zero reflects their weak [diagonal dominance](@entry_id:143614).

#### Comparison of Jacobi and Gauss-Seidel

For the class of matrices arising from the discretization of elliptic PDEs (which are often **M-matrices**—having positive diagonals, non-positive off-diagonals, and being non-singular), there is a rigorous theoretical comparison between Jacobi and Gauss-Seidel. The **Stein-Rosenberg Theorem** states that for such problems, if the methods converge, then Gauss-Seidel converges asymptotically faster than Jacobi. Specifically, $0 \le \rho(B_{GS})  \rho(B_J)  1$ .

A more quantitative relationship exists for matrices that are **consistently ordered**, a property held by matrices from standard [finite difference schemes](@entry_id:749380) on rectangular grids with natural node ordering. For such matrices, the spectral radii are related by:

$\rho(B_{GS}) = [\rho(B_J)]^2$

This remarkable result allows for a precise comparison. For the 2D Poisson equation on an $n \times n$ grid, the Jacobi spectral radius can be shown to be $\rho(B_J) = \cos(\frac{\pi}{n+1})$. Consequently, $\rho(B_{GS}) = \cos^2(\frac{\pi}{n+1})$. For fine meshes where $n$ is large, we can use a Taylor expansion $\cos(x) \approx 1 - x^2/2$ to find the [asymptotic behavior](@entry_id:160836) :

$\rho(B_J) \approx 1 - \frac{\pi^2}{2(n+1)^2}$

$\rho(B_{GS}) \approx 1 - \frac{\pi^2}{(n+1)^2}$

Since the [rate of convergence](@entry_id:146534) is proportional to $-\ln(\rho)$, this implies that for fine grids, the asymptotic convergence rate of Gauss-Seidel is approximately twice that of Jacobi. This means Gauss-Seidel requires roughly half the number of iterations to achieve a similar error reduction.

### Practical Implementation and Advanced Concepts

#### Monitoring Convergence: Error versus Residual

In practice, we must decide when to stop the iteration. The true measure of convergence is the **error**, $e^k = x^k - x^*$, but the exact solution $x^*$ is unknown. Therefore, we monitor the **residual**, $r^k = b - A x^k$, which is computable. The two are fundamentally linked by the relation :

$r^k = b - A x^k = A x^* - A x^k = -A(x^k - x^*) = -A e^k$

This implies $e^k = -A^{-1} r^k$. Taking norms, we can bound the error norm using the [residual norm](@entry_id:136782):

$\lVert e^k \rVert \le \lVert A^{-1} \rVert \lVert r^k \rVert$

This shows that a small residual implies a small error, but the relationship is mediated by $\lVert A^{-1} \rVert$. This is a critical insight: if the matrix $A$ is ill-conditioned (i.e., its condition number $\kappa(A) = \lVert A \rVert \lVert A^{-1} \rVert$ is large), a significant reduction in the residual may still correspond to a small or even no reduction in the error.

#### Limitations and the Role of Preconditioning

Classical point-wise methods have limitations. One significant issue arises in systems with zero entries on the diagonal. For example, augmented systems arising from [mixed formulations](@entry_id:167436) or the use of Lagrange multipliers, such as in certain constrained thermal problems, can lead to a matrix $K$ with zero diagonal entries. In such a case, the matrix $D$ is singular, and the Jacobi method is not even defined .

This highlights the need for more sophisticated splittings. The framework $A = M-N$ is, in essence, a preconditioning framework where $M$ is the preconditioner. A robust choice of $M$ can handle cases where simple methods fail. For the [saddle-point problem](@entry_id:178398) with a zero diagonal, a **block Gauss-Seidel** splitting can be effective. For example, considering a block matrix $K = \begin{pmatrix} A  C \\ C^T  0 \end{pmatrix}$, a lower-triangular block preconditioner $M = \begin{pmatrix} A  0 \\ C^T  -S \end{pmatrix}$ can be constructed. If $S$ is chosen as the exact **Schur complement**, $S = C^T A^{-1} C$, the resulting [iteration matrix](@entry_id:637346) can be shown to be nilpotent (e.g., $B^2=0$), meaning the method converges to the exact solution in a fixed, small number of iterations . This demonstrates the power of advanced [preconditioning](@entry_id:141204) and serves as a conceptual bridge from simple stationary methods to more powerful techniques like preconditioned Krylov subspace methods, which are the subject of subsequent chapters.