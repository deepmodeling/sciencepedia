## Introduction
Systems of [linear ordinary differential equations](@entry_id:276013) are fundamental to modeling how interconnected quantities evolve over time, appearing in fields from engineering to biology. However, analyzing these systems equation by equation can be cumbersome and obscure the underlying structure. This article addresses this challenge by introducing the powerful framework of linear algebra, which recasts complex systems into a single, elegant [matrix equation](@entry_id:204751): $x'(t) = A(t)x(t) + f(t)$. This transformation is not merely a notational convenience; it unlocks a suite of powerful analytical tools that reveal deep insights into the system's behavior.

Throughout the following chapters, you will gain a comprehensive understanding of this essential technique. In **Principles and Mechanisms**, you will learn how to convert systems of ODEs and single higher-order equations into matrix form, and master the cornerstone eigenvalue method for finding solutions. The chapter will also explore deeper concepts like [diagonalization](@entry_id:147016) and the [matrix exponential](@entry_id:139347). In **Applications and Interdisciplinary Connections**, we will see this theory in action, exploring how it provides crucial insights into real-world problems in [mechanical vibrations](@entry_id:167420), [electrical circuits](@entry_id:267403), and [chemical kinetics](@entry_id:144961). Finally, **Hands-On Practices** will offer a set of targeted problems to help you solidify your skills in applying these concepts.

## Principles and Mechanisms

The study of systems of [linear ordinary differential equations](@entry_id:276013) is foundational to nearly every branch of science and engineering. From [modeling electrical circuits](@entry_id:263743) and [mechanical vibrations](@entry_id:167420) to describing chemical reactions and population dynamics, these systems provide a framework for understanding how multiple interacting quantities evolve over time. While a system of equations can be written and studied component by component, a far more powerful and insightful approach is to employ the language and tools of linear algebra. By representing a linear system in matrix form, we not only achieve a compact and elegant notation but also unlock a rich theoretical structure that simplifies analysis, reveals profound connections between seemingly disparate problems, and provides systematic methods for finding solutions.

### From Systems of Equations to a Single Matrix Equation

A system of [first-order linear differential equations](@entry_id:164869) involves several functions of a single [independent variable](@entry_id:146806) (typically time, $t$), where the derivative of each function is expressed as a [linear combination](@entry_id:155091) of all the functions in the system, plus potentially a term that depends only on $t$.

Consider a general system of $n$ linear first-order ODEs:
$$
\begin{align*}
x_1'(t)  = a_{11}(t)x_1(t) + a_{12}(t)x_2(t) + \dots + a_{1n}(t)x_n(t) + f_1(t) \\
x_2'(t)  = a_{21}(t)x_1(t) + a_{22}(t)x_2(t) + \dots + a_{2n}(t)x_n(t) + f_2(t) \\
\vdots  \\
x_n'(t)  = a_{n1}(t)x_1(t) + a_{n2}(t)x_2(t) + \dots + a_{nn}(t)x_n(t) + f_n(t)
\end{align*}
$$

This cumbersome collection of equations can be elegantly recast into a single [matrix equation](@entry_id:204751). We define the **state vector** $\vec{x}(t)$ and the **forcing vector** $\vec{f}(t)$ as:
$$
\vec{x}(t) = \begin{pmatrix} x_1(t) \\ x_2(t) \\ \vdots \\ x_n(t) \end{pmatrix}, \quad \vec{f}(t) = \begin{pmatrix} f_1(t) \\ f_2(t) \\ \vdots \\ f_n(t) \end{pmatrix}
$$
The coefficients $a_{ij}(t)$ are organized into the **[coefficient matrix](@entry_id:151473)** $A(t)$:
$$
A(t) = \begin{pmatrix}
a_{11}(t) & a_{12}(t) & \dots & a_{1n}(t) \\
a_{21}(t) & a_{22}(t) & \dots & a_{2n}(t) \\
\vdots & \vdots & \ddots & \vdots \\
a_{n1}(t) & a_{n2}(t) & \dots & a_{nn}(t)
\end{pmatrix}
$$
Using the rules of [matrix-vector multiplication](@entry_id:140544), the entire system simplifies to the compact form:
$$
\vec{x}'(t) = A(t)\vec{x}(t) + \vec{f}(t)
$$
If the forcing vector $\vec{f}(t)$ is identically zero, the system is called **homogeneous**. Otherwise, it is **non-homogeneous**. For much of our initial analysis, we will focus on systems with constant coefficients, where the matrix $A$ does not depend on $t$.

For instance, a dynamic system involving three [state variables](@entry_id:138790) might be described by the equations [@problem_id:2185688]:
$$
\begin{aligned}
x_1'(t) & = 5x_1(t) - 7x_3(t) + \cos(t) \\
x_2'(t) & = 2x_1(t) + 4x_2(t) - x_3(t) - t^{3} \\
x_3'(t) & = -3x_1(t) + 6x_2(t) + \exp(-2t)
\end{aligned}
$$
To write this in matrix form, we identify the coefficients of $x_1, x_2,$ and $x_3$ for each equation to form the rows of $A$, and we collect the remaining terms into $\vec{f}(t)$. Notice the coefficient of $x_2$ in the first equation is zero, and the coefficient of $x_3$ in the third equation is zero. This gives:
$$
A = \begin{pmatrix} 5 & 0 & -7 \\ 2 & 4 & -1 \\ -3 & 6 & 0 \end{pmatrix}, \quad \vec{f}(t) = \begin{pmatrix} \cos(t) \\ -t^3 \\ \exp(-2t) \end{pmatrix}
$$

In some physical models, the equations may not be given with the derivatives already isolated. In such cases, algebraic manipulation is required first. Consider a model of two coupled electronic circuits with currents $i_1(t)$ and $i_2(t)$, governed by equations derived from Kirchhoff's Laws [@problem_id:2185682]:
$$
\begin{aligned}
L_1 i_1' + M i_2' + R_1 i_1 & = 0 \\
M i_1' + L_2 i_2' + R_2 i_2 & = 0
\end{aligned}
$$
Here, $L_1, L_2$ are inductances, $R_1, R_2$ are resistances, and $M$ is the [mutual inductance](@entry_id:264504). To express this in the standard form $\vec{i}' = A\vec{i}$, we must first solve for the derivative vector $\vec{i}' = \begin{pmatrix} i_1' \\ i_2' \end{pmatrix}$. We can group the terms to write:
$$
\begin{pmatrix} L_1 & M \\ M & L_2 \end{pmatrix} \begin{pmatrix} i_1' \\ i_2' \end{pmatrix} + \begin{pmatrix} R_1 & 0 \\ 0 & R_2 \end{pmatrix} \begin{pmatrix} i_1 \\ i_2 \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}
$$
Let's call the first matrix $L$ and the second $R$. The system is $L\vec{i}' + R\vec{i} = \vec{0}$. To isolate $\vec{i}'$, we multiply by the inverse of the matrix $L$, provided it exists. For a physical system, the condition $L_1 L_2 - M^2 > 0$ ensures that $\det(L) \neq 0$ and $L$ is invertible. This yields:
$$
\vec{i}' = -L^{-1}R\vec{i}
$$
The [system matrix](@entry_id:172230) is therefore $A = -L^{-1}R$. Performing the [matrix inversion](@entry_id:636005) and multiplication gives the final explicit form of $A$. This example highlights that the conversion to standard form can involve substantive linear algebraic steps.

### Unifying Higher-Order Equations

One of the most significant advantages of the matrix framework is its ability to transform any single $n$-th order linear ODE into an equivalent system of $n$ first-order linear ODEs. This allows us to apply the same systematic solution methods to a much broader class of problems.

The procedure is straightforward. Given an $n$-th order equation in $y(t)$, we define a state vector whose components are $y(t)$ and its first $n-1$ derivatives. Let's illustrate with a ubiquitous example from physics: the [damped harmonic oscillator](@entry_id:276848) [@problem_id:1692322]. The displacement $x(t)$ from equilibrium is governed by the second-order equation:
$$
m \frac{d^2x}{dt^2} + b \frac{dx}{dt} + kx = 0
$$
To convert this to a [first-order system](@entry_id:274311), we define a state vector with two components: the position and the velocity. Let $v_1(t) = x(t)$ and $v_2(t) = x'(t)$. We now need to find equations for $v_1'$ and $v_2'$. The first is immediate from our definition:
$$
v_1' = \frac{d}{dt}(x) = x' = v_2
$$
For the second, we have $v_2' = \frac{d}{dt}(x') = x''$. We find an expression for $x''$ from the original ODE:
$$
x'' = -\frac{k}{m}x - \frac{b}{m}x'
$$
Substituting our [state variables](@entry_id:138790) $v_1$ and $v_2$ gives:
$$
v_2' = -\frac{k}{m}v_1 - \frac{b}{m}v_2
$$
We can now write these two first-order equations in matrix form:
$$
\frac{d}{dt}\begin{pmatrix} v_1 \\ v_2 \end{pmatrix} = \begin{pmatrix} 0 & 1 \\ -\frac{k}{m} & -\frac{b}{m} \end{pmatrix} \begin{pmatrix} v_1 \\ v_2 \end{pmatrix}
$$
This technique is completely general. For a third-order equation like $y''' + p(t)y'' + q(t)y = 0$ [@problem_id:2185680], we define the [state vector](@entry_id:154607) $\vec{x}(t) = \begin{pmatrix} y(t) \\ y'(t) \\ y''(t) \end{pmatrix}$. The derivatives of the components are:
$$
\begin{aligned}
x_1' = y' = x_2 \\
x_2' = y'' = x_3 \\
x_3' = y''' = -q(t)y - p(t)y'' = -q(t)x_1 - p(t)x_3
\end{aligned}
$$
The corresponding matrix system is:
$$
\vec{x}' = \begin{pmatrix} 0 & 1 & 0 \\ 0 & 0 & 1 \\ -q(t) & 0 & -p(t) \end{pmatrix} \vec{x}
$$
The resulting [coefficient matrix](@entry_id:151473) is an example of a **companion matrix**. This pattern—ones on the superdiagonal and coefficients in the last row—holds for any $n$-th order linear ODE, providing a universal bridge from higher-order equations to [first-order systems](@entry_id:147467).

### The Superposition Principle and General Solutions

For a homogeneous linear system $\vec{x}' = A\vec{x}$, the set of all possible solutions forms a vector space. This is the essence of the **Principle of Superposition**. It states that if $\vec{x}_1(t)$ and $\vec{x}_2(t)$ are both solutions to the system, then any linear combination of them, $\vec{x}(t) = c_1\vec{x}_1(t) + c_2\vec{x}_2(t)$ for any scalar constants $c_1$ and $c_2$, is also a solution. This can be easily verified by substitution:
$$
\frac{d}{dt}(c_1\vec{x}_1 + c_2\vec{x}_2) = c_1\vec{x}_1' + c_2\vec{x}_2' = c_1(A\vec{x}_1) + c_2(A\vec{x}_2) = A(c_1\vec{x}_1 + c_2\vec{x}_2)
$$
This principle is immensely powerful. For an $n$-dimensional system, if we can find a set of $n$ [linearly independent solutions](@entry_id:185441), $\{\vec{x}_1(t), \vec{x}_2(t), \dots, \vec{x}_n(t)\}$, called a **[fundamental set of solutions](@entry_id:177810)**, then the **general solution** can be written as their [linear combination](@entry_id:155091):
$$
\vec{x}(t) = c_1\vec{x}_1(t) + c_2\vec{x}_2(t) + \dots + c_n\vec{x}_n(t)
$$
The constants $c_1, \dots, c_n$ are determined by imposing an initial condition, $\vec{x}(t_0) = \vec{x}_0$.

Suppose we are given that $\vec{x}_1(t) = \begin{pmatrix} \exp(-3t) \\ \exp(-3t) \end{pmatrix}$ and $\vec{x}_2(t) = \begin{pmatrix} \exp(t) \\ -\exp(t) \end{pmatrix}$ are two solutions to a $2 \times 2$ [homogeneous system](@entry_id:150411) [@problem_id:2185684]. The general solution is:
$$
\vec{x}(t) = c_1 \begin{pmatrix} \exp(-3t) \\ \exp(-3t) \end{pmatrix} + c_2 \begin{pmatrix} \exp(t) \\ -\exp(t) \end{pmatrix}
$$
To find the unique solution satisfying the initial condition $\vec{x}(0) = \begin{pmatrix} 3 \\ 1 \end{pmatrix}$, we substitute $t=0$:
$$
\begin{pmatrix} 3 \\ 1 \end{pmatrix} = c_1 \begin{pmatrix} 1 \\ 1 \end{pmatrix} + c_2 \begin{pmatrix} 1 \\ -1 \end{pmatrix} = \begin{pmatrix} c_1 + c_2 \\ c_1 - c_2 \end{pmatrix}
$$
This gives a simple system of algebraic equations for $c_1$ and $c_2$, which we can solve to find the specific constants for our [particular solution](@entry_id:149080).

### Solving Systems with the Eigenvalue Method

The [superposition principle](@entry_id:144649) guarantees that if we find enough independent solutions, we can construct any solution. But how do we find these [fundamental solutions](@entry_id:184782) in the first place? The answer lies in a beautiful connection to the linear algebra concept of eigenvalues and eigenvectors.

Let's consider the constant-coefficient [homogeneous system](@entry_id:150411) $\vec{x}' = A\vec{x}$. We seek solutions that have a simple [exponential time](@entry_id:142418) dependence, inspired by the scalar equation $x' = \lambda x$, whose solution is $x(t) = C e^{\lambda t}$. Let's hypothesize a solution of the form:
$$
\vec{x}(t) = \vec{v} e^{\lambda t}
$$
where $\vec{v}$ is a constant vector and $\lambda$ is a scalar constant. Differentiating this gives $\vec{x}'(t) = \lambda \vec{v} e^{\lambda t}$. Substituting our proposed solution into the ODE system yields:
$$
\lambda \vec{v} e^{\lambda t} = A (\vec{v} e^{\lambda t})
$$
Since $e^{\lambda t}$ is a non-zero scalar, we can divide it out:
$$
\lambda \vec{v} = A \vec{v}
$$
This is the defining equation for an **eigenvalue** $\lambda$ and its corresponding **eigenvector** $\vec{v}$ of the matrix $A$. This is a profound result: if we can find the eigenvalues and eigenvectors of the [coefficient matrix](@entry_id:151473) $A$, we can immediately construct solutions to the system of differential equations. Specifically, for each eigenpair $(\lambda, \vec{v})$, the vector function $\vec{x}(t) = \vec{v}e^{\lambda t}$ is a solution.

If an $n \times n$ matrix $A$ has $n$ [linearly independent](@entry_id:148207) eigenvectors $\vec{v}_1, \dots, \vec{v}_n$ with corresponding eigenvalues $\lambda_1, \dots, \lambda_n$ (which is guaranteed if the eigenvalues are all distinct), then we have found a [fundamental set of solutions](@entry_id:177810):
$$
\{ \vec{v}_1 e^{\lambda_1 t}, \vec{v}_2 e^{\lambda_2 t}, \dots, \vec{v}_n e^{\lambda_n t} \}
$$
The general solution is then:
$$
\vec{x}(t) = c_1 \vec{v}_1 e^{\lambda_1 t} + c_2 \vec{v}_2 e^{\lambda_2 t} + \dots + c_n \vec{v}_n e^{\lambda_n t}
$$
This "eigenvalue method" is a cornerstone of [solving linear systems](@entry_id:146035). For example, if we are told that for a matrix $A$, the vector $\vec{v} = \begin{pmatrix} 2 \\ 1 \end{pmatrix}$ and scalar $\lambda=3$ satisfy $A\vec{v}=\lambda\vec{v}$ [@problem_id:2185732], we don't even need to know the entries of $A$ to construct a solution. Based on our derivation, we know immediately that $\vec{x}(t) = \begin{pmatrix} 2 \\ 1 \end{pmatrix} e^{3t}$ is a solution to $\vec{x}'=A\vec{x}$.

As a comprehensive example, consider solving the initial value problem for the system $\vec{x}' = A\vec{x}$ where $A = \begin{pmatrix} -2 & 4 & 1 \\ -1 & 3 & 1 \\ -4 & 4 & 3 \end{pmatrix}$ and $\vec{x}(0) = \begin{pmatrix} 2 \\ 1 \\ 2 \end{pmatrix}$ [@problem_id:2185672].
1.  **Find Eigenvalues:** We solve the characteristic equation $\det(A - \lambda I) = 0$. This yields a cubic polynomial in $\lambda$, which for this matrix is $(\lambda-2)(\lambda-3)(\lambda+1)=0$. The eigenvalues are $\lambda_1=2$, $\lambda_2=3$, and $\lambda_3=-1$.
2.  **Find Eigenvectors:** For each eigenvalue, we solve the system $(A-\lambda I)\vec{v} = \vec{0}$ to find the corresponding eigenvector. This yields $\vec{v}_1 = \begin{pmatrix} 1 \\ 1 \\ 0 \end{pmatrix}$, $\vec{v}_2 = \begin{pmatrix} 1 \\ 1 \\ 1 \end{pmatrix}$, and $\vec{v}_3 = \begin{pmatrix} 1 \\ 0 \\ 1 \end{pmatrix}$.
3.  **Form General Solution:** The general solution is $\vec{x}(t) = c_1\vec{v}_1 e^{2t} + c_2\vec{v}_2 e^{3t} + c_3\vec{v}_3 e^{-t}$.
4.  **Apply Initial Condition:** Setting $t=0$ and equating to $\vec{x}(0)$ gives a system of linear equations for $c_1, c_2, c_3$. Solving this system provides the unique constants for the particular solution.

### A Deeper Perspective: Decoupling and the Matrix Exponential

The success of the eigenvalue method is not a coincidence; it reflects a deep structural property of linear systems.

#### Decoupling through Diagonalization

Imagine if our [coefficient matrix](@entry_id:151473) $A$ were a diagonal matrix, $D$.
$$
A = D = \begin{pmatrix} \lambda_1 & 0 & \dots \\ 0 & \lambda_2 & \\ \vdots & & \ddots \end{pmatrix}
$$
The system $\vec{x}' = D\vec{x}$ would then be:
$$
\begin{aligned}
x_1' = \lambda_1 x_1 \\
x_2' = \lambda_2 x_2 \\
 \vdots
\end{aligned}
$$
This is a **decoupled** system. Each equation is a simple, independent scalar ODE whose solution is $x_i(t) = c_i e^{\lambda_i t}$. The system is trivial to solve.

What if $A$ is not diagonal, but is **diagonalizable**? This means there exists an invertible matrix $P$ such that $A = PDP^{-1}$, or equivalently, $D = P^{-1}AP$, where $D$ is a diagonal matrix. The columns of this matrix $P$ are precisely the linearly independent eigenvectors of $A$, and the diagonal entries of $D$ are the corresponding eigenvalues.

We can use this property to decouple the original system. Let's introduce a [change of variables](@entry_id:141386) $\vec{x}(t) = P\vec{y}(t)$ [@problem_id:2185690]. Substituting this into $\vec{x}' = A\vec{x}$:
$$
(P\vec{y})' = A(P\vec{y}) \implies P\vec{y}' = AP\vec{y}
$$
Multiplying on the left by $P^{-1}$, we get:
$$
\vec{y}' = (P^{-1}AP)\vec{y} \implies \vec{y}' = D\vec{y}
$$
We have transformed the original coupled system in the $\vec{x}$ coordinates into a simple, decoupled system in the $\vec{y}$ coordinates! The solution for $\vec{y}(t)$ is trivial to write down. To find the solution for our original variable $\vec{x}(t)$, we simply transform back: $\vec{x}(t) = P\vec{y}(t)$. This reveals the true nature of the eigenvalue method: it is a [coordinate transformation](@entry_id:138577) into the system's "natural" basis (the eigenvectors), where the dynamics are elementary.

#### The Matrix Exponential

There is an even more formal and powerful way to express the solution to $\vec{x}'=A\vec{x}$. For the scalar case $x'=ax$ with initial condition $x(0)=x_0$, the solution is $x(t) = e^{at}x_0$. We can define a matrix analogue, the **[matrix exponential](@entry_id:139347)**, $e^{At}$, using the same [power series expansion](@entry_id:273325):
$$
e^{At} = I + At + \frac{A^2t^2}{2!} + \frac{A^3t^3}{3!} + \dots = \sum_{k=0}^{\infty} \frac{(At)^k}{k!}
$$
This series can be shown to converge for any square matrix $A$. One of its most important properties is revealed by differentiating the series term-by-term with respect to $t$ [@problem_id:2185727]:
$$
\frac{d}{dt} e^{At} = \frac{d}{dt} \sum_{k=0}^{\infty} \frac{A^k t^k}{k!} = \sum_{k=1}^{\infty} \frac{A^k (k t^{k-1})}{k!} = \sum_{k=1}^{\infty} \frac{A^k t^{k-1}}{(k-1)!}
$$
Factoring out one matrix $A$ and re-indexing the sum (with $m = k-1$) gives:
$$
\frac{d}{dt} e^{At} = A \left( \sum_{m=0}^{\infty} \frac{A^m t^m}{m!} \right) = A e^{At}
$$
This proves that the [matrix function](@entry_id:751754) $\Psi(t) = e^{At}$ is a **[fundamental matrix](@entry_id:275638) solution** to the matrix differential equation $\Psi' = A\Psi$. Consequently, the unique solution to the [initial value problem](@entry_id:142753) $\vec{x}'=A\vec{x}$ with $\vec{x}(0)=\vec{x}_0$ is given concisely by:
$$
\vec{x}(t) = e^{At}\vec{x}_0
$$
The matrix exponential provides a complete, formal solution. Computing it can be challenging, but if $A$ is diagonalizable ($A=PDP^{-1}$), it simplifies greatly to $e^{At} = P e^{Dt} P^{-1}$, where $e^{Dt}$ is a diagonal matrix with entries $e^{\lambda_i t}$. This connects the formal solution back to the practical eigenvalue method.

### Qualitative Analysis of 2D Systems

While finding exact analytic solutions is important, it is often equally valuable to understand the qualitative behavior of a system. For the system $\vec{x}' = A\vec{x}$, the origin $\vec{x}=\vec{0}$ is always an **[equilibrium point](@entry_id:272705)** (or fixed point), since $\vec{x}' = A\vec{0} = \vec{0}$. The central question of stability is: if a solution starts near the origin, does it stay near the origin (stable), approach the origin (asymptotically stable), or move away from it (unstable)?

The stability of the origin is completely determined by the eigenvalues of $A$. Since solutions are [linear combinations](@entry_id:154743) of terms like $\vec{v}e^{\lambda t}$, the long-term behavior is dictated by the sign of the real part of $\lambda$.
- If all eigenvalues have a negative real part ($\operatorname{Re}(\lambda_i)  0$), all solutions will decay to zero, and the origin is **asymptotically stable**.
- If at least one eigenvalue has a positive real part ($\operatorname{Re}(\lambda_i) > 0$), most solutions will grow without bound, and the origin is **unstable**.
- If eigenvalues have non-positive real parts, with at least one having a zero real part, the situation is more complex, leading to **stable** or unstable behavior depending on the algebraic multiplicity of the zero-real-part eigenvalues.

For a $2 \times 2$ matrix $A$, we can classify the stability without explicitly calculating the eigenvalues. The characteristic equation is $\lambda^2 - \operatorname{tr}(A)\lambda + \det(A) = 0$, where $\operatorname{tr}(A)$ is the trace and $\det(A)$ is the determinant of $A$. The eigenvalues are given by the quadratic formula:
$$
\lambda = \frac{\operatorname{tr}(A) \pm \sqrt{\operatorname{tr}(A)^2 - 4\det(A)}}{2}
$$
From this, we can deduce the nature of the [equilibrium point](@entry_id:272705) directly from the trace and determinant. For instance, to have an **asymptotically [stable spiral](@entry_id:269578)** (also called a [stable focus](@entry_id:274240)), we need the eigenvalues to be a [complex conjugate pair](@entry_id:150139) with a negative real part [@problem_id:2185712].
1.  **Negative Real Part:** The real part is $\frac{\operatorname{tr}(A)}{2}$. For this to be negative, we must have $\operatorname{tr}(A)  0$.
2.  **Complex Conjugates:** The eigenvalues are complex if the discriminant is negative: $\operatorname{tr}(A)^2 - 4\det(A)  0$.
3.  For [asymptotic stability](@entry_id:149743), we also require $\det(A) = \lambda_1 \lambda_2 > 0$. If $\lambda_1, \lambda_2$ are complex conjugates $\alpha \pm i\beta$, their product is $\alpha^2 + \beta^2$, which is always positive. The condition $\operatorname{tr}(A)0$ already ensures $\alpha  0$. So the [necessary and sufficient conditions](@entry_id:635428) for an asymptotically [stable spiral](@entry_id:269578) are $\operatorname{tr}(A)0$ and $\operatorname{tr}(A)^2 - 4\det(A)  0$.

This [trace-determinant plane](@entry_id:163457) analysis is a powerful tool for quickly understanding how a system's behavior changes as its parameters are varied, without needing to solve the system at every step. It is a prime example of the deep insights afforded by the matrix representation of [linear systems](@entry_id:147850).