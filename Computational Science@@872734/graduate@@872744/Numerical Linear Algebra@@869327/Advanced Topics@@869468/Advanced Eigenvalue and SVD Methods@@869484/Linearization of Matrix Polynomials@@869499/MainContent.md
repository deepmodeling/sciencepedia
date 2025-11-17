## Introduction
The [polynomial eigenvalue problem](@entry_id:753575) (PEP), a cornerstone of modern computational science and engineering, presents a significant challenge due to its inherent nonlinearity. Solving for the eigenvalues and eigenvectors of matrix polynomials is crucial for understanding phenomena ranging from [mechanical vibrations](@entry_id:167420) to the stability of numerical algorithms. The key to tackling this nonlinear problem lies in a powerful and elegant transformation: linearization. This technique recasts the high-degree polynomial problem into a larger, but linear, system that can be solved using the mature and robust tools of numerical linear algebra.

This article provides a thorough guide to the theory and practice of [linearization](@entry_id:267670). We will begin in the **Principles and Mechanisms** chapter by dissecting the core idea of converting a PEP into a generalized eigenvalue problem (GEP). We will formalize this transformation with precise definitions, introduce the concept of [strong linearization](@entry_id:755534) to handle the complete spectral structure, and examine canonical constructions like companion pencils. Next, the **Applications and Interdisciplinary Connections** chapter will bridge theory and practice by showcasing how [linearization](@entry_id:267670) is applied to solve tangible problems in engineering and physics, while also exploring the critical numerical challenges of stability, scaling, and structure preservation. Finally, the **Hands-On Practices** section will offer a series of targeted exercises designed to solidify your understanding of these fundamental concepts, from verifying the eigenstructure of a companion pencil to appreciating the benefits of using different polynomial bases for improved numerical stability.

## Principles and Mechanisms

The solution of the [polynomial eigenvalue problem](@entry_id:753575) (PEP), finding scalars $\lambda$ and nonzero vectors $x$ such that $P(\lambda)x = 0$, is a cornerstone of many applications in science and engineering. While the problem is nonlinear in $\lambda$, its solution is most commonly achieved by transforming it into a linear problem of a larger dimension. This process, known as **linearization**, is the central mechanism we will explore in this chapter. We will dissect the theoretical underpinnings of linearization, establish the conditions for a valid transformation, present canonical constructions, and discuss the practical workflow for solving the PEP numerically.

### From Polynomial to Linear: The Core Idea

At its heart, linearization is a technique of variable substitution that recasts a high-degree polynomial equation into a larger system of degree-one equations. To grasp this intuitively, consider the quadratic matrix polynomial (QEP) given by

$$
P(\lambda)x = (A_2 \lambda^2 + A_1 \lambda + A_0)x = 0
$$

where $A_i \in \mathbb{C}^{n \times n}$ are coefficient matrices and $x \in \mathbb{C}^n$ is the eigenvector we seek. The challenge is the $\lambda^2$ term. We can eliminate it by introducing a new vector variable. Let us define a new vector $v_1 = \lambda x$. The original equation can then be expressed using both $x$ and $v_1$:

$$
A_2 \lambda (\lambda x) + A_1 (\lambda x) + A_0 x = 0 \implies A_2 \lambda v_1 + A_1 v_1 + A_0 x = 0
$$

This gives us a system of two vector equations, one algebraic and one definitional:

$$
\begin{cases} (\lambda A_2 + A_1)v_1 + A_0 x = 0 \\ \lambda x - v_1 = 0 \end{cases}
$$

This system can be written in a single matrix-vector equation by defining a new, larger vector $v = \begin{pmatrix} v_1 \\ x \end{pmatrix} \in \mathbb{C}^{2n}$. The system becomes a generalized eigenvalue problem (GEP) $L(\lambda)v=0$:

$$
\begin{pmatrix} \lambda A_2 + A_1  A_0 \\ -I  \lambda I \end{pmatrix} \begin{pmatrix} v_1 \\ x \end{pmatrix} = 0
$$

The resulting $2n \times 2n$ matrix $L(\lambda)$ is an [affine function](@entry_id:635019) of $\lambda$, known as a **[matrix pencil](@entry_id:751760)**. We have successfully converted the quadratic $n \times n$ problem into a linear $2n \times 2n$ problem. This construction, known as the **first [companion form](@entry_id:747524)**, demonstrates the essence of [linearization](@entry_id:267670): embedding the PEP into a GEP of a larger size [@problem_id:3556314]. The genius of this approach is that the eigenvalues of the pencil $L(\lambda)$ are the same as the eigenvalues of the original polynomial $P(\lambda)$.

### Formalizing Equivalence: Definitions of Linearization

For a linearization to be valid, the new linear problem must be "equivalent" to the original polynomial problem. This equivalence must be mathematically precise. A fundamental property we require is that the finite eigenvalues of the pencil and the polynomial must be identical, including their algebraic and geometric multiplicities.

First, we must distinguish between two classes of matrix polynomials. A matrix polynomial $P(\lambda)$ is called **regular** if its determinant, $\det P(\lambda)$, is not identically the zero polynomial. Otherwise, $P(\lambda)$ is called **singular**. For a regular polynomial, $\det P(\lambda)$ is a scalar polynomial whose roots are a [discrete set](@entry_id:146023) of points in the complex plane; these are the finite eigenvalues of $P(\lambda)$. If a polynomial is singular, any $\lambda \in \mathbb{C}$ can be an eigenvalue, and the problem is often ill-posed. The theory of [linearization](@entry_id:267670) is most cleanly developed for regular polynomials [@problem_id:3556354].

The most rigorous and general definition of linearization is based on the concept of unimodular equivalence. A square matrix polynomial $U(\lambda)$ is **unimodular** if its determinant is a nonzero constant, which implies that its inverse $U(\lambda)^{-1}$ is also a matrix polynomial. A pencil $L(\lambda)$ of size $dn \times dn$ is a **[linearization](@entry_id:267670)** of an $n \times n$ matrix polynomial $P(\lambda)$ of degree $d$ if there exist [unimodular matrix](@entry_id:148345) polynomials $E(\lambda)$ and $F(\lambda)$ such that:

$$
E(\lambda) L(\lambda) F(\lambda) = \begin{pmatrix} P(\lambda)  0 \\ 0  I_{(d-1)n} \end{pmatrix}
$$

This relationship ensures that the elementary divisor structure of $L(\lambda)$ related to finite eigenvalues is identical to that of $P(\lambda)$ [@problem_id:3556353]. Elementary divisors encode the full Jordan structure of an eigenvalue (i.e., both its algebraic and geometric multiplicities). This deep connection guarantees that the finite spectra are perfectly matched. A direct consequence of this equivalence is a simpler, albeit weaker, condition on the [determinants](@entry_id:276593) [@problem_id:3556331]. Taking determinants on both sides of the unimodular equivalence relation, we find that:

$$
\det(E(\lambda)) \det(L(\lambda)) \det(F(\lambda)) = \det(P(\lambda))
$$

Since $E(\lambda)$ and $F(\lambda)$ are unimodular, their determinants are nonzero constants. This implies that for some nonzero constant $c$,

$$
\det(L(\lambda)) = c \cdot \det(P(\lambda))
$$

This identity confirms that the roots of $\det L(\lambda)$ and $\det P(\lambda)$ are the same, which means the finite eigenvalues and their algebraic multiplicities are preserved [@problem_id:3556314].

### Handling Infinity: The Reversal Polynomial and Strong Linearization

A regular polynomial of degree $d$ is expected to have $dn$ eigenvalues, but what happens if the degree of $\det P(\lambda)$ is less than $dn$? This occurs when the leading [coefficient matrix](@entry_id:151473) $A_d$ is singular (i.e., $\det(A_d) = 0$). In such cases, the "missing" eigenvalues are said to be at infinity [@problem_id:3556354]. To analyze these infinite eigenvalues, we use a mapping that brings infinity to the origin.

This is accomplished via the **[reversal polynomial](@entry_id:754325)**. The reversal of grade $d$ of $P(\lambda)$ is defined as:

$$
\operatorname{rev}_d P(\lambda) = \lambda^d P(1/\lambda) = \sum_{i=0}^d A_{d-i} \lambda^i = A_d + A_{d-1}\lambda + \dots + A_0\lambda^d
$$

With this definition, an eigenvalue of $P(\lambda)$ at $\lambda = \infty$ corresponds to an eigenvalue of $\operatorname{rev}_d P(\lambda)$ at $\lambda = 0$. An eigenvalue at $\lambda=0$ exists if and only if the constant term of the polynomial is singular. For $\operatorname{rev}_d P(\lambda)$, the constant term is $A_d$. Thus, $P(\lambda)$ has an eigenvalue at infinity if and only if $A_d$ is singular [@problem_id:3556312].

It is crucial here to distinguish between the **degree** of a polynomial, which is the highest power with a nonzero [coefficient matrix](@entry_id:151473), and its **grade**, which is a formal integer $d$ used in its representation and in constructing the [linearization](@entry_id:267670). If we choose a grade $d$ that is strictly larger than the degree $k$ of $P(\lambda)$, we are implicitly setting the leading coefficients $A_{k+1}, \dots, A_d$ to zero. Since $A_d=0$ in this case, this choice artificially introduces eigenvalues at infinity. For a regular polynomial of degree $k$ with nonsingular $A_k$, representing it with grade $d > k$ results in exactly $n(d-k)$ eigenvalues at infinity [@problem_id:3556293].

A good [linearization](@entry_id:267670) must preserve not only the finite eigenvalues but also this infinite eigenstructure. This leads to the definition of a **[strong linearization](@entry_id:755534)**. A pencil $L(\lambda)$ is a [strong linearization](@entry_id:755534) of $P(\lambda)$ if $L(\lambda)$ is a linearization of $P(\lambda)$ and, additionally, the reversal of the pencil, $\operatorname{rev}_1 L(\lambda)$, is a linearization of the reversal of the polynomial, $\operatorname{rev}_d P(\lambda)$ [@problem_id:3556353]. This dual property ensures that the complete spectral information of $P(\lambda)$—finite eigenvalues, infinite eigenvalues, and their full Jordan structures—is faithfully encoded in the pencil $L(\lambda)$ [@problem_id:3556312].

For singular polynomials, which possess a [continuous spectrum](@entry_id:153573) and a non-trivial nullspace, strong linearizations also preserve the **minimal indices**, which are degrees of the polynomial vectors forming a basis for the nullspace. This complete structural preservation makes strong linearizations the gold standard for solving polynomial [eigenvalue problems](@entry_id:142153).

### Canonical Constructions: Companion Pencils

With the theoretical framework in place, we can now examine some canonical constructions of linearizations. The most widely known are the **Frobenius companion pencils**. For a degree-$d$ matrix polynomial $P(\lambda) = \sum_{i=0}^d A_i \lambda^i$, two classical forms are the first and second companion pencils.

If $P(\lambda)$ is monic (i.e., $A_d = I$), the **second companion pencil** can be written as $L(\lambda) = \lambda I_{dn} - C$, where $C$ is the block companion matrix [@problem_id:3556335]:

$$
C = \begin{pmatrix}
0  I_n  0  \cdots  0 \\
0  0  I_n  \cdots  0 \\
\vdots  \vdots  \ddots  \ddots  \vdots \\
0  0  \cdots  0  I_n \\
-A_0  -A_1  \cdots  -A_{d-2}  -A_{d-1}
\end{pmatrix}
$$

A closely related form, often called the **first companion pencil**, is the block transpose of a similar construction. For a [monic polynomial](@entry_id:152311) of degree $d$, it can be written as [@problem_id:3556338]:

$$
L(\lambda) = \begin{pmatrix}
\lambda I_n + A_{d-1}  A_{d-2}  \cdots  A_0 \\
-I_n  \lambda I_n  \cdots  0 \\
\vdots  \ddots  \ddots  \vdots \\
0  \cdots  -I_n  \lambda I_n
\end{pmatrix}
$$
(Note: The [exact forms](@entry_id:269145) and naming conventions can vary, but the underlying structure and properties are consistent). For a general polynomial (not necessarily monic), these pencils are constructed as generalized [eigenvalue problems](@entry_id:142153) $L(\lambda) = \lambda B + A$. For instance, the first companion pencil for a general $P(\lambda)$ is:

$$
L(\lambda) = \lambda \begin{pmatrix} A_d  0  \cdots  0 \\ 0  I_n  \cdots  0 \\ \vdots  \ddots  \ddots  \vdots \\ 0  \cdots  0  I_n \end{pmatrix} + \begin{pmatrix} A_{d-1}  A_{d-2}  \cdots  A_0 \\ -I_n  0  \cdots  0 \\ \vdots  \ddots  \ddots  \vdots \\ 0  \cdots  -I_n  0 \end{pmatrix}
$$

These companion pencils are strong linearizations for any regular matrix polynomial $P(\lambda)$. If $A_d$ is nonsingular, $P(\lambda)$ has $dn$ finite eigenvalues and no infinite eigenvalues. The [companion linearization](@entry_id:747525) $L(\lambda)$ will also have $dn$ finite eigenvalues and no infinite eigenvalues, as its $\lambda$-[coefficient matrix](@entry_id:151473) will be invertible [@problem_id:3556331].

### From Theory to Practice: Numerical Solution and Eigenvector Recovery

Linearization provides a practical pathway to solving the PEP numerically. The standard workflow is as follows:
1.  Given the matrix polynomial $P(\lambda)$ with coefficients $A_0, \dots, A_d$.
2.  Construct a companion pencil, such as $L(\lambda) = \lambda B + A$, of size $dn \times dn$.
3.  Solve the resulting generalized eigenvalue problem $Av = -\lambda Bv$ using a numerically stable algorithm. The standard method for dense, moderate-sized pencils is the **QZ algorithm**.
4.  The QZ algorithm computes the generalized eigenvalues $\lambda$ and the corresponding eigenvectors $v$ of the pencil.
5.  Recover the eigenvectors $x$ of the original polynomial $P(\lambda)$ from the eigenvectors $v$ of the pencil.

The QZ algorithm is a backward stable method that computes the generalized Schur decomposition of the pair $(A, B)$, from which the eigenvalues are readily obtained. For a dense $dn \times dn$ pencil, its computational cost is $\mathcal{O}((dn)^3)$ floating-point operations, and it requires $\mathcal{O}((dn)^2)$ memory to store the matrices. It is important to note that the standard QZ algorithm does not preserve the sparse block structure of companion pencils; it densifies the matrices during its iterations [@problem_id:3556297].

A critical final step is **eigenvector recovery**. Finding the eigenvalues is often only half the battle. Fortunately, the eigenvectors of the original polynomial are embedded within the eigenvectors of the companion pencil. The exact relationship depends on the chosen [companion form](@entry_id:747524). For the first companion pencil shown in the previous section, if $v = \begin{bmatrix} v_1^T  v_2^T  \cdots  v_d^T \end{bmatrix}^T$ is an eigenvector of $L(\lambda)$ for a finite eigenvalue $\lambda$, then the corresponding eigenvector $x$ of $P(\lambda)$ is simply the last block, $x=v_d$. The other blocks are related by $v_k = \lambda^{d-k} v_d$ [@problem_id:3556314]. For another common [companion form](@entry_id:747524), the eigenvector $x$ is the first block, and the remaining blocks follow a "Vandermonde" structure, i.e., $v = \begin{bmatrix} x^T  (\lambda x)^T  \cdots  (\lambda^{d-1}x)^T \end{bmatrix}^T$ [@problem_id:3556338]. This explicit structure allows for robust and straightforward recovery of the desired physical eigenvectors.

### A Broader Perspective: The Fiedler Family of Linearizations

The classical companion pencils are just two examples from a much larger universe of possible linearizations. A significant advancement in the field was the discovery of **Fiedler pencils**, a unified family of linearizations that includes the classical companion forms as special cases.

The construction of a Fiedler pencil for a degree-$d$ polynomial is parameterized by a permutation $\sigma$ of the indices $\{0, 1, \dots, d-1\}$. This permutation dictates the order in which elementary block-matrix factors, built from the coefficients $A_i$, are multiplied to form the pencil $L_\sigma(\lambda) = \lambda B_\sigma + A_\sigma$ [@problem_id:3556306].

The Fiedler family is theoretically important for several reasons:
1.  **Generality:** For any regular matrix polynomial $P(\lambda)$, every Fiedler pencil is a [strong linearization](@entry_id:755534). This holds regardless of whether the leading coefficient $A_d$ is singular or if the polynomial is monic.
2.  **Unification:** The first and second companion forms correspond to the identity permutation $\sigma = (0, 1, \dots, d-1)$ and the reverse-order permutation $\sigma = (d-1, \dots, 1, 0)$, respectively, bringing these classical forms under a single theoretical roof.
3.  **Structural Variety:** Different permutations can generate pencils with different block structures. For instance, specific palindromic [permutations](@entry_id:147130) can produce block-symmetric or block-tridiagonal pencils. This is immensely useful when the original polynomial has symmetries (e.g., palindromic or alternating), as a structure-preserving linearization can lead to more efficient and accurate numerical solutions.

The discovery of Fiedler pencils and their generalizations has opened a rich area of research, providing a systematic way to generate a wide variety of linearizations, allowing practitioners to choose a [linearization](@entry_id:267670) whose structure is best suited for their specific problem.