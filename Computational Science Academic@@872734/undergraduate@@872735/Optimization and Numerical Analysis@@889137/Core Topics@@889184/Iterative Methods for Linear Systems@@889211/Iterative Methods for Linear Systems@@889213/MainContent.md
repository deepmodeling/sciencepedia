## Introduction
Solving [systems of linear equations](@entry_id:148943) of the form $A\mathbf{x} = \mathbf{b}$ is a fundamental problem in computational mathematics. While direct methods like Gaussian elimination are effective for small systems, they become computationally expensive and memory-intensive for the massive, sparse systems that arise in modern science and engineering. This challenge necessitates a different approach: [iterative methods](@entry_id:139472), which trade a finite number of exact operations for a sequence of approximations that converge toward the true solution.

This article provides a comprehensive introduction to these powerful techniques. The first chapter, **Principles and Mechanisms**, will lay the groundwork by explaining the mechanics of classical stationary methods like Jacobi, Gauss-Seidel, and SOR, and delve into the crucial theory that governs their convergence. The second chapter, **Applications and Interdisciplinary Connections**, will showcase the remarkable utility of these methods in solving real-world problems, from analyzing [electrical circuits](@entry_id:267403) and economic models to simulating physical phenomena governed by [partial differential equations](@entry_id:143134). Finally, the **Hands-On Practices** chapter offers practical exercises to solidify your understanding of these core concepts. We begin our exploration by examining the foundational principles that define iterative solvers and the mechanisms behind the most fundamental techniques.

## Principles and Mechanisms

In the study of numerical linear algebra, solving the system of equations $A\mathbf{x} = \mathbf{b}$ is a foundational task. While direct methods, such as Gaussian elimination or LU factorization, provide an exact solution in a finite number of steps (barring round-off error), their computational cost can be prohibitive for very large systems. Furthermore, many real-world problems, particularly those arising from the [discretization of partial differential equations](@entry_id:748527), produce matrices that are **sparse**—meaning they are composed mostly of zero entries. Direct methods often destroy this sparsity, leading to excessive memory usage.

This is the primary motivation for **[iterative methods](@entry_id:139472)**. Instead of a fixed sequence of operations, these methods begin with an initial guess, $\mathbf{x}^{(0)}$, and generate a sequence of increasingly accurate approximations, $\mathbf{x}^{(1)}, \mathbf{x}^{(2)}, \dots$, that ideally converge to the true solution $\mathbf{x}$. The application of such methods is widespread, from modeling heat flow in microprocessors [@problem_id:2182368] to solving complex systems in economics and engineering. This chapter will explore the principles and mechanisms of several fundamental iterative techniques.

### Stationary Iterative Methods: A General Framework

The simplest class of iterative solvers are known as **[stationary iterative methods](@entry_id:144014)**. Their defining characteristic is that the computation for generating the next approximation, $\mathbf{x}^{(k+1)}$, from the current one, $\mathbf{x}^{(k)}$, is the same at every step. Most of these methods can be expressed in a universal form:
$$
\mathbf{x}^{(k+1)} = T\mathbf{x}^{(k)} + \mathbf{c}
$$
Here, $T$ is a fixed $n \times n$ matrix called the **iteration matrix**, and $\mathbf{c}$ is a fixed vector. The specific forms of $T$ and $\mathbf{c}$ depend on how the original matrix $A$ is "split" to define the iterative scheme. If the sequence $\{\mathbf{x}^{(k)}\}$ converges to a vector $\mathbf{x}^*$, then this limit vector must be a fixed point of the iteration, satisfying $\mathbf{x}^* = T\mathbf{x}^* + \mathbf{c}$. The central challenge in designing an [iterative method](@entry_id:147741) is to ensure that this fixed point is the desired solution to $A\mathbf{x} = \mathbf{b}$ and that the iteration converges to it.

### The Jacobi Method

The Jacobi method is one of the most straightforward iterative techniques. Its derivation stems from a simple algebraic rearrangement of the original system $A\mathbf{x} = \mathbf{b}$. For each row $i$ of the system, we write out the equation:
$$
\sum_{j=1}^{n} a_{ij} x_{j} = a_{i1}x_1 + a_{i2}x_2 + \dots + a_{ii}x_i + \dots + a_{in}x_n = b_i
$$
Assuming the diagonal entry $a_{ii}$ is non-zero, we can isolate the term $x_i$:
$$
a_{ii}x_i = b_i - \sum_{j \neq i} a_{ij} x_j
$$
$$
x_i = \frac{1}{a_{ii}} \left( b_i - \sum_{j \neq i} a_{ij} x_j \right)
$$
This rearrangement provides an expression for each variable in terms of the others. The Jacobi method turns this set of equations into an iterative rule [@problem_id:2182332]. To compute the new approximation $x_i^{(k+1)}$, we substitute the components of the *previous* approximation, $\mathbf{x}^{(k)}$, into the right-hand side:
$$
x_i^{(k+1)} = \frac{1}{a_{ii}} \left( b_i - \sum_{\substack{j=1 \\ j\neq i}}^{n} a_{ij}x_{j}^{(k)} \right)
$$
This process is performed for all components $i=1, \dots, n$ to complete one iteration. A key feature of the Jacobi method is that all components of $\mathbf{x}^{(k+1)}$ can be computed simultaneously, as each new component $x_i^{(k+1)}$ depends only on the values from the previous vector $\mathbf{x}^{(k)}$.

To illustrate, consider the system [@problem_id:2182306]:
$$
\begin{pmatrix} 5  & -1  & 2 \\ 2  & 8  & -1 \\ -1  & 1  & 4 \end{pmatrix}
\begin{pmatrix} x_1 \\ x_2 \\ x_3 \end{pmatrix}
=
\begin{pmatrix} 12 \\ -16.5 \\ 7 \end{pmatrix}
$$
The Jacobi update rules are:
$$
\begin{align*}
x_{1}^{(k+1)}  &= \frac{1}{5}(12 - (-1)x_{2}^{(k)} - 2x_{3}^{(k)}) \\
x_{2}^{(k+1)}  &= \frac{1}{8}(-16.5 - 2x_{1}^{(k)} - (-1)x_{3}^{(k)}) \\
x_{3}^{(k+1)}  &= \frac{1}{4}(7 - (-1)x_{1}^{(k)} - 1x_{2}^{(k)})
\end{align*}
$$
Starting with an initial guess of $\mathbf{x}^{(0)} = (0, 0, 0)^T$, the first iteration yields:
$$
\mathbf{x}^{(1)} = \left( \frac{12}{5}, -\frac{16.5}{8}, \frac{7}{4} \right)^T = (2.4, -2.0625, 1.75)^T
$$
The second iteration then uses these values to compute $\mathbf{x}^{(2)}$:
$$
x_{2}^{(2)} = \frac{1}{8}(-16.5 - 2x_{1}^{(1)} + x_{3}^{(1)}) = \frac{1}{8}(-16.5 - 2(2.4) + 1.75) = -2.44375
$$
This process is repeated until the difference between successive iterates, $\|\mathbf{x}^{(k+1)} - \mathbf{x}^{(k)}\|$, falls below a specified tolerance.

### The Gauss-Seidel Method

The Jacobi method can be seen as somewhat inefficient because it does not use the most up-to-date information. When computing $x_i^{(k+1)}$, the new values $x_1^{(k+1)}, \dots, x_{i-1}^{(k+1)}$ have already been calculated, yet the Jacobi update rule ignores them. The **Gauss-Seidel method** rectifies this by immediately using the newly computed components within the same iteration [@problem_id:2182322].

Assuming we update the components in their natural order ($i=1, 2, \dots, n$), the update rule becomes:
$$
x_i^{(k+1)} = \frac{1}{a_{ii}} \left( b_i - \sum_{j=1}^{i-1} a_{ij}x_{j}^{(k+1)} - \sum_{j=i+1}^{n} a_{ij}x_{j}^{(k)} \right)
$$
Notice the change in the first summation: for components $j  i$, we use the new values from the current iteration, $k+1$. For components $j  i$, we must still use the old values from iteration $k$. For example, in a $3 \times 3$ system, the update for $x_2^{(k+1)}$ would explicitly be:
$$
x_2^{(k+1)} = \frac{1}{a_{22}} \left( b_2 - a_{21}x_{1}^{(k+1)} - a_{23}x_{3}^{(k)} \right)
$$
This sequential dependency means that Gauss-Seidel cannot be parallelized as easily as Jacobi, but this use of newer information often leads to a faster rate of convergence.

### Successive Over-Relaxation (SOR)

The Successive Over-Relaxation (SOR) method can be viewed as an extrapolation of the Gauss-Seidel method. At each step, we first compute the Gauss-Seidel update, let's call it $x_{i, \text{GS}}^{(k+1)}$, and then we "push" the new value beyond this point. The SOR update is a weighted average of the previous value $x_i^{(k)}$ and the Gauss-Seidel update [@problem_id:2182358]:
$$
x_i^{(k+1)} = (1-\omega) x_i^{(k)} + \omega x_{i, \text{GS}}^{(k+1)}
$$
Substituting the expression for $x_{i, \text{GS}}^{(k+1)}$ gives the full SOR formula:
$$
x_i^{(k+1)} = (1-\omega) x_i^{(k)} + \frac{\omega}{a_{ii}} \left( b_i - \sum_{j=1}^{i-1} a_{ij}x_j^{(k+1)} - \sum_{j=i+1}^{n} a_{ij}x_j^{(k)} \right)
$$
The **[relaxation parameter](@entry_id:139937)**, $\omega$, controls the nature of the [extrapolation](@entry_id:175955).
- If $\omega = 1$, the SOR method reduces exactly to the Gauss-Seidel method.
- If $0 \lt \omega \lt 1$, the method is termed "[under-relaxation](@entry_id:756302)," taking a more conservative step than Gauss-Seidel.
- If $1 \lt \omega \lt 2$, the method is termed "over-relaxation." This is the most common use case, as a carefully chosen $\omega  1$ can dramatically accelerate convergence for certain classes of problems.

### The Theory of Convergence

A critical question for any [iterative method](@entry_id:147741) is: will it converge? And if so, how fast? The answer lies in analyzing the behavior of the iteration matrix $T$.

#### The Spectral Radius Condition

Let $\mathbf{x}$ be the true solution, so $A\mathbf{x} = \mathbf{b}$. Since $\mathbf{x}$ is also a fixed point of the iteration, we have $\mathbf{x} = T\mathbf{x} + \mathbf{c}$. Now, let's define the error at iteration $k$ as $\mathbf{e}^{(k)} = \mathbf{x} - \mathbf{x}^{(k)}$. We can find a relationship for how the error propagates from one step to the next [@problem_id:1369779]:
$$
\mathbf{e}^{(k+1)} = \mathbf{x} - \mathbf{x}^{(k+1)} = (T\mathbf{x} + \mathbf{c}) - (T\mathbf{x}^{(k)} + \mathbf{c}) = T(\mathbf{x} - \mathbf{x}^{(k)}) = T\mathbf{e}^{(k)}
$$
By applying this relationship recursively, we find that the error at step $k$ is related to the initial error $\mathbf{e}^{(0)}$ by $\mathbf{e}^{(k)} = T^k \mathbf{e}^{(0)}$. For the method to converge for *any* initial guess $\mathbf{x}^{(0)}$ (and thus any initial error $\mathbf{e}^{(0)}$), the error $\mathbf{e}^{(k)}$ must go to zero as $k \to \infty$. This occurs if and only if the matrix $T^k$ approaches the [zero matrix](@entry_id:155836).

A [fundamental theorem of linear algebra](@entry_id:190797) states that $\lim_{k \to \infty} T^k = 0$ if and only if the **[spectral radius](@entry_id:138984)** of $T$, denoted $\rho(T)$, is less than 1. The spectral radius is defined as the maximum absolute value of the eigenvalues of $T$. Thus, the necessary and sufficient condition for a stationary [iterative method](@entry_id:147741) to converge for any initial guess is:
$$
\rho(T)  1
$$
For example, if the Gauss-Seidel [iteration matrix](@entry_id:637346) for a system has a [spectral radius](@entry_id:138984) of $\rho(T_G) = \cos(\pi/8)$, the method is guaranteed to converge because $0  \cos(\pi/8)  1$. However, if $\rho(T_G) = \ln(3) \approx 1.099$, convergence is not guaranteed and the method will likely diverge [@problem_id:1369793].

#### Sufficient Conditions for Convergence

Calculating the eigenvalues of the [iteration matrix](@entry_id:637346) $T$ can be computationally expensive. Fortunately, we can often guarantee convergence by checking simpler properties of the original matrix $A$.

A matrix $A$ is **strictly diagonally dominant** if, for every row, the absolute value of the diagonal element is greater than the sum of the absolute values of all other elements in that row.
$$
|a_{ii}|  \sum_{j \neq i} |a_{ij}| \quad \text{for all } i=1, \dots, n
$$
The Levy–Desplanques theorem states that if a matrix is strictly diagonally dominant, it is invertible. More importantly for our purposes, if $A$ is strictly diagonally dominant, then the Jacobi method is guaranteed to converge. This can be shown by proving that the [infinity-norm](@entry_id:637586) of the Jacobi [iteration matrix](@entry_id:637346) is less than 1. Consider the matrix from a previous example [@problem_id:2182352]:
$$
A = \begin{pmatrix} 10   -3   5 \\ 4   -8   -2.5 \\ 6   -5   12 \end{pmatrix}
$$
- Row 1: $|10| = 10  |-3| + |5| = 8$
- Row 2: $|-8| = 8  |4| + |-2.5| = 6.5$
- Row 3: $|12| = 12  |6| + |-5| = 11$
Since the condition holds for all rows, the matrix is strictly diagonally dominant, and the Jacobi method is guaranteed to converge for this system.

Another important class of matrices are **[symmetric positive definite](@entry_id:139466) (SPD)** matrices. A matrix $A$ is symmetric if $A = A^T$. A [symmetric matrix](@entry_id:143130) $A$ is positive definite if $\mathbf{x}^T A \mathbf{x}  0$ for all non-zero vectors $\mathbf{x}$. It can be proven that if $A$ is SPD, the Gauss-Seidel method (and the SOR method for $0  \omega  2$) is guaranteed to converge. A practical way to check for the SPD property is **Sylvester's criterion**: a [symmetric matrix](@entry_id:143130) is [positive definite](@entry_id:149459) if and only if all its [leading principal minors](@entry_id:154227) (determinants of the top-left $1\times1, 2\times2, \dots, n\times n$ sub-matrices) are positive. For a $2 \times 2$ matrix with a parameter $\alpha$ [@problem_id:2182341],
$$
A = \begin{pmatrix} 2   \alpha \\ \alpha   8 \end{pmatrix}
$$
the matrix is symmetric for any real $\alpha$. The [leading principal minors](@entry_id:154227) are $\Delta_1 = 2$ and $\Delta_2 = \det(A) = 16 - \alpha^2$. For $A$ to be SPD, we need $\Delta_1  0$ (which is true) and $\Delta_2  0$. The condition $16 - \alpha^2  0$ implies $\alpha^2  16$, or $-4  \alpha  4$. For any $\alpha$ in this range, Gauss-Seidel convergence is assured.

### Beyond Stationary Methods: Krylov Subspace Methods

While stationary methods are simple to implement, their convergence can be slow. A more powerful and modern class of techniques are **Krylov subspace methods**. These methods are not stationary; the computations at each step evolve.

Given a matrix $A$ and an initial [residual vector](@entry_id:165091) $\mathbf{r}_0 = \mathbf{b} - A\mathbf{x}_0$, the associated **Krylov subspace** of dimension $m$ is the linear span of the vectors formed by repeatedly applying $A$ to $\mathbf{r}_0$:
$$
\mathcal{K}_m(A, \mathbf{r}_0) = \text{span}\{\mathbf{r}_0, A\mathbf{r}_0, A^2\mathbf{r}_0, \dots, A^{m-1}\mathbf{r}_0\}
$$
Krylov methods work by finding an optimal approximate solution $\mathbf{x}_m$ within the affine space $\mathbf{x}_0 + \mathcal{K}_m(A, \mathbf{r}_0)$. The definition of "optimal" distinguishes different methods.

The **Conjugate Gradient (CG)** method, for instance, is the premier method for SPD systems. It generates a sequence of search directions that are mutually conjugate with respect to $A$, guaranteeing convergence in at most $n$ steps in exact arithmetic.

For general non-symmetric systems where CG is not applicable, the **Generalized Minimal Residual (GMRES)** method is a popular choice. The principle of GMRES is elegantly simple: at each step $m$, it finds the vector $\mathbf{x}_m \in \mathbf{x}_0 + \mathcal{K}_m(A, \mathbf{r}_0)$ that minimizes the Euclidean norm of the residual, $\|\mathbf{b} - A\mathbf{x}_m\|_2$.

The practical implementation of GMRES relies on the **Arnoldi iteration**, a procedure that generates an orthonormal basis $\{ \mathbf{q}_1, \mathbf{q}_2, \dots, \mathbf{q}_m \}$ for the Krylov subspace $\mathcal{K}_m(A, \mathbf{r}_0)$. The process works as follows [@problem_id:2182305]:
1.  Start with $\mathbf{q}_1 = \mathbf{r}_0 / \|\mathbf{r}_0\|_2$.
2.  For $j=1, 2, \dots, m$:
    a. Compute $\mathbf{w} = A\mathbf{q}_j$.
    b. Orthogonalize $\mathbf{w}$ against all previous basis vectors: $\hat{\mathbf{w}} = \mathbf{w} - \sum_{i=1}^j h_{ij}\mathbf{q}_i$, where $h_{ij} = \mathbf{q}_i^T \mathbf{w}$.
    c. The norm of the resulting vector gives the next coefficient in a Hessenberg matrix: $h_{j+1, j} = \|\hat{\mathbf{w}}\|_2$.
    d. The next [basis vector](@entry_id:199546) is $\mathbf{q}_{j+1} = \hat{\mathbf{w}} / h_{j+1, j}$.

The GMRES algorithm uses the basis vectors $\mathbf{q}_i$ and the coefficients $h_{ij}$ generated by this process to efficiently solve the [residual minimization](@entry_id:754272) problem at each step. These advanced methods form the backbone of modern [large-scale scientific computing](@entry_id:155172).