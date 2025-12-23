## Introduction
While the [standard eigenvalue problem](@entry_id:755346), $Ax = \lambda x$, is a cornerstone of linear algebra, many complex physical phenomena in science and engineering are modeled by equations where the eigenvalue parameter appears nonlinearly. This gives rise to polynomial and rational [eigenvalue problems](@entry_id:142153) (PEPs and REPs), which require more advanced theoretical and computational machinery. The central challenge lies in solving these nonlinear problems efficiently and accurately, as direct application of standard linear eigensolvers is not possible. This article bridges that gap by providing a thorough exploration of the modern numerical techniques designed to tackle these important problem classes.

This article is structured to guide you from foundational concepts to practical application. The first chapter, **Principles and Mechanisms**, delves into the formal definitions of PEPs and REPs and introduces the pivotal technique of [linearization](@entry_id:267670)—the process of converting these nonlinear problems into solvable linear ones. We will examine the properties of various linearizations and the numerical subtleties that affect solution accuracy. The second chapter, **Applications and Interdisciplinary Connections**, illustrates how these abstract problems manifest in real-world scenarios, with a focus on [structural mechanics](@entry_id:276699) and control theory, showing how mathematical structure informs physical understanding. Finally, **Hands-On Practices** will offer a chance to engage directly with these methods through guided problem-solving exercises, solidifying your understanding of how to implement these powerful techniques.

## Principles and Mechanisms

This chapter delves into the fundamental principles and core solution mechanisms for polynomial and rational [eigenvalue problems](@entry_id:142153). We will begin by formally defining the [polynomial eigenvalue problem](@entry_id:753575) and its essential characteristics. Subsequently, we will explore the central technique of [linearization](@entry_id:267670), which transforms these nonlinear problems into linear ones amenable to standard numerical methods. We will then examine the numerical challenges associated with this transformation, such as conditioning and stability, leading to a discussion of modern, structured linearizations. The chapter will then extend these concepts to the more general class of rational [eigenvalue problems](@entry_id:142153). Finally, we will address methods tailored for large-scale problems where explicit linearization is computationally prohibitive.

### The Polynomial Eigenvalue Problem (PEP)

The [standard eigenvalue problem](@entry_id:755346), $Ax = \lambda x$, is a cornerstone of linear algebra, describing the characteristic behavior of a linear operator represented by the matrix $A$. However, many physical systems, particularly those involving vibrations, acoustics, and [structural mechanics](@entry_id:276699), are modeled by [systems of differential equations](@entry_id:148215) whose analysis leads to [eigenvalue problems](@entry_id:142153) where the parameter $\lambda$ appears as a polynomial.

#### Fundamental Definitions

A **matrix polynomial** $P(\lambda)$ of degree $d$ is an $n \times n$ [matrix-valued function](@entry_id:199897) of a scalar variable $\lambda \in \mathbb{C}$ of the form:
$$
P(\lambda) = \sum_{i=0}^{d} A_i \lambda^i
$$
where the coefficient matrices $A_i \in \mathbb{C}^{n \times n}$ are constant matrices. The **Polynomial Eigenvalue Problem (PEP)** consists of finding scalars $\lambda$ and corresponding nonzero vectors $x \in \mathbb{C}^n$ that satisfy the equation:
$$
P(\lambda)x = 0
$$
A scalar $\lambda$ for which such a nonzero vector $x$ exists is called a **finite eigenvalue**, and $x$ is the corresponding **right eigenvector**. Similarly, a nonzero vector $y \in \mathbb{C}^n$ satisfying $y^*P(\lambda) = 0$ is a **left eigenvector**. The pair $(\lambda, x)$ is referred to as a (right) **polynomial eigenpair**. This is a direct generalization of the standard eigenproblem ($d=1, A_1 = -I, A_0 = A$) and the [generalized eigenproblem](@entry_id:168055) ($d=1, A_1 = -B, A_0 = A$) .

A crucial property of a matrix polynomial is its **regularity**. A matrix polynomial $P(\lambda)$ is said to be **regular** if its determinant, $\det(P(\lambda))$, is not identically zero as a polynomial in $\lambda$. If $\det(P(\lambda)) \equiv 0$, the polynomial is called **singular**. For a regular PEP, the eigenvalues are the roots of the scalar characteristic polynomial $\det(P(\lambda))=0$. A singular PEP, by contrast, has an eigenvalue for every $\lambda \in \mathbb{C}$, and its structure is more complex, described by minimal indices and minimal bases which characterize the null space of $P(\lambda)$ over the field of [rational functions](@entry_id:154279) in $\lambda$. For the remainder of our core discussion, we will primarily focus on regular matrix polynomials.

The definition of eigenvalues can be extended to include the [point at infinity](@entry_id:154537). An **infinite eigenvalue** is a concept that arises when the leading [coefficient matrix](@entry_id:151473), $A_d$, is singular. To handle this formally, we introduce the **[reversal polynomial](@entry_id:754325)** of grade $d$:
$$
\text{rev}_d P(\mu) = \mu^d P(1/\mu) = \sum_{i=0}^{d} A_{d-i} \mu^i = A_d + A_{d-1}\mu + \dots + A_0 \mu^d
$$
By this definition, the infinite eigenvalues of $P(\lambda)$ correspond precisely to the zero eigenvalues of $\text{rev}_d P(\mu)$. An equivalent condition for an infinite eigenvalue is the existence of a nonzero vector $x$ such that $A_d x = 0$. The [geometric multiplicity](@entry_id:155584) of the infinite eigenvalue is therefore equal to the dimension of the [null space](@entry_id:151476) of $A_d$, i.e., $\dim(\ker(A_d))$ . A more unified perspective is offered by the **homogeneous formulation**, which considers eigenpairs $(\alpha, \beta) \in \mathbb{C}^2 \setminus \{(0,0)\}$. A finite eigenvalue $\lambda$ corresponds to the pair $(\lambda, 1)$, while an infinite eigenvalue corresponds to $(1, 0)$.

### The Core Mechanism: Linearization

Solving the nonlinear equation $P(\lambda)x = 0$ directly is a challenging task. The most successful and widely used strategy is to transform the PEP into an equivalent, but larger, Generalized Eigenvalue Problem (GEP) of the form $(A - \lambda B)z = 0$. This process is known as **[linearization](@entry_id:267670)**. The resulting GEP can then be solved by mature and numerically robust algorithms.

#### Formal Definition of Linearization

A [matrix pencil](@entry_id:751760) $L(\lambda) = A - \lambda B$ of size $nd \times nd$ is a **[linearization](@entry_id:267670)** of an $n \times n$ matrix polynomial $P(\lambda)$ of degree $d$ if there exist [unimodular matrix](@entry_id:148345) polynomials $E(\lambda)$ and $F(\lambda)$ (i.e., their determinants are nonzero constants) of size $nd \times nd$ such that
$$
E(\lambda)L(\lambda)F(\lambda) = \begin{pmatrix} P(\lambda) & 0 \\ 0 & I_{n(d-1)} \end{pmatrix}
$$
This relationship, known as unimodular equivalence, implies that $L(\lambda)$ and the [block-diagonal matrix](@entry_id:145530) containing $P(\lambda)$ share the same finite [elementary divisors](@entry_id:139388). Since the finite [elementary divisors](@entry_id:139388) determine the finite eigenvalues and their multiplicities, a linearization preserves all finite eigenvalues of $P(\lambda)$ along with their algebraic and geometric multiplicities .

However, this definition alone is insufficient to guarantee the preservation of the eigenstructure at infinity. For this, we need the stronger concept of a **[strong linearization](@entry_id:755534)**. A [linearization](@entry_id:267670) $L(\lambda)$ is a [strong linearization](@entry_id:755534) of $P(\lambda)$ if, in addition to the above, its reversal, $\text{rev}_1 L(\lambda)$, is a linearization of the [reversal polynomial](@entry_id:754325) $\text{rev}_d P(\lambda)$. This additional condition ensures that the infinite eigenvalues and their multiplicities are also preserved. In essence, a [strong linearization](@entry_id:755534) transforms the entire eigenstructure of the PEP into that of a larger GEP, making it the gold standard for solving PEPs numerically .

#### Companion Linearizations

There is no unique linearization for a given PEP; in fact, there are entire families of them. The most widely known are the **Frobenius companion linearizations**. For a PEP of degree $d$, two common forms are the first and second companion pencils. For instance, for a cubic polynomial ($d=3$) $P(\lambda) = A_3\lambda^3 + A_2\lambda^2 + A_1\lambda + A_0$, the first companion pencil is given by:
$$
L_1(\lambda) = \lambda \begin{pmatrix} I & 0 & 0 \\ 0 & I & 0 \\ 0 & 0 & A_3 \end{pmatrix} - \begin{pmatrix} 0 & I & 0 \\ 0 & 0 & I \\ -A_0 & -A_1 & -A_2 \end{pmatrix}
$$
The second companion pencil can be constructed by reversing the order of the coefficient blocks:
$$
L_2(\lambda) = \lambda \begin{pmatrix} A_3 & 0 & 0 \\ 0 & I & 0 \\ 0 & 0 & I \end{pmatrix} - \begin{pmatrix} -A_2 & -A_1 & -A_0 \\ I & 0 & 0 \\ 0 & I & 0 \end{pmatrix}
$$
These two pencils are not identical, but they are part of a larger family of **Fiedler pencils**. They can be shown to be strictly equivalent, meaning one can be transformed into the other via multiplication by constant invertible matrices. For example, $L_2(\lambda) = \Pi L_1(\lambda) \Pi^T$ where $\Pi$ is a block anti-diagonal [permutation matrix](@entry_id:136841). Since they are strictly equivalent and are both strong linearizations (assuming $A_d$ is nonsingular), they are spectrally equivalent and yield the same set of eigenvalues .

#### Solving the Linearized Problem

Once the PEP is converted into a GEP $(A,B)$, where $L(\lambda) = A-\lambda B$, we can employ powerful numerical tools. The standard algorithm for solving dense GEPs is the **QZ algorithm**. This algorithm computes a **generalized Schur decomposition**, finding unitary matrices $Q$ and $Z$ such that $T = Q^*AZ$ and $S = Q^*BZ$ are both upper triangular.

The eigenvalues of the pencil $(A,B)$ can then be read directly from the diagonals of $T$ and $S$. For each diagonal index $i=1, \dots, nd$:
-   If $s_{ii} \neq 0$, the corresponding eigenvalue is finite and given by the ratio $\lambda_i = t_{ii}/s_{ii}$.
-   If $s_{ii} = 0$, the corresponding eigenvalue is infinite. For a regular pencil, this implies $t_{ii} \neq 0$.

For example, when using the first [companion linearization](@entry_id:747525) for a [quadratic eigenvalue problem](@entry_id:753899) (QEP), the number of infinite eigenvalues is determined by the rank of the leading coefficient $A_2$. Specifically, there are $n - \text{rank}(A_2)$ infinite eigenvalues, which manifest as exactly that many zero entries on the diagonal of the resulting Schur matrix $S$ . The QZ algorithm is an iterative process. In practice, it often proceeds by first reducing the pencil to a condensed Hessenberg-triangular form. During the iteration, if a subdiagonal entry of the Hessenberg matrix becomes numerically zero, the problem decouples, or **deflates**, allowing a subset of eigenvalues to be considered converged and the algorithm to proceed on a smaller problem .

### Numerical Considerations and Advanced Linearizations

While mathematically elegant, the "linearize and solve" strategy is fraught with numerical subtleties. The choice of [linearization](@entry_id:267670) can dramatically affect the accuracy and stability of the computed solution.

#### Conditioning and Backward Error

The sensitivity of an eigenvalue to perturbations in the input data is measured by its **condition number**. For a simple eigenvalue $\lambda$ of a PEP with right and left eigenvectors $x$ and $y$, the condition number is given by:
$$
\kappa_{\text{pep}}(\lambda) = \frac{\|x\|_2 \|y\|_2}{|y^* P'(\lambda) x|}
$$
where $P'(\lambda)$ is the derivative of the matrix polynomial with respect to $\lambda$. For the linearized GEP $(A,B)$, the condition number of the corresponding eigenvalue is:
$$
\kappa_{\text{penc}}(\lambda) = \frac{\|z\|_2 \|w\|_2}{|w^* B z|}
$$
where $z$ and $w$ are the right and left eigenvectors of the pencil .

A crucial point is that even for a [strong linearization](@entry_id:755534), these two condition numbers are generally not equal. A poorly chosen linearization can result in $\kappa_{\text{penc}}(\lambda) \gg \kappa_{\text{pep}}(\lambda)$, meaning the [eigenvalue problem](@entry_id:143898) for the pencil is much more sensitive to perturbations than the original PEP. This often occurs when the norms of the coefficient matrices, $\|A_i\|$, have a **large [dynamic range](@entry_id:270472)**. For instance, if some $\|A_i\|$ are very large and others very small, standard companion forms can be poorly scaled, leading to a large [backward error](@entry_id:746645) for the computed eigenvalues when interpreted in the context of the original PEP .

A primary strategy to combat these issues is **scaling**. This involves transformations of the variable $\lambda$ and the polynomial $P(\lambda)$ itself to balance the norms of the coefficient matrices, aiming to make them all of order one. Proper scaling, combined with equilibration of the resulting pencil, is a critical step for achieving numerical stability .

#### Beyond Companion Forms: Structured Linearizations

The numerical deficiencies of companion linearizations, especially for problems with specific structures (e.g., symmetric, palindromic) or poor scaling, have motivated the development of new classes of linearizations. One of the most important modern developments is the framework of **block minimal bases pencils**.

These pencils, which include families known as block Kronecker linearizations, are constructed based on the concept of dual minimal bases. A key advantage is that they often exhibit much better conditioning and [backward stability](@entry_id:140758) properties than Frobenius companion forms. For example, for a polynomial with highly unbalanced coefficient norms, a block minimal bases pencil can yield computed eigenvalues with median backward errors that are orders of magnitude smaller than those from a companion pencil. This is because their structure distributes the influence of the coefficient matrices more evenly throughout the pencil, avoiding the concentration of all coefficients in a single row or column that makes companion forms so sensitive to scaling . The choice of [linearization](@entry_id:267670) is therefore a critical aspect of algorithm design, with modern structured linearizations offering significant advantages in robustness.

### The Rational Eigenvalue Problem (REP)

A further generalization leads to the **Rational Eigenvalue Problem (REP)**, where the matrix entries are rational functions of $\lambda$. Such problems arise in a variety of applications, including the analysis of fluid-structure interactions, electronic circuits, and acoustic modeling of [porous materials](@entry_id:152752).

#### Definition and Key Concepts

An REP is the problem of finding $(\lambda, x)$ such that $R(\lambda)x = 0$, where $R(\lambda)$ is a matrix whose entries are rational functions. A key distinction in REPs is between **eigenvalues** and **poles**. A scalar $\lambda_0$ is a **pole** of $R(\lambda)$ if the function is not analytic at $\lambda_0$ (i.e., it "blows up"). Conversely, $\lambda_0$ is an **eigenvalue** only if $R(\lambda)$ is analytic at $\lambda_0$ and the matrix $R(\lambda_0)$ is singular. Thus, the sets of [poles and eigenvalues](@entry_id:263134) are disjoint .

REPs can be represented in various ways. Two important representations are:
1.  **Matrix-Fraction Description (MFD)**: $R(\lambda) = Q(\lambda)P(\lambda)^{-1}$, where $P(\lambda)$ and $Q(\lambda)$ are matrix polynomials. If this factorization is **right coprime**, the poles of $R(\lambda)$ are the eigenvalues of $P(\lambda)$ (where $\det(P(\lambda))=0$), and the eigenvalues of $R(\lambda)$ are the eigenvalues of $Q(\lambda)$ (where $\det(Q(\lambda))=0$) that are not also poles .
2.  **State-Space Realization**: $R(\lambda) = C(\lambda E - A)^{-1}B + D$. This form is standard in control theory and is a common way REPs arise from systems of [differential-algebraic equations](@entry_id:748394). Here, the poles of $R(\lambda)$ are a subset of the eigenvalues of the pencil $(\lambda E - A)$. If the realization is **minimal** (controllable and observable), the poles are precisely the eigenvalues of $(\lambda E - A)$.

As with PEPs, the [standard solution](@entry_id:183092) strategy for REPs is linearization. The state-space form naturally provides a [linearization](@entry_id:267670). The REP $R(\lambda)x=0$ can be transformed into the GEP:
$$
\begin{pmatrix} A & B \\ C & D \end{pmatrix} \begin{pmatrix} v \\ x \end{pmatrix} = \lambda \begin{pmatrix} E & 0 \\ 0 & 0 \end{pmatrix} \begin{pmatrix} v \\ x \end{pmatrix}
$$
where $v = (\lambda E - A)^{-1}Bx$. The numerical analysis of REPs often involves assessing the quality of an approximate eigenpair $(\hat{\lambda}, \hat{x})$. This can be done by formulating a structured **backward error**, which measures the smallest perturbation to the data matrices (e.g., $A,B,C,D,E$) that makes $(\hat{\lambda}, \hat{x})$ an exact eigenpair of a nearby REP. This provides a rigorous way to validate computed solutions in the context of the underlying system representation .

### Methods for Large-Scale Problems

For many real-world applications, the dimension $n$ of the coefficient matrices is very large (e.g., $10^5$ or more). In such cases, forming the $nd \times nd$ linearization explicitly is computationally infeasible due to memory and time constraints. For these **large-scale** problems, **[iterative methods](@entry_id:139472)** are required.

A common approach is the **"linearize-then-Arnoldi"** strategy. One implicitly forms the linearized operator, for example $\mathcal{O} = B^{-1}A$, and applies an iterative Krylov subspace method like the Arnoldi algorithm to find approximations to a few extremal eigenvalues.

However, this approach inherits the potential numerical stability issues of the underlying linearization. A more robust alternative is to use **[structure-preserving methods](@entry_id:755566)** that work directly with the polynomial structure, avoiding the explicit formation of the $nd \times nd$ pencil. For a [quadratic eigenvalue problem](@entry_id:753899) (QEP), one such method is the **Second-Order Arnoldi (SOAR)** algorithm. SOAR constructs a Krylov-like subspace directly from the [second-order system](@entry_id:262182), generating an orthonormal basis of $n$-vectors. Compared to a linearize-then-Arnoldi approach which generates a basis of $2n$-vectors, SOAR has significant advantages :
-   **Memory Footprint**: SOAR requires approximately half the storage for its basis vectors ($nm$ vs. $2nm$ complex numbers for an iteration of length $m$).
-   **Backward Error**: By working directly with the matrices $M, C, K$, SOAR avoids the scaling issues inherent in [linearization](@entry_id:267670) and typically yields a small [backward error](@entry_id:746645) with respect to the QEP structure.

Standard SOAR can suffer from its own numerical instabilities. The **Two-level Orthogonal Arnoldi (TOAR)** algorithm is a more sophisticated variant that adds a second level of [orthogonalization](@entry_id:149208) to the process. TOAR provides enhanced stability, particularly for problems where the [coefficient matrix](@entry_id:151473) norms are badly unbalanced or the leading matrix is ill-conditioned, which are precisely the scenarios where classical SOAR can fail . These second-order methods represent a powerful class of algorithms for tackling large-scale polynomial [eigenvalue problems](@entry_id:142153) robustly and efficiently.