## Introduction
Solving [systems of linear equations](@entry_id:148943) is a cornerstone of computational science and engineering. While direct methods like Gaussian elimination provide exact solutions, they can be computationally prohibitive for the massive systems that arise from discretizing differential equations or analyzing large networks. This is where iterative methods come into play, offering a powerful alternative that starts with an initial guess and progressively refines it to converge upon a solution. The Jacobi method stands as one of the most fundamental and intuitive of these iterative techniques, offering a clear window into the principles of iterative solvers. This article demystifies the Jacobi method, addressing how an approximate solution can be systematically improved and under what conditions this process is guaranteed to succeed.

Across the following chapters, you will gain a comprehensive understanding of this essential algorithm. The first chapter, **Principles and Mechanisms**, will break down the mathematical foundation of the method, from its simple component-wise update rule to its matrix formulation and the critical theory governing its convergence. Next, in **Applications and Interdisciplinary Connections**, we will explore the remarkable versatility of the Jacobi method, seeing how it models physical phenomena like heat flow, analyzes social networks, informs economic models, and serves as a vital component in advanced algorithms. Finally, **Hands-On Practices** will provide you with the opportunity to apply these concepts and solidify your understanding through targeted exercises.

## Principles and Mechanisms

The Jacobi method is a foundational iterative algorithm for approximating the solution to a system of linear equations, $A\mathbf{x} = \mathbf{b}$. Unlike direct methods, which aim to compute the exact solution in a finite number of steps (e.g., Gaussian elimination), iterative methods begin with an initial guess for the solution and successively refine it. The core principle of the Jacobi method is its elegant simplicity: it updates each component of the solution vector using only information from the previous iteration, a feature that has profound implications for both its implementation and theoretical analysis.

### The Component-wise Formulation

The most intuitive way to understand the Jacobi method is by examining the system of equations component by component. For an $n \times n$ system, we have $n$ [linear equations](@entry_id:151487):
$$
\sum_{j=1}^{n} a_{ij} x_j = b_i, \quad \text{for } i = 1, 2, \dots, n
$$
The fundamental assumption for the Jacobi method is that all diagonal entries $a_{ii}$ are non-zero. This allows us to isolate the $i$-th variable, $x_i$, in the $i$-th equation:
$$
a_{ii} x_i = b_i - \sum_{j \neq i} a_{ij} x_j
$$
$$
x_i = \frac{1}{a_{ii}} \left( b_i - \sum_{j \neq i} a_{ij} x_j \right)
$$
This rearrangement directly inspires the iterative scheme. If we have an approximation to the solution vector, denoted $\mathbf{x}^{(k)} = (x_1^{(k)}, x_2^{(k)}, \dots, x_n^{(k)})^T$ at iteration $k$, we can compute a new, hopefully better, approximation $\mathbf{x}^{(k+1)}$ by using the old values on the right-hand side of the equation. This leads to the **Jacobi update rule**:

$$
x_i^{(k+1)} = \frac{1}{a_{ii}} \left( b_i - \sum_{j \neq i} a_{ij} x_j^{(k)} \right), \quad \text{for } i = 1, 2, \dots, n
$$

For instance, consider a $3 \times 3$ system with generic coefficients :
$$
\begin{pmatrix} \alpha & \beta & \gamma \\ \delta & \epsilon & \zeta \\ \eta & \theta & \iota \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \\ x_3 \end{pmatrix} = \begin{pmatrix} d_1 \\ d_2 \\ d_3 \end{pmatrix}
$$
The Jacobi update for the first component, $x_1^{(k+1)}$, is found by isolating $x_1$ in the first equation and evaluating the remaining terms using the $k$-th iterate:
$$
\alpha x_1^{(k+1)} + \beta x_2^{(k)} + \gamma x_3^{(k)} = d_1 \implies x_1^{(k+1)} = \frac{1}{\alpha} \left( d_1 - \beta x_2^{(k)} - \gamma x_3^{(k)} \right)
$$
A crucial observation from this formula is that the calculation of each new component $x_i^{(k+1)}$ depends *only* on the components of the previous iteration vector, $\mathbf{x}^{(k)}$. The new values $x_j^{(k+1)}$ for $j \neq i$ are not required. This computational independence means that all $n$ components of $\mathbf{x}^{(k+1)}$ can be computed simultaneously, making the Jacobi method inherently parallelizable . This stands in contrast to methods like the Gauss-Seidel iteration, where the update for $x_i^{(k+1)}$ immediately uses the newly computed values $x_1^{(k+1)}, \dots, x_{i-1}^{(k+1)}$, enforcing a sequential order of computation.

Let's ground this with a numerical example . Consider the system:
$$
\begin{align*}
10x_1 - 2x_2 + x_3 = 21 \\
x_1 + 8x_2 - 3x_3 = -11 \\
-2x_1 + x_2 + 5x_3 = 10
\end{align*}
$$
The Jacobi update rules are:
$$
x_1^{(k+1)} = \frac{1}{10} (21 + 2x_2^{(k)} - x_3^{(k)})
$$
$$
x_2^{(k+1)} = \frac{1}{8} (-11 - x_1^{(k)} + 3x_3^{(k)})
$$
$$
x_3^{(k+1)} = \frac{1}{5} (10 + 2x_1^{(k)} - x_2^{(k)})
$$
Starting with an initial guess $\mathbf{x}^{(0)} = \begin{pmatrix} 1 & 1 & 1 \end{pmatrix}^T$, the first iteration yields:
$$
x_1^{(1)} = \frac{1}{10} (21 + 2(1) - 1) = \frac{22}{10} = \frac{11}{5}
$$
$$
x_2^{(1)} = \frac{1}{8} (-11 - 1 + 3(1)) = -\frac{9}{8}
$$
$$
x_3^{(1)} = \frac{1}{5} (10 + 2(1) - 1) = \frac{11}{5}
$$
Thus, the new approximation is $\mathbf{x}^{(1)} = \begin{pmatrix} \frac{11}{5} & -\frac{9}{8} & \frac{11}{5} \end{pmatrix}^T$. This process is repeated until the sequence of vectors $\mathbf{x}^{(k)}$ converges to a stable solution.

### The Matrix Formulation and Fixed-Point Iteration

For a deeper analysis of the method, particularly its convergence properties, it is essential to express the iteration in matrix-vector form. We begin by splitting the matrix $A$ into three parts: its diagonal ($D$), its strictly lower-triangular part ($-L$), and its strictly upper-triangular part ($-U$).
$$
A = D - L - U
$$
Here, $D$ is a diagonal matrix with $D_{ii} = a_{ii}$, $-L$ contains the entries of $A$ below the main diagonal, and $-U$ contains the entries above the main diagonal. For instance, if $A = \begin{pmatrix} a_{11} & a_{12} \\ a_{21} & a_{22} \end{pmatrix}$, then $D = \begin{pmatrix} a_{11} & 0 \\ 0 & a_{22} \end{pmatrix}$, $L = \begin{pmatrix} 0 & 0 \\ -a_{21} & 0 \end{pmatrix}$, and $U = \begin{pmatrix} 0 & -a_{12} \\ 0 & 0 \end{pmatrix}$.

The linear system $A\mathbf{x} = \mathbf{b}$ can now be written as $(D - L - U)\mathbf{x} = \mathbf{b}$. Following the same logic as in the component-wise derivation, we isolate the term involving the easily invertible matrix $D$:
$$
D\mathbf{x} = (L+U)\mathbf{x} + \mathbf{b}
$$
The Jacobi iteration is formed by using the old iterate $\mathbf{x}^{(k)}$ on the right side to compute the new iterate $\mathbf{x}^{(k+1)}$ on the left:
$$
D\mathbf{x}^{(k+1)} = (L+U)\mathbf{x}^{(k)} + \mathbf{b}
$$
Since we assume all diagonal elements are non-zero, the diagonal matrix $D$ is invertible. Multiplying by $D^{-1}$ gives the [standard matrix](@entry_id:151240) form of the Jacobi iteration :
$$
\mathbf{x}^{(k+1)} = D^{-1}(L+U)\mathbf{x}^{(k)} + D^{-1}\mathbf{b}
$$
This equation has the general form of a **[fixed-point iteration](@entry_id:137769)**, $\mathbf{x}^{(k+1)} = \mathbf{g}(\mathbf{x}^{(k)})$, where the function is $\mathbf{g}(\mathbf{x}) = T_J\mathbf{x} + \mathbf{c}$. We can identify the **Jacobi [iteration matrix](@entry_id:637346)** $T_J$ and the constant vector $\mathbf{c}$ as:
$$
T_J = D^{-1}(L+U) \quad \text{and} \quad \mathbf{c} = D^{-1}\mathbf{b}
$$
It's important to note that since $D$ is diagonal, its inverse $D^{-1}$ is simply the diagonal matrix with entries $1/a_{ii}$. The [iteration matrix](@entry_id:637346) $T_J$ can also be written as $T_J = I - D^{-1}A$. The entries of $T_J$ are given by $(T_J)_{ii} = 0$ and $(T_J)_{ij} = -a_{ij}/a_{ii}$ for $i \neq j$.

As a concrete example , for the system with $A = \begin{pmatrix} 5 & 1 & -2 \\ -1 & 8 & 3 \\ 2 & -4 & 10 \end{pmatrix}$ and $\mathbf{b} = \begin{pmatrix} 4 \\ -2 \\ 1 \end{pmatrix}$, the entry $(T_J)_{32}$ is $-a_{32}/a_{33} = -(-4)/10 = 2/5$. The second component of the constant vector $\mathbf{c}$ is $c_2 = b_2/a_{22} = -2/8 = -1/4$.

The requirement that $a_{ii} \neq 0$ is not merely a technicality for ensuring convergence; it is a fundamental prerequisite for the method to be well-defined. If any diagonal element $a_{ii}$ is zero, the update formula for $x_i^{(k+1)}$ involves division by zero, and the iteration cannot proceed .

### Convergence of the Jacobi Method

The central question for any [iterative method](@entry_id:147741) is whether the sequence of approximations $\mathbf{x}^{(k)}$ converges to the true solution $\mathbf{x}$. Let $\mathbf{x}$ be the exact solution, so it satisfies $A\mathbf{x} = \mathbf{b}$, which also means it is a fixed point of the iteration: $\mathbf{x} = T_J\mathbf{x} + \mathbf{c}$.

Let the error at iteration $k$ be $\mathbf{e}^{(k)} = \mathbf{x}^{(k)} - \mathbf{x}$. We can find the relationship between successive errors by subtracting the [fixed-point equation](@entry_id:203270) from the iteration equation:
$$
\mathbf{x}^{(k+1)} - \mathbf{x} = (T_J\mathbf{x}^{(k)} + \mathbf{c}) - (T_J\mathbf{x} + \mathbf{c}) = T_J(\mathbf{x}^{(k)} - \mathbf{x})
$$
This gives the simple and elegant [error propagation formula](@entry_id:636274):
$$
\mathbf{e}^{(k+1)} = T_J \mathbf{e}^{(k)}
$$
By repeatedly applying this relation, we find that the error at step $k$ is related to the initial error $\mathbf{e}^{(0)} = \mathbf{x}^{(0)} - \mathbf{x}$ by $\mathbf{e}^{(k)} = T_J^k \mathbf{e}^{(0)}$. For the error to vanish as $k \to \infty$ for any arbitrary initial error $\mathbf{e}^{(0)}$, the matrix power $T_J^k$ must go to the [zero matrix](@entry_id:155836). This occurs if and only if all eigenvalues of $T_J$ have a magnitude less than 1.

The **[spectral radius](@entry_id:138984)** of a matrix, denoted $\rho(T_J)$, is the maximum absolute value of its eigenvalues. The necessary and sufficient condition for the Jacobi method to converge for any initial guess $\mathbf{x}^{(0)}$ is:
$$
\rho(T_J)  1
$$
The spectral radius not only determines *if* the method converges but also *how fast*. For large $k$, the error reduction is governed by the eigenvalue with the largest magnitude. Specifically, the asymptotic rate of convergence is given by the spectral radius itself. The ratio of the norms of successive error vectors approaches $\rho(T_J)$ as the number of iterations becomes large :
$$
\lim_{k \to \infty} \frac{\|\mathbf{e}^{(k+1)}\|}{\|\mathbf{e}^{(k)}\|} = \rho(T_J)
$$
A value of $\rho(T_J)$ close to 1 implies slow convergence, while a value close to 0 implies rapid convergence.

### A Practical Condition: Diagonal Dominance

While the [spectral radius](@entry_id:138984) provides a complete theoretical answer to convergence, computing it can be as difficult as solving the original linear system. A more practical tool is needed to guarantee convergence. This is provided by the property of **[strict diagonal dominance](@entry_id:154277)**.

A matrix $A$ is said to be **strictly diagonally dominant** (by rows) if, for every row, the absolute value of the diagonal entry is greater than the sum of the [absolute values](@entry_id:197463) of all other entries in that row:
$$
|a_{ii}|  \sum_{j \neq i} |a_{ij}| \quad \text{for all } i = 1, \dots, n
$$
A key theorem in numerical analysis states that if a matrix $A$ is strictly diagonally dominant, then the Jacobi method is guaranteed to converge for any starting vector $\mathbf{x}^{(0)}$. This condition is sufficient, but not necessary; the method can converge even for matrices that do not satisfy this property. However, it provides a simple and powerful check.

For example, let's determine for which values of a parameter $\alpha$ the matrix below is strictly diagonally dominant :
$$
A = \begin{pmatrix} -12  \alpha  3 \\ 2\alpha  15  -5 \\ 1  -2  4\alpha \end{pmatrix}
$$
We must satisfy three inequalities:
1.  Row 1: $|-12| > |\alpha| + |3| \implies 12 > |\alpha| + 3 \implies |\alpha|  9$.
2.  Row 2: $|15| > |2\alpha| + |-5| \implies 15 > 2|\alpha| + 5 \implies 10 > 2|\alpha| \implies |\alpha|  5$.
3.  Row 3: $|4\alpha| > |1| + |-2| \implies 4|\alpha| > 3 \implies |\alpha| > \frac{3}{4}$.

For convergence to be guaranteed, all three conditions must hold. The intersection of these conditions is $\frac{3}{4}  |\alpha|  5$. Therefore, for any $\alpha \in (-5, -3/4) \cup (3/4, 5)$, the Jacobi method will converge.

### Advanced Interpretations of the Jacobi Method

#### The Jacobi Method as Coordinate Descent

When the matrix $A$ is symmetric and positive definite (SPD), the problem of solving $A\mathbf{x} = \mathbf{b}$ is equivalent to finding the unique vector $\mathbf{x}$ that minimizes the quadratic form:
$$
\phi(\mathbf{x}) = \frac{1}{2}\mathbf{x}^T A \mathbf{x} - \mathbf{b}^T \mathbf{x}
$$
The gradient of this [quadratic form](@entry_id:153497) is $\nabla \phi(\mathbf{x}) = A\mathbf{x} - \mathbf{b}$, and setting the gradient to zero retrieves our original linear system. From this optimization perspective, the Jacobi method can be interpreted as a simultaneous coordinate-wise minimization algorithm .

At each step, to get from $\mathbf{x}^{(k)}$ to $\mathbf{x}^{(k+1)}$, the Jacobi method updates each component $x_i^{(k+1)}$ to the value that would minimize the [quadratic form](@entry_id:153497) $\phi$ along the $i$-th coordinate direction, assuming all other coordinates are fixed at their values from the previous iterate, $\mathbf{x}^{(k)}$.
Let's see this for the $i$-th component. We want to find the value $\xi$ that minimizes the function $g(\xi) = \phi(x_1^{(k)}, \dots, x_{i-1}^{(k)}, \xi, x_{i+1}^{(k)}, \dots, x_n^{(k)})$. To find the minimum, we set the derivative to zero:
$$
\frac{dg}{d\xi} = \frac{\partial \phi}{\partial x_i} \bigg|_{\mathbf{x}=(x_1^{(k)}, \dots, \xi, \dots, x_n^{(k)})^T} = 0
$$
The $i$-th component of the gradient $\nabla \phi(\mathbf{x})$ is $(A\mathbf{x} - \mathbf{b})_i = \sum_{j=1}^n a_{ij}x_j - b_i$. Evaluating this with our coordinate-fixed vector gives:
$$
a_{ii}\xi + \sum_{j \neq i} a_{ij}x_j^{(k)} - b_i = 0
$$
Solving for the optimal $\xi$, we get:
$$
\xi = \frac{1}{a_{ii}}\left(b_i - \sum_{j \neq i} a_{ij}x_j^{(k)}\right)
$$
This is precisely the Jacobi update rule for $x_i^{(k+1)}$. Thus, each step of the Jacobi method finds the "best" new value for each coordinate independently, based on the current state of all other coordinates, and then updates all coordinates simultaneously.

#### The Jacobi Method as a Smoother

In [scientific computing](@entry_id:143987), particularly in the solution of [partial differential equations](@entry_id:143134) (PDEs), the Jacobi method plays a vital role as a **smoother**. When a PDE like the Poisson equation is discretized on a grid, it often results in a very large, sparse linear system $A\mathbf{x}=\mathbf{b}$, where the matrix $A$ is a discrete version of a [differential operator](@entry_id:202628) like the Laplacian.

The error vector $\mathbf{e}^{(k)}$ at any stage can be decomposed into a sum of eigenvectors of the matrix $A$. These eigenvectors, often called Fourier modes, correspond to different spatial frequencies. Low-index eigenvectors represent smooth, low-frequency error components, while high-index eigenvectors represent oscillatory, high-frequency error components.

A smoother is an iterative method that is particularly effective at reducing the high-frequency components of the error, even if it is slow at reducing the low-frequency components. The weighted Jacobi method, defined by the iteration
$$
\mathbf{x}^{(k+1)} = (1-\omega)\mathbf{x}^{(k)} + \omega (T_J \mathbf{x}^{(k)} + \mathbf{c}) = (I - \omega D^{-1}A)\mathbf{x}^{(k)} + \omega D^{-1}\mathbf{b}
$$
is an excellent example of a smoother for an appropriate choice of the weight $\omega$. The error at each step is multiplied by the iteration matrix $G_\omega = I - \omega D^{-1}A$. The eigenvalues of $G_\omega$, known as damping factors, determine how quickly each error mode is reduced.

Let's analyze this for the 1D discrete Laplacian matrix on an $N$-interval grid . For this matrix, $D=2I$, and its eigenvalues are $\lambda_j = 2 - 2\cos(\frac{j\pi}{N})$ for $j=1, \dots, N-1$. The damping factor for the $j$-th mode is $\mu_j(\omega) = 1 - \omega(\lambda_j/2) = 1 - \omega(1 - \cos(\frac{j\pi}{N}))$.

With a [specific weight](@entry_id:275111), such as $\omega = 2/3$, the damping factors become $\mu_j = \frac{1}{3} + \frac{2}{3}\cos(\frac{j\pi}{N})$.
For the lowest frequency error (smooth, $j=1$), the damping factor is $|\mu_1| = \frac{1}{3}(1 + 2\cos(\frac{\pi}{N}))$.
For the highest frequency error (oscillatory, $j=N-1$), the damping factor is $|\mu_{N-1}| = \frac{1}{3}|1 + 2\cos(\frac{(N-1)\pi}{N})| = \frac{1}{3}|1 - 2\cos(\frac{\pi}{N})|$.
For large $N$, $\cos(\frac{\pi}{N}) \approx 1$, so $|\mu_1| \approx 1$, indicating very slow damping. In contrast, $|\mu_{N-1}| \approx \frac{1}{3}|1-2| = \frac{1}{3}$, indicating significant damping.

The ratio of the magnitudes of these damping factors, $\mathcal{S} = \frac{|\mu_1|}{|\mu_{N-1}|} = \frac{1+2\cos(\frac{\pi}{N})}{2\cos(\frac{\pi}{N})-1}$, is large for large $N$. This confirms that the weighted Jacobi method damps high-frequency errors much more effectively than low-frequency errors. This "smoothing" property is precisely what makes it a crucial component of more advanced and powerful solvers like [multigrid methods](@entry_id:146386), which use the Jacobi smoother to eliminate oscillatory errors before addressing the smooth errors on coarser grids.