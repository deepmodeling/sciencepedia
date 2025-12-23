## Introduction
Systems of [linear equations](@entry_id:151487) are a cornerstone of quantitative modeling, providing the mathematical framework to describe a vast array of phenomena from [electrical circuits](@entry_id:267403) to economic equilibria. Despite their apparent simplicity, understanding how to reliably and efficiently find their solutions presents a significant challenge, especially for large-scale or numerically sensitive problems. This article provides a comprehensive exploration of this fundamental topic. It begins by establishing the core principles and mechanisms, showing how systems are represented using matrices and vectors and detailing the direct and [iterative methods](@entry_id:139472) used to solve them. It then broadens the perspective to highlight the diverse applications and interdisciplinary connections, demonstrating how linear systems model everything from statistical data to [network flows](@entry_id:268800). Finally, the journey concludes with hands-on practices that solidify these theoretical concepts. By navigating through these sections, you will gain a robust understanding of both the theory behind [linear systems](@entry_id:147850) and the practical techniques essential for their solution in modern computational science.

## Principles and Mechanisms

A [system of linear equations](@entry_id:140416) is a collection of one or more [linear equations](@entry_id:151487) involving the same set of variables. These systems are foundational to countless models in science, engineering, and economics, describing everything from electrical circuits and mechanical structures to market equilibria. This chapter delves into the core principles governing such systems and the primary mechanisms—both analytical and numerical—used to solve them. We will explore their representation, the conditions for the [existence and uniqueness of solutions](@entry_id:177406), and the practical methods for finding those solutions.

### From Equations to Matrices and Vectors

A system of $m$ [linear equations](@entry_id:151487) in $n$ unknowns, $x_1, x_2, \dots, x_n$, is typically written as:
$$
\begin{align*}
a_{11}x_1 + a_{12}x_2 + \dots + a_{1n}x_n = b_1 \\
a_{21}x_1 + a_{22}x_2 + \dots + a_{2n}x_n = b_2 \\
\vdots \qquad  \qquad \vdots \\
a_{m1}x_1 + a_{m2}x_2 + \dots + a_{mn}x_n = b_m
\end{align*}
$$
Here, the coefficients $a_{ij}$ and the constants $b_i$ are known values. While this form is explicit, it can be cumbersome. A more compact and powerful representation is the matrix-vector equation $A\mathbf{x} = \mathbf{b}$, where:
$$
A = \begin{pmatrix}
a_{11}  a_{12}  \dots  a_{1n} \\
a_{21}  a_{22}  \dots  a_{2n} \\
\vdots  \vdots  \ddots  \vdots \\
a_{m1}  a_{m2}  \dots  a_{mn}
\end{pmatrix}, \quad
\mathbf{x} = \begin{pmatrix}
x_1 \\ x_2 \\ \vdots \\ x_n
\end{pmatrix}, \quad
\mathbf{b} = \begin{pmatrix}
b_1 \\ b_2 \\ \vdots \\ b_m
\end{pmatrix}
$$
$A$ is the **[coefficient matrix](@entry_id:151473)**, $\mathbf{x}$ is the **vector of unknowns**, and $\mathbf{b}$ is the **constant vector**. This form is not merely notational; it allows us to use the powerful tools of linear algebra to analyze and solve the system.

There is a third, equally important perspective: the **vector equation**. The product $A\mathbf{x}$ can be interpreted as a [linear combination](@entry_id:155091) of the columns of $A$, with the entries of $\mathbf{x}$ acting as the weights. Let $\mathbf{a}_1, \mathbf{a}_2, \dots, \mathbf{a}_n$ be the column vectors of $A$. Then the system $A\mathbf{x} = \mathbf{b}$ is equivalent to:
$$
x_1\mathbf{a}_1 + x_2\mathbf{a}_2 + \dots + x_n\mathbf{a}_n = \mathbf{b}
$$
This interpretation reframes the problem: solving the system is equivalent to finding the specific weights ($x_1, \dots, x_n$) needed to express the vector $\mathbf{b}$ as a linear combination of the column vectors of $A$.

Consider a practical example from [metallurgy](@entry_id:158855) . A new alloy is to be created by blending three source alloys, A, B, and C, to achieve a target composition of 45.0 kg of Copper, 13.0 kg of Tin, and 42.0 kg of Zinc. The compositions of the source alloys are:
*   Alloy A: 60% Copper, 10% Tin, 30% Zinc
*   Alloy B: 20% Copper, 40% Tin, 40% Zinc
*   Alloy C: 50% Copper, 0% Tin, 50% Zinc

If we let $x_A, x_B, x_C$ be the masses (in kg) of each source alloy used, the [mass balance](@entry_id:181721) for each metal gives us a system of three linear equations. For Copper, the total mass is $0.60x_A + 0.20x_B + 0.50x_C = 45.0$. Formulating similar equations for Tin and Zinc, we can express this entire problem as a single vector equation. The composition of each alloy becomes a column vector, and we seek the weights $x_A, x_B, x_C$ that combine these vectors to produce the target composition vector:
$$
x_A\begin{pmatrix} 0.60 \\ 0.10 \\ 0.30 \end{pmatrix} + x_B\begin{pmatrix} 0.20 \\ 0.40 \\ 0.40 \end{pmatrix} + x_C\begin{pmatrix} 0.50 \\ 0 \\ 0.50 \end{pmatrix} = \begin{pmatrix} 45.0 \\ 13.0 \\ 42.0 \end{pmatrix}
$$
This vector equation beautifully captures the essence of the blending problem and is equivalent to the matrix form $A\mathbf{x} = \mathbf{b}$.

### The Question of Existence and Uniqueness

Before attempting to find a solution, we must ask two fundamental questions:
1.  **Existence:** Does at least one solution exist?
2.  **Uniqueness:** If a solution exists, is it the only one?

The answer to these questions determines whether a system has no solution, exactly one solution, or infinitely many solutions.

#### Consistency and Inconsistency

A [system of linear equations](@entry_id:140416) is **consistent** if it has one or more solutions. It is **inconsistent** if it has no solution. Inconsistency often arises when the equations impose contradictory constraints. For instance, consider a production plan for three experimental alloys that must satisfy the following resource constraints :
$$
\begin{cases}
x_1 + x_2 - 4x_3 = 1 \\
3x_1 + 4x_2 - 9x_3 = 5 \\
-2x_1 + 14x_3 = 7
\end{cases}
$$
We can attempt to solve this through substitution or elimination. From the third equation, we can express $x_1$ in terms of $x_3$: $x_1 = 7x_3 - \frac{7}{2}$. Substituting this into the first two equations would allow us to solve for $x_2$ and $x_3$. However, a more direct approach reveals the system's nature. Let's try to eliminate $x_1$ from the first two equations. Multiplying the first equation by 3 and subtracting it from the second gives:
$$
(3x_1 + 4x_2 - 9x_3) - 3(x_1 + x_2 - 4x_3) = 5 - 3(1)
$$
This simplifies to $x_2 + 3x_3 = 2$. Now, let's use the third equation again. From $x_1 = 7x_3 - \frac{7}{2}$, substituting into the first equation yields:
$$
(7x_3 - \frac{7}{2}) + x_2 - 4x_3 = 1
$$
This simplifies to $x_2 + 3x_3 = \frac{9}{2}$. We have now derived two incompatible conditions: $x_2 + 3x_3 = 2$ and $x_2 + 3x_3 = 4.5$. Since $2 \neq 4.5$, no values of $x_2$ and $x_3$ can satisfy both simultaneously. The system is inconsistent; it is impossible to meet all three resource constraints.

#### The Structure of Solution Sets

When a system $A\mathbf{x} = \mathbf{b}$ is consistent, the set of all its solutions has a remarkable geometric and algebraic structure. This structure is intimately linked to the solution set of the corresponding **[homogeneous system](@entry_id:150411)**, $A\mathbf{x} = \mathbf{0}$. The [solution set](@entry_id:154326) of the [homogeneous system](@entry_id:150411), known as the **[null space](@entry_id:151476)** of $A$, is always a subspace (i.e., it contains the origin and is closed under addition and scalar multiplication).

The fundamental theorem on the [structure of solutions](@entry_id:152035) states that if $A\mathbf{x} = \mathbf{b}$ is consistent and $\mathbf{x}_p$ is any single specific solution (a **[particular solution](@entry_id:149080)**), then the complete solution set is given by:
$$
S_{NH} = \{ \mathbf{x}_p + \mathbf{z} \mid A\mathbf{z} = \mathbf{0} \}
$$
In other words, every solution to the non-[homogeneous system](@entry_id:150411) is the sum of one [particular solution](@entry_id:149080) and a solution from the [homogeneous system](@entry_id:150411). Geometrically, this means the [solution set](@entry_id:154326) of $A\mathbf{x} = \mathbf{b}$ is a translation of the [null space](@entry_id:151476) of $A$ by the vector $\mathbf{x}_p$.

For example, imagine a system in $\mathbb{R}^3$ where the homogeneous solution set $S_H$ (the [null space](@entry_id:151476)) is a line passing through the origin. If the non-[homogeneous system](@entry_id:150411) $A\mathbf{x} = \mathbf{b}$ (with $\mathbf{b} \neq \mathbf{0}$) is consistent, its solution set $S_{NH}$ will be a line parallel to $S_H$. It is the same line, just shifted away from the origin by a particular solution vector $\mathbf{x}_p$ . Since $\mathbf{b} \neq \mathbf{0}$, the [zero vector](@entry_id:156189) is not a solution to the non-[homogeneous system](@entry_id:150411), so this shifted line will not pass through the origin.

#### Guarantees of Existence: The Role of Pivots

While we can test individual systems for consistency, can we say anything about consistency based on properties of the matrix $A$ alone? A key concept here is that of a **[pivot position](@entry_id:156455)**. A [pivot position](@entry_id:156455) in a matrix is the location of a leading 1 in its [reduced row echelon form](@entry_id:150479) (or the first non-zero entry in a row of any [echelon form](@entry_id:153067)).

A crucial theorem states: The system $A\mathbf{x} = \mathbf{b}$ is consistent for *every* vector $\mathbf{b}$ in $\mathbb{R}^m$ if and only if the matrix $A$ has a [pivot position](@entry_id:156455) in every row .

The reasoning is tied to the process of Gaussian elimination. When we row-reduce the [augmented matrix](@entry_id:150523) $[A | \mathbf{b}]$, an inconsistency appears if and only if we obtain a row of the form $[0 \ 0 \ \dots \ 0 | c]$ where $c \neq 0$. If $A$ has a pivot in every row, it means that the [echelon form](@entry_id:153067) of $A$ has no rows that are entirely zero. Consequently, it is impossible for the [row reduction](@entry_id:153590) process to generate a row of the form $[0 \ \dots \ 0 | c]$ with $c \neq 0$. This guarantees that a solution can always be found, regardless of the choice of $\mathbf{b}$. In the language of vector spaces, this condition is equivalent to stating that the columns of $A$ span the entire space $\mathbb{R}^m$, meaning any vector $\mathbf{b}$ can be formed as their [linear combination](@entry_id:155091).

### Direct Methods for Solving Linear Systems

Direct methods aim to find the exact solution to a system in a finite number of steps, assuming perfect arithmetic. The most fundamental direct method is Gaussian elimination.

#### Gaussian Elimination and Its Computational Cost

Gaussian elimination systematically transforms the [augmented matrix](@entry_id:150523) $[A|\mathbf{b}]$ into an upper triangular form $[U|\mathbf{c}]$ through a sequence of [elementary row operations](@entry_id:155518). This process is called **forward elimination**. The equivalent system $U\mathbf{x} = \mathbf{c}$ can then be solved easily by **[back substitution](@entry_id:138571)**, starting from the last equation and working upwards.

While straightforward, this process has a computational cost that is critical for large-scale problems. The dominant cost comes from the [floating-point operations](@entry_id:749454) (multiplications and divisions). For a dense $n \times n$ system, the forward elimination phase requires approximately $\frac{2}{3}n^3$ operations, while [back substitution](@entry_id:138571) requires approximately $n^2$ operations. The total number of multiplications and divisions can be shown to be approximately $\frac{n^3}{3}$. More precisely, the exact count of multiplications and divisions is $\frac{n(n^2+3n-1)}{3}$ . For a relatively small $10 \times 10$ system, this amounts to $\frac{10(100+30-1)}{3} = 430$ operations. For large $n$, the $n^3$ dependence means that doubling the size of the system increases the computation time by a factor of eight.

#### Numerical Stability and the Need for Pivoting

The theoretical elegance of Gaussian elimination can be deceptive. In practice, computers use [finite-precision arithmetic](@entry_id:637673), leading to [rounding errors](@entry_id:143856). These errors can be catastrophic if not handled carefully. A major source of instability occurs when a pivot element (the diagonal element $a_{kk}$ used to eliminate entries below it) is very small in magnitude compared to other entries in its column.

Consider a simple system representing a robotic arm control model where $\epsilon$ is a small parameter, say $\epsilon = 1.00 \times 10^{-4}$ :
$$
\begin{align*}
(1.00 \times 10^{-4}) x_1 + x_2 = 1 \\
x_1 + x_2 = 2
\end{align*}
The exact solution is $x_1 \approx 1.0001$ and $x_2 \approx 0.9999$. Let's solve this using Gaussian elimination on a hypothetical computer with 3-significant-figure rounding arithmetic.

**Without Pivoting:** The first pivot is tiny: $1.00 \times 10^{-4}$. The multiplier for the second row is $m_{21} = \frac{1}{1.00 \times 10^{-4}} = 1.00 \times 10^{4}$. When we update the second row's second element, we compute $1 - (1.00 \times 10^{4}) \times 1 = -9999$. Rounded to 3 significant figures, this is $-1.00 \times 10^{4}$. A similar calculation for the right-hand side gives $2 - (1.00 \times 10^{4}) \times 1 = -9998$, which also rounds to $-1.00 \times 10^{4}$. The second equation becomes $(-1.00 \times 10^{4})x_2 = -1.00 \times 10^{4}$, yielding $x_2 = 1.00$. Substituting back into the first equation gives $(1.00 \times 10^{-4})x_1 + 1.00 = 1$, which results in $x_1 = 0$. The computed solution $(0, 1)$ is drastically incorrect, especially for $x_1$. The small pivot caused the original value of `1` in the second row to be completely lost in a large subtraction ("catastrophic cancellation").

**With Partial Pivoting:** The **partial pivoting** strategy avoids this. Before each elimination step, we inspect the current column from the diagonal downwards and swap rows to bring the element with the largest absolute value into the pivot position. In our example, $|a_{21}| = 1$ is much larger than $|a_{11}| = 10^{-4}$. We swap the two rows:
$$
\begin{align*}
x_1 + x_2 = 2 \\
(1.00 \times 10^{-4}) x_1 + x_2 = 1
\end{align*}
Now the pivot is $1$. The multiplier is $m_{21} = 1.00 \times 10^{-4}$. The new second equation's coefficient for $x_2$ is $1 - (1.00 \times 10^{-4}) \times 1 = 0.9999$, which rounds to $1.00$. The right-hand side becomes $1 - (1.00 \times 10^{-4}) \times 2 = 0.9998$, which also rounds to $1.00$. The second equation is now $1.00 x_2 = 1.00$, so $x_2 = 1.00$. Back substitution gives $x_1 + 1.00 = 2$, yielding $x_1=1.00$. The solution $(1, 1)$ is extremely close to the true solution. Pivoting is essential for the numerical stability of Gaussian elimination.

#### LU Factorization

Gaussian elimination can be formalized through **LU factorization** (or decomposition). This process factors the [coefficient matrix](@entry_id:151473) $A$ into the product of a [lower triangular matrix](@entry_id:201877) $L$ and an upper triangular matrix $U$, such that $A = LU$. The matrix $U$ is the [upper triangular matrix](@entry_id:173038) obtained at the end of forward elimination. The matrix $L$, which typically has 1s on its diagonal (Doolittle method), stores the multipliers used during elimination.

Once this factorization is computed, solving $A\mathbf{x} = \mathbf{b}$ becomes a two-step process. We substitute $A=LU$ to get $LU\mathbf{x} = \mathbf{b}$. We then define an intermediate vector $\mathbf{y} = U\mathbf{x}$.
1.  **Solve $L\mathbf{y} = \mathbf{b}$ for $\mathbf{y}$.** Since $L$ is lower triangular, this is solved efficiently using **[forward substitution](@entry_id:139277)**.
2.  **Solve $U\mathbf{x} = \mathbf{y}$ for $\mathbf{x}$.** Since $U$ is upper triangular, this is solved efficiently using **[backward substitution](@entry_id:168868)**.

As an illustration , suppose we have already found the LU factorization of a matrix $A$ and are given:
$$
L = \begin{pmatrix} 1  0  0 \\ 2  1  0 \\ -1  3  1 \end{pmatrix}, \quad
U = \begin{pmatrix} 2  -1  3 \\ 0  5  -2 \\ 0  0  -1 \end{pmatrix}, \quad
\mathbf{b} = \begin{pmatrix} 8 \\ 21 \\ -2 \end{pmatrix}
$$
First, we solve $L\mathbf{y} = \mathbf{b}$:
$y_1 = 8$
$2y_1 + y_2 = 21 \implies 16 + y_2 = 21 \implies y_2 = 5$
$-y_1 + 3y_2 + y_3 = -2 \implies -8 + 15 + y_3 = -2 \implies y_3 = -9$.
So, $\mathbf{y} = \begin{pmatrix} 8 \\ 5 \\ -9 \end{pmatrix}$.

Next, we solve $U\mathbf{x} = \mathbf{y}$:
$-x_3 = -9 \implies x_3 = 9$
$5x_2 - 2x_3 = 5 \implies 5x_2 - 18 = 5 \implies x_2 = \frac{23}{5}$
$2x_1 - x_2 + 3x_3 = 8 \implies 2x_1 - \frac{23}{5} + 27 = 8 \implies x_1 = -\frac{36}{5}$.
The solution is $\mathbf{x} = \begin{pmatrix} -36/5 \\ 23/5 \\ 9 \end{pmatrix}$.

The primary advantage of LU factorization is that the computationally expensive part (the $O(n^3)$ factorization of $A$) is done only once. If we need to solve the system for many different right-hand side vectors $\mathbf{b}$, each subsequent solution only requires the two $O(n^2)$ substitution steps, which is much faster.

### Sensitivity and Conditioning

The solution to a system of linear equations can be highly sensitive to small changes in the input data. The concept of **conditioning** measures this sensitivity. A system is **well-conditioned** if small perturbations in $A$ or $\mathbf{b}$ lead to small changes in the solution $\mathbf{x}$. A system is **ill-conditioned** if small perturbations can cause large changes in the solution.

Geometrically, in two dimensions, an [ill-conditioned system](@entry_id:142776) corresponds to two lines that are nearly parallel. Their intersection point is poorly defined; a tiny shift in one line can cause the intersection point to move dramatically.

Consider the system :
$$
\begin{pmatrix} 1.0  0.99 \\ 0.99  0.98 \end{pmatrix} \mathbf{x} = \begin{pmatrix} 1.99 \\ 1.97 \end{pmatrix}
$$
The solution to this system is $\mathbf{x}_{orig} = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$. Now, let's introduce a very small perturbation to the vector $\mathbf{b}$, changing $b_2$ from $1.97$ to $1.98$. The new system is:
$$
\begin{pmatrix} 1.0  0.99 \\ 0.99  0.98 \end{pmatrix} \mathbf{x} = \begin{pmatrix} 1.99 \\ 1.98 \end{pmatrix}
$$
The change in the input vector is $\Delta\mathbf{b} = \begin{pmatrix} 0 \\ 0.01 \end{pmatrix}$, which is very small. The solution to the new system is $\mathbf{x}_{new} = A^{-1}\mathbf{b}'$. The change in the solution is $\Delta\mathbf{x} = \mathbf{x}_{new} - \mathbf{x}_{orig} = A^{-1}(\mathbf{b}' - \mathbf{b}) = A^{-1}\Delta\mathbf{b}$. The inverse of this matrix is:
$$
A^{-1} = \frac{1}{-0.0001} \begin{pmatrix} 0.98  -0.99 \\ -0.99  1.0 \end{pmatrix} = \begin{pmatrix} -9800  9900 \\ 9900  -10000 \end{pmatrix}
$$
The large entries in the inverse are a hallmark of ill-conditioning. The change in the solution is:
$$
\Delta\mathbf{x} = \begin{pmatrix} -9800  9900 \\ 9900  -10000 \end{pmatrix} \begin{pmatrix} 0 \\ 0.01 \end{pmatrix} = \begin{pmatrix} 99 \\ -100 \end{pmatrix}
$$
A tiny change of $0.01$ in one component of $\mathbf{b}$ has produced a massive change in the solution vector $\mathbf{x}$. The Euclidean norm of this change is $||\Delta\mathbf{x}||_2 = \sqrt{99^2 + (-100)^2} \approx 141$. This extreme sensitivity means that in the presence of even small measurement or rounding errors, the computed solution for an [ill-conditioned system](@entry_id:142776) may be meaningless.

### Iterative Methods for Solving Linear Systems

For very large and sparse systems (where most entries in $A$ are zero), direct methods like Gaussian elimination can be inefficient or infeasible. They tend to "fill in" the zeros, destroying the sparsity and requiring immense memory and computation. **Iterative methods** provide an alternative by starting with an initial guess for the solution and successively refining it until it converges to the true solution.

#### The Fixed-Point Iteration Framework

Many [iterative methods](@entry_id:139472) are based on rewriting the system $A\mathbf{x} = \mathbf{b}$ into an equivalent **fixed-point** form:
$$
\mathbf{x} = T\mathbf{x} + \mathbf{c}
$$
where $T$ is an **[iteration matrix](@entry_id:637346)** and $\mathbf{c}$ is a constant vector. Once in this form, we can define an iterative scheme. Starting with an initial guess $\mathbf{x}^{(0)}$, we generate a sequence of approximations:
$$
\mathbf{x}^{(k+1)} = T\mathbf{x}^{(k)} + \mathbf{c} \quad \text{for } k=0, 1, 2, \dots
$$
If this sequence converges, its limit will be the solution to the original system.

A common way to derive such a scheme is to split the matrix $A$ into its diagonal, strictly lower triangular, and strictly upper triangular parts. Let $A = D - L - U$, where $D$ is the diagonal of $A$, $-L$ is the strictly lower triangular part of $A$, and $-U$ is the strictly upper triangular part of $A$. The system $A\mathbf{x}=\mathbf{b}$ becomes $(D-L-U)\mathbf{x} = \mathbf{b}$.

The **Jacobi method** is derived by rearranging this to isolate the term with the diagonal matrix $D$:
$$
D\mathbf{x} = (L+U)\mathbf{x} + \mathbf{b}
$$
Assuming $D$ is invertible (i.e., no diagonal entries are zero), we can multiply by $D^{-1}$:
$$
\mathbf{x} = D^{-1}(L+U)\mathbf{x} + D^{-1}\mathbf{b}
$$
This is now in the fixed-point form $\mathbf{x} = T\mathbf{x} + \mathbf{c}$, with the Jacobi iteration matrix $T_J = D^{-1}(L+U)$ and constant vector $\mathbf{c}_J = D^{-1}\mathbf{b}$ .

#### Convergence of Iterative Methods

The crucial question for an [iterative method](@entry_id:147741) is whether the sequence $\mathbf{x}^{(k)}$ converges to the correct solution. The theoretical condition for convergence is that the **spectral radius** (the maximum absolute value of the eigenvalues) of the iteration matrix $T$ must be less than 1: $\rho(T) \lt 1$.

Calculating the spectral radius can be as difficult as solving the system itself. Fortunately, there are simpler, [sufficient conditions](@entry_id:269617) that can be checked directly from the matrix $A$. One of the most important is **[strict diagonal dominance](@entry_id:154277)**. An $n \times n$ matrix $A$ is strictly [diagonally dominant](@entry_id:748380) if, for every row, the absolute value of the diagonal element is strictly greater than the sum of the absolute values of all other elements in that row.
$$
|a_{ii}| > \sum_{j \neq i} |a_{ij}| \quad \text{for all } i = 1, \dots, n
$$
A key theorem states that if a matrix $A$ is strictly diagonally dominant, then both the Jacobi and the **Gauss-Seidel** methods (a related iterative scheme) are guaranteed to converge to the unique solution of $A\mathbf{x}=\mathbf{b}$ for any starting vector $\mathbf{x}^{(0)}$.

Let's check this condition for the following matrix :
$$
A = \begin{pmatrix} 9  -2  3 \\ 1  -5  2 \\ -4  1  6 \end{pmatrix}
$$
*   **Row 1:** $|9| > |-2| + |3| \implies 9 > 5$. (True)
*   **Row 2:** $|-5| > |1| + |2| \implies 5 > 3$. (True)
*   **Row 3:** $|6| > |-4| + |1| \implies 6 > 5$. (True)

Since the condition holds for every row, the matrix is strictly [diagonally dominant](@entry_id:748380). Therefore, we can say with certainty, without running the iteration, that the Gauss-Seidel method (and the Jacobi method) will converge for any system involving this [coefficient matrix](@entry_id:151473). This provides a powerful and practical a priori check for the reliability of [iterative solvers](@entry_id:136910).