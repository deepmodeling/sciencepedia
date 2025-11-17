## Introduction
In the era of big data and complex simulations, solving problems involving enormous matrices is a central challenge in computational science. Direct methods for [solving linear systems](@entry_id:146035) or finding eigenvalues, which scale poorly with matrix size, quickly become infeasible. Krylov subspace methods offer a powerful and elegant alternative, providing a framework for iterative algorithms that can efficiently tackle these massive-scale problems. Instead of manipulating the large matrix directly, these methods cleverly explore a small, carefully constructed subspace to find an approximate solution, making them the cornerstone of modern [numerical linear algebra](@entry_id:144418).

Understanding *why* and *how* these methods work requires a grasp of their underlying mathematical structure, from their construction to their deep connection with polynomial approximation. This article provides a comprehensive exploration of Krylov subspaces. We will begin in "Principles and Mechanisms" by defining these subspaces, detailing their construction via the Arnoldi and Lanczos algorithms, and examining their fundamental properties. Next, "Applications and Interdisciplinary Connections" will showcase their remarkable versatility across fields like computational physics, control theory, and machine learning. Finally, "Hands-On Practices" will offer concrete computational exercises to solidify the theoretical concepts. This journey will equip you with a robust understanding of the engine behind many of the most important numerical algorithms in use today.

## Principles and Mechanisms

Following the introduction to their broad utility, we now delve into the mathematical principles and computational mechanisms that govern Krylov subspaces. This family of subspaces provides a powerful framework for reducing high-dimensional linear algebra problems into a sequence of much smaller, more manageable ones. Our exploration will cover their fundamental definition and construction, their intrinsic properties related to the underlying operator and starting vector, their role in [projection methods](@entry_id:147401) for [solving linear systems](@entry_id:146035) and eigenvalue problems, and an advanced perspective on their convergence behavior through the lens of [polynomial approximation theory](@entry_id:753571).

### Definition and Construction of Krylov Subspaces

At its core, a Krylov subspace is a vector space built from the successive application of a matrix to an initial vector.

Formally, for a given square matrix $A \in \mathbb{C}^{n \times n}$ and a nonzero starting vector $b \in \mathbb{C}^n$, the **$m$-th Krylov subspace**, denoted $\mathcal{K}_m(A, b)$, is the linear span of the first $m$ vectors in the **Krylov sequence** $\{b, Ab, A^2b, \dots\}$:
$$
\mathcal{K}_m(A, b) = \operatorname{span}\{b, Ab, A^2b, \dots, A^{m-1}b\}
$$
This subspace represents the space of all vectors that can be reached from $b$ by applying polynomials in $A$ of degree less than $m$. Specifically, any vector $v \in \mathcal{K}_m(A,b)$ can be written as $v = p(A)b$ for some polynomial $p$ of degree at most $m-1$.

While the definition is straightforward, the basis $\{b, Ab, \dots, A^{m-1}b\}$ is often poorly conditioned for numerical computations, as the vectors $A^k b$ tend to align with the [dominant eigenvector](@entry_id:148010) of $A$. A more stable approach is to construct an orthonormal basis for the nested sequence of Krylov subspaces $\mathcal{K}_1 \subset \mathcal{K}_2 \subset \dots$. The standard algorithm for this purpose is the **Arnoldi process**.

The Arnoldi process is an iterative procedure that uses a modified Gram-Schmidt method to generate a sequence of [orthonormal vectors](@entry_id:152061) $v_1, v_2, \dots, v_m$, called **Arnoldi vectors**, such that for each $k \in \{1, \dots, m\}$, the set $\{v_1, \dots, v_k\}$ forms an [orthonormal basis](@entry_id:147779) for $\mathcal{K}_k(A, b)$. The process starts by normalizing the initial vector: $v_1 = b / \|b\|_2$. Then, for $j=1, 2, \dots, m$, it computes the next vector $v_{j+1}$ by orthogonalizing $Av_j$ against all previous vectors $\{v_1, \dots, v_j\}$ and normalizing the result.

The coefficients generated during this [orthogonalization](@entry_id:149208) process are of paramount importance. They populate an $(m+1) \times m$ **upper Hessenberg matrix**, denoted $\bar{H}_m$. The relationship between $A$, the orthonormal basis vectors, and the Hessenberg matrix is encapsulated in the fundamental **Arnoldi relation**:
$$
A V_m = V_{m+1} \bar{H}_m
$$
where $V_m = [v_1, v_2, \dots, v_m]$ and $V_{m+1} = [v_1, v_2, \dots, v_{m+1}]$ are matrices whose columns are the Arnoldi vectors. The entries of $\bar{H}_m$, denoted $h_{i,j}$, are the projection coefficients $h_{i,j} = v_i^T A v_j$ for $i \leq j$, and the subdiagonal entries $h_{j+1,j}$ are the norms of the residual vectors before normalization. This relation can also be written as a recurrence:
$$
A v_j = \sum_{i=1}^{j+1} h_{i,j} v_i
$$
The Arnoldi relation is the cornerstone of nearly all Krylov subspace methods. It establishes that the action of the large matrix $A$ on the subspace $\mathcal{K}_m(A,b)$ is completely described by the small Hessenberg matrix $\bar{H}_m$. Left-multiplying the Arnoldi relation by $V_m^T$ and using the [orthonormality](@entry_id:267887) of the columns of $V_m$ yields $V_m^T A V_m = H_m$, where $H_m$ is the $m \times m$ [principal submatrix](@entry_id:201119) of $\bar{H}_m$. This shows that $H_m$ is the matrix representation of the [orthogonal projection](@entry_id:144168) of $A$ onto $\mathcal{K}_m(A,b)$.

As a concrete illustration, consider performing two steps of the Arnoldi process for the symmetric matrix $A = \begin{bmatrix} 4 & 1 & 0 \\ 1 & 3 & 1 \\ 0 & 1 & 2 \end{bmatrix}$ with the starting vector $b=e_1$. Since $b$ is already normalized, $v_1 = e_1$. The first iteration proceeds by computing $Av_1 = [4, 1, 0]^T$. The coefficient $h_{11}$ is $v_1^T(Av_1) = 4$. The residual is $Av_1 - h_{11}v_1 = [0, 1, 0]^T$. Its norm is $h_{21} = 1$, and normalizing gives $v_2 = [0, 1, 0]^T$. The second iteration proceeds with $Av_2 = [1, 3, 1]^T$. The coefficients are $h_{12} = v_1^T(Av_2) = 1$ and $h_{22} = v_2^T(Av_2) = 3$. The resulting $2 \times 2$ Hessenberg matrix is $H_2 = \begin{pmatrix} 4 & 1 \\ 1 & 3 \end{pmatrix}$ [@problem_id:3554225]. Notice that because $A$ is symmetric, $H_2$ is also symmetric (and thus tridiagonal). This specialized version of the Arnoldi process for symmetric matrices is known as the **Lanczos algorithm**.

### Fundamental Properties of Krylov Subspaces

The structure and growth of a Krylov subspace are dictated not by the matrix $A$ in isolation, but by the interplay between $A$ and the starting vector $b$.

#### Invariance under Affine Transformations

A key property of Krylov subspaces is their invariance under affine transformations of the generating matrix. For any non-zero scalar $\alpha$ and any scalar $\beta$, the Krylov subspace generated by the matrix $\alpha A + \beta I$ is identical to the one generated by $A$:
$$
\mathcal{K}_m(\alpha A + \beta I, b) = \mathcal{K}_m(A, b)
$$
This can be demonstrated by showing that the [generating sets](@entry_id:190106) for both subspaces span the same space. The vector $(\alpha A + \beta I)b = \alpha(Ab) + \beta b$ is clearly a [linear combination](@entry_id:155091) of $\{b, Ab\}$, so $\mathcal{K}_2(\alpha A + \beta I, b) \subseteq \mathcal{K}_2(A, b)$. Conversely, since $\alpha \neq 0$, we can write $Ab = \frac{1}{\alpha}[(\alpha A + \beta I)b - \beta b]$, showing that $Ab$ lies in $\mathcal{K}_2(\alpha A + \beta I, b)$, which implies the reverse inclusion. By induction, this holds for any degree $m$ [@problem_id:3554240]. This property is foundational to the theory of [preconditioning](@entry_id:141204), where linear systems are transformed to improve convergence properties without altering the underlying search spaces.

#### The Dimension of Krylov Subspaces and Breakdown

The dimension of $\mathcal{K}_m(A, b)$ is not always equal to $m$. It is defined as the number of linearly independent vectors in the Krylov sequence $\{b, Ab, \dots, A^{m-1}b\}$. The sequence of dimensions, $\dim(\mathcal{K}_1) \leq \dim(\mathcal{K}_2) \leq \dots$, is non-decreasing. The dimension ceases to grow at step $d$ if $A^{d}b$ is a linear combination of the preceding vectors $\{b, Ab, \dots, A^{d-1}b\}$. The smallest such integer $d$ is the degree of the **[minimal polynomial](@entry_id:153598) of $A$ with respect to $b$**, $\mu_{A,b}(x)$. This is the unique [monic polynomial](@entry_id:152311) of least degree for which $\mu_{A,b}(A)b = 0$. Once this point is reached, the dimension of the Krylov subspace stabilizes at $d$: $\dim(\mathcal{K}_m(A, b)) = d$ for all $m \geq d$.

This phenomenon is simplest to observe when the starting vector $b$ is an eigenvector of $A$ with eigenvalue $\lambda$. In this case, $Ab = \lambda b$. The Krylov sequence becomes $\{b, \lambda b, \lambda^2 b, \dots\}$, and the subspace $\mathcal{K}_m(A,b)$ is simply $\operatorname{span}\{b\}$ for all $m \geq 1$. The [minimal polynomial](@entry_id:153598) is $\mu_{A,b}(x) = x-\lambda$, which has degree $1$, and the dimension of the subspace is always $1$ [@problem_id:3554222].

More generally, the dimension of the Krylov subspace is determined by the structure of $A$ (its Jordan form) and the components of $b$ along the Jordan chains. For a matrix $A$ with a single Jordan block of size $J$ for eigenvalue $\lambda$, and a starting vector $b$ whose deepest component along the associated Jordan chain is at index $s$, the minimal polynomial is $(x-\lambda)^s$. The vectors $\{b, (A-\lambda I)b, \dots, (A-\lambda I)^{s-1}b\}$ are [linearly independent](@entry_id:148207), while $(A-\lambda I)^s b = 0$. Since $\mathcal{K}_k(A,b)$ has the same span as $\mathcal{K}_k(A-\lambda I, b)$, the dimension grows linearly until it reaches this degree. The dimension of the $k$-th Krylov subspace is precisely $\dim \mathcal{K}_{k}(A,b) = \min(k, s)$ [@problem_id:3554217].

In the Arnoldi process, this dimensional saturation manifests as a **breakdown**. If the dimension of $\mathcal{K}_m(A,b)$ is $d  m$, then at step $d$ of the process, the vector $Av_d$ must lie entirely within the subspace $\mathcal{K}_d(A,b) = \operatorname{span}\{v_1, \dots, v_d\}$. After orthogonalizing $Av_d$ against $\{v_1, \dots, v_d\}$, the resulting residual vector will be zero. Its norm, $h_{d+1,d}$, will be zero, and the process terminates as it is impossible to compute the next orthonormal vector $v_{d+1}$. Such a breakdown is not a failure; rather, it is an informative event. A zero subdiagonal entry $h_{d+1,d}=0$ signifies that the subspace $\mathcal{K}_d(A,b)$ is an **invariant subspace** of $A$. For example, if we apply Arnoldi to $A = \operatorname{diag}(5,3,3)$ with starting vector $b = e_2$, we find $Ab = 3b$. The process generates $q_1 = e_2$ and finds $Aq_1 = 3q_1$. The residual to be normalized is $Aq_1 - (q_1^T A q_1)q_1 = 3q_1 - 3q_1 = 0$. The breakdown occurs at the first step, with $h_{2,1}=0$, indicating that $\mathcal{K}_1(A,b)=\operatorname{span}\{b\}$ is an [invariant subspace](@entry_id:137024), and the algorithm has "deflated" or found an exact eigenpair $(3, e_2)$ [@problem_id:3554255].

### Krylov Subspaces for Projection Methods

The primary utility of Krylov subspaces lies in their use as search spaces for **[projection methods](@entry_id:147401)**. The core idea is to project a large-scale problem involving $A$ onto a small Krylov subspace $\mathcal{K}_m$, solve the resulting small-scale problem, and then "lift" the solution back to the high-dimensional space.

#### Approximating Eigenvalues: The Rayleigh-Ritz Procedure

To find approximate eigenvalues of $A$, we can seek approximate eigenpairs $(\theta, y)$ within the Krylov subspace, where $y \in \mathcal{K}_m(A,b)$. The **Rayleigh-Ritz procedure** formalizes this by enforcing a Galerkin condition on the residual $Ay - \theta y$, requiring it to be orthogonal to the search space $\mathcal{K}_m(A,b)$. If $\{v_1, \dots, v_m\}$ is the orthonormal basis from Arnoldi, we write $y=V_m z$ for some $z \in \mathbb{C}^m$. The condition $V_m^T(AV_m z - \theta V_m z) = 0$ simplifies, using $V_m^T A V_m = H_m$ and $V_m^T V_m = I$, to:
$$
H_m z = \theta z
$$
This means that the best approximations for eigenvalues of $A$ from $\mathcal{K}_m(A,b)$ are simply the eigenvalues of the small Hessenberg matrix $H_m$. These are called **Ritz values**. The corresponding eigenvectors $z$ of $H_m$ can be lifted to form the **Ritz vectors** $y=V_m z$, which serve as approximate eigenvectors of $A$.

The quality of a Ritz pair $(\theta, y)$ is measured by the norm of the residual $\|Ay - \theta y\|_2$. A remarkable result relates this [residual norm](@entry_id:136782) directly to the Arnoldi quantities. If $(\theta, z)$ is an eigenpair of $H_m$ with $\|z\|_2=1$, the corresponding Ritz vector is $y=V_m z$. The [residual norm](@entry_id:136782) is given by the elegant formula:
$$
\|Ay - \theta y\|_2 = h_{m+1,m} |e_m^T z|
$$
where $e_m$ is the last canonical basis vector in $\mathbb{R}^m$. This shows that Ritz values with eigenvectors of $H_m$ that have small last components tend to be better approximations. It also shows that as the process nears a breakdown ($h_{m+1,m} \to 0$), the residuals for all Ritz pairs tend to zero [@problem_id:3554225].

For a symmetric matrix $A$, the Arnoldi process simplifies to the Lanczos algorithm, and the Hessenberg matrix $H_m$ becomes a [symmetric tridiagonal matrix](@entry_id:755732) $T_m$. The Ritz values are then the eigenvalues of this small, structured matrix, which are much easier to compute. For instance, for $A=\operatorname{diag}(1,2,4,8)$ and a specific starting vector $b$, the first two Lanczos steps produce the [tridiagonal matrix](@entry_id:138829) $T_2 = \begin{pmatrix} 15/4  \sqrt{115}/4 \\ \sqrt{115}/4  507/92 \end{pmatrix}$, whose eigenvalues approximate those of $A$ [@problem_id:3554237].

#### Solving Linear Systems: A Petrov-Galerkin Perspective

Krylov methods are most famous for [solving linear systems](@entry_id:146035) $Ax=b$. We seek an approximate solution $x_m$ in the affine space $x_0 + \mathcal{K}_m(A, r_0)$, where $x_0$ is an initial guess and $r_0 = b - Ax_0$ is the initial residual. The approximation has the form $x_m = x_0 + V_m y_m$ for some coefficient vector $y_m \in \mathbb{C}^m$. The choice of $y_m$ is determined by a **Petrov-Galerkin condition**, which imposes an orthogonality constraint on the corresponding residual $r_m = b - Ax_m$. The condition is $r_m \perp \mathcal{L}_m$ for some chosen $m$-dimensional [test space](@entry_id:755876) $\mathcal{L}_m$. Different choices of $\mathcal{L}_m$ lead to different methods.

Two of the most important choices are:

1.  **Full Orthogonalization Method (FOM)**: Here, the [test space](@entry_id:755876) is chosen to be the same as the search space, $\mathcal{L}_m = \mathcal{K}_m(A, r_0)$. This is a Galerkin condition. It requires the residual to be orthogonal to the Krylov subspace itself: $r_m \perp \mathcal{K}_m(A,r_0)$. Using the Arnoldi basis $V_m$, this translates to $V_m^T r_m = 0$. Substituting $r_m = r_0 - A V_m y_m$ and using the Arnoldi relation, this leads to a small $m \times m$ linear system for the coefficients $y_m$:
    $$
    H_m y_m = \beta e_1
    $$
    where $\beta = \|r_0\|_2$ and $v_1 = r_0 / \beta$. The FOM solution is obtained by solving this small system [@problem_id:3554235].

2.  **Generalized Minimal Residual method (GMRES)**: Instead of imposing an [orthogonality condition](@entry_id:168905) directly, GMRES seeks the solution $x_m$ that minimizes the Euclidean norm of the residual, $\|r_m\|_2$. Using the Arnoldi relation, the residual can be written as $r_m = r_0 - V_{m+1} \bar{H}_m y_m = V_{m+1}(\beta e_1 - \bar{H}_m y_m)$. Since $V_{m+1}$ has orthonormal columns, minimizing $\|r_m\|_2$ is equivalent to solving the small $(m+1) \times m$ linear [least-squares problem](@entry_id:164198):
    $$
    \min_{y_m \in \mathbb{C}^m} \|\beta e_1 - \bar{H}_m y_m\|_2
    $$
    The solution to this least-squares problem is characterized by the [normal equations](@entry_id:142238), which state that the residual of the small problem, $\beta e_1 - \bar{H}_m y_m$, is orthogonal to the columns of $\bar{H}_m$. This, in turn, implies that the full-space residual $r_m$ satisfies the oblique [orthogonality condition](@entry_id:168905) $r_m \perp A\mathcal{K}_m(A,r_0)$. Thus, GMRES also fits into the Petrov-Galerkin framework, but with the [test space](@entry_id:755876) $\mathcal{L}_m = A\mathcal{K}_m(A,r_0)$ [@problem_id:3554256] [@problem_id:3554235].

### The Polynomial Interpretation of Krylov Methods

A deeper understanding of Krylov subspace methods, particularly their convergence, comes from viewing them through the lens of [polynomial approximation](@entry_id:137391).

#### Krylov Methods as Polynomial Filters

An iterate $x_m$ in a Krylov method is of the form $x_m = x_0 + q_{m-1}(A)r_0$ for some polynomial $q_{m-1}$ of degree at most $m-1$. The corresponding residual is $r_m = r_0 - A q_{m-1}(A) r_0$. If we define a new polynomial $p_m(z) = 1 - z q_{m-1}(z)$, we see that $p_m$ is a polynomial of degree at most $m$ that satisfies the crucial constraint $p_m(0)=1$. The residual can then be expressed as:
$$
r_m = p_m(A) r_0
$$
This reveals that a Krylov method for linear systems generates a sequence of polynomials $\{p_m\}$ and applies them as "filters" to the initial residual. The constraint $p_m(0)=1$ is necessary and arises directly from the fact that the correction to the solution lies in $\mathcal{K}_m(A, r_0)$ [@problem_id:3554244].

The GMRES algorithm, by minimizing $\|r_m\|_2$, is implicitly finding the polynomial $p_m \in \Pi_m$ (the space of polynomials of degree at most $m$) with $p_m(0)=1$ that minimizes the norm of the resulting vector:
$$
\|r_m^{\text{GMRES}}\|_2 = \min_{p \in \Pi_m, p(0)=1} \|p(A)r_0\|_2
$$

#### Convergence Analysis via Polynomial Approximation

This polynomial formulation is the key to analyzing the convergence of GMRES. While the exact norm $\|p(A)r_0\|_2$ depends on $r_0$ in a complex way, we can obtain bounds by considering the [matrix norm](@entry_id:145006) $\|p(A)\|_2$.

If $A$ is a **[normal matrix](@entry_id:185943)** ($A^H A = A A^H$), then for any polynomial $p$, $\|p(A)\|_2 = \max_{\lambda \in \sigma(A)} |p(\lambda)|$, where $\sigma(A)$ is the spectrum of $A$. This leads to the elegant convergence bound:
$$
\|r_m\|_2 \leq \left( \min_{p \in \Pi_m, p(0)=1} \max_{\lambda \in \sigma(A)} |p(\lambda)| \right) \|r_0\|_2
$$
This bound transforms the analysis of an iterative algorithm into a classic problem in approximation theory: find the polynomial of degree $m$ that is 1 at the origin and has the smallest possible maximum magnitude over the spectrum of $A$ [@problem_id:3554244]. If the spectrum $\sigma(A)$ is contained in a [compact set](@entry_id:136957) $\mathcal{S}$ not containing the origin, we can bound the convergence rate by solving this min-max problem over $\mathcal{S}$.

For the important case where $A$ is [symmetric positive definite](@entry_id:139466) with eigenvalues in an interval $[\alpha, \beta]$ where $0  \alpha \leq \beta$, the optimal polynomial is a scaled and shifted version of the classical **Chebyshev polynomial**, giving the well-known GMRES (and Conjugate Gradient) convergence estimate for this case [@problem_id:3554244]. For more complex spectral sets, such as ellipses in the complex plane, other families of extremal polynomials, like Faber polynomials, are required.

If $A$ is **non-normal**, the situation is more complex. The norm $\|p(A)\|_2$ can be much larger than $\max_{\lambda \in \sigma(A)}|p(\lambda)|$. If $A$ is diagonalizable, $A=V\Lambda V^{-1}$, the bound becomes:
$$
\|r_m\|_2 \leq \kappa(V) \left( \min_{p \in \Pi_m, p(0)=1} \max_{\lambda \in \sigma(A)} |p(\lambda)| \right) \|r_0\|_2
$$
where $\kappa(V)=\|V\|_2 \|V^{-1}\|_2$ is the condition number of the eigenvector matrix. A large $\kappa(V)$ indicates that the matrix is highly non-normal, and convergence may be slow even if the eigenvalues are favorably distributed. This inequality highlights that for [non-normal matrices](@entry_id:137153), the eigenvalues alone do not tell the full story of convergence behavior [@problem_id:3554244].