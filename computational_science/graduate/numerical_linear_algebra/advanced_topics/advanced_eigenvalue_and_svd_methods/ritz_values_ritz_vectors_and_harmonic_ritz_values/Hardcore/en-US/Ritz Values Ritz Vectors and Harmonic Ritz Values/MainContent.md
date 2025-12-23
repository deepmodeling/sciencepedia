## Introduction
Solving for the [eigenvalues and eigenvectors](@entry_id:138808) of large matrices is a fundamental task in science and engineering, but direct computation is often impossible due to prohibitive computational costs. Iterative [projection methods](@entry_id:147401) provide a powerful alternative by approximating these eigenpairs from a much smaller, manageable subspace. However, the most common of these, the Rayleigh-Ritz procedure, excels at finding eigenvalues on the exterior of the spectrum but struggles to accurately approximate [interior eigenvalues](@entry_id:750739), creating a significant knowledge gap for many applications. This article provides a comprehensive exploration of [projection methods](@entry_id:147401) to address this challenge.

Across the following sections, you will gain a deep understanding of these powerful numerical techniques. The first section, **"Principles and Mechanisms,"** will dissect the mathematical foundations of the standard Rayleigh-Ritz method and introduce the harmonic Rayleigh-Ritz procedure, a crucial variant designed specifically to target [interior eigenvalues](@entry_id:750739). The second section, **"Applications and Interdisciplinary Connections,"** will move from theory to practice, demonstrating how these methods are the engine behind sophisticated algorithms for both [eigenvalue problems](@entry_id:142153) and the acceleration of linear system solvers in fields like [seismology](@entry_id:203510) and electromagnetics. Finally, the **"Hands-On Practices"** section will offer a series of guided problems to solidify your conceptual and practical understanding, tackling issues from algorithmic efficiency to [numerical stability](@entry_id:146550).

## Principles and Mechanisms

In the pursuit of eigenpairs for large-scale matrices, direct methods are often computationally infeasible. Instead, iterative projection-based techniques are employed, which approximate the eigenpairs from a carefully constructed low-dimensional subspace. This chapter elucidates the foundational principles and mechanisms of two of the most important families of [projection methods](@entry_id:147401): the Rayleigh-Ritz procedure and the harmonic Rayleigh-Ritz procedure. We will dissect their mathematical formulations, explore their geometric interpretations, analyze their strengths and weaknesses, and discuss practical considerations for their implementation.

### The Rayleigh-Ritz Projection Principle

The core idea of [projection methods](@entry_id:147401) is to replace the original $n$-dimensional [eigenvalue problem](@entry_id:143898), $Au = \lambda u$, with a more manageable problem of dimension $m \ll n$ defined on a chosen trial subspace $\mathcal{V} \subset \mathbb{C}^n$. The Rayleigh-Ritz method is the most fundamental of these techniques, specified by a particular choice of projection condition.

Let $\mathcal{V}$ be an $m$-dimensional subspace of $\mathbb{C}^n$. We seek an approximate eigenpair $(\theta, u)$, where the approximate eigenvector $u$ is constrained to lie in $\mathcal{V}$ (i.e., $u \in \mathcal{V} \setminus \{0\}$) and the approximate eigenvalue $\theta \in \mathbb{C}$ is a scalar. The original equation $Au - \lambda u = 0$ will not generally have a solution within this restricted setting. We are therefore left with a residual, $r = Au - \theta u$, which is generally non-zero. The Rayleigh-Ritz method, also known as a Galerkin [projection method](@entry_id:144836), seeks to determine $(\theta, u)$ by enforcing that this residual is orthogonal to the trial subspace $\mathcal{V}$.

This is the **Galerkin [orthogonality condition](@entry_id:168905)**:
$$
Au - \theta u \perp \mathcal{V}
$$
This condition means that for every vector $v \in \mathcal{V}$, the inner product $\langle Au - \theta u, v \rangle = 0$. A pair $(\theta, u)$ that satisfies this condition is called a **Ritz pair**, with $\theta$ being a **Ritz value** and $u$ a **Ritz vector** .

To turn this abstract condition into a computational algorithm, we introduce a basis for the subspace $\mathcal{V}$. The formulation depends on the properties of this basis .

1.  **Orthonormal Basis**: Let the columns of the matrix $Q \in \mathbb{C}^{n \times m}$ form an orthonormal basis for $\mathcal{V}$, such that $Q^*Q = I_m$. Any vector $u \in \mathcal{V}$ can be uniquely expressed as $u = Qy$ for some coefficient vector $y \in \mathbb{C}^m$. The Galerkin condition $r \perp \mathcal{V}$ is equivalent to requiring that the residual be orthogonal to each [basis vector](@entry_id:199546), which can be written in matrix form as $Q^*r = 0$. Substituting $u=Qy$ and $r = Au - \theta u$ yields:
    $$
    Q^*(A(Qy) - \theta(Qy)) = 0
    $$
    By linearity, this becomes:
    $$
    (Q^*AQ)y - \theta(Q^*Q)y = 0
    $$
    Since $Q^*Q = I_m$, the condition simplifies to a [standard eigenvalue problem](@entry_id:755346) of size $m \times m$:
    $$
    (Q^*AQ)y = \theta y
    $$
    The matrix $H = Q^*AQ$ is the [orthogonal projection](@entry_id:144168) of the operator $A$ onto the subspace $\mathcal{V}$. Its eigenvalues are the Ritz values $\theta$, and its eigenvectors $y$ provide the coordinates of the corresponding Ritz vectors $u = Qy$.

2.  **Non-Orthonormal Basis**: If we use a general basis for $\mathcal{V}$ whose columns are represented by a full-rank matrix $W \in \mathbb{C}^{n \times m}$, the same derivation applies. We set $u = Wy$ and enforce the [orthogonality condition](@entry_id:168905) $W^*r = 0$:
    $$
    W^*(A(Wy) - \theta(Wy)) = 0
    $$
    This leads to the $m \times m$ **[generalized eigenvalue problem](@entry_id:151614) (GEP)**:
    $$
    (W^*AW)y = \theta(W^*W)y
    $$
    Here, the matrix $W^*W$ is the Gram matrix of the basis vectors. Since $W$ has full column rank, $W^*W$ is Hermitian [positive definite](@entry_id:149459) and thus invertible, ensuring the GEP is well-posed.

### Geometric and Variational Characterizations of Ritz Pairs

The Galerkin condition $r \perp \mathcal{V}$ has several profound geometric and variational interpretations, which provide deeper insight into the nature of Ritz approximations . Let $P_{\mathcal{V}} = QQ^*$ be the orthogonal projector onto the subspace $\mathcal{V}$.

The condition $r \perp \mathcal{V}$ is equivalent to stating that the orthogonal projection of the residual onto $\mathcal{V}$ is zero: $P_{\mathcal{V}}r = 0$. Substituting $r = Au - \theta u$:
$$
P_{\mathcal{V}}(Au - \theta u) = 0 \implies P_{\mathcal{V}}(Au) - P_{\mathcal{V}}(\theta u) = 0
$$
Since $u \in \mathcal{V}$, it is a fixed point of the projector, so $P_{\mathcal{V}}u = u$. This gives the elegant geometric statement:
$$
P_{\mathcal{V}}(Au) = \theta u
$$
This equation reveals that for a Ritz pair $(\theta, u)$, the vector $\theta u$ is the orthogonal projection of the vector $Au$ onto the subspace $\mathcal{V}$. This carries a crucial implication: among all vectors $v \in \mathcal{V}$, the vector $\theta u$ is the unique vector that minimizes the Euclidean distance $\|Au - v\|_2$. The Ritz pair is therefore the solution to a local best-approximation problem.

Furthermore, a key property connects the Ritz value to the **Rayleigh quotient**, defined for any non-zero vector $x \in \mathbb{C}^n$ as:
$$
\rho(x) = \frac{x^*Ax}{x^*x}
$$
If $(\theta, u)$ is a Ritz pair, the Galerkin condition implies $r \perp u$ (since $u \in \mathcal{V}$). Taking the inner product gives $u^*r = 0$:
$$
u^*(Au - \theta u) = 0 \implies u^*Au - \theta u^*u = 0
$$
Since $u \neq 0$, we can divide by $u^*u$, which yields:
$$
\theta = \frac{u^*Au}{u^*u} = \rho(u)
$$
Thus, every Ritz value is the Rayleigh quotient of its corresponding Ritz vector. For Hermitian matrices, the Ritz values can be shown to be the stationary values of the Rayleigh quotient restricted to the subspace $\mathcal{V}$. This variational characterization forms the basis of the celebrated Courant-Fischer min-max theorem for Ritz values.

It is important to note that the condition $P_{\mathcal{V}}(Au) = \theta u$ does not imply that $\mathcal{V}$ is an **invariant subspace** of $A$. An invariant subspace requires $Au \in \mathcal{V}$ for *all* $u \in \mathcal{V}$. The Ritz condition only requires this for the specific Ritz vectors, and even then, only the projected component of $Au$ is involved. If the residual $r = Au - \theta u$ is non-zero, then $Au$ has a component outside of $\mathcal{V}$.

### The Challenge of Interior Eigenvalues: Harmonic Ritz Methods

The standard Rayleigh-Ritz procedure, particularly when applied to Krylov subspaces $\mathcal{K}_k(A,v) = \mathrm{span}\{v, Av, \dots, A^{k-1}v\}$, is remarkably effective at finding the extremal eigenvalues of a Hermitian matrix. However, its convergence towards [interior eigenvalues](@entry_id:750739) is typically slow and unreliable . This limitation motivates the development of alternative [projection methods](@entry_id:147401) designed specifically to target interior parts of the spectrum.

The **harmonic Rayleigh-Ritz method** is a powerful technique for this purpose. It is a **Petrov-Galerkin** method, meaning its trial subspace $\mathcal{V}$ and test subspace $\mathcal{W}$ are different. Given a target shift $\sigma \in \mathbb{C}$ near a desired interior eigenvalue, the harmonic Ritz method enforces the oblique [orthogonality condition](@entry_id:168905):
$$
Au - \theta u \perp (A - \sigma I)\mathcal{V}
$$
The [test space](@entry_id:755876) is chosen to be $\mathcal{W} = (A - \sigma I)\mathcal{V}$. For a Ritz pair $(\theta, u)$ from this method, $u \in \mathcal{V}$ and the residual $r=Au-\theta u$ is orthogonal to every vector in $(A-\sigma I)\mathcal{V}$ . This leads to a different GEP:
$$
(Q^*(A - \sigma I)^*AQ) y = \theta (Q^*(A - \sigma I)^*Q) y
$$
where $u = Qy$ and $Q$ is an orthonormal basis for $\mathcal{V}$ [@problem_id:3_574_731]. The solutions $\theta$ are called **harmonic Ritz values**.

The power of this method comes from its connection to the **[shift-and-invert](@entry_id:141092)** strategy. An eigenvalue $\lambda$ of $A$ near the shift $\sigma$ corresponds to an eigenvalue $\mu = (\lambda - \sigma)^{-1}$ of the inverted operator $(A - \sigma I)^{-1}$. Crucially, if $\lambda$ is an interior eigenvalue of $A$, $\mu$ will be a large-magnitude, extremal eigenvalue of $(A - \sigma I)^{-1}$. The harmonic Ritz method can be shown to be equivalent to performing a standard Rayleigh-Ritz procedure on the operator $(A - \sigma I)^{-1}$ (with respect to an appropriate subspace) and then mapping the resulting Ritz values $\mu$ back to the spectrum of $A$ via the transformation $\theta = \sigma + 1/\mu$. By turning an interior eigenvalue problem into an extremal one, the harmonic method leverages the strength of the standard Rayleigh-Ritz procedure on a transformed problem.

We can quantify this advantage with a simple model. Consider a Hermitian matrix $A$ and a trial subspace spanned by $\mathbf{v} = \cos(\alpha)\mathbf{u}_j + \sin(\alpha)\mathbf{u}_{j+1}$, where $\mathbf{u}_j, \mathbf{u}_{j+1}$ are consecutive eigenvectors. Let $\lambda_j$ be the target interior eigenvalue. The error in the standard Ritz value $\theta_R$ and the harmonic Ritz value $\theta_H$ (with shift $\sigma$) can be derived . For a small angle $\alpha$ between the trial vector and the true eigenvector $\mathbf{u}_j$, the errors are approximately:
$$
|\theta_R - \lambda_j| \approx \delta \sin^2(\alpha)
$$
$$
|\theta_H - \lambda_j| \approx \left| \frac{a}{b} \right| \delta \sin^2(\alpha)
$$
where $\delta = \lambda_{j+1} - \lambda_j$ is the [spectral gap](@entry_id:144877), $a = \lambda_j - \sigma$, and $b = \lambda_{j+1} - \sigma$. The ratio of the errors is approximately $|a/b|$. If the shift $\sigma$ is chosen close to the target $\lambda_j$, then $|a|$ is small, and this ratio is much less than 1, indicating that the harmonic Ritz value is significantly more accurate. For instance, if $|a| \ll \delta$, then $|b| \approx \delta$ and the error reduction factor is about $|a|/\delta$. However, if the shift $\sigma$ is poorly chosen, the [harmonic approximation](@entry_id:154305) can be less accurate than the standard one.

### Considerations for Non-Normal Matrices

The analysis of [projection methods](@entry_id:147401) becomes significantly more complex when the matrix $A$ is **non-normal** ($A^*A \neq AA^*$). In this case, the eigenvectors may be ill-conditioned and are no longer orthogonal.

A central issue is the relationship between the [residual norm](@entry_id:136782) and the eigenvalue error. For a [normal matrix](@entry_id:185943), a small [residual norm](@entry_id:136782) implies a small eigenvalue error; specifically, for any Ritz pair $(z,v)$, the distance from the Ritz value $z$ to the spectrum $\lambda(A)$ is bounded by the [residual norm](@entry_id:136782): $\mathrm{dist}(z, \lambda(A)) \le \|r\|$ . This provides a reliable [a posteriori error estimate](@entry_id:634571).

For a [non-normal matrix](@entry_id:175080), this is no longer true. A Ritz pair can have an arbitrarily small [residual norm](@entry_id:136782) $\|r\|$ while the Ritz value $z$ is far from any true eigenvalue. The link between residuals and eigenvalue error is broken. The proper tool for understanding this phenomenon is the **pseudospectrum**. The $\epsilon$-[pseudospectrum](@entry_id:138878), $\Lambda_{\epsilon}(A)$, is the set of complex numbers $z$ that are "nearly" eigenvalues, defined as:
$$
\Lambda_{\epsilon}(A) = \{ z \in \mathbb{C} : \sigma_{\min}(A - zI) \le \epsilon \}
$$
where $\sigma_{\min}$ is the smallest [singular value](@entry_id:171660). An equivalent definition is that $z \in \Lambda_{\epsilon}(A)$ if and only if $\|(A - zI)^{-1}\| \ge 1/\epsilon$. For any Ritz pair $(z,v)$ with $\|v\|=1$, it can be shown that $1 \le \|(A-zI)^{-1}\| \|r\|$, which implies $z \in \Lambda_{\|r\|}(A)$.

This is the fundamental result: a Ritz value is guaranteed only to lie within the $\|r\|$-pseudospectrum of $A$. For [normal matrices](@entry_id:195370), $\Lambda_\epsilon(A)$ is simply the union of $\epsilon$-disks around the eigenvalues. For [non-normal matrices](@entry_id:137153), $\Lambda_\epsilon(A)$ can be a much larger set, extending far into the complex plane. This explains why a small $\|r\|$ does not guarantee proximity to an eigenvalue. A practical reliability test for a computed Ritz value $z$ is to examine the structure of the pseudospectrum: if the connected component of $\Lambda_{\|r\|}(A)$ containing $z$ is small, isolated, and contains a single eigenvalue, then $z$ can be considered a reliable approximation .

The harmonic Ritz method remains a vital tool for non-normal problems. The convergence analysis, however, must account for the separate roles of [left and right eigenvectors](@entry_id:173562). The [oblique projection](@entry_id:752867) condition $(Au - \theta u) \perp (A - \sigma I)\mathcal{V}$ is effective because it forces the residual to be nearly orthogonal to the left [invariant subspace](@entry_id:137024), which accelerates convergence of the Ritz value . A unique feature of the harmonic method is that its Ritz values can lie outside the **field of values** of $A$ ($F(A) = \{x^*Ax : \|x\|=1\}$). While standard Ritz values are always confined to $F(A)$, harmonic Ritz values are not, which allows them to effectively approximate [interior eigenvalues](@entry_id:750739) that may lie far from the boundary of $F(A)$ .

### Block Methods and Multiplicity

In many applications, one is interested in computing not just a single eigenpair, but a cluster of them simultaneously. **Block [projection methods](@entry_id:147401)** are designed for this purpose, operating on a block trial subspace $\mathcal{V}$ of dimension $mk$, which can be thought of as seeking $k$ eigenvectors at once.

The **block Rayleigh-Ritz procedure** is a direct generalization of the single-vector case. Given an [orthonormal basis](@entry_id:147779) $Q \in \mathbb{C}^{n \times m}$ for $\mathcal{V}$, the procedure solves the $m \times m$ projected eigenproblem $H y = \lambda y$, where $H = Q^*AQ$. This yields $m$ Ritz pairs $(\lambda_i, Qy_i)$ that approximate a cluster of eigenpairs of $A$ .

A critical question is whether a cluster of distinct eigenvalues of $A$ will be approximated by a cluster of distinct Ritz values. For Hermitian matrices, the theory of [invariant subspace](@entry_id:137024) approximation (e.g., the Davis-Kahan $\sin\Theta$ theorem) provides the answer. If the trial subspace $\mathcal{V}$ is a good approximation of the true invariant subspace $\mathcal{U}$ (i.e., the [principal angles](@entry_id:201254) between them are small), and if the true eigenvalues have sufficient spectral gaps both within the cluster and to the rest of the spectrum, then the Ritz values will be accurate approximations and will remain separated .

Similarly, the **block harmonic Rayleigh-Ritz procedure** can be formulated to find multiple [interior eigenvalues](@entry_id:750739) near a shift $\sigma$. It leads to the $m \times m$ generalized eigenvalue problem :
$$
(Q^*(A-\sigma I)^*AQ)y = \theta (Q^*(A-\sigma I)^*Q)y
$$
A practical issue that can arise in this formulation is the occurrence of **spurious multiplicity**, where the projected GEP has degenerate solutions that do not correspond to any true [spectral multiplicity](@entry_id:184061) of $A$. This [pathology](@entry_id:193640) occurs if the [matrix pencil](@entry_id:751760) $(M_A, M_B) = (Q^*(A-\sigma I)^*AQ, Q^*(A-\sigma I)^*Q)$ is **singular**, meaning $\det(M_A - \lambda M_B)$ is identically zero. To ensure the projected problem is well-posed and has a [discrete set](@entry_id:146023) of $m$ solutions, the pencil must be **regular**. A [sufficient condition](@entry_id:276242) for regularity is that the matrix $M_B = Q^*(A-\sigma I)^*Q$ is nonsingular . This highlights that the [well-posedness](@entry_id:148590) of the harmonic Ritz method depends on a delicate interaction between the operator, the shift, and the chosen subspace.