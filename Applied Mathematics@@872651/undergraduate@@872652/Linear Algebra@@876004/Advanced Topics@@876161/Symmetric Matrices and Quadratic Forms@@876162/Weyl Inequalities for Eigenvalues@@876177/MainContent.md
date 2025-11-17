## Introduction
In linear algebra, eigenvalues offer deep insights into the properties of a matrix. A fundamental question arises when combining systems: if we know the eigenvalues of matrices $A$ and $B$, what can we say about the eigenvalues of their sum, $A+B$? The relationship is not a simple sum, but a more subtle interplay described by a powerful set of bounds known as Weyl's inequalities. These inequalities address this knowledge gap by providing a rigorous framework to constrain the eigenvalues of the sum, but only under the critical condition that the matrices are Hermitian (or symmetric for real matrices).

This article provides a comprehensive exploration of Weyl's inequalities. Across the following chapters, you will gain a robust understanding of this cornerstone of [matrix analysis](@entry_id:204325).

- The first chapter, **Principles and Mechanisms**, delves into the theoretical foundations of the inequalities. It introduces the Courant-Fischer [minimax principle](@entry_id:170647) and uses it to derive the bounds for both extremal and intermediate eigenvalues, establishing why the Hermitian property is essential.

- The second chapter, **Applications and Interdisciplinary Connections**, demonstrates the immense practical utility of these bounds. We will explore how Weyl's inequalities are applied in perturbation theory, quantum mechanics, stability analysis in engineering, network science, and numerical methods.

- Finally, the **Hands-On Practices** section provides opportunities to apply these concepts through guided problems, solidifying your intuition and analytical skills.

By navigating these sections, you will learn not only the mathematical statement of Weyl's inequalities but also how to wield them as a predictive tool in diverse scientific and engineering contexts.

## Principles and Mechanisms

In the study of linear algebra, understanding the eigenvalues of a matrix is of paramount importance. They reveal fundamental properties of the linear transformation the matrix represents. A central question that arises naturally is: if we know the eigenvalues of two matrices, $A$ and $B$, what can we determine about the eigenvalues of their sum, $A+B$? At first glance, one might hope for a simple relationship, such as the eigenvalues of the sum being the sum of the individual eigenvalues. However, this is only true in very specific circumstances. In general, the relationship is far more subtle and is described not by equalities, but by a powerful set of inequalities known as **Weyl's inequalities**.

This chapter explores the principles and mechanisms behind Weyl's inequalities. These inequalities provide rigorous bounds on the eigenvalues of the sum of two **Hermitian matrices**. A matrix $M$ is defined as **Hermitian** if it is equal to its own [conjugate transpose](@entry_id:147909), denoted $M = M^\dagger$. For real matrices, this condition simplifies to being **symmetric**, where $M = M^T$. A key property of Hermitian matrices is that their eigenvalues are always real, which makes them suitable for representing physical observables like energy in quantum mechanics or stress in materials science.

It is crucial to emphasize that the results we will discuss are specific to Hermitian matrices. For general, non-Hermitian matrices, such relationships do not hold. To illustrate this, consider two real, [non-symmetric matrices](@entry_id:153254):
$$
A = \begin{pmatrix} 1 & 10 \\ 0 & 2 \end{pmatrix} \quad \text{and} \quad B = \begin{pmatrix} 3 & 0 \\ 10 & 4 \end{pmatrix}
$$
Since both matrices are triangular, their eigenvalues are simply their diagonal entries. The eigenvalues of $A$ are $\{1, 2\}$, so its largest eigenvalue is $\lambda_1(A) = 2$. The eigenvalues of $B$ are $\{3, 4\}$, so its largest eigenvalue is $\lambda_1(B) = 4$. One might naively guess that the largest eigenvalue of their sum, $C=A+B$, is bounded by $\lambda_1(A) + \lambda_1(B) = 6$. However, calculating the sum gives:
$$
C = A+B = \begin{pmatrix} 4 & 10 \\ 10 & 6 \end{pmatrix}
$$
The eigenvalues of $C$ are the roots of the characteristic equation $\lambda^2 - 10\lambda - 76 = 0$, which are $5 \pm \sqrt{101}$. The largest eigenvalue is $\lambda_1(C) = 5 + \sqrt{101} \approx 15.05$. In this case, $\lambda_1(A+B)$ is significantly greater than $\lambda_1(A) + \lambda_1(B)$ [@problem_id:1402053]. This [counterexample](@entry_id:148660) highlights why the Hermitian property is an essential prerequisite for Weyl's inequalities.

### The Courant-Fischer Minimax Principle

The theoretical foundation for Weyl's inequalities is the **Courant-Fischer [minimax principle](@entry_id:170647)**. This theorem provides a way to characterize the eigenvalues of a Hermitian matrix without computing its [characteristic polynomial](@entry_id:150909). It does so using the **Rayleigh quotient**, defined for a non-zero vector $x$ as:
$$
R_M(x) = \frac{x^\dagger M x}{x^\dagger x}
$$
For a Hermitian matrix $M$, the Rayleigh quotient is always a real number. If $x$ is an eigenvector of $M$ with eigenvalue $\lambda$, then $R_M(x) = \lambda$. The Courant-Fischer theorem extends this, stating that all eigenvalues can be found by optimizing the Rayleigh quotient over subspaces of varying dimensions.

Let $M$ be an $n \times n$ Hermitian matrix with eigenvalues sorted in descending order: $\lambda_1 \ge \lambda_2 \ge \dots \ge \lambda_n$. The theorem states:
$$
\lambda_k = \max_{\dim(S)=k} \left( \min_{x \in S, x\neq 0} R_M(x) \right) = \min_{\dim(S)=n-k+1} \left( \max_{x \in S, x\neq 0} R_M(x) \right)
$$
where $S$ denotes a subspace of the vector space $\mathbb{C}^n$. The first part, the "max-min" formulation, is particularly useful. For instance, the largest eigenvalue is simply the maximum value of the Rayleigh quotient over all vectors: $\lambda_1 = \max_{x \neq 0} R_M(x)$. This [variational characterization of eigenvalues](@entry_id:155784) is the key tool used to prove Weyl's inequalities.

### Bounds for Extremal Eigenvalues

Let's begin by applying this principle to the most straightforward cases: the largest and smallest eigenvalues of a sum of two $n \times n$ Hermitian matrices, $A$ and $B$. Let the eigenvalues of $A$, $B$, and $C = A+B$ be denoted by $\{\alpha_i\}$, $\{\beta_i\}$, and $\{\gamma_i\}$ respectively, all sorted in descending order.

The largest eigenvalue of the sum, $\gamma_1$, can be expressed using the Rayleigh quotient:
$$
\gamma_1 = \max_{x \neq 0} R_{A+B}(x) = \max_{x \neq 0} \frac{x^\dagger(A+B)x}{x^\dagger x} = \max_{x \neq 0} \left( \frac{x^\dagger A x}{x^\dagger x} + \frac{x^\dagger B x}{x^\dagger x} \right)
$$
Since the maximum of a sum is less than or equal to the sum of the maxima, we have:
$$
\gamma_1 \le \max_{x \neq 0} \frac{x^\dagger A x}{x^\dagger x} + \max_{x \neq 0} \frac{x^\dagger B x}{x^\dagger x}
$$
Recognizing the terms on the right as the largest eigenvalues of $A$ and $B$, we arrive at the inequality for the largest eigenvalue:
$$
\gamma_1 \le \alpha_1 + \beta_1
$$
This result, known as the [subadditivity](@entry_id:137224) of the maximum eigenvalue, is a cornerstone of [matrix analysis](@entry_id:204325). For example, in a quantum system where a Hamiltonian $A$ is perturbed by an interaction $B$, this inequality provides a direct upper bound on the new highest energy level [@problem_id:1402039]. If the eigenvalues of $A$ are $\{4, 1, 1\}$ and the eigenvalues of $B$ are $\{\sqrt{2}, 0, -\sqrt{2}\}$, then the largest eigenvalue of $A+B$ cannot exceed $4 + \sqrt{2} \approx 5.414$.

A similar argument can be made for the smallest eigenvalue. Using the "min-max" characterization $\lambda_n = \min_{x \neq 0} R_M(x)$, we find:
$$
\gamma_n = \min_{x \neq 0} (R_A(x) + R_B(x)) \ge \min_{x \neq 0} R_A(x) + \min_{x \neq 0} R_B(x)
$$
This leads to the inequality for the [smallest eigenvalue](@entry_id:177333):
$$
\gamma_n \ge \alpha_n + \beta_n
$$
For instance, if matrix $A$ has a smallest eigenvalue of $1$ and matrix $B$ has a [smallest eigenvalue](@entry_id:177333) of $4$, then their sum $A+B$ must have a smallest eigenvalue of at least $1+4=5$ [@problem_id:1402081].

While $\gamma_1 \le \alpha_1 + \beta_1$ provides an upper bound, a lower bound is also available. A more complete set of bounds for the largest eigenvalue is given by:
$$
\max(\alpha_1 + \beta_n, \alpha_n + \beta_1) \le \gamma_1 \le \alpha_1 + \beta_1
$$
Consider matrices $A$ and $B$ with eigenvalues $\alpha = \{5, 2, -1\}$ and $\beta = \{7, 0, -4\}$. The largest eigenvalue of their sum, $\gamma_1$, is bounded above by $\gamma_1 \le 5+7=12$. For the lower bound, we check $\alpha_1+\beta_3 = 5+(-4)=1$ and $\alpha_3+\beta_1 = -1+7=6$. Thus, $\gamma_1$ must be greater than or equal to $\max(1, 6) = 6$. The complete range for the largest eigenvalue is therefore $[6, 12]$. These bounds are tight, meaning there exist specific matrices $A$ and $B$ with these spectra for which $\gamma_1$ can achieve both the minimum value of $6$ and the maximum value of $12$ [@problem_id:1402043].

### The General Weyl Inequalities

The principles applied to the extremal eigenvalues can be generalized to any eigenvalue $\gamma_k$. This yields the full Weyl inequalities. For $n \times n$ Hermitian matrices $A$ and $B$ with eigenvalues $\{\alpha_i\}$ and $\{\beta_i\}$ sorted in descending order, the eigenvalues $\{\gamma_i\}$ of $C=A+B$ satisfy several related bounds.

A commonly cited version of Weyl's inequality states:
$$
\alpha_k + \beta_n \le \gamma_k \le \alpha_k + \beta_1 \quad \text{for } k=1, \dots, n
$$
This provides a simple, direct interval for each $\gamma_k$. A more powerful and sharper set of bounds is given by:
$$
\max_{i+j=k+n} (\alpha_i + \beta_j) \le \gamma_k \le \min_{i+j=k+1} (\alpha_i + \beta_j) \quad \text{for } k=1, \dots, n
$$
Here, the indices $i$ and $j$ range from $1$ to $n$. Let's analyze this with a concrete example. Suppose $A$ and $B$ are $3 \times 3$ [symmetric matrices](@entry_id:156259). The eigenvalues of $A$ are $\{10, 5, -2\}$ and the eigenvalues of $B$ are $\{4, 1, -3\}$. We want to find the tightest possible interval for $\gamma_2$, the middle eigenvalue of $C=A+B$. Here, $n=3$ and $k=2$.

First, we find the upper bound using the condition $i+j=k+1=3$. The possible pairs of indices $(i,j)$ are $(1,2)$ and $(2,1)$.
- For $(i,j)=(1,2)$: $\alpha_1 + \beta_2 = 10 + 1 = 11$.
- For $(i,j)=(2,1)$: $\alpha_2 + \beta_1 = 5 + 4 = 9$.
The upper bound is the minimum of these values: $U = \min(11, 9) = 9$.

Next, we find the lower bound using the condition $i+j=k+n=5$. The possible pairs of indices $(i,j)$ are $(2,3)$ and $(3,2)$.
- For $(i,j)=(2,3)$: $\alpha_2 + \beta_3 = 5 + (-3) = 2$.
- For $(i,j)=(3,2)$: $\alpha_3 + \beta_2 = -2 + 1 = -1$.
The lower bound is the maximum of these values: $L = \max(2, -1) = 2$.

Therefore, we can guarantee that the eigenvalue $\gamma_2$ lies within the interval $[2, 9]$ [@problem_id:1402031]. It is instructive to note that in this particular case, the simpler inequality $\alpha_2 + \beta_3 \le \gamma_2 \le \alpha_2 + \beta_1$ gives the same result: $5+(-3) \le \gamma_2 \le 5+4$, or $2 \le \gamma_2 \le 9$. However, the more general formula is guaranteed to be the sharpest possible bound based only on spectral information. This process can be repeated for any eigenvalue [@problem_id:1390096].

### Applications and Special Cases

Weyl's inequalities are not merely a theoretical curiosity; they have profound implications in various fields, particularly in perturbation theory.

#### Perturbation Theory

In many scientific and engineering contexts, we start with a system described by a matrix $A$ and introduce a small change, or **perturbation**, represented by a matrix $E$. The new system is described by $A+E$. We are often interested in how much the eigenvalues of $A$ can shift due to this perturbation. Weyl's inequality provides a direct answer.

Let's use the inequality $\alpha_k + \epsilon_n \le \gamma_k \le \alpha_k + \epsilon_1$, where $\{\epsilon_i\}$ are the eigenvalues of the Hermitian perturbation $E$. Rearranging gives:
$$
\epsilon_n \le \gamma_k - \alpha_k \le \epsilon_1
$$
The shift in the $k$-th eigenvalue is $\delta\lambda_k = \gamma_k - \alpha_k$. The eigenvalues of $E$ are bounded by its largest absolute eigenvalue, which is the **spectral norm**, $\|E\|_2$. That is, $-\|E\|_2 \le \epsilon_n \le \epsilon_1 \le \|E\|_2$. Combining these facts yields a powerful result:
$$
|\delta\lambda_k| = |\gamma_k - \alpha_k| \le \|E\|_2
$$
This means the magnitude of the change in *any* eigenvalue is bounded by the [spectral norm](@entry_id:143091) of the perturbation matrix. For example, if a system is perturbed by a matrix $E$ whose eigenvalues are $\pm\sqrt{0.05}$, the [spectral norm](@entry_id:143091) is $\|E\|_2 = \sqrt{0.05} \approx 0.224$. Therefore, no eigenvalue of the original system can shift by more than approximately $0.224$ [@problem_id:1402064]. This provides a robust guarantee on the stability of a system's eigenvalues under small perturbations. Similarly, if we know a perturbation $V$ has a [spectral norm](@entry_id:143091) no greater than $0.25$, and the unperturbed maximum eigenvalue is $6$, then the new maximum eigenvalue cannot exceed $6+0.25=6.25$ [@problem_id:1402073].

#### Shift by a Scalar Matrix

A particularly elegant special case occurs when the perturbation is a scalar multiple of the identity matrix, $E = cI$. The matrix $cI$ is Hermitian, and all of its $n$ eigenvalues are equal to $c$. Thus, $\epsilon_1 = \epsilon_n = c$. Applying Weyl's inequality $\lambda_k(A) + \lambda_n(cI) \le \lambda_k(A+cI) \le \lambda_k(A) + \lambda_1(cI)$, we get:
$$
\lambda_k(A) + c \le \lambda_k(A+cI) \le \lambda_k(A) + c
$$
This forces an equality. The eigenvalues of $A+cI$, which we can call $\mu_k$, are precisely $\mu_k = \lambda_k(A) + c$. This confirms the elementary and intuitive result that adding a scalar multiple of the identity simply shifts all eigenvalues by that scalar amount. Seeing this emerge from a general and powerful inequality like Weyl's serves as a strong validation of the theorem's correctness [@problem_id:1402026].

#### Commuting Matrices and Equality

A natural question is: when do the inequalities become equalities? The inequalities define a range of possible values for the eigenvalues of the sum. For non-[commuting matrices](@entry_id:192389), the eigenvectors of $A$ and $B$ are different, and the interaction between them leads to the [eigenvalue spread](@entry_id:188513) described by the inequalities.

The situation changes dramatically if $A$ and $B$ **commute**, i.e., $AB=BA$. A [fundamental theorem of linear algebra](@entry_id:190797) states that two Hermitian matrices commute if and only if they are **simultaneously diagonalizable**. This means there exists a single [unitary matrix](@entry_id:138978) $U$ that diagonalizes both $A$ and $B$. In other words, there is a common basis of eigenvectors for both matrices.

Let $\{v_k\}$ be this common set of eigenvectors. Then we have $Av_k = \alpha'_k v_k$ and $Bv_k = \beta'_k v_k$ for each $k$. The sets $\{\alpha'_k\}$ and $\{\beta'_k\}$ are the eigenvalues of $A$ and $B$, but now they are specifically ordered according to the common [eigenbasis](@entry_id:151409). For the sum $A+B$, we have:
$$
(A+B)v_k = Av_k + Bv_k = \alpha'_k v_k + \beta'_k v_k = (\alpha'_k + \beta'_k)v_k
$$
This shows that $v_k$ is also an eigenvector of $A+B$, with eigenvalue $\alpha'_k + \beta'_k$. Therefore, if $A$ and $B$ commute, there exists an ordering of their eigenvalues such that the eigenvalues of $A+B$ are exactly the pairwise sums of the eigenvalues of $A$ and $B$ [@problem_id:1402070]. In this special case, the [eigenvalue problem](@entry_id:143898) for the sum has a precise, simple solution, and the Weyl inequalities are satisfied with equality for this specific pairing.

In summary, Weyl's inequalities provide a rigorous and remarkably tight framework for understanding the spectrum of a sum of Hermitian matrices. Rooted in the variational principles of the Courant-Fischer theorem, they offer essential bounds that are indispensable in perturbation theory and numerous other applications across science and engineering. They elegantly delineate the possible from the impossible, constraining the behavior of eigenvalues when matrices are combined.