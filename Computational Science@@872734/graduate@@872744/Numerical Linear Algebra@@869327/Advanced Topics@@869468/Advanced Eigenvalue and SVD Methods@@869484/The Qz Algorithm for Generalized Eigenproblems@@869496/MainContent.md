## Introduction
The [generalized eigenvalue problem](@entry_id:151614), expressed as $A\boldsymbol{x} = \lambda B\boldsymbol{x}$, represents a critical extension of the standard eigenproblem and arises frequently in scientific and engineering disciplines. While seemingly simple, its solution is fraught with numerical challenges. Naive approaches, such as converting it to a standard problem via [matrix inversion](@entry_id:636005), can fail catastrophically when the matrix $B$ is ill-conditioned or singular. This creates a need for a robust and numerically stable algorithm that can handle general matrix pairs without compromising accuracy.

This article provides an in-depth exploration of the QZ algorithm, the state-of-the-art method for solving the [generalized eigenproblem](@entry_id:168055). Across the following sections, we will dissect this powerful tool. The first section, **Principles and Mechanisms**, lays the theoretical foundation, explaining the structure of matrix pencils and detailing the step-by-step mechanics of the algorithm. The second section, **Applications and Interdisciplinary Connections**, demonstrates the algorithm's far-reaching impact in fields like control theory and computational physics. Finally, **Hands-On Practices** will offer concrete problems to solidify understanding. We begin by examining the core principles that make the QZ algorithm a cornerstone of modern [numerical linear algebra](@entry_id:144418).

## Principles and Mechanisms

The QZ algorithm provides a robust and numerically stable framework for solving the [generalized eigenproblem](@entry_id:168055) $A\boldsymbol{x} = \lambda B\boldsymbol{x}$. Its design is rooted in fundamental principles of [matrix theory](@entry_id:184978) and [finite-precision arithmetic](@entry_id:637673). This chapter elucidates these principles, from the formal definition of generalized eigenvalues to the intricate mechanics of the algorithm itself.

### The Generalized Eigenvalue Problem

The [standard eigenvalue problem](@entry_id:755346) $A\boldsymbol{x} = \lambda\boldsymbol{x}$ is a special case of the **[generalized eigenproblem](@entry_id:168055)**, which for two square matrices $A, B \in \mathbb{C}^{n \times n}$, seeks a scalar $\lambda$ and a non-zero vector $\boldsymbol{x}$ satisfying:

$$
A\boldsymbol{x} = \lambda B\boldsymbol{x}
$$

This equation can be rewritten as $(A - \lambda B)\boldsymbol{x} = \mathbf{0}$. For a non-trivial solution $\boldsymbol{x}$ to exist, the matrix $(A - \lambda B)$ must be singular. The family of matrices $A - \lambda B$, parameterized by $\lambda$, is known as a **[matrix pencil](@entry_id:751760)**.

#### Regular and Singular Pencils

A crucial distinction in the theory of matrix pencils is between regular and singular pencils. The characteristic polynomial of the pencil is defined as $p(\lambda) = \det(A - \lambda B)$.

A [matrix pencil](@entry_id:751760) $(A, B)$ is defined as **regular** if the polynomial $p(\lambda)$ is not identically zero for all $\lambda \in \mathbb{C}$. Conversely, if $p(\lambda) \equiv 0$ for all $\lambda$, the pencil is **singular** [@problem_id:3594712]. A regular pencil is characterized by the existence of at least one value $\lambda_0$ for which the matrix $A - \lambda_0 B$ is invertible. A singular pencil, in contrast, is singular for every choice of $\lambda$. For example, the $3 \times 3$ pencil formed by the matrices

$$
A = \begin{pmatrix} 1  0  0 \\ 0  1  0 \\ 0  0  0 \end{pmatrix}, \quad B = \begin{pmatrix} 0  0  0 \\ 0  1  0 \\ 0  0  0 \end{pmatrix}
$$

is singular, because for any $\lambda$, the matrix $A - \lambda B$ has a row of zeros, making its determinant identically zero [@problem_id:3594712]. The QZ algorithm is fundamentally designed to operate on regular pencils, as a singular pencil does not possess a well-defined, discrete set of eigenvalues.

#### Finite and Infinite Eigenvalues

For a regular pencil, the **finite generalized eigenvalues** are the roots of the [characteristic equation](@entry_id:149057) $p(\lambda) = \det(A - \lambda B) = 0$. The degree of this polynomial, let's say $d = \deg(p(\lambda))$, is at most $n$. The coefficient of the $\lambda^n$ term is $(-1)^n \det(B)$. Consequently, if $B$ is nonsingular, the degree is exactly $n$, and all $n$ generalized eigenvalues are finite [@problem_id:3594712].

If $B$ is singular, then $\det(B) = 0$, and the degree $d$ of the [characteristic polynomial](@entry_id:150909) will be less than $n$. In this scenario, the pencil has $d$ finite eigenvalues. A fundamental theorem states that a regular $n \times n$ pencil always has exactly $n$ generalized eigenvalues in the [extended complex plane](@entry_id:165233) $\mathbb{C} \cup \{\infty\}$, when counted with their algebraic multiplicities. The discrepancy between $n$ and $d$ is accounted for by **infinite eigenvalues**. The algebraic multiplicity of the eigenvalue at infinity is defined as $n - d$ [@problem_id:3594674].

It is a common misconception that a [singular matrix](@entry_id:148101) $B$ implies the pencil $(A,B)$ is singular. This is not true. Consider the regular pencil with $A = \begin{pmatrix} 1  0 \\ 0  0 \end{pmatrix}$ and $B = \begin{pmatrix} 0  0 \\ 0  1 \end{pmatrix}$. Here, $B$ is singular, but $\det(A - \lambda B) = \det \begin{pmatrix} 1  0 \\ 0  -\lambda \end{pmatrix} = -\lambda$. Since this polynomial is not identically zero, the pencil is regular. Its degree is $d=1$, so there is one finite eigenvalue at $\lambda=0$. With $n=2$, the multiplicity of the infinite eigenvalue is $n-d = 2-1=1$ [@problem_id:3594674].

### The Generalized Schur Decomposition (QZ)

The QZ algorithm computes the **generalized Schur decomposition** of a pencil $(A,B)$. It asserts the existence of unitary matrices $Q, Z \in \mathbb{C}^{n \times n}$ such that:

$$
S = Q^* A Z \quad \text{and} \quad T = Q^* B Z
$$

where $S$ and $T$ are both upper triangular matrices. The pencil $(S,T)$ is equivalent to $(A,B)$, meaning it has the same generalized eigenvalues. Because $S$ and $T$ are triangular, the eigenvalues can be easily extracted from their diagonal elements. The pairs $(\alpha_i, \beta_i) = (s_{ii}, t_{ii})$ for $i=1, \dots, n$ represent the eigenvalues in **[homogeneous coordinates](@entry_id:154569)**.

- If $t_{ii} \neq 0$, the corresponding eigenvalue is finite and is given by the ratio $\lambda_i = s_{ii} / t_{ii}$.
- If $t_{ii} = 0$, the corresponding eigenvalue is infinite (for a regular pencil, this implies $s_{ii} \neq 0$).

This formulation is numerically robust. It naturally handles infinite eigenvalues and avoids explicit division by zero or numerically small values, which could lead to overflow or catastrophic loss of precision [@problem_id:3594674] [@problem_id:3594673].

### Algorithmic Motivation: Stability over Naivety

If $B$ is invertible, one could transform the generalized problem $A\boldsymbol{x} = \lambda B\boldsymbol{x}$ into a standard eigenproblem $(B^{-1}A)\boldsymbol{x} = \lambda\boldsymbol{x}$. However, this approach is often numerically disastrous. If $B$ is ill-conditioned (i.e., its condition number $\kappa(B) = \|B\|\|B^{-1}\|$ is very large), any small errors in the data for $B$ or rounding errors incurred during computation can be magnified enormously when computing $B^{-1}$. Furthermore, the matrix multiplication to form $B^{-1}A$ can involve adding numbers of vastly different magnitudes, leading to a loss of information from the smaller terms, a phenomenon known as "swamping" [@problem_id:3594686].

For example, for the pencil where $A$ and $B$ are upper triangular, the generalized eigenvalues are simply the ratios of their diagonal elements, $\lambda_1 = 3/10^{-8} = 3 \times 10^8$, $\lambda_2 = -1$, and $\lambda_3 = -10^{-8}$ [@problem_id:3594686]. The matrix $B$ is extremely ill-conditioned, with $\kappa_{\infty}(B) \approx 4.2 \times 10^9$. Explicitly computing $B^{-1}A$ in finite precision would corrupt the information related to the smaller eigenvalues, leading to inaccurate results.

The QZ algorithm circumvents these issues by working directly with $A$ and $B$ and exclusively employing unitary transformations. Unitary (or orthogonal in the real case) matrices are perfectly conditioned with a [2-norm](@entry_id:636114) of 1. Their application does not amplify rounding errors. This property ensures the **[backward stability](@entry_id:140758)** of the algorithm [@problem_id:3594680]. A [backward stable algorithm](@entry_id:633945) guarantees that the computed result is the exact solution to a slightly perturbed problem. In the context of the QZ algorithm, the computed Schur form $(\widehat{S}, \widehat{T})$ is the exact Schur form of a nearby pencil $(A+\Delta A, B+\Delta B)$, where the perturbations $\Delta A$ and $\Delta B$ are small relative to the norms of $A$ and $B$. This is the best one can hope for in [finite-precision arithmetic](@entry_id:637673).

### The Mechanism of the QZ Algorithm

The QZ algorithm proceeds in two major stages.

#### Stage 1: Reduction to Hessenberg-Triangular Form

The first stage is a direct, non-iterative reduction of the general pencil $(A, B)$ to a more structured form. The goal is to find unitary matrices $Q_1$ and $Z_1$ such that $H = Q_1^* A Z_1$ is an **upper Hessenberg matrix** (zeros below the first subdiagonal, $h_{ij}=0$ for $i > j+1$) and $T = Q_1^* B Z_1$ is an upper triangular matrix. This reduction costs $O(n^3)$ floating-point operations [@problem_id:3594756].

The reduction is itself a two-step process:
1.  **Triangularize B:** First, a [unitary matrix](@entry_id:138978) $Q_1$ is constructed as a product of Householder reflectors to transform $B$ into an [upper triangular matrix](@entry_id:173038) $R_0 = Q_1^* B$. This is equivalent to performing a QR decomposition of $B$. The same transformation is applied to $A$, yielding $A_1 = Q_1^* A$.
2.  **Reduce A to Hessenberg:** Next, the [dense matrix](@entry_id:174457) $A_1$ is reduced to upper Hessenberg form while preserving the [triangularity](@entry_id:756167) of $R_0$. This is achieved by a sequence of carefully choreographed Givens rotations. To zero out an element $a_{jk}$ (with $j > k+1$), a left-sided Givens rotation is applied to rows $j-1$ and $j$. This creates a "bulge" (a nonzero element) in the corresponding position of the [triangular matrix](@entry_id:636278). A right-sided Givens rotation is then immediately applied to columns $j-1$ and $j$ to annihilate this bulge and restore the triangular structure. This process is repeated until $A_1$ is fully reduced to Hessenberg form.

#### Stage 2: The Iterative QZ Algorithm on the H-T Form

The second stage is an iterative process, analogous to the QR algorithm for standard [eigenproblems](@entry_id:748835), that operates on the Hessenberg-triangular (H-T) pencil $(H, T)$. The goal is to drive the subdiagonal elements of $H$ to zero, eventually converging to the generalized Schur form where both matrices are (quasi-)triangular.

The H-T structure is essential for efficiency. An [iterative method](@entry_id:147741) on a dense pencil would have a computational cost of $O(n^4)$ per step due to widespread fill-in. The H-T form constrains the influence of each transformation, allowing for an $O(n^2)$ cost per iteration and an overall $O(n^3)$ algorithm [@problem_id:3594779].

A single iteration, known as a **QZ step with implicit shift**, performs a "bulge chase":
1.  **Choose a Shift:** A shift $\sigma$ is chosen, typically from the eigenvalues of the trailing $2 \times 2$ sub-pencil of $(H,T)$. This strategy, known as a double-shift, improves convergence rates, especially for real matrices with complex eigenvalues.

2.  **Introduce the Bulge:** An orthogonal rotation $Q_1$ is constructed. It is implicitly determined by the shift $\sigma$ and the first column of the pencil, specifically as the rotation that would zero out the second element of the vector $(H - \sigma T)\boldsymbol{e}_1$. For example, in a $3 \times 3$ problem with a chosen shift $\sigma=2$, the first column of $(H-2R)$ might be $\begin{pmatrix} -1  2  0 \end{pmatrix}^T$. The first Givens rotation $Q_1$ would be constructed to transform the vector $\begin{pmatrix} -1 \\ 2 \end{pmatrix}$ to $\begin{pmatrix} \rho \\ 0 \end{pmatrix}$, which requires a rotation with sine/cosine ratio $s/c = -2$ [@problem_id:3594769].

3.  **Chase the Bulge:** Applying $Q_1^T$ from the left to $(H, T)$ creates a nonzero element just below the diagonal in $T$, spoiling its [triangularity](@entry_id:756167). A right-sided rotation $Z_1$ is immediately applied to restore $T$'s structure. This application of $Z_1$ to $H$ moves the initial perturbation, creating a new nonzero "bulge" just below the subdiagonal of $H$ (e.g., at position $(3,1)$). This bulge is then systematically "chased" down the diagonal.

The general step $k$ of the chase proceeds as follows [@problem_id:3594782]:
- A left Givens rotation $G_k^T$ on rows $(k+1, k+2)$ is applied to annihilate the current bulge element $h_{k+2,k}$.
- This creates a fill-in element $r_{k+2,k+1}$ in $T$.
- A right Givens rotation $J_k$ on columns $(k+1, k+2)$ is applied to annihilate $r_{k+2,k+1}$, restoring $T$'s triangular structure.
- This right rotation moves the bulge in $H$ to position $(k+3, k+1)$, setting up the next step.

This sequence of local transformations continues until the bulge is chased off the bottom-right corner of the matrix. This completes one full QZ iteration, after which the subdiagonal elements of $H$ are typically smaller, leading to convergence.

### Pathologies and Robust Implementation

The theory and mechanics of the QZ algorithm are built upon the assumption that the pencil $(A,B)$ is **regular**.

If the pencil is **singular**, the [characteristic polynomial](@entry_id:150909) is identically zero. This implies that for any $\lambda$, the matrix $A - \lambda B$ is singular. In the generalized Schur form, this would manifest as a diagonal pair $(\alpha_i, \beta_i) = (0,0)$ [@problem_id:3594780]. This corresponds to an indeterminate eigenvalue $0/0$. The QZ algorithm is not designed to handle this; the iterative steps may stagnate or break down because the subproblems used to determine shifts become ill-posed [@problem_id:3594780].

If the pencil is **near-singular**, it is regular but close to a singular pencil. This is reflected by a diagonal pair $(\alpha_i, \beta_i)$ being very close to $(0,0)$. The corresponding eigenvalue $\lambda_i = \alpha_i/\beta_i$ is extremely ill-conditioned, and small [rounding errors](@entry_id:143856) can cause massive changes in its computed value. This makes deflation decisions unreliable and introduces the risk of numerical overflow or [underflow](@entry_id:635171) [@problem_id:3594780].

Robust implementations must gracefully handle these situations as well as the special case of infinite eigenvalues.
- **Homogeneous Coordinates:** Eigenvalues should always be represented by the pair $(\alpha_i, \beta_i)$ rather than the ratio $\lambda_i$. This provides a stable representation for both very large and infinite eigenvalues [@problem_id:3594673].
- **Reordering:** The QZ algorithm can be augmented with routines to reorder the diagonal blocks of the final Schur form $(S,T)$. This allows, for example, for the grouping of all infinite or large-magnitude eigenvalues, which can aid in analysis and deflation of the pencil [@problem_id:3594673].
- **Deflation and Detection:** If a $2 \times 2$ block of $T$ becomes numerically singular, it signals a pair of very large (potentially [complex conjugate](@entry_id:174888)) eigenvalues. If both the $S$ and $T$ blocks are simultaneously tiny, it indicates near-singularity of the pencil itself. In such cases, more advanced rank-revealing techniques may be required to properly deflate the problem [@problem_id:3594673].

By combining stable unitary transformations, a structured two-stage approach, and careful handling of potential numerical pathologies, the QZ algorithm provides the state-of-the-art method for solving the generalized eigenvalue problem.