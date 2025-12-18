## Introduction
Solving large-scale [systems of linear equations](@entry_id:148943) is a fundamental challenge in scientific computing, particularly when these systems arise from the [discretization of partial differential equations](@entry_id:748527) (PDEs). While direct methods are suitable for small problems, they become computationally prohibitive for the massive, sparse matrices typical of high-resolution simulations. This creates a critical knowledge gap that is filled by [iterative methods](@entry_id:139472), which offer a more efficient alternative by generating a sequence of approximate solutions that converge towards the exact answer.

This article provides a comprehensive exploration of three foundational [stationary iterative methods](@entry_id:144014): the Jacobi, Gauss-Seidel, and Successive Over-Relaxation (SOR) methods. By understanding these classical techniques, you will build a solid foundation for tackling more advanced numerical algorithms.

The journey is structured across three chapters. In "Principles and Mechanisms," you will learn the core theory of matrix splitting, understand how the iteration matrices are derived, and analyze the mathematical conditions that govern their convergence. Next, "Applications and Interdisciplinary Connections" will demonstrate how these methods are applied to solve real-world problems in physics and engineering, explore their crucial role as smoothers in modern [multigrid solvers](@entry_id:752283), and reveal their surprising connections to fields like optimization and machine learning. Finally, "Hands-On Practices" will provide you with practical coding exercises to solidify your understanding and apply these methods to complex numerical scenarios.

## Principles and Mechanisms

The solution of large-scale [linear systems](@entry_id:147850) of equations, particularly those arising from the [discretization of partial differential equations](@entry_id:748527) (PDEs), is a cornerstone of [scientific computing](@entry_id:143987). While direct methods like Gaussian elimination are effective for smaller systems, their computational cost and memory requirements become prohibitive for the large, sparse systems typical in PDE applications. This necessitates the use of [iterative methods](@entry_id:139472), which generate a sequence of approximate solutions that ideally converge to the true solution. In this chapter, we will explore the principles and mechanisms of three classical [stationary iterative methods](@entry_id:144014): the Jacobi, Gauss-Seidel, and Successive Over-Relaxation (SOR) methods.

### The Framework of Stationary Iterative Methods

A stationary iterative method for solving the linear system $A\mathbf{x} = \mathbf{b}$ begins with an initial guess $\mathbf{x}^{(0)}$ and generates a sequence of approximations $\mathbf{x}^{(1)}, \mathbf{x}^{(2)}, \dots$ using a fixed rule. The foundation of these methods lies in the concept of a **matrix splitting**. We decompose the matrix $A$ into two parts, $A = M - N$, where $M$ is chosen to be a matrix that is "easy" to invert (e.g., diagonal or triangular) and is a good approximation to $A$.

Substituting this splitting into the original system gives $M\mathbf{x} - N\mathbf{x} = \mathbf{b}$. This arrangement naturally suggests an iterative scheme:
$$
M\mathbf{x}^{(k+1)} = N\mathbf{x}^{(k)} + \mathbf{b}
$$
Since $M$ is invertible, we can write the iteration explicitly for the next approximation $\mathbf{x}^{(k+1)}$:
$$
\mathbf{x}^{(k+1)} = M^{-1}N\mathbf{x}^{(k)} + M^{-1}\mathbf{b}
$$
This is the canonical form of a stationary linear iteration, $\mathbf{x}^{(k+1)} = G\mathbf{x}^{(k)} + \mathbf{c}$, where the **[iteration matrix](@entry_id:637346)** is $G = M^{-1}N$ and the constant vector is $\mathbf{c} = M^{-1}\mathbf{b}$.

An alternative but equivalent formulation is the **residual-correction form**. The residual at step $k$ is defined as $\mathbf{r}^{(k)} = \mathbf{b} - A\mathbf{x}^{(k)}$, which measures how well the current approximation satisfies the equation. Consider an update of the form:
$$
\mathbf{x}^{(k+1)} = \mathbf{x}^{(k)} + M^{-1}(\mathbf{b} - A\mathbf{x}^{(k)})
$$
This form is intuitively appealing: we update the current solution $\mathbf{x}^{(k)}$ by a correction term, which is the preconditioned residual $M^{-1}\mathbf{r}^{(k)}$. To see its equivalence to the splitting form, we can rearrange the terms. Let's substitute $N = M-A$ into the [iteration matrix](@entry_id:637346) $G$:
$$
G = M^{-1}N = M^{-1}(M-A) = I - M^{-1}A
$$
Then, the iteration becomes $\mathbf{x}^{(k+1)} = (I - M^{-1}A)\mathbf{x}^{(k)} + M^{-1}\mathbf{b} = \mathbf{x}^{(k)} - M^{-1}A\mathbf{x}^{(k)} + M^{-1}\mathbf{b} = \mathbf{x}^{(k)} + M^{-1}(\mathbf{b} - A\mathbf{x}^{(k)})$, confirming the two forms are identical  .

The convergence of the method depends entirely on the properties of the iteration matrix $G$. Let $\mathbf{x}$ be the exact solution, so $A\mathbf{x} = \mathbf{b}$, which also means $\mathbf{x} = G\mathbf{x} + \mathbf{c}$. The error at iteration $k$ is $\mathbf{e}^{(k)} = \mathbf{x} - \mathbf{x}^{(k)}$. Subtracting the iterative update from the exact solution equation, we find the **[error propagation](@entry_id:136644)** relationship:
$$
\mathbf{x} - \mathbf{x}^{(k+1)} = (G\mathbf{x} + \mathbf{c}) - (G\mathbf{x}^{(k)} + \mathbf{c}) = G(\mathbf{x} - \mathbf{x}^{(k)})
$$
$$
\mathbf{e}^{(k+1)} = G \mathbf{e}^{(k)}
$$
This simple relation shows that after $k$ steps, the error is $\mathbf{e}^{(k)} = G^k \mathbf{e}^{(0)}$. For the error to vanish as $k \to \infty$ for any initial error $\mathbf{e}^{(0)}$, it is necessary and sufficient that $\lim_{k \to \infty} G^k = 0$. This condition holds if and only if the **spectral radius** of $G$, denoted $\rho(G)$, is strictly less than 1. The spectral radius is defined as $\rho(G) = \max \{|\lambda| : \lambda \text{ is an eigenvalue of } G\}$.

The [spectral radius](@entry_id:138984) governs the asymptotic rate of convergence. Specifically, by Gelfand's formula, $\rho(G) = \lim_{k\to\infty} \|G^k\|^{1/k}$ for any [matrix norm](@entry_id:145006). This means that for large $k$, the error is reduced by a factor of approximately $\rho(G)$ at each iteration: $\|\mathbf{e}^{(k+1)}\| \approx \rho(G) \|\mathbf{e}^{(k)}\|$. A similar analysis shows that the residual propagates according to $\mathbf{r}^{(k+1)} = (I - AM^{-1})\mathbf{r}^{(k)}$, and since the matrices $G = I - M^{-1}A$ and $I - AM^{-1}$ are similar (if $A$ is nonsingular, $I-AM^{-1} = A(I-M^{-1}A)A^{-1}$), they share the same eigenvalues and thus the same spectral radius. Therefore, the asymptotic reduction factor for the [residual norm](@entry_id:136782) is also $\rho(G)$ .

### Classical Splitting Methods

The choice of the splitting matrix $M$ defines the specific method. For a matrix $A$, we can write its [canonical decomposition](@entry_id:634116) as $A = D - L - U$, where $D$ is the diagonal part of $A$, $-L$ is the strictly lower-triangular part, and $-U$ is the strictly upper-triangular part.

#### The Jacobi Method

The simplest choice for $M$ is the diagonal part of $A$, which is trivial to invert. This defines the Jacobi method:
- **Splitting**: $M_J = D$, so $N_J = M_J - A = D - (D-L-U) = L+U$.
- **Iteration Formula**: $D\mathbf{x}^{(k+1)} = (L+U)\mathbf{x}^{(k)} + \mathbf{b}$.
- **Iteration Matrix**: $B_J = D^{-1}(L+U) = I - D^{-1}A$.

In component form, the update for the $i$-th component $x_i$ uses only values from the previous iteration $k$:
$$
x_i^{(k+1)} = \frac{1}{a_{ii}} \left( b_i - \sum_{j \neq i} a_{ij} x_j^{(k)} \right)
$$
This structure means all components can be updated simultaneously, making the method highly parallelizable.

#### The Gauss-Seidel Method

An intuitive improvement on the Jacobi method is to use the most recently computed information as soon as it becomes available. When computing $x_i^{(k+1)}$, the values $x_1^{(k+1)}, \dots, x_{i-1}^{(k+1)}$ have already been determined. Using these new values leads to the Gauss-Seidel method.
- **Component-wise Update**:
$$
x_i^{(k+1)} = \frac{1}{a_{ii}} \left( b_i - \sum_{j=1}^{i-1} a_{ij} x_j^{(k+1)} - \sum_{j=i+1}^{n} a_{ij} x_j^{(k)} \right)
$$
This sequential dependency means the updates cannot be performed in parallel. To find the matrix form, we can write $\sum_{j=1}^{i-1} a_{ij} x_j^{(k+1)}$ as the $i$-th component of $-L\mathbf{x}^{(k+1)}$ and $\sum_{j=i+1}^{n} a_{ij} x_j^{(k)}$ as the $i$-th component of $-U\mathbf{x}^{(k)}$. The equation system becomes $D\mathbf{x}^{(k+1)} = \mathbf{b} + L\mathbf{x}^{(k+1)} + U\mathbf{x}^{(k)}$.
- **Iteration Formula**: $(D-L)\mathbf{x}^{(k+1)} = U\mathbf{x}^{(k)} + \mathbf{b}$.
- **Splitting**: $M_{GS} = D-L$ and $N_{GS} = U$.
- **Iteration Matrix**: $B_{GS} = (D-L)^{-1}U$.

#### The Successive Over-Relaxation (SOR) Method

The SOR method can be viewed as an extrapolation of the Gauss-Seidel method. Let $\tilde{\mathbf{x}}^{(k+1)}$ be the vector that would be computed by a Gauss-Seidel step. The SOR method computes the new iterate $\mathbf{x}^{(k+1)}$ as a weighted average of the previous iterate $\mathbf{x}^{(k)}$ and the Gauss-Seidel update:
$$
\mathbf{x}^{(k+1)} = (1-\omega)\mathbf{x}^{(k)} + \omega \tilde{\mathbf{x}}^{(k+1)}
$$
where $\omega$ is a **[relaxation parameter](@entry_id:139937)**. When $\omega \in (0, 1)$, the method is called [under-relaxation](@entry_id:756302). When $\omega \in (1, 2)$, it is called over-relaxation.
The component-wise update is :
$$
x_i^{(k+1)} = (1-\omega)x_i^{(k)} + \frac{\omega}{a_{ii}} \left( b_i - \sum_{j=1}^{i-1} a_{ij} x_j^{(k+1)} - \sum_{j=i+1}^{n} a_{ij} x_j^{(k)} \right)
$$
By rearranging this equation and assembling it into matrix form, we arrive at the SOR iteration formula:
$$
(D-\omega L)\mathbf{x}^{(k+1)} = ((1-\omega)D + \omega U)\mathbf{x}^{(k)} + \omega \mathbf{b}
$$
- **Iteration Matrix**: $B_{SOR}(\omega) = (D-\omega L)^{-1}((1-\omega)D + \omega U)$.
- **Splitting**: This corresponds to a splitting matrix $M_{SOR} = \frac{1}{\omega}(D-\omega L)$ .

Notice that if we set $\omega=1$, the term $(1-\omega)D$ vanishes, and the equation becomes $(D-L)\mathbf{x}^{(k+1)} = U\mathbf{x}^{(k)} + \mathbf{b}$, which is exactly the Gauss-Seidel method. Thus, Gauss-Seidel is a special case of SOR with $\omega=1$ . The purpose of $\omega$ is to accelerate convergence, and its optimal choice is a critical aspect of the method.

### Convergence Analysis for a Model Problem

To gain concrete insight into the performance of these methods, we analyze them for a model problem: the one-dimensional Poisson equation $-u''(x)=f(x)$ on $(0,1)$ with $u(0)=u(1)=0$. Discretizing with $n$ interior points and grid spacing $h=1/(n+1)$ yields the $n \times n$ matrix $A = \frac{1}{h^2}\text{tridiag}(-1, 2, -1)$. The constant factor $1/h^2$ scales the eigenvalues but does not affect the iteration matrices for these methods. For simplicity, we first analyze the matrix $A' = h^2 A = \text{tridiag}(-1, 2, -1)$, which has $D' = 2I$.

#### Jacobi Convergence

The Jacobi iteration matrix is $B_J = I - (D')^{-1}A' = I - \frac{1}{2}A' = \frac{1}{2}\text{tridiag}(1, 0, 1)$. To find its spectral radius, we must find its eigenvalues. The [eigenvalue problem](@entry_id:143898) $B_J \mathbf{v} = \mu \mathbf{v}$ leads to the difference equation $\frac{1}{2}(v_{j-1} + v_{j+1}) = \mu v_j$ with boundary conditions $v_0 = v_{n+1} = 0$. The solutions to this recurrence are of the form $v_j = \sin(j\theta)$. Substituting this form and solving reveals the $n$ distinct eigenvalues :
$$
\mu_j = \cos\left(\frac{j\pi}{n+1}\right), \quad \text{for } j=1, 2, \dots, n
$$
The spectral radius is the maximum of their absolute values, which occurs for $j=1$ or $j=n$:
$$
\rho(B_J) = \cos\left(\frac{\pi}{n+1}\right)
$$
Expressing this in terms of the grid spacing $h=1/(n+1)$, we get $\rho(B_J) = \cos(\pi h)$. For fine grids, $h \to 0$, and we can use a Taylor expansion: $\rho(B_J) \approx 1 - \frac{1}{2}(\pi h)^2$. The convergence rate approaches 1 (i.e., convergence stalls) as the grid is refined, and the number of iterations required to reduce the error by a fixed amount scales as $O(n^2)$ or $O(h^{-2})$. This is unacceptably slow for practical problems.

#### Gauss-Seidel Convergence

Directly finding the eigenvalues of the non-symmetric Gauss-Seidel matrix $B_{GS} = (D'-L')^{-1}U'$ is more challenging. However, the matrix $A'$ belongs to a special class of matrices called **consistently ordered** matrices. For such matrices, there is a remarkable relationship between the eigenvalues of the Jacobi and Gauss-Seidel methods: the non-zero eigenvalues of $B_{GS}$ are the squares of the non-zero eigenvalues of $B_J$. This directly implies that their spectral radii are related by:
$$
\rho(B_{GS}) = \rho(B_J)^2 = \cos^2\left(\frac{\pi}{n+1}\right) = \cos^2(\pi h)
$$

For small $h$, $\rho(B_{GS}) \approx (1 - \frac{1}{2}(\pi h)^2)^2 \approx 1 - (\pi h)^2$. The Gauss-Seidel method converges approximately twice as fast as the Jacobi method for this model problem, but its performance still degrades significantly on fine grids.

#### SOR Convergence and Optimal Relaxation

The power of SOR lies in choosing $\omega$ to dramatically improve convergence. For [consistently ordered matrices](@entry_id:176621), there is a precise relationship between an eigenvalue $\mu$ of the SOR matrix $B_{SOR}(\omega)$ and a corresponding eigenvalue $\lambda$ of the Jacobi matrix $B_J$ :
$$
(\mu + \omega - 1)^2 = \mu \omega^2 \lambda^2
$$
The spectral radius of $B_{SOR}(\omega)$ is determined by the largest Jacobi eigenvalue, $\lambda = \rho(B_J)$. Our goal is to choose $\omega$ to minimize the magnitude of the largest root $\mu$ of this equation. A detailed analysis shows that as $\omega$ increases from $0$, $\rho(B_{SOR}(\omega))$ decreases, until a critical value $\omega_{\text{opt}}$ where the roots for $\mu$ transition from real to complex. Beyond this point, all roots have the same modulus $|\mu| = \omega-1$, which increases with $\omega$. The minimum is thus achieved at this transition point, which corresponds to the discriminant of the quadratic in $\sqrt{\mu}$ being zero. This yields the optimal [relaxation parameter](@entry_id:139937) :
$$
\omega_{\text{opt}} = \frac{2}{1+\sqrt{1-\rho(B_J)^2}}
$$
For our 1D model problem, we substitute $\rho(B_J) = \cos(\pi/(n+1))$:
$$
\omega_{\text{opt}} = \frac{2}{1+\sqrt{1-\cos^2(\pi/(n+1))}} = \frac{2}{1+\sin(\pi/(n+1))}
$$
. At this optimal value, the [spectral radius](@entry_id:138984) of SOR is $\rho(B_{SOR}(\omega_{\text{opt}})) = \omega_{\text{opt}} - 1$. For small $h$, $\sin(\pi h) \approx \pi h$, so $\omega_{\text{opt}} \approx \frac{2}{1+\pi h} \approx 2(1-\pi h)$. The [spectral radius](@entry_id:138984) is $\rho(B_{SOR}(\omega_{\text{opt}})) \approx 1 - 2\pi h$. This is a major improvement: the error reduction factor's deviation from 1 is now $O(h)$ instead of $O(h^2)$. Nonetheless, convergence still slows down as the grid is refined.

### General Convergence Conditions

While the model problem analysis is insightful, more general conditions are needed for arbitrary matrices.

One of the most useful [sufficient conditions](@entry_id:269617) for convergence is **[strict diagonal dominance](@entry_id:154277)**. A matrix $A$ is strictly diagonally dominant by rows if for every row $i$, the absolute value of the diagonal element is greater than the sum of the absolute values of the off-diagonal elements: $|a_{ii}| > \sum_{j \neq i} |a_{ij}|$.

We can use the **Gershgorin Circle Theorem** to prove that [strict diagonal dominance](@entry_id:154277) of $A$ guarantees the convergence of the Jacobi method. The theorem states that every eigenvalue of a matrix $G$ lies in one of its Gershgorin discs, centered at the diagonal entries $g_{ii}$ with radius $R_i = \sum_{j \neq i} |g_{ij}|$. For the Jacobi matrix $B_J = I - D^{-1}A$, the diagonal entries are all zero. The radii are $R_i = \sum_{j \neq i} |-a_{ij}/a_{ii}| = \frac{1}{|a_{ii}|}\sum_{j \neq i} |a_{ij}|$. The condition of [strict diagonal dominance](@entry_id:154277) directly implies that $R_i  1$ for all $i$. Therefore, all Gershgorin discs, and thus all eigenvalues of $B_J$, are contained strictly inside the unit circle in the complex plane, which means $\rho(B_J)  1$ . A similar proof holds for Gauss-Seidel.

It is crucial to recognize that this is a *sufficient* condition, not a *necessary* one. The Poisson matrix, for example, is not strictly [diagonally dominant](@entry_id:748380) (it is weakly [diagonally dominant](@entry_id:748380) for interior rows), yet we have shown that Jacobi and Gauss-Seidel do converge. For the Poisson matrix, the Gershgorin bound on the spectral radius is $\rho(B_J) \le 1$, which is inconclusive. This highlights that while [diagonal dominance](@entry_id:143614) is a convenient check, its failure does not imply divergence . Another powerful result is that for any **[symmetric positive definite](@entry_id:139466) (SPD)** matrix, the SOR method is guaranteed to converge for any [relaxation parameter](@entry_id:139937) $\omega \in (0, 2)$.

### The Role of Iterative Methods as Smoothers

A modern perspective on these classical methods is to view them not as standalone solvers, but as components in more powerful algorithms like [multigrid methods](@entry_id:146386). In this context, their role is not to eliminate the error entirely, but to **smooth** it.

This behavior is best understood using **Local Fourier Analysis (LFA)**. On a uniform, infinite grid, the error can be decomposed into Fourier modes $\varphi_{\theta}(j) = \exp(i j \theta)$, where $\theta \in (-\pi, \pi]$ represents the frequency. A stationary iteration acts on each Fourier mode by multiplying it by a complex number called the **amplification factor** or **symbol**, denoted $g(\theta)$.

For the weighted Jacobi method applied to the periodic 1D Poisson operator, the [error propagation](@entry_id:136644) operator is $G = I - \omega D^{-1}A$. The symbol of the operator $A$ is $a(\theta) = 2(1-\cos\theta)$, and the symbol of $D=2I$ is simply 2. The [amplification factor](@entry_id:144315) is therefore :
$$
g_J(\theta) = 1 - \omega \frac{a(\theta)}{2} = 1 - \omega(1-\cos\theta)
$$
Let's analyze the magnitude of this factor for different frequencies :
-   **Low Frequencies ($\theta \approx 0$)**: The error components are smooth and oscillating slowly. Here, $\cos\theta \approx 1 - \theta^2/2$, so $g_J(\theta) \approx 1 - \omega\theta^2/2$. The magnitude $|g_J(\theta)|$ is very close to 1. This means the iteration is extremely ineffective at damping low-frequency error components.
-   **High Frequencies ($\theta \approx \pi$)**: The error components are jagged and oscillating rapidly. Here, $\cos\pi = -1$. The amplification factor is $g_J(\pi) = 1 - 2\omega$. By choosing an appropriate weight, such as $\omega=1/2$, we get $g_J(\pi) = 0$, meaning the highest frequency is eliminated in one step. Other high frequencies are also strongly damped.

This analysis reveals the dual nature of the iteration: it is a poor solver for low-frequency error but an excellent one for high-frequency error. This is the property of a **smoother**. An iteration like Jacobi or Gauss-Seidel effectively "cleans up" the oscillatory parts of the error, leaving behind a smooth residual error.

This behavior is the fundamental principle behind [multigrid methods](@entry_id:146386). A few steps of a smoother are applied on a fine grid. The remaining error, which is now predominantly smooth (low-frequency), can be accurately approximated on a much coarser grid. On this coarse grid, the problem is smaller and cheaper to solve. Furthermore, what was low-frequency on the fine grid becomes relatively high-frequency on the coarse grid, making the smoother effective again. The solution to the coarse-grid problem is then interpolated back to the fine grid to correct the approximation. This **[coarse-grid correction](@entry_id:140868)** is highly effective at eliminating the smooth error components that the smoother cannot handle, while the smoother is highly effective at eliminating the high-frequency components that the coarse grid cannot even represent. This complementary action is what gives [multigrid methods](@entry_id:146386) their remarkable, grid-independent efficiency .