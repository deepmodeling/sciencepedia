## Introduction
Large systems of linear equations of the form $A \mathbf{x} = \mathbf{b}$ are a cornerstone of computational modeling, appearing in fields from engineering and physics to economics and data science. While direct solvers like Gaussian elimination can provide an exact solution, their computational cost and memory usage become prohibitive for the vast, sparse systems that often arise from real-world problems. The phenomenon of "fill-in," where the solution process destroys sparsity, makes direct methods impractical for many large-scale applications.

This article explores a powerful alternative: stationary iterative methods. Instead of calculating the solution in a single, complex operation, these algorithms start with an initial guess and generate a sequence of progressively better approximations that converge to the true solution. This approach is not only more efficient for sparse matrices but also forms the foundation for some of the most advanced numerical techniques in use today.

Across the following chapters, you will gain a thorough understanding of these fundamental algorithms. The **"Principles and Mechanisms"** chapter will deconstruct how methods like Jacobi, Gauss-Seidel, and SOR are derived from matrix splittings and establish the mathematical principles governing their convergence. In **"Applications and Interdisciplinary Connections,"** we will see these methods in action, solving problems ranging from the simulation of physical fields to the analysis of economic and social networks. Finally, the **"Hands-On Practices"** chapter will provide an opportunity to implement and compare these methods, solidifying your understanding through practical experience.

## Principles and Mechanisms

In the preceding chapter, we introduced the challenge of solving large systems of linear equations, $A \mathbf{x} = \mathbf{b}$, which are ubiquitous in computational science and engineering. While direct methods like Gaussian elimination provide an exact solution in a finite number of steps, their computational cost, often scaling as $\mathcal{O}(n^3)$, and significant memory requirements can render them impractical for the vast, sparse systems that arise from discretizing partial differential equations or modeling large networks. A particularly severe issue with direct methods on sparse matrices is **fill-in**, where the process of elimination introduces new nonzero entries into the matrix factors, destroying the very sparsity that makes the problem tractable and leading to catastrophic increases in memory and computational time [@problem_id:2396408].

Iterative methods offer a powerful alternative. Instead of seeking an exact solution in one go, they begin with an initial guess and progressively refine it, ideally converging toward the true solution. This chapter focuses on the simplest and most foundational class of these algorithms: **stationary iterative methods**.

### The Fixed-Point Iteration Framework

The core idea behind stationary iterative methods is to rearrange the original equation $A \mathbf{x} = \mathbf{b}$ into an equivalent **fixed-point equation** of the form:
$$
\mathbf{x} = G \mathbf{x} + \mathbf{c}
$$
where $G$ is an $n \times n$ matrix and $\mathbf{c}$ is an $n \times 1$ vector. A solution to the original system is now a "fixed point" of the function $f(\mathbf{x}) = G \mathbf{x} + \mathbf{c}$, meaning a vector $\mathbf{x}^\ast$ such that $\mathbf{x}^\ast = G \mathbf{x}^\ast + \mathbf{c}$.

This formulation naturally suggests an iterative procedure. Starting with an initial guess $\mathbf{x}^{(0)}$, we can generate a sequence of approximations using the recurrence relation:
$$
\mathbf{x}^{(k+1)} = G \mathbf{x}^{(k)} + \mathbf{c}
$$
where $k=0, 1, 2, \dots$ is the iteration index.

This method is called **stationary** because the iteration matrix $G$ and the constant vector $\mathbf{c}$ are fixed throughout the process; they do not change from one iteration to the next. This stands in contrast to non-stationary methods, such as the Conjugate Gradient method, where the update parameters and search directions are recalculated at every step based on the current state of the iteration [@problem_id:2160060].

A key advantage of this iterative approach, particularly in contexts like econometric modeling or transient simulations, is the ability to use **warm starts**. When solving a sequence of slightly perturbed systems, the solution from the previous step serves as an excellent initial guess for the current one, often drastically reducing the number of iterations needed for convergence [@problem_id:2396408].

### Deriving Classical Stationary Methods from Matrix Splitting

The transformation of $A\mathbf{x} = \mathbf{b}$ into a fixed-point form is systematically achieved through a **matrix splitting**. We express the matrix $A$ as a difference of two matrices, $A = M - N$, where $M$ is chosen to be easily invertible.

Substituting this splitting into the original system gives:
$$
(M - N)\mathbf{x} = \mathbf{b}
$$
$$
M\mathbf{x} = N\mathbf{x} + \mathbf{b}
$$
Since $M$ is invertible, we can write:
$$
\mathbf{x} = M^{-1}N\mathbf{x} + M^{-1}\mathbf{b}
$$
This is now in the desired fixed-point form, immediately identifying the iteration matrix $G = M^{-1}N$ and the constant vector $\mathbf{c} = M^{-1}\mathbf{b}$. The corresponding iterative method is $\mathbf{x}^{(k+1)} = M^{-1}N\mathbf{x}^{(k)} + M^{-1}\mathbf{b}$.

The classical stationary methods—Jacobi, Gauss-Seidel, and Successive Over-Relaxation (SOR)—arise from different choices of the splitting $M$ and $N$, based on the canonical decomposition of the matrix $A$ into its diagonal, strictly lower-triangular, and strictly upper-triangular parts [@problem_id:2596855]. Let us define $D$ as the diagonal of $A$, $-L$ as the strictly lower-triangular part of $A$, and $-U$ as the strictly upper-triangular part of $A$. With this notation, the decomposition is written as:
$$
A = D - L - U
$$

#### The Jacobi Method

The Jacobi method employs the simplest possible splitting by choosing $M$ to be the diagonal part of $A$. This is feasible as long as all diagonal entries of $A$ are non-zero.
- **Splitting**: $M_J = D$ and $N_J = L+U$.
- **Iteration**: The update rule $D\mathbf{x}^{(k+1)} = (L+U)\mathbf{x}^{(k)} + \mathbf{b}$ leads to the standard Jacobi form $\mathbf{x}^{(k+1)} = T_J \mathbf{x}^{(k)} + \mathbf{c}_J$, where:
  - **Jacobi Iteration Matrix**: $T_J = D^{-1}(L+U) = I - D^{-1}A$
  - **Constant Vector**: $\mathbf{c}_J = D^{-1}\mathbf{b}$ [@problem_id:2216366]

A key feature of the Jacobi method is that the computation of each component $x_i^{(k+1)}$ depends only on the components of the previous vector $\mathbf{x}^{(k)}$. This means all components of the new vector can be computed simultaneously. This property, known as a method of **simultaneous displacements**, makes the Jacobi method "embarrassingly parallel" and highly scalable on modern distributed-memory architectures, as communication is typically limited to exchanging data between processors holding adjacent parts of the vector [@problem_id:2396408].

#### The Gauss-Seidel Method

The Gauss-Seidel method aims to accelerate convergence by using the most up-to-date information available. When computing the $i$-th component of the new vector, $x_i^{(k+1)}$, it uses the already computed new values $x_j^{(k+1)}$ for $j  i$. This is a method of **successive displacements**.
- **Splitting**: The splitting matrix $M$ is chosen to be the lower-triangular part of $A$, including the diagonal: $M_{GS} = D-L$ and $N_{GS} = U$.
- **Iteration**: The update rule $(D-L)\mathbf{x}^{(k+1)} = U\mathbf{x}^{(k)} + \mathbf{b}$ defines the Gauss-Seidel iteration, with:
  - **Gauss-Seidel Iteration Matrix**: $T_{GS} = (D-L)^{-1}U$
  - **Constant Vector**: $\mathbf{c}_{GS} = (D-L)^{-1}\mathbf{b}$ [@problem_id:2596855]

The sequential nature of the Gauss-Seidel update—where the computation for row $i$ depends on the result from row $i-1$—makes it less amenable to parallelization than the Jacobi method.

#### The Successive Over-Relaxation (SOR) Method

The SOR method is an extrapolation of the Gauss-Seidel method, introducing a **relaxation parameter** $\omega > 0$ to potentially accelerate convergence. The SOR update is a weighted average of the previous iterate and the Gauss-Seidel update.
- **Splitting**: The splitting is $M_{SOR} = \frac{1}{\omega}(D - \omega L)$ and $N_{SOR} = \frac{1}{\omega}((1-\omega)D + \omega U)$.
- **Iteration**: This splitting leads to the iteration matrix:
  - **SOR Iteration Matrix**: $T_{SOR}(\omega) = (D - \omega L)^{-1}((1-\omega)D + \omega U)$

Note that for $\omega=1$, SOR reduces to the Gauss-Seidel method. For $0  \omega  1$, the method is technically "under-relaxation," while for $\omega > 1$, it is "over-relaxation."

### The Principle of Convergence

For an iterative method to be useful, the sequence of approximations $\mathbf{x}^{(k)}$ must converge to the true solution $\mathbf{x}^\ast$. To understand when this happens, we analyze the evolution of the error vector, $\mathbf{e}^{(k)} = \mathbf{x}^{(k)} - \mathbf{x}^\ast$.

Since $\mathbf{x}^{(k+1)} = G \mathbf{x}^{(k)} + \mathbf{c}$ and the true solution satisfies $\mathbf{x}^\ast = G \mathbf{x}^\ast + \mathbf{c}$, subtracting these equations gives the error propagation formula:
$$
\mathbf{e}^{(k+1)} = \mathbf{x}^{(k+1)} - \mathbf{x}^\ast = (G \mathbf{x}^{(k)} + \mathbf{c}) - (G \mathbf{x}^\ast + \mathbf{c}) = G(\mathbf{x}^{(k)} - \mathbf{x}^\ast) = G \mathbf{e}^{(k)}
$$
By recursion, the error at step $k$ is related to the initial error $\mathbf{e}^{(0)}$ by $\mathbf{e}^{(k)} = G^k \mathbf{e}^{(0)}$. The iteration converges to the unique solution for any initial guess $\mathbf{x}^{(0)}$ if and only if the error vanishes as $k \to \infty$ for any initial error $\mathbf{e}^{(0)}$. This requires the matrix powers $G^k$ to approach the zero matrix.

A fundamental theorem of linear algebra states that $\lim_{k \to \infty} G^k = 0$ if and only if the **spectral radius** of $G$, denoted $\rho(G)$, is strictly less than 1. The spectral radius is defined as the maximum absolute value (or modulus, for complex eigenvalues) of the eigenvalues of $G$:
$$
\rho(G) = \max_{i} |\lambda_i(G)|
$$
Thus, the necessary and sufficient condition for the convergence of a stationary iterative method is:
$$
\rho(G)  1
$$
The smaller the spectral radius, the faster the asymptotic rate of convergence.

To make this concrete, consider the Jacobi method for a general $2 \times 2$ system $A = \begin{pmatrix} a_{11}  a_{12} \\ a_{21}  a_{22} \end{pmatrix}$. The iteration matrix is $T_J = \begin{pmatrix} 0  -a_{12}/a_{11} \\ -a_{21}/a_{22}  0 \end{pmatrix}$. Its eigenvalues $\lambda$ are found from the characteristic equation $\lambda^2 - \frac{a_{12}a_{21}}{a_{11}a_{22}} = 0$. The spectral radius is $\rho(T_J) = \sqrt{\left|\frac{a_{12}a_{21}}{a_{11}a_{22}}\right|}$. The convergence condition $\rho(T_J)  1$ is therefore equivalent to $\left|\frac{a_{12}a_{21}}{a_{11}a_{22}}\right|  1$ [@problem_id:2163209].

This condition has a profound implication: if an iterative method converges (i.e., $\rho(G)  1$), the matrix $I-G$ is invertible. Since $T_J = I - D^{-1}A$, the matrix $I - T_J = D^{-1}A$ must be invertible. As $D$ is invertible, this implies that the original matrix $A$ must also be invertible (non-singular) [@problem_id:2442128]. The contrapositive is also true: if $A$ is singular, then $1$ must be an eigenvalue of $T_J$, which implies $\rho(T_J) \ge 1$, and the Jacobi method cannot be guaranteed to converge to a unique solution [@problem_id:2442128]. For singular but consistent systems, the iterates may enter a cycle or converge to one of many possible solutions, depending on the initial guess [@problem_id:2442112, @problem_id:2442128].

For the SOR method, it can be proven that a necessary condition for convergence is $0  \omega  2$. For $\omega \ge 2$, the spectral radius of the SOR iteration matrix for any matrix $A$ with non-zero diagonal entries satisfies $\rho(T_{SOR}(\omega)) \ge |\omega-1| \ge 1$. Thus, for $\omega > 2$, the method is guaranteed to diverge, and for $\omega = 2$, it is marginal and generally does not converge [@problem_id:2442123].

### Sufficient Conditions for Convergence

While the spectral radius provides a definitive test for convergence, computing eigenvalues for large matrices is itself a difficult problem. Therefore, it is useful to have simpler, sufficient conditions that guarantee convergence based on the properties of the matrix $A$ itself.

#### Strict Diagonal Dominance

One of the most well-known sufficient conditions is **strict diagonal dominance (SDD)**. A matrix $A$ is strictly diagonally dominant if, for every row, the absolute value of the diagonal element is strictly greater than the sum of the absolute values of all other elements in that row:
$$
|A_{ii}| > \sum_{j \neq i} |A_{ij}| \quad \text{for all } i
$$
The **Gershgorin Circle Theorem** states that every eigenvalue of a matrix lies within at least one of the "Gershgorin discs" in the complex plane, where the $i$-th disc is centered at $A_{ii}$ with a radius equal to the sum of the absolute values of the off-diagonal entries in that row.

If $A$ is SDD, we can use this theorem to prove that the Jacobi method converges. The radius of the $i$-th Gershgorin disc for the Jacobi matrix $T_J = D^{-1}(L+U)$ is $R_i = \sum_{j \neq i} |(T_J)_{ij}| = \frac{1}{|A_{ii}|} \sum_{j \neq i} |A_{ij}|$. The SDD condition on $A$ directly implies that $R_i  1$ for all $i$. Since all diagonal entries of $T_J$ are zero, all its Gershgorin discs are centered at the origin with radii less than 1. Therefore, all eigenvalues of $T_J$ must have a magnitude less than 1, proving that $\rho(T_J)  1$ [@problem_id:2384240]. It can be similarly shown that SDD also guarantees convergence for the Gauss-Seidel method.

This condition has a clear physical interpretation in many applications. In the finite element analysis of elastic structures, for instance, the stiffness matrix $K$ being SDD means that the local "self-stiffness" at each degree of freedom ($K_{ii}$) is greater than the sum of all coupling stiffnesses to other degrees of freedom ($\sum_{j \neq i} |K_{ij}|$). This describes a system where inter-node connections are comparatively weak, ensuring stability for iterative solvers [@problem_id:2384240]. A similar principle applies to systems with complex coefficients, such as those from AC circuit analysis, where SDD of the nodal admittance matrix guarantees convergence [@problem_id:2442073].

It is critical to remember that strict diagonal dominance is a *sufficient*, but not *necessary*, condition. Many systems that are not SDD still converge. For example, it is possible to construct matrices where the Jacobi or Gauss-Seidel methods converge even when the diagonal dominance condition is violated [@problem_id:2442152, @problem_id:2442074].

#### Symmetric Positive Definite Matrices

Another important class of matrices are **symmetric positive definite (SPD)** matrices. For these matrices, it is a theorem that the Gauss-Seidel method always converges. Furthermore, the SOR method is guaranteed to converge for any relaxation parameter $\omega$ in the range $(0, 2)$. The Jacobi method, however, is not guaranteed to converge for all SPD matrices, although it does for the important subclass arising from the discretization of elliptic PDEs like the Poisson equation.

### The Dynamics of Error Reduction

Understanding convergence requires more than a simple yes/no answer. We must also consider how the error behaves during the iteration, including its rate of decay and its structure.

#### Asymptotic vs. Transient Behavior

The spectral radius $\rho(G)$ dictates the **asymptotic rate of convergence**. For large $k$, the error is typically reduced by a factor of approximately $\rho(G)$ at each step. However, the short-term, or **transient**, behavior can be different.

If the iteration matrix $G$ is **normal** (meaning it commutes with its conjugate transpose, $G G^H = G^H G$), then the norm of the error decreases monotonically, as $\|G^k\|_2 = \rho(G)^k$. However, for a general **non-normal** matrix, the norm of its powers, $\|G^k\|_2$, can be much larger than $\rho(G)^k$ for small $k$. This can lead to a period of transient error growth before the asymptotic decay eventually takes over. This behavior is bounded by the inequality:
$$
\|\mathbf{e}^{(k)}\|_2 \le \kappa_2(X)\rho(G)^k \|\mathbf{e}^{(0)}\|_2
$$
where $G = X\Lambda X^{-1}$ is the eigendecomposition of $G$, and $\kappa_2(X) = \|X\|_2 \|X^{-1}\|_2$ is the condition number of the eigenvector matrix $X$. A large $\kappa_2(X)$, indicative of a poorly conditioned (nearly parallel) set of eigenvectors, can permit significant transient error growth even when $\rho(G)$ is small [@problem_id:2428535].

#### Frequency-Dependent Damping and Smoothing

A powerful way to analyze the dynamics of error reduction is to decompose the error vector into the eigenbasis of the iteration matrix. For many problems, such as the 1D Poisson equation discretized with finite differences, the eigenvectors are discrete sine waves of different frequencies. For the Jacobi method applied to this problem, the eigenvectors of $A$ are also eigenvectors of the Jacobi matrix $T_J$. The corresponding eigenvalue (amplification factor) for the $k$-th sine mode is $\mu_k = \cos(\frac{k\pi}{n+1})$ [@problem_id:2442105, @problem_id:2442132].

This has a critical consequence:
- **High-frequency error components** (corresponding to mid-range $k$, where $\frac{k\pi}{n+1}$ is near $\pi/2$) have small amplification factors $|\mu_k|$. These error components are damped very quickly. For $k = (n+1)/2$, $\mu_k=0$, and that error mode is eliminated in a single step [@problem_id:2442105].
- **Low-frequency error components** (corresponding to small $k$, where $\frac{k\pi}{n+1}$ is near $0$) have amplification factors $|\mu_k|$ close to 1. These smooth error components are damped very slowly.

The spectral radius is determined by the most persistent (slowest-decaying) mode, which is the lowest frequency mode: $\rho(T_J) = |\mu_1| = \cos(\frac{\pi}{n+1})$ [@problem_id:2442105]. This property of rapidly reducing high-frequency error while leaving low-frequency error largely untouched is known as **smoothing**, and it is the foundational principle behind the remarkable efficiency of multigrid methods.

#### The Role of Matrix Ordering

The structure of the $L$ and $U$ matrices depends on the order in which the unknowns are numbered. A reordering of the unknowns corresponds to a permutation similarity transform on the system matrix: $A' = PAP^T$, where $P$ is a permutation matrix.
- For the **Jacobi method**, the new iteration matrix is $T'_J = P T_J P^T$. Since $T'_J$ is similar to $T_J$, they share the same eigenvalues. Thus, the spectral radius and asymptotic convergence rate of the Jacobi method are **invariant** to the ordering of the unknowns [@problem_id:2442116].
- For the **Gauss-Seidel method**, the reordering fundamentally changes which matrix entries fall into the lower and upper triangles. The new iteration matrix $T'_{GS}$ is, in general, **not similar** to the original $T_{GS}$. Consequently, their spectral radii can differ, and the convergence rate of Gauss-Seidel is **dependent on the ordering** of unknowns [@problem_id:2442116]. This opens the possibility of accelerating Gauss-Seidel by choosing an optimal ordering (e.g., red-black ordering for the Poisson problem).

### Extensions and Further Concepts

#### Block Iterative Methods

For systems with a natural block structure, such as those arising from coupled physics problems, it can be advantageous to iterate on blocks of variables at a time. The definitions of Jacobi and Gauss-Seidel can be extended to this **block** setting, where the splitting $A=D_B - L_B - U_B$ is based on block-diagonal, strictly block-lower, and strictly block-upper matrices. In the block Jacobi method, one solves systems involving the block-diagonal matrices at each step. For certain classes of matrices, such as the **consistently ordered** matrices that often arise in discretizations, there is a direct relationship between the spectral radii of the block methods. For example, for a consistently ordered block-tridiagonal matrix, the spectral radii are related by $\rho(T_{GS}) = [\rho(T_J)]^2$, implying that block Gauss-Seidel converges asymptotically twice as fast as block Jacobi [@problem_id:2442115].

#### Preconditioning

The methods discussed so far can be viewed as specific instances of a more general concept: **preconditioning**. Instead of solving $A\mathbf{x} = \mathbf{b}$, we solve an equivalent preconditioned system, such as:
$$
P^{-1}A\mathbf{x} = P^{-1}\mathbf{b}
$$
where $P$ is an invertible matrix called a **preconditioner**. The goal is to choose a $P$ such that the new system matrix, $P^{-1}A$, is "easier" to solve iteratively. For the stationary scheme $\mathbf{x}^{(k+1)} = (I - P^{-1}A) \mathbf{x}^{(k)} + P^{-1}\mathbf{b}$, the iteration matrix is $G = I - P^{-1}A$.

The ideal preconditioner would make the spectral radius $\rho(I - P^{-1}A)$ as close to zero as possible. This is achieved if the preconditioned matrix $P^{-1}A$ is a close approximation of the identity matrix $I$. This, in turn, implies that the fundamental goal of preconditioning is to find a matrix $P$ that is a good approximation of $A$ (so $P \approx A$) but is also cheap to invert (i.e., solving systems $P\mathbf{y}=\mathbf{r}$ is fast) [@problem_id:2194412]. The Jacobi method itself can be seen as using a very simple preconditioner, $P=D$, the diagonal of $A$. More advanced preconditioners, such as those from incomplete LU factorizations (ILU), provide a better approximation to $A$ and can lead to dramatically faster convergence.