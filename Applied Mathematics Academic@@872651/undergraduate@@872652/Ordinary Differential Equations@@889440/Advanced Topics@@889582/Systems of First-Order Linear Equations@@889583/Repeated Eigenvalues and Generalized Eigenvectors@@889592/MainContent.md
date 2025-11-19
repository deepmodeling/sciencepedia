## Introduction
The study of linear [systems of ordinary differential equations](@entry_id:266774), represented as $\mathbf{x}' = A\mathbf{x}$, is a cornerstone of [applied mathematics](@entry_id:170283). The solution hinges on understanding the [eigenvalues and eigenvectors](@entry_id:138808) of the matrix $A$. In many cases, a full set of linearly independent eigenvectors provides a straightforward path to the general solution. However, a significant challenge arises when an eigenvalue is repeated and the matrix fails to produce a corresponding number of independent eigenvectors. This situation, known as having a "defective" matrix, leaves a gap in our [solution set](@entry_id:154326) and requires a more advanced approach.

This article provides a comprehensive guide to navigating and solving these systems. Over the next three chapters, you will develop a robust understanding of this crucial topic.
*   The first chapter, **Principles and Mechanisms**, delves into the algebraic challenge of [defective matrices](@entry_id:194492). It formally introduces the concept of [generalized eigenvectors](@entry_id:152349) and Jordan chains, demonstrating how to construct the missing [linearly independent solutions](@entry_id:185441). It also explores the elegant [matrix exponential](@entry_id:139347) method as an alternative path to the complete solution.
*   The second chapter, **Applications and Interdisciplinary Connections**, shifts focus to the real world, revealing how [repeated eigenvalues](@entry_id:154579) model critical phenomena. You will see how the mathematical structure of [generalized eigenvectors](@entry_id:152349) describes physical behaviors like [critical damping](@entry_id:155459) in mechanical and electrical systems and has profound implications in control theory.
*   Finally, **Hands-On Practices** will offer a curated set of problems to apply these techniques, solidifying your ability to solve systems involving [repeated eigenvalues](@entry_id:154579) from start to finish.

We begin by examining the underlying principles that necessitate this extended theory and the mechanisms used to forge new solutions when standard methods fall short.

## Principles and Mechanisms

In the study of linear [systems of ordinary differential equations](@entry_id:266774), $\mathbf{x}' = A\mathbf{x}$, the eigenvalues and eigenvectors of the matrix $A$ are paramount. When $A$ possesses a full set of linearly independent eigenvectors, these form a basis for the solution space, and the general solution can be constructed as a [linear combination](@entry_id:155091) of simple exponential solutions, $\mathbf{x}(t) = \mathbf{v}e^{\lambda t}$. However, a complication arises when the number of [linearly independent](@entry_id:148207) eigenvectors is insufficient to form a basis. This chapter delves into the principles and mechanisms for handling such cases, which are characterized by [repeated eigenvalues](@entry_id:154579).

### The Challenge of Defective Matrices

The foundation of [solving linear systems](@entry_id:146035) rests on our ability to find $n$ [linearly independent solutions](@entry_id:185441) for an $n \times n$ system. The character of the eigenvalues of the [coefficient matrix](@entry_id:151473) $A$ dictates the path to finding these solutions. A critical distinction arises when an eigenvalue appears more than once as a root of the characteristic equation, $\det(A - \lambda I) = 0$.

We define two types of [multiplicity](@entry_id:136466) for an eigenvalue $\lambda$:

1.  **Algebraic Multiplicity**: The number of times $\lambda$ appears as a root of the characteristic polynomial.
2.  **Geometric Multiplicity**: The dimension of the [eigenspace](@entry_id:150590) corresponding to $\lambda$, which is the number of [linearly independent](@entry_id:148207) eigenvectors associated with it. This is calculated as $\dim(\ker(A - \lambda I))$.

For any eigenvalue, the [geometric multiplicity](@entry_id:155584) is always less than or equal to its [algebraic multiplicity](@entry_id:154240). When the geometric multiplicity of an eigenvalue is strictly less than its algebraic multiplicity, we say the matrix $A$ is **defective**. The "defect" is precisely the inability to find a full basis of eigenvectors for the vector space. This situation is not merely a mathematical curiosity; it arises in the models of various physical systems.

Consider a [chemical engineering](@entry_id:143883) process with two identical, well-stirred tanks containing a brine solution [@problem_id:2196283]. The amount of salt in each tank, $x_1(t)$ and $x_2(t)$, is modeled by a system $\mathbf{x}' = A\mathbf{x}$ with the matrix $A = k \begin{pmatrix} -1  0 \\ 1  -1 \end{pmatrix}$. The characteristic polynomial is $\det(A - \lambda I) = (-k - \lambda)^2 = 0$. This gives a single eigenvalue $\lambda = -k$ with an **algebraic multiplicity of 2**.

To find the [geometric multiplicity](@entry_id:155584), we examine the eigenspace by solving $(A - (-k)I)\mathbf{v} = \mathbf{0}$, which is $(A + kI)\mathbf{v} = \mathbf{0}$:
$$
k \begin{pmatrix} 0  0 \\ 1  0 \end{pmatrix} \begin{pmatrix} v_1 \\ v_2 \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}
$$
This equation simplifies to $kv_1 = 0$, which implies $v_1 = 0$. The vector $v_2$ can be any non-zero value. Thus, all eigenvectors are scalar multiples of $\begin{pmatrix} 0 \\ 1 \end{pmatrix}$. Since the eigenspace is spanned by a single vector, its dimension is 1. The **[geometric multiplicity](@entry_id:155584) is 1**.

Since the geometric multiplicity (1) is less than the algebraic multiplicity (2), the matrix $A$ is defective. We can find only one solution of the form $\mathbf{x}(t) = \mathbf{v}e^{-kt}$. This is insufficient to describe the two-dimensional state of the system. We must develop a method to find a second, [linearly independent solution](@entry_id:174476).

### Forging New Solutions with Generalized Eigenvectors

When faced with a [defective matrix](@entry_id:153580), our standard ansatz, $\mathbf{x}(t) = \mathbf{v}e^{\lambda t}$, proves insufficient. To discover the form of a second solution, we can draw an analogy from scalar constant-coefficient ODEs. For an equation like $y'' - 2\lambda y' + \lambda^2 y = 0$, the characteristic equation has a repeated root $r = \lambda$, yielding solutions $e^{\lambda t}$ and $t e^{\lambda t}$. The presence of the term $t e^{\lambda t}$ suggests that a similar structure might exist for systems of ODEs.

Let's explore this intuition by proposing a solution of the form:
$$
\mathbf{x}(t) = t e^{\lambda t} \mathbf{v}_1 + e^{\lambda t} \mathbf{v}_2
$$
where $\mathbf{v}_1$ and $\mathbf{v}_2$ are constant vectors to be determined. We substitute this into the differential equation $\mathbf{x}' = A\mathbf{x}$ [@problem_id:2196297].

First, we differentiate our proposed solution with respect to $t$:
$$
\mathbf{x}'(t) = (e^{\lambda t} + \lambda t e^{\lambda t})\mathbf{v}_1 + \lambda e^{\lambda t}\mathbf{v}_2 = t e^{\lambda t} (\lambda \mathbf{v}_1) + e^{\lambda t} (\mathbf{v}_1 + \lambda \mathbf{v}_2)
$$
Next, we substitute $\mathbf{x}(t)$ and $\mathbf{x}'(t)$ into the system equation:
$$
t e^{\lambda t} (\lambda \mathbf{v}_1) + e^{\lambda t} (\mathbf{v}_1 + \lambda \mathbf{v}_2) = A(t e^{\lambda t} \mathbf{v}_1 + e^{\lambda t} \mathbf{v}_2) = t e^{\lambda t} (A\mathbf{v}_1) + e^{\lambda t} (A\mathbf{v}_2)
$$
For this equality to hold for all $t$, the vector coefficients of the [linearly independent](@entry_id:148207) functions $t e^{\lambda t}$ and $e^{\lambda t}$ must be equal.

1.  Equating coefficients of $t e^{\lambda t}$:
    $$ \lambda \mathbf{v}_1 = A\mathbf{v}_1 \quad \implies \quad (A - \lambda I)\mathbf{v}_1 = \mathbf{0} $$
    This is the familiar definition of an eigenvector. Thus, $\mathbf{v}_1$ must be a standard eigenvector corresponding to the eigenvalue $\lambda$.

2.  Equating coefficients of $e^{\lambda t}$:
    $$ \mathbf{v}_1 + \lambda \mathbf{v}_2 = A\mathbf{v}_2 \quad \implies \quad (A - \lambda I)\mathbf{v}_2 = \mathbf{v}_1 $$
    This is a new and crucial relationship. The vector $\mathbf{v}_2$ is not an eigenvector itself (since $(A - \lambda I)\mathbf{v}_2 \neq \mathbf{0}$), but it is mapped to the eigenvector $\mathbf{v}_1$ by the operator $(A - \lambda I)$. This vector $\mathbf{v}_2$ is called a **[generalized eigenvector](@entry_id:154062) of rank 2**.

This pair of vectors, $\{\mathbf{v}_1, \mathbf{v}_2\}$, linked by the operator $(A - \lambda I)$, forms a **Jordan chain** of length 2. The process to find them is sequential: first, find an eigenvector $\mathbf{v}_1$; then, solve the system $(A - \lambda I)\mathbf{v}_2 = \mathbf{v}_1$ to find the [generalized eigenvector](@entry_id:154062) $\mathbf{v}_2$. For instance, in a model of a critically damped magnetic levitation device with matrix $A = \begin{pmatrix} 0  1 \\ -4  -4 \end{pmatrix}$, the repeated eigenvalue is $\lambda=-2$ with eigenvector $\mathbf{v}_1 = \begin{pmatrix} 1 \\ -2 \end{pmatrix}$ [@problem_id:2196313]. To find $\mathbf{v}_2$, we solve $(A+2I)\mathbf{v}_2 = \mathbf{v}_1$:
$$
\begin{pmatrix} 2  1 \\ -4  -2 \end{pmatrix} \mathbf{v}_2 = \begin{pmatrix} 1 \\ -2 \end{pmatrix}
$$
This system has infinitely many solutions. A common practice is to choose one by setting a component to a convenient value (e.g., zero), which yields a unique vector such as $\mathbf{v}_2 = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$.

The concept can be extended. A vector $\mathbf{w}$ is a **[generalized eigenvector](@entry_id:154062) of rank $k$** if $(A - \lambda I)^k \mathbf{w} = \mathbf{0}$ and $(A - \lambda I)^{k-1} \mathbf{w} \neq \mathbf{0}$ [@problem_id:2196320]. In this framework, a standard eigenvector is a [generalized eigenvector](@entry_id:154062) of rank 1. Our vector $\mathbf{v}_2$ is of rank 2 because $(A - \lambda I)^2 \mathbf{v}_2 = (A - \lambda I)\mathbf{v}_1 = \mathbf{0}$, while $(A - \lambda I)^1 \mathbf{v}_2 = \mathbf{v}_1 \neq \mathbf{0}$.

### Constructing General Solutions for Defective Systems

For a $2 \times 2$ defective system with repeated eigenvalue $\lambda$, we now have two [linearly independent solutions](@entry_id:185441):
$$
\mathbf{x}_1(t) = e^{\lambda t} \mathbf{v}_1
$$
$$
\mathbf{x}_2(t) = t e^{\lambda t} \mathbf{v}_1 + e^{\lambda t} \mathbf{v}_2 = e^{\lambda t} (t\mathbf{v}_1 + \mathbf{v}_2)
$$
The general solution is a [linear combination](@entry_id:155091) of these two:
$$
\mathbf{x}(t) = c_1 \mathbf{x}_1(t) + c_2 \mathbf{x}_2(t) = c_1 e^{\lambda t}\mathbf{v}_1 + c_2 e^{\lambda t}(t\mathbf{v}_1 + \mathbf{v}_2)
$$
This structure naturally extends to cases with longer Jordan chains. Suppose a $3 \times 3$ matrix $A$ has an eigenvalue $\lambda$ with algebraic multiplicity 3 but geometric multiplicity 1. This requires a Jordan chain of length 3, $\{\mathbf{v}_1, \mathbf{v}_2, \mathbf{v}_3\}$, defined by:
$$
(A - \lambda I)\mathbf{v}_1 = \mathbf{0}
$$
$$
(A - \lambda I)\mathbf{v}_2 = \mathbf{v}_1
$$
$$
(A - \lambda I)\mathbf{v}_3 = \mathbf{v}_2
$$
A [fundamental theorem of linear algebra](@entry_id:190797) guarantees that a set of vectors forming a Jordan chain is always linearly independent, and can therefore serve as a basis. The three [linearly independent solutions](@entry_id:185441) derived from this chain are:
$$
\mathbf{x}_1(t) = e^{\lambda t} \mathbf{v}_1
$$
$$
\mathbf{x}_2(t) = e^{\lambda t} (t\mathbf{v}_1 + \mathbf{v}_2)
$$
$$
\mathbf{x}_3(t) = e^{\lambda t} \left(\frac{t^2}{2} \mathbf{v}_1 + t\mathbf{v}_2 + \mathbf{v}_3\right)
$$
The general solution is then $\mathbf{x}(t) = c_1 \mathbf{x}_1(t) + c_2 \mathbf{x}_2(t) + c_3 \mathbf{x}_3(t)$ [@problem_id:2196275]. The appearance of polynomial terms in $t$ (i.e., $t$ and $t^2/2$) is a hallmark of solutions associated with Jordan chains.

### The Matrix Exponential for Defective Systems

A more powerful and systematic way to derive these solutions is through the matrix exponential, $e^{At}$, where the general solution to an [initial value problem](@entry_id:142753) is given by $\mathbf{x}(t) = e^{At}\mathbf{x}(0)$. While calculating $e^{At}$ from its [power series](@entry_id:146836) definition is often impractical, we can exploit the structure of [defective matrices](@entry_id:194492) to simplify the process.

Let $A$ be a matrix with a repeated eigenvalue $\lambda$. We can decompose $A$ as:
$$
A = \lambda I + (A - \lambda I) = \lambda I + N
$$
The matrix $N = A - \lambda I$ has a special property: it is **nilpotent**, meaning that for some integer $k \ge 1$, $N^k = \mathbf{0}$. The smallest such $k$ is the size of the largest Jordan block for $\lambda$. For a $2 \times 2$ [defective matrix](@entry_id:153580), it can be shown that $(A-\lambda I)^2$ is the [zero matrix](@entry_id:155836), so $N^2 = \mathbf{0}$ [@problem_id:2196302].

Since the identity matrix $I$ commutes with any matrix, we have $e^{At} = e^{(\lambda I + N)t} = e^{\lambda t I}e^{Nt} = e^{\lambda t}I e^{Nt} = e^{\lambda t}e^{Nt}$. The [power series](@entry_id:146836) for the nilpotent part, $e^{Nt}$, terminates:
$$
e^{Nt} = I + Nt + \frac{(Nt)^2}{2!} + \dots + \frac{(Nt)^{k-1}}{(k-1)!}
$$
For a $2 \times 2$ [defective matrix](@entry_id:153580) where $N^2 = \mathbf{0}$, this series simplifies dramatically:
$$
e^{Nt} = I + Nt
$$
This gives a compact and elegant formula for the matrix exponential:
$$
e^{At} = e^{\lambda t}(I + tN) = e^{\lambda t}(I + t(A - \lambda I))
$$
This formula provides a direct method for solving any $2 \times 2$ defective system. For the chemical process with $A = \begin{pmatrix} 3  2 \\ -2  -1 \end{pmatrix}$ and initial conditions $c(0) = \begin{pmatrix} 1.00 \\ 0.50 \end{pmatrix}$, we found $\lambda=1$ is a repeated eigenvalue [@problem_id:2196302]. The matrix $N = A-I = \begin{pmatrix} 2  2 \\ -2  -2 \end{pmatrix}$. The solution is:
$$
\mathbf{c}(t) = e^{At}\mathbf{c}(0) = e^{t}(I + tN)\mathbf{c}(0) = e^{t} \left( \begin{pmatrix} 1 \\ 0.5 \end{pmatrix} + t \begin{pmatrix} 2  2 \\ -2  -2 \end{pmatrix} \begin{pmatrix} 1 \\ 0.5 \end{pmatrix} \right) = e^{t} \left( \begin{pmatrix} 1 \\ 0.5 \end{pmatrix} + t \begin{pmatrix} 3 \\ -3 \end{pmatrix} \right) = e^t \begin{pmatrix} 1 + 3t \\ 0.5 - 3t \end{pmatrix}
$$
This solution clearly shows the polynomial term $t$ multiplying the exponential, a direct consequence of the matrix's defective nature. The contrast is stark when compared to a non-defective (diagonalizable) matrix with the same repeated eigenvalue, such as $A_2 = \begin{pmatrix} \lambda  0 \\ 0  \lambda \end{pmatrix}$. Here, $N = \mathbf{0}$, so $e^{A_2t} = e^{\lambda t}I$, and the solution is purely exponential, $\mathbf{x}_2(t) = e^{\lambda t}\mathbf{x}_0$, without any terms involving $t$ [@problem_id:2196271].

### Phase Portraits for Repeated Eigenvalues: Proper and Improper Nodes

The algebraic properties of [defective matrices](@entry_id:194492) have profound geometric consequences, which are best visualized in the phase plane for $2 \times 2$ systems. The [equilibrium point](@entry_id:272705) at the origin can be classified based on the eigenvalues of $A$.

When a matrix has a repeated real eigenvalue $\lambda$, the origin is a **node**. The stability is determined by the sign of $\lambda$: asymptotically stable if $\lambda  0$, and unstable if $\lambda > 0$. The distinction between a "proper" and "improper" node depends on the [geometric multiplicity](@entry_id:155584).

*   **Proper Node (or Star Node)**: This occurs when the geometric multiplicity equals the [algebraic multiplicity](@entry_id:154240) (i.e., the matrix is not defective). For a $2 \times 2$ system, this means there are two [linearly independent](@entry_id:148207) eigenvectors. Every vector is an eigenvector, and trajectories are straight lines radiating from (or converging to) the origin. The matrix is a scalar multiple of the identity, $A = \lambda I$.

*   **Improper Node**: This occurs when the matrix is defective. For a $2 \times 2$ system, there is only a one-dimensional eigenspace, spanned by a single eigenvector $\mathbf{v}_1$.
    *   Trajectories corresponding to [initial conditions](@entry_id:152863) on the line spanned by $\mathbf{v}_1$ are straight lines.
    *   All other trajectories are curved. As $t \to \infty$ (for stable nodes, $\lambda  0$) or $t \to -\infty$ (for unstable nodes, $\lambda > 0$), the term in the solution with the highest power of $t$ dominates. In the solution $\mathbf{x}(t) = e^{\lambda t}( (c_1 + c_2 t)\mathbf{v}_1 + c_2 \mathbf{v}_2)$, the vector component becomes parallel to $\mathbf{v}_1$ for large $|t|$.
    *   Consequently, all trajectories approach the origin tangent to the line defined by the eigenvector $\mathbf{v}_1$ [@problem_id:2196290, @problem_id:2196312].

For example, the system with matrix $A = \begin{pmatrix} -2  1 \\ -1  -4 \end{pmatrix}$ has a repeated eigenvalue $\lambda=-3$ and is defective [@problem_id:2196290]. Since $\lambda  0$, the origin is stable. Because the matrix is defective, the trajectories are not all straight lines. This equilibrium is therefore classified as an **asymptotically stable [improper node](@entry_id:164704)**. Similarly, for the system with $A = \begin{pmatrix} -1  -1 \\ 1  -3 \end{pmatrix}$ and $\lambda=-2$, all trajectories approach the origin along the direction of the eigenvector $\mathbf{v}_1 = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$ [@problem_id:2196312].

### A Complete Analysis: Solving with a Jordan Basis

Let's conclude by synthesizing these concepts to solve a more complex initial value problem. Consider a $3 \times 3$ system $\mathbf{x}'=A\mathbf{x}$ where $A$ has a single eigenvalue $\lambda$ with a Jordan chain of length 3, $\{\mathbf{v}_1, \mathbf{v}_2, \mathbf{v}_3\}$. This chain forms a basis for $\mathbb{R}^3$. Any solution $\mathbf{x}(t)$ can be uniquely expressed in this basis:
$$
\mathbf{x}(t) = c_1(t)\mathbf{v}_1 + c_2(t)\mathbf{v}_2 + c_3(t)\mathbf{v}_3
$$
This approach transforms the coupled system for $\mathbf{x}(t)$ into a simpler, uncoupled system for the coordinates $c_i(t)$. Differentiating this expression and substituting into $\mathbf{x}'=A\mathbf{x}$ yields:
$$
c_1'(t)\mathbf{v}_1 + c_2'(t)\mathbf{v}_2 + c_3'(t)\mathbf{v}_3 = c_1(t)A\mathbf{v}_1 + c_2(t)A\mathbf{v}_2 + c_3(t)A\mathbf{v}_3
$$
Using the definitions $A\mathbf{v}_1 = \lambda\mathbf{v}_1$, $A\mathbf{v}_2 = \lambda\mathbf{v}_2 + \mathbf{v}_1$, and $A\mathbf{v}_3 = \lambda\mathbf{v}_3 + \mathbf{v}_2$, we get:
$$
c_1'(t)\mathbf{v}_1 + c_2'(t)\mathbf{v}_2 + c_3'(t)\mathbf{v}_3 = (\lambda c_1(t) + c_2(t))\mathbf{v}_1 + (\lambda c_2(t) + c_3(t))\mathbf{v}_2 + \lambda c_3(t)\mathbf{v}_3
$$
By equating the coefficients of the basis vectors, we obtain a simple triangular system for the coordinates:
$$
\begin{aligned}
c_1'(t) = \lambda c_1(t) + c_2(t) \\
c_2'(t) = \lambda c_2(t) + c_3(t) \\
c_3'(t) = \lambda c_3(t)
\end{aligned}
$$
This system can be solved sequentially from bottom to top. As demonstrated in the analysis of a critically damped electromechanical actuator model [@problem_id:2196303], given [initial conditions](@entry_id:152863) for the coordinates, one can find explicit solutions for $c_1(t)$, $c_2(t)$, and $c_3(t)$ using methods like [variation of constants](@entry_id:196393). For an initial state $\mathbf{x}(0) = c_1(0)\mathbf{v}_1 + c_2(0)\mathbf{v}_2 + c_3(0)\mathbf{v}_3$, the solutions for the coordinates take the form:
$$
\begin{aligned}
c_3(t) = c_3(0)e^{\lambda t} \\
c_2(t) = (c_2(0) + c_3(0)t)e^{\lambda t} \\
c_1(t) = \left(c_1(0) + c_2(0)t + c_3(0)\frac{t^2}{2}\right)e^{\lambda t}
\end{aligned}
$$
This result provides the full time evolution of the system's components along each of the [generalized eigenvector](@entry_id:154062) directions and explicitly reveals the polynomial-in-time growth that characterizes the dynamics of defective systems.