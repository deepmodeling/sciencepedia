## Introduction
In [functional analysis](@entry_id:146220), the study of [linear operators](@entry_id:149003) on [vector spaces](@entry_id:136837) provides a powerful lens through which to understand complex systems. A fundamental strategy for analyzing these operators is to decompose their action by identifying special, invariant directions—a concept that generalizes the familiar idea of eigenvectors from linear algebra. This leads to the notion of the **[point spectrum](@entry_id:274057)**, the set of all eigenvalues, which often encodes the essential characteristics of the operator and the system it represents. However, moving from finite-dimensional settings to the infinite-dimensional spaces central to functional analysis introduces profound new behaviors and challenges our intuition.

This article provides a comprehensive introduction to the theory and application of the [point spectrum](@entry_id:274057). It bridges the gap between the concrete calculations of linear algebra and the abstract framework required for infinite-[dimensional analysis](@entry_id:140259). Across three chapters, you will gain a robust understanding of this crucial concept. The journey begins in **"Principles and Mechanisms"**, where we will rigorously define the [point spectrum](@entry_id:274057) and explore its core properties, examining how it behaves for special classes of operators like self-adjoint and [unitary operators](@entry_id:151194). Next, **"Applications and Interdisciplinary Connections"** will reveal the power of the [point spectrum](@entry_id:274057) by showcasing its role in solving problems in quantum mechanics, dynamical systems, and differential equations. Finally, **"Hands-On Practices"** will allow you to solidify your knowledge by working through carefully selected problems, connecting abstract theory to concrete computation.

## Principles and Mechanisms

The study of [linear operators](@entry_id:149003) is central to functional analysis, providing a framework to understand transformations on [vector spaces](@entry_id:136837). A particularly illuminating way to analyze an operator is to decompose its action into simpler, more fundamental components. This is achieved by identifying special vectors that are merely scaled by the operator, a concept that generalizes the familiar ideas of [eigenvectors and eigenvalues](@entry_id:138622) from linear algebra to the broader context of [infinite-dimensional spaces](@entry_id:141268). This chapter delves into the **[point spectrum](@entry_id:274057)**, the set of these characteristic scaling factors, exploring its fundamental properties and its behavior for several crucial classes of operators.

### Definition and Fundamental Concepts

Let $V$ be a vector space over a scalar field $\mathbb{K}$ (which will typically be the real numbers $\mathbb{R}$ or the complex numbers $\mathbb{C}$), and let $T: V \to V$ be a [linear operator](@entry_id:136520). A scalar $\lambda \in \mathbb{K}$ is called an **eigenvalue** of $T$ if there exists a **non-zero** vector $v \in V$ such that

$$
Tv = \lambda v
$$

The non-zero vector $v$ is called an **eigenvector** of $T$ corresponding to the eigenvalue $\lambda$. The requirement that an eigenvector be non-zero is crucial; otherwise, any scalar $\lambda$ would satisfy $T(0) = 0 = \lambda \cdot 0$, rendering the definition trivial.

The set of all eigenvalues of an operator $T$ is known as its **[point spectrum](@entry_id:274057)**, denoted by $\sigma_p(T)$.

Conceptually, eigenvectors represent directions in the vector space that are invariant under the transformation $T$. When $T$ acts on an eigenvector, the vector's direction is preserved, and its magnitude is simply scaled by the corresponding eigenvalue.

To make this concrete, consider a [linear operator](@entry_id:136520) $T$ on the real vector space $\mathbb{R}^3$ defined by $T(x,y,z) = (x+y+z, 2y+z, 2x+y)$. Let's test if the vector $v = (1,1,1)$ is an eigenvector. Applying the operator yields:

$$
T(1,1,1) = (1+1+1, 2(1)+1, 2(1)+1) = (3,3,3)
$$

We can see that the resulting vector is a scalar multiple of the original vector $v$:

$$
(3,3,3) = 3 \cdot (1,1,1)
$$

Thus, we have $Tv = 3v$. This confirms that $v = (1,1,1)$ is an eigenvector of $T$, and the corresponding eigenvalue is $\lambda = 3$. Therefore, $3 \in \sigma_p(T)$ [@problem_id:1897546].

In [finite-dimensional spaces](@entry_id:151571), such as $\mathbb{R}^n$ or $\mathbb{C}^n$, where an operator $T$ can be represented by a square matrix $A$, finding the [point spectrum](@entry_id:274057) is a standard procedure. The eigenvalue equation $Av = \lambda v$ can be rewritten as $(A - \lambda I)v = 0$, where $I$ is the identity matrix. For this equation to have a non-zero solution for $v$, the matrix $(A - \lambda I)$ must be singular, which means its determinant must be zero. This gives rise to the **[characteristic equation](@entry_id:149057)**:

$$
\det(A - \lambda I) = 0
$$

The roots of this polynomial equation in $\lambda$ constitute the [point spectrum](@entry_id:274057) of the operator. For example, let's find the eigenvalues for the operator on $\mathbb{C}^2$ represented by the matrix $A = \begin{pmatrix} 0  -i \\ i  0 \end{pmatrix}$ [@problem_id:1897522]. The characteristic equation is:

$$
\det \begin{pmatrix} -\lambda  -i \\ i  -\lambda \end{pmatrix} = (-\lambda)(-\lambda) - (i)(-i) = \lambda^2 - (-i^2) = \lambda^2 - 1 = 0
$$

The equation $\lambda^2 = 1$ has two solutions: $\lambda_1 = 1$ and $\lambda_2 = -1$. These are the eigenvalues of the operator, so $\sigma_p(T) = \{1, -1\}$.

### The Spectral Mapping Theorem for the Point Spectrum

A powerful and elegant property relates the point [spectrum of an operator](@entry_id:272027) $T$ to the [point spectrum](@entry_id:274057) of functions of that operator, such as its powers or its inverse. This relationship is a simplified version of what is more broadly known as the [spectral mapping theorem](@entry_id:264489).

Let's begin with powers of an operator. If $\lambda$ is an eigenvalue of $T$ with eigenvector $v$, what can we say about the operator $T^2 = T \circ T$? Applying $T$ twice to $v$ gives:

$$
T^2 v = T(Tv) = T(\lambda v) = \lambda (Tv) = \lambda (\lambda v) = \lambda^2 v
$$

This shows that if $v$ is an eigenvector of $T$ with eigenvalue $\lambda$, it is also an eigenvector of $T^2$ with eigenvalue $\lambda^2$. By induction, this extends to any positive integer power $n$: if $\lambda \in \sigma_p(T)$, then $\lambda^n \in \sigma_p(T^n)$ [@problem_id:1897520].

A compelling example arises from the differential operator $T$ on the space of infinitely differentiable functions on $(0, \infty)$, defined by $(Tf)(x) = x \frac{d}{dx}f(x)$. A function of the form $f(x) = x^\alpha$ is an eigenfunction of this operator, since:

$$
(Tf)(x) = x \frac{d}{dx}(x^\alpha) = x (\alpha x^{\alpha-1}) = \alpha x^\alpha = \alpha f(x)
$$

So, for any $\alpha \in \mathbb{R}$, $f(x) = x^\alpha$ is an [eigenfunction](@entry_id:149030) with eigenvalue $\alpha$. If we are given that $\lambda = 5$ is an eigenvalue, we know from the property just derived that the operator $T^4$ must have an eigenvalue of $5^4 = 625$.

This principle also extends to invertible operators. If an operator $T$ is invertible, its kernel contains only the [zero vector](@entry_id:156189), which implies that $0$ cannot be an eigenvalue. Now, let $\lambda \in \sigma_p(T)$ with a corresponding eigenvector $v$. Since $T$ is invertible and $\lambda \neq 0$, we can write:

$$
Tv = \lambda v
$$

Applying the inverse operator $T^{-1}$ to both sides yields:

$$
T^{-1}(Tv) = T^{-1}(\lambda v)
$$

$$
v = \lambda T^{-1}v
$$

Dividing by the non-zero scalar $\lambda$, we find:

$$
T^{-1}v = \frac{1}{\lambda} v
$$

This demonstrates that if $\lambda$ is an eigenvalue of an invertible operator $T$, then its reciprocal $\lambda^{-1}$ is an eigenvalue of the inverse operator $T^{-1}$, corresponding to the same eigenvector $v$ [@problem_id:1897506]. As an illustration, consider the [diagonal operator](@entry_id:262993) on the Hilbert space $l^2$ of square-summable sequences, defined by $T(x_1, x_2, \dots) = (\frac{1}{2}x_1, \frac{2}{3}x_2, \dots, \frac{n}{n+1}x_n, \dots)$. The [standard basis vectors](@entry_id:152417) $e_n = (0, \dots, 1, \dots)$ are eigenvectors, with $Te_n = \frac{n}{n+1}e_n$. For $n=5$, the eigenvalue is $\lambda = \frac{5}{6}$. The inverse operator is easily seen to be $T^{-1}(y_1, y_2, \dots) = (2y_1, \frac{3}{2}y_2, \dots, \frac{n+1}{n}y_n, \dots)$. As our principle predicts, the eigenvalue of $T^{-1}$ corresponding to the eigenvector $e_5$ is $\frac{1}{\lambda} = \frac{6}{5}$.

### Point Spectra of Special Classes of Operators

The structure of a Hilbert space, equipped with an inner product $\langle \cdot, \cdot \rangle$, allows us to define special classes of operators whose spectral properties are particularly constrained and physically significant.

#### Idempotent and Projection Operators

An operator $P: V \to V$ is called **idempotent** if applying it twice is the same as applying it once, i.e., $P^2 = P$. Such operators are also known as projections. The [point spectrum](@entry_id:274057) of any [idempotent operator](@entry_id:276377) is remarkably restricted.

Let $\lambda$ be an eigenvalue of $P$ with eigenvector $v \neq 0$, so $Pv = \lambda v$. Applying $P$ again, we get $P^2v = P(\lambda v) = \lambda(Pv) = \lambda(\lambda v) = \lambda^2 v$. But since $P^2=P$, we also have $P^2v = Pv = \lambda v$. Equating the two expressions gives:

$$
\lambda^2 v = \lambda v \implies (\lambda^2 - \lambda)v = 0
$$

As $v$ is non-zero, the scalar part must be zero: $\lambda^2 - \lambda = 0$, or $\lambda(\lambda - 1) = 0$. This implies that the only possible eigenvalues for an [idempotent operator](@entry_id:276377) are $0$ and $1$. Therefore, for any [idempotent operator](@entry_id:276377) $P$, $\sigma_p(P) \subseteq \{0, 1\}$ [@problem_id:1897541].

If the projection $P$ is **non-trivial** (meaning it is neither the zero operator $0$ nor the identity operator $I$), then both $0$ and $1$ must be eigenvalues.
*   Since $P \neq 0$, its range must contain a non-[zero vector](@entry_id:156189) $u$. For such a vector, $u = Pw$ for some $w$. Applying $P$ gives $Pu = P(Pw) = P^2w = Pw = u$. So $Pu=1 \cdot u$, and $1$ is an eigenvalue.
*   Since $P \neq I$, there must be a vector $v$ for which $Pv \neq v$. Consider the non-zero vector $z = v - Pv$. Applying $P$ to $z$ gives $Pz = P(v-Pv) = Pv - P^2v = Pv - Pv = 0$. So $Pz = 0 \cdot z$, and $0$ is an eigenvalue.

Thus, for any non-trivial [idempotent operator](@entry_id:276377), the [point spectrum](@entry_id:274057) is precisely $\{0, 1\}$ [@problem_id:1897531]. This holds true for the important subclass of **orthogonal projections** in a Hilbert space, which are idempotent operators that are also self-adjoint.

#### Self-Adjoint Operators

In a complex Hilbert space $H$, every [bounded linear operator](@entry_id:139516) $T$ has a unique **adjoint operator** $T^*$, which satisfies $\langle Tx, y \rangle = \langle x, T^*y \rangle$ for all $x, y \in H$. An operator is **self-adjoint** if $T = T^*$. This class of operators is foundational in quantum mechanics, where physical observables (like position, momentum, or energy) are represented by [self-adjoint operators](@entry_id:152188). A key postulate is that the possible outcomes of a measurement are the eigenvalues of the corresponding operator. This requires the eigenvalues to be real numbers, a property that is guaranteed for [self-adjoint operators](@entry_id:152188).

To prove this, let $T$ be self-adjoint and let $\lambda$ be an eigenvalue with eigenvector $v \neq 0$. Consider the inner product $\langle Tv, v \rangle$:

$$
\langle Tv, v \rangle = \langle \lambda v, v \rangle = \lambda \langle v, v \rangle = \lambda \|v\|^2
$$

Now, using the self-adjoint property $T = T^*$:

$$
\langle Tv, v \rangle = \langle v, T^*v \rangle = \langle v, Tv \rangle = \langle v, \lambda v \rangle = \overline{\lambda} \langle v, v \rangle = \overline{\lambda} \|v\|^2
$$

Equating the two results, we get $\lambda \|v\|^2 = \overline{\lambda} \|v\|^2$. Since $v$ is an eigenvector, $\|v\|^2 \neq 0$, so we must have $\lambda = \overline{\lambda}$, which means $\lambda$ is a real number.

As an application, consider an observable in a [two-level quantum system](@entry_id:190799) represented by the matrix $M = \begin{pmatrix} 3  2 - i \\ 2 + i  1 \end{pmatrix}$. This matrix is self-adjoint since its diagonal entries are real and the off-diagonal entry $m_{12} = 2-i$ is the [complex conjugate](@entry_id:174888) of $m_{21} = 2+i$. Therefore, its eigenvalues must be real. By solving the [characteristic equation](@entry_id:149057) $\det(M - \lambda I) = \lambda^2 - 4\lambda - 2 = 0$, we find the possible measurement outcomes to be the real eigenvalues $\lambda = 2 \pm \sqrt{6}$ [@problem_id:1897549].

#### Unitary Operators

Another vital class of operators on a Hilbert space are **[unitary operators](@entry_id:151194)**. An operator $U$ is unitary if it preserves the inner product, meaning $\langle Ux, Uy \rangle = \langle x, y \rangle$ for all $x, y \in H$. This is equivalent to the condition $U^*U = UU^* = I$, where $I$ is the [identity operator](@entry_id:204623). Unitary operators represent symmetries or dynamics that preserve the geometry of the state space, such as rotations or time evolution in a closed quantum system.

The eigenvalues of a unitary operator have a defining characteristic: their modulus must be 1. Let $\lambda$ be an eigenvalue of a [unitary operator](@entry_id:155165) $U$ with eigenvector $v \neq 0$. The norm-preserving property of $U$ implies $\|Uv\| = \|v\|$. We can compute the squared norm of $Uv$ in two ways:

1.  Using the norm-preserving property directly: $\|Uv\|^2 = \|v\|^2$.
2.  Using the [eigenvalue equation](@entry_id:272921) $Uv = \lambda v$: $\|Uv\|^2 = \|\lambda v\|^2 = |\lambda|^2 \|v\|^2$.

Equating these gives $|\lambda|^2 \|v\|^2 = \|v\|^2$. Since $\|v\| \neq 0$, we conclude that $|\lambda|^2 = 1$, which means $|\lambda|=1$ [@problem_id:1897552]. All eigenvalues of a unitary operator must lie on the unit circle in the complex plane.

### The Intriguing Case of an Empty Point Spectrum

In finite-dimensional [complex vector spaces](@entry_id:264355), the Fundamental Theorem of Algebra guarantees that the characteristic polynomial always has at least one root. Consequently, every [linear operator](@entry_id:136520) on a finite-dimensional complex space has at least one eigenvalue. One of the most striking differences in infinite dimensions is that this is no longer true. There exist important operators that have no eigenvalues at all.

#### The Shift Operator

Consider the Hilbert space $l^2$ of square-summable complex sequences. The **right [shift operator](@entry_id:263113)** $T: l^2 \to l^2$ is defined as:

$$
T(x_1, x_2, x_3, \dots) = (0, x_1, x_2, x_3, \dots)
$$

This operator models a one-step time delay in a discrete system. Let's search for an eigenvalue $\lambda \in \mathbb{C}$ and a non-zero eigenvector $x = (x_1, x_2, \dots) \in l^2$ such that $Tx = \lambda x$ [@problem_id:1897556]. Writing this equation component by component, we have:

$$
(0, x_1, x_2, \dots) = (\lambda x_1, \lambda x_2, \lambda x_3, \dots)
$$

This gives a system of equations:
1.  $0 = \lambda x_1$
2.  $x_1 = \lambda x_2$
3.  $x_2 = \lambda x_3$
...and in general, $x_{n-1} = \lambda x_n$ for $n \ge 2$.

Let's analyze this. If $\lambda = 0$, the first equation $0 = 0 \cdot x_1$ is uninformative. But the subsequent equations become $x_1 = 0$, $x_2=0$, and so on. This forces the entire sequence $x$ to be the zero vector, which cannot be an eigenvector. Thus, $0$ is not an eigenvalue.

If $\lambda \neq 0$, the first equation $0 = \lambda x_1$ immediately implies $x_1 = 0$. Using the recursive relation $x_n = \lambda^{-1} x_{n-1}$, we find:
$x_2 = \lambda^{-1} x_1 = 0$
$x_3 = \lambda^{-1} x_2 = 0$
...and so on. Again, we are forced to conclude that $x=0$.

In all cases, the only solution to the eigenvalue equation is the [zero vector](@entry_id:156189). Therefore, the right [shift operator](@entry_id:263113) has no eigenvectors, and its [point spectrum](@entry_id:274057) is the empty set: $\sigma_p(T) = \emptyset$.

#### The Multiplication Operator

Another canonical example is the **multiplication operator** on a [function space](@entry_id:136890) like $L^2[a,b]$. Consider the operator $M$ on $L^2[0, 2]$ defined by $(Mf)(x) = xf(x)$ [@problem_id:1897509]. An eigenvalue $\lambda$ would require a non-zero function $f \in L^2[0,2]$ such that $Mf = \lambda f$. This means:

$$
xf(x) = \lambda f(x) \quad \text{for almost every } x \in [0, 2]
$$

This can be rewritten as $(x - \lambda)f(x) = 0$ almost everywhere. For any $x$ where $x \neq \lambda$, this equation forces $f(x)=0$. The only point where $f(x)$ could potentially be non-zero is $x=\lambda$. However, a function that is non-zero only on a single point (or any [set of measure zero](@entry_id:198215)) is equivalent to the zero function in an $L^p$ space. The norm of such a function is zero:

$$
\|f\|^2 = \int_0^2 |f(x)|^2 dx = 0
$$

Thus, any function satisfying the [eigenvalue equation](@entry_id:272921) must be the [zero vector](@entry_id:156189) in $L^2[0,2]$. Consequently, the multiplication operator $M$ has no eigenvalues, and its [point spectrum](@entry_id:274057) is also empty.

These examples demonstrate that the concept of the [point spectrum](@entry_id:274057), while powerful, does not tell the whole story for operators on [infinite-dimensional spaces](@entry_id:141268). The fact that an operator can have an empty [point spectrum](@entry_id:274057) yet still have a rich and non-trivial structure motivates the introduction of the continuous and residual spectra, which together with the [point spectrum](@entry_id:274057), form the complete [spectrum of an operator](@entry_id:272027).