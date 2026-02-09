## Introduction
Solving large, sparse systems of linear equations, $Ax=b$, is a foundational challenge in computational science and engineering, particularly in fields like Computational Fluid Dynamics (CFD) where they arise from the discretization of partial differential equations. While direct solvers are effective for small problems, their prohibitive computational and memory costs for large-scale systems necessitate the use of iterative methods. Among the most fundamental of these are stationary iterative methods, which generate a sequence of approximate solutions through a consistent, repeated application of a single update rule. These methods form the bedrock upon which more complex and efficient modern solvers are built. This article addresses the need for a comprehensive understanding of their principles, limitations, and, most crucially, their modern role in high-performance scientific computing.

Across the following chapters, you will gain a deep understanding of this important class of numerical methods. The first chapter, **Principles and Mechanisms**, delves into the core theory, explaining how these methods are derived from matrix splittings, analyzing their convergence properties using the concept of the spectral radius, and detailing the classical formulations of the Jacobi, Gauss-Seidel, and SOR methods. The second chapter, **Applications and Interdisciplinary Connections**, shifts focus to practical utility, demonstrating why these methods are now primarily used as essential components—smoothers and preconditioners—within advanced multigrid and Krylov solvers, and exploring their connections to other scientific domains. Finally, **Hands-On Practices** will provide you with the opportunity to apply these theoretical concepts to concrete problems, solidifying your knowledge. We begin by examining the fundamental principles and mechanisms that govern all stationary iterative methods.

## Principles and Mechanisms

The solution of large, sparse linear systems of equations of the form $A x = b$ is a cornerstone of computational science, particularly in fields like Computational Fluid Dynamics (CFD) where such systems arise from the discretization of partial differential equations. While direct methods like LU decomposition are effective for smaller systems, their computational cost and memory requirements become prohibitive for the large-scale problems encountered in practice. This motivates the use of iterative methods, which generate a sequence of approximate solutions $\{x^{(k)}\}$ that ideally converge to the true solution $x^*$. Among these, stationary iterative methods represent a foundational class, characterized by an update rule that is applied uniformly at each step. This chapter elucidates the core principles of these methods, from their fundamental construction to their convergence properties and their modern application as components in more advanced solvers.

### General Formulation of Stationary Iterations

The fundamental concept underlying all stationary iterative methods is the **matrix splitting**. We decompose the system matrix $A$ into the difference of two matrices, $A = M - N$, where $M$ is a nonsingular matrix chosen to be "easily invertible" in a computational sense. Substituting this splitting into the original system $A x = b$ yields $(M - N) x = b$, which can be rearranged to $M x = N x + b$.

This algebraic rearrangement directly inspires an iterative scheme. If we have an approximation $x^{(k)}$ to the solution $x$, we can define the next approximation $x^{(k+1)}$ by solving the system:

$M x^{(k+1)} = N x^{(k)} + b$

Since $M$ was chosen to be easily invertible, computing $x^{(k+1)}$ is computationally inexpensive. For instance, if $M$ is diagonal or triangular, this step is trivial. By multiplying by $M^{-1}$, we can express the iteration in an explicit **fixed-point form** [@problem_id:3365947]:

$x^{(k+1)} = M^{-1} N x^{(k)} + M^{-1} b$

This equation reveals the structure of the iteration. It is an affine map of the form $x^{(k+1)} = T x^{(k)} + c$, where the matrix $T = M^{-1} N$ is called the **iteration matrix** and the vector $c = M^{-1} b$ is a constant term. The properties of the iteration matrix $T$ govern the entire behavior of the method, most critically its convergence.

An alternative but equivalent perspective is to view the iteration as a corrective process. Let the **residual** at step $k$ be defined as $r^{(k)} = b - A x^{(k)}$, which measures how well the current approximation $x^{(k)}$ satisfies the original equation. The iteration can be expressed as an update to $x^{(k)}$:

$x^{(k+1)} = x^{(k)} + \delta^{(k)}$

where $\delta^{(k)}$ is a correction term. By substituting the general form $M x^{(k+1)} = N x^{(k)} + b$ and using $N=M-A$, we can derive this correction.
$M(x^{(k+1)} - x^{(k)}) = N x^{(k)} + b - M x^{(k)} = (M-A)x^{(k)} + b - M x^{(k)} = b - A x^{(k)} = r^{(k)}$.
This gives the correction $\delta^{(k)} = M^{-1} r^{(k)}$, leading to the **corrective form** of the iteration [@problem_id:3365938]:

$x^{(k+1)} = x^{(k)} + M^{-1} r^{(k)}$

This form is highly intuitive: the next approximation is found by adding a correction to the current one, where the correction is the preconditioned residual. The matrix $M^{-1}$ acts as a preconditioner, transforming the residual before it is used to update the solution.

### Convergence, Error, and Residual Propagation

A stationary method is only useful if the sequence of approximates $\{x^{(k)}\}$ converges to the true solution $x^*$, where $A x^* = b$. To analyze this, we examine the evolution of the **error vector**, $e^{(k)} = x^* - x^{(k)}$.

Subtracting the fixed-point iteration equation $x^{(k+1)} = T x^{(k)} + c$ from the corresponding equation for the exact solution, $x^* = T x^* + c$ (which holds if the method can converge), we find the **error propagation equation** [@problem_id:3365938]:

$x^* - x^{(k+1)} = (T x^* + c) - (T x^{(k)} + c) = T(x^* - x^{(k)})$

$e^{(k+1)} = T e^{(k)}$

By repeated application, we see that $e^{(k)} = T^k e^{(0)}$, where $e^{(0)}$ is the initial error. The iteration converges for any arbitrary initial guess $x^{(0)}$ if and only if the error vanishes as $k \to \infty$, which requires that $\lim_{k \to \infty} T^k = 0$. This condition is met if and only if the **spectral radius** of the iteration matrix $T$, denoted $\rho(T)$, is strictly less than one. The spectral radius is defined as the maximum absolute value of the eigenvalues of $T$ [@problem_id:2596855]:

$\rho(T) = \max_i |\lambda_i(T)|  1$

The spectral radius thus serves as the primary measure of a method's convergence rate. A smaller spectral radius implies faster convergence, as it represents the factor by which the magnitude of the error is reduced in the "worst-case" eigendirection at each iteration.

Similarly, we can derive an equation for the propagation of the residual [@problem_id:3365938]. Starting from $r^{(k+1)} = b - A x^{(k+1)}$ and using the corrective form $x^{(k+1)} = x^{(k)} + M^{-1} r^{(k)}$, we get:

$r^{(k+1)} = b - A(x^{(k)} + M^{-1} r^{(k)}) = (b - A x^{(k)}) - A M^{-1} r^{(k)} = r^{(k)} - A M^{-1} r^{(k)}$

$r^{(k+1)} = (I - A M^{-1}) r^{(k)}$

The matrix $(I - A M^{-1})$ governs the evolution of the residual. Note that the error propagation matrix $T = I - M^{-1} A$ and the residual propagation matrix are similar matrices ($I-AM^{-1} = M(I-M^{-1}A)M^{-1}$), and therefore share the same eigenvalues and spectral radius.

### Classical Stationary Methods

The general framework of matrix splitting gives rise to several classical methods, each defined by a specific choice of $M$ based on the canonical decomposition of the matrix $A$ into its diagonal ($D$), strictly lower triangular ($-L$), and strictly upper triangular ($-U$) parts, such that $A = D - L - U$ [@problem_id:2596855]. We assume $D$ contains the diagonal entries of $A$, while $L$ and $U$ are defined to have positive entries corresponding to the negated off-diagonal entries of $A$.

#### The Jacobi Method

The Jacobi method is conceptually the simplest. It is based on a splitting where $M$ is just the diagonal part of $A$, i.e., $M = D$. This makes its inversion trivial. The remainder is $N = M - A = D - (D - L - U) = L + U$.

The iteration matrix is therefore:

$T_J = M^{-1} N = D^{-1}(L+U)$

The update formula becomes $x^{(k+1)} = D^{-1}(L+U)x^{(k)} + D^{-1}b$ [@problem_id:3365919]. In component form, this means that to compute the $i$-th component of the new vector $x^{(k+1)}$, we use only the components of the old vector $x^{(k)}$. This structure makes the Jacobi method highly parallelizable.

#### The Gauss-Seidel Method

The Gauss-Seidel (GS) method aims to improve on Jacobi by using the most recently computed information as soon as it is available. When computing the components of $x^{(k+1)}$ in order (from $1$ to $n$), the GS method uses the new values $x_{j}^{(k+1)}$ for $j  i$ to compute $x_{i}^{(k+1)}$. This sequential dependency leads to a different splitting.

The update rule can be written in matrix form as $D x^{(k+1)} = b + L x^{(k+1)} + U x^{(k)}$. Moving all terms with $x^{(k+1)}$ to the left gives $(D - L)x^{(k+1)} = U x^{(k)} + b$. This corresponds to the splitting $M = D-L$ and $N = U$ [@problem_id:3365920].

The Gauss-Seidel iteration matrix is:

$T_{GS} = M^{-1} N = (D-L)^{-1}U$

Because $D-L$ is lower triangular, its inverse is not computed explicitly; rather, the system $(D-L)x^{(k+1)} = \text{rhs}$ is solved efficiently via forward substitution. The inherent sequential nature of GS makes it less amenable to parallelization than Jacobi.

#### Successive Over-Relaxation (SOR)

SOR can be viewed as an extrapolated version of Gauss-Seidel, designed to accelerate convergence. It introduces a **relaxation parameter**, $\omega$, and computes the new iterate as a weighted average of the previous iterate and the standard GS update. This leads to the splitting $M = \frac{1}{\omega}(D - \omega L)$ and $N = \frac{1}{\omega}((1-\omega)D + \omega U)$.

The SOR iteration matrix is [@problem_id:2596855]:

$T_{SOR}(\omega) = (D-\omega L)^{-1}((1-\omega)D + \omega U)$

The choice of $\omega$ is critical. For symmetric positive definite matrices, convergence is guaranteed only for $\omega \in (0, 2)$. If $\omega=1$, SOR reduces to the Gauss-Seidel method. If $\omega \in (0, 1)$, the method is termed "under-relaxed," while for $\omega \in (1, 2)$, it is "over-relaxed." The optimal choice of $\omega$ can dramatically improve convergence over GS, but finding this optimal value can be difficult.

#### Symmetric Successive Over-Relaxation (SSOR)

A notable variant of SOR is the Symmetric SOR (SSOR) method, which consists of two consecutive SOR sweeps per iteration: a forward sweep (as in standard SOR) followed by a backward sweep that updates components in reverse order. A single SSOR step maps $x^{(k)} \to x^{(k+1)}$ via an intermediate step $x^{(k+1/2)}$.

1.  **Forward Sweep:** $(D - \omega L) x^{(k+1/2)} = ((1-\omega)D + \omega U) x^{(k)} + \omega b$
2.  **Backward Sweep:** $(D - \omega U) x^{(k+1)} = ((1-\omega)D + \omega L) x^{(k+1/2)} + \omega b$

By composing these two steps, we can derive the SSOR iteration matrix. Let $T_{fwd}(\omega) = (D - \omega L)^{-1}((1-\omega)D + \omega U)$ be the forward sweep matrix and $T_{back}(\omega) = (D - \omega U)^{-1}((1-\omega)D + \omega L)$ be the backward sweep matrix. The combined SSOR iteration matrix is the product of these two [@problem_id:3365991]:

$T_{SSOR}(\omega) = T_{back}(\omega) T_{fwd}(\omega) = (D - \omega U)^{-1} ((1-\omega)D + \omega L) (D - \omega L)^{-1} ((1-\omega)D + \omega U)$

Although more complex, the resulting iteration matrix for SSOR (with an appropriate $\omega$) has properties that make it a valuable preconditioner for other, more advanced iterative methods.

### Quantitative Convergence Analysis for Model Problems

To gain a quantitative understanding of convergence behavior, we can analyze these methods for a model problem: the linear system arising from the finite difference discretization of the Poisson equation. For the one-dimensional problem $-u''=f$ on a uniform grid, the matrix $A$ is tridiagonal with entries $(2, -1, -1)$.

For a simple $3 \times 3$ system matrix of this type, a direct calculation of the Jacobi iteration matrix $T_J = D^{-1}(L+U)$ yields eigenvalues $\{-\frac{\sqrt{2}}{2}, 0, \frac{\sqrt{2}}{2}\}$. The spectral radius is thus $\rho(T_J) = \frac{\sqrt{2}}{2} \approx 0.707$ [@problem_id:3365947]. For the same matrix, the Gauss-Seidel iteration matrix $T_{GS}$ has a spectral radius of $\rho(T_{GS}) = 1/2$ [@problem_id:3365920]. For a $2 \times 2$ system, the GS spectral radius is $1/4$ [@problem_id:2596855].

These small examples already suggest that Gauss-Seidel converges faster than Jacobi. A more general and powerful tool for this analysis is **Local Fourier Analysis (LFA)**. For the 2D Poisson equation on an $n_x \times n_y$ grid, the eigenvalues of the Jacobi iteration matrix can be found using discrete Fourier analysis. The spectral radius is found to be [@problem_id:3365919]:

$\rho(T_J) = \frac{1}{2} \left( \cos\left(\frac{\pi}{n_x+1}\right) + \cos\left(\frac{\pi}{n_y+1}\right) \right)$

This result is critically important. As the grid is refined (i.e., $n_x, n_y \to \infty$), the arguments of the cosine terms approach zero, and thus $\rho(T_J) \to \frac{1}{2}(1+1) = 1$. A spectral radius approaching 1 signifies extremely slow convergence. This demonstrates that the convergence of the Jacobi method (and other stationary methods) deteriorates rapidly on finer grids.

For matrices arising from such discretizations, which are "consistently ordered," a direct relationship exists between the spectral radii of Jacobi and Gauss-Seidel: $\rho(T_{GS}) = [\rho(T_J)]^2$. While this implies that Gauss-Seidel converges roughly twice as fast as Jacobi, its convergence also degrades on finer grids, as its spectral radius also approaches 1. This grid-dependent performance limits the utility of stationary methods as standalone solvers for large-scale PDE problems.

### Optimization of Iteration Parameters

Some methods, like Richardson, weighted Jacobi, and SOR, include a parameter that can be tuned to optimize performance. Let us consider the simple **Richardson iteration**, given by $x^{(k+1)} = x^{(k)} + \omega(b - A x^{(k)})$, where the iteration matrix is $T(\omega) = I - \omega A$.

If $A$ is symmetric positive definite (SPD) with eigenvalues $\lambda_i$ lying in an interval $[\alpha, \beta]$ where $0  \alpha \le \beta$, the eigenvalues of $T(\omega)$ are $1 - \omega \lambda_i$. The spectral radius is $\rho(T(\omega)) = \max_i |1 - \omega \lambda_i|$. The optimal $\omega$ is the one that minimizes this maximum value over the entire interval $[\alpha, \beta]$. This minimax problem is solved by choosing $\omega$ such that the amplification factor $|1-\omega \lambda|$ has equal magnitude at the endpoints of the eigenvalue spectrum, i.e., $|1-\omega\alpha| = |1-\omega\beta|$. This leads to the optimal relaxation parameter [@problem_id:3437849]:

$\omega_{opt} = \frac{2}{\alpha + \beta}$

The corresponding minimal spectral radius, which represents the best possible convergence factor for Richardson iteration, is:

$\rho_{min} = \frac{\beta - \alpha}{\beta + \alpha} = \frac{\kappa(A) - 1}{\kappa(A) + 1}$

where $\kappa(A) = \beta/\alpha$ is the spectral condition number of the matrix $A$. This fundamental result explicitly connects the best achievable convergence rate to the condition number of the matrix; large condition numbers lead to spectral radii close to 1 and thus slow convergence.

A similar optimization can be performed for the **weighted Jacobi method**, whose iteration matrix is $T_{wJ}(\omega) = I - \omega D^{-1} A$. For the 1D Poisson problem, an analysis shows that the spectral radius is a function of $\omega$ and the grid size $n$. If we restrict the search for an optimal $\omega$ to the interval $(0, 1]$, the minimum spectral radius is achieved at $\omega=1$ (standard Jacobi), resulting in $\rho(T_J) = \cos(\frac{\pi}{n+1})$ [@problem_id:3365938].

### Stationary Methods as Smoothers in Multigrid

The observation that stationary methods converge slowly on fine grids, but that their performance is linked to properties like the condition number, hints at their modern role in scientific computing. They are typically not used as solvers, but rather as **smoothers** within multigrid algorithms.

The core idea of multigrid is to use a hierarchy of grids to efficiently eliminate different frequency components of the error. Low-frequency (or "smooth") error components are difficult to reduce on a fine grid but can be accurately represented and solved for on a coarser grid. High-frequency (or "oscillatory") error components, on the other hand, are effectively reduced by just a few iterations of a simple stationary method. The process of reducing high-frequency error is called **smoothing**.

Local Fourier Analysis (LFA) is the standard tool for quantifying the smoothing properties of a method. On a periodic grid, the error can be decomposed into Fourier modes. A smoother acts by amplifying each mode $\theta$ by a factor $g(\theta)$, known as the **symbol** or **amplification factor** of the iteration. For the weighted Jacobi method applied to the 1D Poisson problem, this symbol is $g(\theta) = 1 - \omega(1 - \cos\theta)$ [@problem_id:3365908].

In a standard multigrid setup with grid coarsening by a factor of two, the high-frequency modes are those with wave numbers $\theta \in \Theta_H$, where $\Theta_H = (-\pi, \pi]^d \setminus (-\pi/2, \pi/2]^d$. An effective smoother is one that strongly damps these modes. The **smoothing factor**, $\mu$, is defined as the maximum amplification factor over all high-frequency modes [@problem_id:3365945]:

$\mu = \sup_{\theta \in \Theta_H} |g(\theta)|$

The goal of a smoother is to achieve $\mu \ll 1$. In an ideal two-grid method, the coarse-grid correction perfectly eliminates all low-frequency error, while the smoother tackles the high-frequency error. The overall convergence factor of the two-grid cycle, $\rho_{TG}$, is then bounded by $\mu^\nu$, where $\nu$ is the number of smoothing steps. A smoothing factor $\mu$ that is independent of grid size leads to a grid-independent multigrid convergence rate, which is the key to the efficiency of multigrid methods.

This shifts the optimization goal. Instead of choosing $\omega$ to minimize the overall spectral radius $\rho(T)$, we choose it to minimize the smoothing factor $\mu$. For the weighted Jacobi method on the 1D Poisson problem, minimizing $|g(\theta)|$ for high frequencies $\theta \in (\pi/2, \pi]$ leads to an optimal choice of $\omega = 2/3$ [@problem_id:3365908]. This value is different from the one that minimizes the overall spectral radius but is optimal for the specific task of smoothing.

#### Robustness and Anisotropic Problems

The effectiveness of a smoother can be severely challenged by problem characteristics, such as anisotropy. Consider the anisotropic diffusion operator $-\partial_{xx} u - \epsilon \partial_{yy} u$, where the diffusivity in the y-direction is much smaller, $\epsilon \ll 1$. The discrete operator exhibits strong coupling between grid points in the x-direction and weak coupling in the y-direction.

For such problems, standard pointwise smoothers like Gauss-Seidel with lexicographic ordering fail dramatically. An error mode that is smooth in the strong direction ($x$) but highly oscillatory in the weak direction ($y$) is barely damped. The LFA symbol for such a mode approaches 1 as $\epsilon \to 0$, meaning the smoother has no effect [@problem_id:3365917]. Physically, the weak connections in the $y$-direction are unable to effectively propagate information to smooth the error.

A robust smoother must implicitly handle the strong connections. The solution is to use **line relaxation**. For instance, in $x$-line Gauss-Seidel, all unknowns on a horizontal line are updated simultaneously by solving a small tridiagonal system. This implicitly inverts the strong part of the operator. The LFA for this method shows that the problematic anisotropic error modes are now effectively damped, with a smoothing factor bounded well below 1, independent of the anisotropy parameter $\epsilon$. This restores robustness to the multigrid solver, ensuring efficient convergence even in the presence of strong anisotropy. This principle of designing smoothers that are implicit in strongly coupled directions is a crucial theme in the development of advanced numerical solvers for complex physical phenomena.