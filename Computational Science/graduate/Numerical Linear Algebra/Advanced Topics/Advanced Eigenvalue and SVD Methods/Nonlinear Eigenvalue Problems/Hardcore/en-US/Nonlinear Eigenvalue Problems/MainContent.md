## Introduction
The [standard eigenvalue problem](@entry_id:755346), a cornerstone of linear algebra, provides powerful insights into systems governed by linear operators. However, many complex phenomena in science and engineering—from the vibrations of damped structures to the [electronic states of molecules](@entry_id:185014)—exhibit a nonlinear dependence on the parameters being sought. This complexity gives rise to the **[nonlinear eigenvalue problem](@entry_id:752640) (NEP)**, a powerful generalization where the system's matrix operator is itself a function of the eigenvalue. This article bridges the gap between the familiar linear case and the richer, more challenging nonlinear framework. Over the next three chapters, you will build a comprehensive understanding of NEPs. The journey begins in **Principles and Mechanisms**, where we will establish the core definitions, explore the classification of NEPs, and delve into the local and global spectral theory. Next, **Applications and Interdisciplinary Connections** will showcase how this theory is used to model critical problems in quantum mechanics, materials science, and engineering. Finally, **Hands-On Practices** will translate theory into action through guided numerical exercises, solidifying your ability to solve and analyze these important problems.

## Principles and Mechanisms

### The Fundamental Eigenvalue Problem

The study of nonlinear eigenvalue problems (NEPs) begins with a direct generalization of the standard and generalized linear [eigenvalue problems](@entry_id:142153). Let $\Omega \subseteq \mathbb{C}$ be an open set. A **[nonlinear eigenvalue problem](@entry_id:752640)** is defined by a [matrix-valued function](@entry_id:199897) $T: \Omega \to \mathbb{C}^{n \times n}$. The central task is to find a scalar $\lambda \in \Omega$, called an **eigenvalue**, and a corresponding nonzero vector $x \in \mathbb{C}^n$, called a **right eigenvector**, that satisfy the equation:

$T(\lambda)x = 0$

The pair $(\lambda, x)$ is referred to as a right **eigenpair**. This definition is the cornerstone of the entire theory. For any fixed value of $\lambda$, the equation $T(\lambda)x = 0$ is a standard linear system for the vector $x$. A nonzero solution $x$ exists if and only if the matrix $T(\lambda)$ is singular. This leads to a common alternative characterization of eigenvalues as the roots of a scalar function:

$\det(T(\lambda)) = 0$

In many practical and theoretical contexts, particularly when the function $T$ is analytic on $\Omega$, the search for eigenvalues is often synonymous with finding the zeros of the determinant. However, it is crucial to understand the precise relationship and limitations of this approach .

If $T$ is analytic and **regular**—meaning the scalar function $\lambda \mapsto \det(T(\lambda))$ is not identically zero on any connected component of $\Omega$—then the equivalence is robust. The Identity Theorem for [analytic functions](@entry_id:139584) ensures that the zeros of $\det(T(\lambda))$ are isolated points. In this well-behaved scenario, every $\lambda$ satisfying $\det(T(\lambda))=0$ is indeed an eigenvalue, and this condition is a practical tool for locating them.

The situation changes dramatically if the problem is **singular**, meaning $\det(T(\lambda)) \equiv 0$ for all $\lambda$ in $\Omega$. In this case, the matrix $T(\lambda)$ is singular for every $\lambda$, and by the fundamental definition, every $\lambda \in \Omega$ is an eigenvalue. The set of eigenvalues forms a continuum, and the determinant condition $\det(T(\lambda))=0$ provides no information to localize or distinguish specific eigenvalues of interest. For such problems, eigenvalues are typically redefined as points where the rank of $T(\lambda)$ decreases, or equivalently, where the dimension of the nullspace $\ker(T(\lambda))$ increases .

It is important to emphasize that the equivalence between $T(\lambda)$ being singular and $\det(T(\lambda)) = 0$ holds for any fixed matrix, regardless of the analytic properties of the function $T(\cdot)$. Analyticity is what guarantees that the set of eigenvalues is discrete in the regular case. For non-analytic functions, the set of zeros of $\det(T(\lambda))$ may not be isolated, even if the function is not identically zero .

### A Taxonomy of Nonlinear Eigenvalue Problems

Nonlinear [eigenvalue problems](@entry_id:142153) arise in a vast range of applications, and their mathematical structure is dictated by the underlying physical or mathematical model. The functional dependence of $T(\lambda)$ on $\lambda$ provides a natural and useful classification scheme. We introduce four broad and significant classes .

**Polynomial Eigenvalue Problems (PEPs)** constitute the most studied class of NEPs. Here, $T(\lambda)$ is a matrix polynomial:

$T(\lambda) = \sum_{k=0}^{d} \lambda^k A_k$

where $A_k \in \mathbb{C}^{n \times n}$ are constant coefficient matrices and $d$ is the degree. A ubiquitous example is the **Quadratic Eigenvalue Problem (QEP)**, where $d=2$, often arising from the analysis of [second-order differential equations](@entry_id:269365). A simple QEP is given by $T_p(\lambda) = A_0 + \lambda A_1 + \lambda^2 A_2$.

**Rational Eigenvalue Problems (REPs)** are characterized by $T(\lambda)$ being a [rational function](@entry_id:270841) of $\lambda$. These problems often emerge from frequency-domain analysis of systems, where terms involving resolvents of [linear operators](@entry_id:149003) appear. A typical form involves a polynomial part plus a sum of terms with [simple poles](@entry_id:175768):

$T_r(\lambda) = P(\lambda) + \sum_{j=1}^m \frac{1}{\lambda - \sigma_j} B_j$

where $P(\lambda)$ is a matrix polynomial and $\sigma_j$ are given poles. An example is $T_r(\lambda) = A_0 + \lambda A_1 - A_2 (\lambda - \sigma)^{-1}$.

**Delay or Exponential Eigenvalue Problems** arise from the stability analysis of systems involving time delays, such as delay-differential equations. After applying the Laplace transform, the characteristic matrix often involves exponential terms of $\lambda$. The general form is a sum of [matrix coefficients](@entry_id:140901) multiplied by exponential functions, possibly with polynomial factors:

$T_d(\lambda) = \sum_{k=0}^m P_k(\lambda) e^{-\tau_k \lambda}$

where $P_k(\lambda)$ are matrix polynomials and $\tau_k \ge 0$ are the delays. A simple example is $T_d(\lambda) = A_0 + A_1 e^{-\tau \lambda} + A_2 e^{-2\tau \lambda}$.

**General Analytic NEPs** encompass all problems where $T(\lambda)$ is an [analytic function](@entry_id:143459) of $\lambda$ but does not fit into the more specific categories above. The dependence on $\lambda$ can involve any [analytic function](@entry_id:143459), such as trigonometric or other transcendental functions. An example of such a problem could be $T_a(\lambda) = A_0 + A_1 \sin(\lambda) + A_2 e^{\lambda^2}$.

This classification is not merely academic; the structure of the problem often dictates the most effective numerical method for its solution.

### Local Spectral Theory: Eigenvalues and Eigenvectors

The local behavior of $T(\lambda)$ near an eigenvalue reveals a rich structure that generalizes the familiar concepts of eigenvectors, multiplicities, and Jordan chains from linear algebra.

#### Simple Eigenvalues, Sensitivity, and the Resolvent

The simplest and most well-behaved case is that of a **simple eigenvalue**. Analogous to right eigenvectors, a **left eigenvector** $y \in \mathbb{C}^n$ corresponding to an eigenvalue $\lambda$ is a nonzero vector satisfying:

$y^* T(\lambda) = 0$

This is equivalent to $T(\lambda)^* y = 0$, meaning $y$ is in the nullspace of the conjugate transpose of $T(\lambda)$. For a simple eigenvalue $\lambda_*$, the nullspaces of both $T(\lambda_*)$ and $T(\lambda_*)^*$ are one-dimensional. The right and left eigenvectors, $x_*$ and $y_*$, are therefore unique up to scaling.

A crucial quantity in the theory of simple eigenvalues is the scalar value $y_*^* T'(\lambda_*) x_*$, where $T'(\lambda)$ is the derivative of the [matrix function](@entry_id:751754) with respect to $\lambda$. For an eigenvalue to be simple (in the sense of having [algebraic multiplicity](@entry_id:154240) one), it is necessary and sufficient that this quantity is nonzero: $y_*^* T'(\lambda_*) x_* \neq 0$ .

This condition is fundamental because it governs both the sensitivity of the eigenvalue and the structure of the [resolvent operator](@entry_id:271964) $T(\lambda)^{-1}$ near $\lambda_*$.

**Eigenvalue Sensitivity:** Consider a small analytic perturbation to the problem, $T(\lambda) \to T(\lambda) + \Delta T(\lambda)$. The simple eigenvalue $\lambda_*$ will be perturbed to a new value $\lambda_* + \delta\lambda$. A first-order analysis shows that the change $\delta\lambda$ is given by:

$\delta\lambda = - \frac{y_*^* \Delta T(\lambda_*) x_*}{y_*^* T'(\lambda_*) x_*}$

This formula is a direct generalization of the Wilkinson condition number formula for the [standard eigenvalue problem](@entry_id:755346). It shows that the sensitivity of $\lambda_*$ is inversely proportional to $|y_*^* T'(\lambda_*) x_*|$. This leads to the definition of the **[eigenvalue condition number](@entry_id:176727)**.

**The Resolvent:** The operator $T(\lambda)^{-1}$, known as the resolvent, is a [meromorphic function](@entry_id:195513) of $\lambda$ in the regular case. At a simple eigenvalue $\lambda_*$, it has a simple pole. The Laurent [series expansion](@entry_id:142878) of the resolvent around this pole is:

$T(\lambda)^{-1} = \frac{R}{\lambda - \lambda_*} + (\text{analytic part})$

The matrix $R$ is the **residue**. A careful derivation shows that the residue is a [rank-one matrix](@entry_id:199014) given by:

$R = \frac{x_* y_*^*}{y_*^* T'(\lambda_*) x_*}$

The residue acts as the spectral projector onto the eigenspace associated with $\lambda_*$. The structure of these formulas makes it natural and convenient to adopt the **normalization** $y_*^* T'(\lambda_*) x_* = 1$. With this scaling of the eigenvectors, the sensitivity formula simplifies to $\delta\lambda = -y_*^* \Delta T(\lambda_*) x_*$, and the residue becomes simply $R = x_* y_*^*$ .

#### Multiple Eigenvalues: Jordan Chains and Multiplicities

When an eigenvalue is not simple, the situation becomes more complex. The quantity $y^* T'(\lambda_*) x$ may be zero for all associated eigenvectors $x$ and $y$, and we must turn to [higher-order derivatives](@entry_id:140882) of $T(\lambda)$ to understand the local structure. This leads to the generalization of Jordan chains .

The **[geometric multiplicity](@entry_id:155584)** of an eigenvalue $\lambda_*$ is defined, as in the linear case, as the dimension of the nullspace of $T(\lambda_*)$:

$g(\lambda_*) = \dim(\ker(T(\lambda_*)))$

This is the number of [linearly independent](@entry_id:148207) eigenvectors that can be found for $\lambda_*$.

A **Jordan chain** of length $\ell$ associated with $\lambda_*$ is a sequence of vectors $(x_0, x_1, \dots, x_{\ell-1})$, where $x_0 \neq 0$, that satisfies a hierarchy of linear equations. These equations arise from considering an analytic vector function $x(\lambda) = \sum_{k=0}^\infty (\lambda-\lambda_*)k x_k$ such that $T(\lambda)x(\lambda)=0$. Substituting the Taylor series for both $T(\lambda)$ and $x(\lambda)$ around $\lambda_*$ and collecting powers of $(\lambda-\lambda_*)$ yields the defining relations for the chain:

$\sum_{j=0}^{k} \frac{1}{j!} T^{(j)}(\lambda_*) x_{k-j} = 0, \quad \text{for } k=0, 1, \dots, \ell-1$

Here, $T^{(j)}(\lambda_*)$ denotes the $j$-th derivative of $T(\lambda)$ evaluated at $\lambda_*$.
For $k=0$, this reduces to $T(\lambda_*)x_0=0$, confirming that the first vector in the chain, $x_0$, must be an eigenvector. For $k \ge 1$, we can rearrange the equation to obtain a recursive scheme for finding the subsequent vectors, known as **[generalized eigenvectors](@entry_id:152349)**:

$T(\lambda_*)x_k = - \sum_{j=1}^{k} \frac{1}{j!} T^{(j)}(\lambda_*) x_{k-j}$

For a given $x_0, \dots, x_{k-1}$, this is a linear system for $x_k$. By the Fredholm alternative, a solution $x_k$ exists if and only if the right-hand side vector is in the range of the matrix $T(\lambda_*)$. The process can be continued until the [solvability condition](@entry_id:167455) fails, which determines the maximal length of the chain starting with $x_0$.

For each eigenvalue $\lambda_*$, there exists a canonical set of $g(\lambda_*)$ Jordan chains, starting with a basis of eigenvectors from $\ker(T(\lambda_*))$. The lengths of these chains, $\ell_1 \ge \ell_2 \ge \dots \ge \ell_g \ge 1$, are called the **partial multiplicities** of $\lambda_*$. The sum of these lengths is the **[algebraic multiplicity](@entry_id:154240)**:

$m(\lambda_*) = \sum_{i=1}^{g(\lambda_*)} \ell_i$

A fundamental theorem states that for an analytic NEP, the algebraic multiplicity of an eigenvalue $\lambda_*$ is equal to the multiplicity of $\lambda_*$ as a zero of the scalar function $\det(T(\lambda))$. An eigenvalue is called **semisimple** if its algebraic and geometric multiplicities are equal ($m=g$), which implies all Jordan chains have length 1. It is called **defective** if its [geometric multiplicity](@entry_id:155584) is strictly less than its algebraic multiplicity ($g  m$), implying the existence of at least one Jordan chain of length greater than 1.

**Example: A Defective Eigenvalue.** Consider the NEP defined by $T(\lambda) = A + \lambda B + \lambda^{-1} C$ with matrices :
$A = \begin{pmatrix} -3  2 \\ -2  0 \end{pmatrix}, \quad B = \begin{pmatrix} 3  0 \\ 1  0 \end{pmatrix}, \quad C = \begin{pmatrix} 0  0 \\ 1  0 \end{pmatrix}$

First, we form the matrix $T(\lambda)$ and compute its determinant:
$T(\lambda) = \begin{pmatrix} -3+3\lambda  2 \\ -2+\lambda+\lambda^{-1}  0 \end{pmatrix}$
$\det(T(\lambda)) = -2(-2+\lambda+\lambda^{-1}) = \frac{-2(\lambda^2 - 2\lambda + 1)}{\lambda} = \frac{-2(\lambda-1)^2}{\lambda}$

The determinant has a zero of order 2 at $\lambda_0 = 1$. Thus, the algebraic multiplicity of this eigenvalue is $m(1)=2$. Now, let's find the [geometric multiplicity](@entry_id:155584) by computing $\dim(\ker(T(1)))$.
$T(1) = A+B+C = \begin{pmatrix} -3+3  2 \\ -2+1+1  0 \end{pmatrix} = \begin{pmatrix} 0  2 \\ 0  0 \end{pmatrix}$
The equation $T(1)x_0=0$ becomes $\begin{pmatrix} 0  2 \\ 0  0 \end{pmatrix} x_0 = 0$, which has the [solution space](@entry_id:200470) spanned by the single vector $x_0 = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$. The [nullspace](@entry_id:171336) is one-dimensional, so the [geometric multiplicity](@entry_id:155584) is $g(1)=1$. Since $g(1)  m(1)$, the eigenvalue $\lambda_0=1$ is defective. There must be a single Jordan chain of length 2.

We seek this chain $(x_0, x_1)$. We already have the eigenvector $x_0 = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$. To find the [generalized eigenvector](@entry_id:154062) $x_1$, we use the constructive formula for $k=1$:
$T(1)x_1 = -T'(1)x_0$

First, we compute the derivative $T'(\lambda) = B - \lambda^{-2} C$, so $T'(1) = B-C = \begin{pmatrix} 3  0 \\ 0  0 \end{pmatrix}$.
The equation for $x_1$ is:
$\begin{pmatrix} 0  2 \\ 0  0 \end{pmatrix} x_1 = - \begin{pmatrix} 3  0 \\ 0  0 \end{pmatrix} \begin{pmatrix} 1 \\ 0 \end{pmatrix} = \begin{pmatrix} -3 \\ 0 \end{pmatrix}$

Let $x_1 = \begin{pmatrix} u \\ v \end{pmatrix}$. The system becomes $2v = -3$ and $0=0$. This gives $v = -3/2$. The value of $u$ is not constrained by this equation. We can impose a [normalization condition](@entry_id:156486), for example $e_1^T x_1 = u = 0$. This yields the [generalized eigenvector](@entry_id:154062) $x_1 = \begin{pmatrix} 0 \\ -3/2 \end{pmatrix}$. The Jordan chain is thus $(x_0, x_1) = \left( \begin{pmatrix} 1 \\ 0 \end{pmatrix}, \begin{pmatrix} 0 \\ -3/2 \end{pmatrix} \right)$.

### Global Spectral Theory and Stability

#### Finiteness of the Spectrum in a Domain

A natural global question is: how many eigenvalues does an NEP have? In general, an analytic NEP can have infinitely many eigenvalues in the complex plane (e.g., $T(\lambda)=\sin(\lambda)I$). However, under reasonable conditions, the number of eigenvalues within any bounded region of the plane is finite.

This powerful result comes from complex analysis . Let $\Omega \subset \mathbb{C}$ be a bounded, [simply connected domain](@entry_id:197423) with a piecewise smooth boundary $\Gamma$. The key theorem states:

**Theorem:** If $T: \mathcal{U} \to \mathbb{C}^{n \times n}$ is analytic on an open set $\mathcal{U}$ containing the closure $\overline{\Omega}$, and if $T(\lambda)$ is invertible for all $\lambda$ on the boundary $\Gamma$, then the set of eigenvalues of $T$ inside $\Omega$ is finite.

The proof relies on the function $f(\lambda) = \det(T(\lambda))$. The conditions imply that $f(\lambda)$ is analytic on $\overline{\Omega}$ and nonzero on its boundary $\Gamma$. By the Identity Principle, since $f$ is not identically zero, its zeros within $\Omega$ must be isolated. A compact set like $\overline{\Omega}$ can only contain a finite number of isolated points, proving the result.

Furthermore, a generalization of the Argument Principle, known as Keldysh's Theorem, provides a formula to count the number of eigenvalues inside $\Omega$, weighted by their algebraic multiplicities:

$N = \frac{1}{2\pi i} \oint_\Gamma \mathrm{tr}\left( T(\lambda)^{-1} T'(\lambda) \right) d\lambda$

This formula connects to the scalar case via Jacobi's formula, $\frac{d}{d\lambda}\ln(\det(T(\lambda))) = \mathrm{tr}(T(\lambda)^{-1} T'(\lambda))$, showing that the integral counts the zeros of the determinant.

These results also extend to infinite-dimensional settings. If $T(\lambda)$ is an analytic family of Fredholm operators of index 0 on a Banach space, the Analytic Fredholm Theorem guarantees that the spectrum is a [discrete set](@entry_id:146023), and thus finite within any compact region where $T(\lambda)$ is invertible on the boundary .

#### The Pseudospectrum of a Nonlinear Problem

The spectrum, the set of exact eigenvalues, provides only a partial picture of a system's behavior. For [non-normal matrices](@entry_id:137153) or operators (where $T(\lambda)T(\lambda)^* \neq T(\lambda)^*T(\lambda)$), eigenvalues can be extremely sensitive to small perturbations. A matrix can be nearly singular (and thus behave as if it has an eigenvalue nearby) even if the exact eigenvalues are far away. The **pseudospectrum** is the tool designed to analyze this phenomenon.

The concept is extended to NEPs by defining a set of "near-eigenvalues" for a given tolerance $\epsilon > 0$. This tolerance can be scaled by a continuous, positive weight function $\omega(\lambda)$ to allow for relative perturbations. The **weighted $\epsilon$-[pseudospectrum](@entry_id:138878)**, denoted $\Lambda_\epsilon^\omega(T)$, is formally defined in several equivalent ways :

1.  **Based on the Smallest Singular Value:** A point $\lambda$ is in the [pseudospectrum](@entry_id:138878) if the matrix $T(\lambda)$ is close to a singular matrix. The distance to the nearest [singular matrix](@entry_id:148101) in the spectral norm is the smallest singular value, $\sigma_{\min}(T(\lambda))$. This gives the primary definition:
    $\Lambda_\epsilon^\omega(T) = \{ \lambda \in \Omega : \sigma_{\min}(T(\lambda)) \le \epsilon \omega(\lambda) \}$

2.  **Based on Perturbations:** Equivalently, the pseudospectrum is the union of the spectra of all nearby problems. A point $\lambda$ is in $\Lambda_\epsilon^\omega(T)$ if there exists a perturbation matrix $\Delta T(\lambda)$ such that $\| \Delta T(\lambda) \|_2 \le \epsilon \omega(\lambda)$ and the perturbed matrix $T(\lambda) + \Delta T(\lambda)$ is singular.
    $\Lambda_\epsilon^\omega(T) = \bigcup_{\| \Delta T(\cdot) \|_2 \le \epsilon \omega(\cdot)} \mathrm{spectrum}(T+\Delta T)$

3.  **Based on the Resolvent Norm:** For any invertible matrix $A$, $\|A^{-1}\|_2 = 1/\sigma_{\min}(A)$. This provides a third characterization: $\lambda$ is in the pseudospectrum if either $T(\lambda)$ is singular (in which case $\|T(\lambda)^{-1}\|_2 = \infty$) or its resolvent has a large norm.
    $\Lambda_\epsilon^\omega(T) = \{ \lambda \in \Omega : \|T(\lambda)^{-1}\|_2 \ge (\epsilon \omega(\lambda))^{-1} \}$

These equivalent definitions provide both a theoretical foundation and practical means for computing and interpreting [pseudospectra](@entry_id:753850). They capture regions in the complex plane where $T(\lambda)$ is ill-conditioned, providing crucial insight into the stability and transient behavior of the underlying system.

### Important Problem Structures and Solution Strategies

#### Structured Nonlinear Eigenvalue Problems

Many NEPs arising from physical models are not generic but possess special algebraic structures, such as symmetry or palindromic properties. Recognizing and exploiting this structure is paramount in numerical computation, as it can lead to more accurate and efficient algorithms that preserve the qualitative properties of the solution, such as spectral symmetries .

-   **Symmetric and Hermitian NEPs:** A problem is symmetric if $T(\lambda) = T(\lambda)^T$ for all $\lambda$, or Hermitian if $T(\lambda) = T(\lambda)^*$. If the coefficient matrices are real, the spectrum of a symmetric or Hermitian NEP is closed under [complex conjugation](@entry_id:174690) (i.e., if $\lambda$ is an eigenvalue, so is $\overline{\lambda}$).

-   **Palindromic NEPs:** These are typically polynomial problems $P(\lambda) = \sum_{k=0}^d \lambda^k P_k$ that exhibit a reversed-and-conjugated coefficient structure, such as $P_k = P_{d-k}^*$. This structure imposes a reciprocal-[conjugate symmetry](@entry_id:144131) on the spectrum: if $\lambda$ is an eigenvalue, then so is $1/\overline{\lambda}$.

-   **Gyroscopic Systems:** These are QEPs of the form $Q(\lambda) = \lambda^2 M + \lambda G + K$, where the mass matrix $M$ and stiffness matrix $K$ are real and symmetric ($M=M^T, K=K^T$), and the gyroscopic matrix $G$ is real and skew-symmetric ($G=-G^T$). This structure forces the spectrum to be symmetric with respect to the imaginary axis: if $\lambda$ is an eigenvalue, then so is $-\overline{\lambda}$.

-   **Damped Mechanical Systems:** These are QEPs of the same form, $Q(\lambda) = \lambda^2 M + \lambda C + K$, but here the matrices $M, C, K$ are real, symmetric, and typically positive (semi-)definite. This models a system with mass, damping, and stiffness. The structure guarantees that all eigenvalues lie in the closed left half of the complex plane, $\mathrm{Re}(\lambda) \le 0$, corresponding to stable or decaying oscillations.

#### Linearization and Invariant Pairs

A powerful and widely used strategy for solving NEPs, particularly PEPs and REPs, is **linearization**. The idea is to transform the $n \times n$ nonlinear problem into a larger, but linear, [generalized eigenvalue problem](@entry_id:151614) (GEP) of the form $(\mathcal{N} - \lambda \mathcal{M})z = 0$, where $\mathcal{M}, \mathcal{N}$ are constant matrices.

For a PEP $P(\lambda) = \sum_{k=0}^d \lambda^k A_k$, a standard example is the second **[companion linearization](@entry_id:747525)**, where the GEP is of size $nd \times nd$:
$\mathcal{N} = \begin{pmatrix} 0  I  \dots  0 \\ \vdots  \vdots  \ddots  \vdots \\ 0  0  \dots  I \\ -A_0  -A_1  \dots  -A_{d-1} \end{pmatrix}, \quad \mathcal{M} = \begin{pmatrix} I  0  \dots  0 \\ 0  I  \dots  0 \\ \vdots  \vdots  \ddots  \vdots \\ 0  0  \dots  A_d \end{pmatrix}$

The eigenvalues of this linear pair $(\mathcal{N}, \mathcal{M})$ are identical to those of the original NEP $P(\lambda)$. This allows the use of mature and robust algorithms for GEPs, such as the QZ algorithm, to solve the NEP.

However, [linearization](@entry_id:267670) is not without its subtleties. The choice of linearization can affect the numerical properties of the problem, particularly the conditioning of the eigenvalues. A [perturbation analysis](@entry_id:178808) shows that the condition number of an eigenvalue computed via a [linearization](@entry_id:267670) can be different from, and often larger than, the condition number of the eigenvalue with respect to the original problem formulation . This discrepancy arises because the perturbation model for the linearized pencil may not correspond naturally to structured perturbations of the original coefficient matrices. A "good" linearization is one that shares its spectral properties with the original problem in a robust way.

A more abstract and general concept for representing a portion of the spectrum and its associated vectors is the **invariant pair** . An invariant pair $(X, S)$, where $X \in \mathbb{C}^{n \times p}$ and $S \in \mathbb{C}^{p \times p}$, generalizes the notion of an invariant subspace from linear algebra. Its definition relies on [matrix functional calculus](@entry_id:189983). For a polynomial NEP $T(\lambda) = \sum_{k=0}^d \lambda^k A_k$, the pair $(X,S)$ is an invariant pair if it satisfies the block equation:

$\sum_{k=0}^d A_k X S^k = 0$

This is sometimes compactly written as $\mathbf{T}(X,S) = 0$. The power of this concept lies in its fundamental property: if $(X,S)$ is an invariant pair with $X$ having full column rank, and if $(\mu, y)$ is an eigenpair of the small matrix $S$ (i.e., $Sy=\mu y$), then $(\mu, Xy)$ is an eigenpair of the original NEP $T(\lambda)$. This means the eigenvalues of the small $p \times p$ matrix $S$ are a subset of the eigenvalues of the large $n \times n$ NEP.

For the standard linear problem $T(\lambda) = A - \lambda I$, the invariant pair condition reduces to $A X I - I X S = 0$, or $AX - XS = 0$. This is precisely the matrix equation defining an [invariant subspace](@entry_id:137024) of $A$, where the columns of $X$ form a basis for that subspace. The invariant pair concept thus provides a powerful theoretical and computational framework for block-based methods, such as subspace [projection methods](@entry_id:147401), for solving large-scale nonlinear [eigenvalue problems](@entry_id:142153).