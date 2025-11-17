## Introduction
In the study of quantitative sciences, transformations are everything. They describe how systems evolve, how data is processed, and how one state changes into another. At the heart of these transformations are [linear operators](@entry_id:149003)—the fundamental, structure-preserving maps between [vector spaces](@entry_id:136837). While the abstract theory of operators is powerful, their true utility is unlocked when they are represented as matrices. This article bridges the gap between the abstract concept of a [linear operator](@entry_id:136520) and its concrete manifestation as a matrix, revealing a rich world of structure, properties, and applications. It addresses the need for a unified perspective that not only explains the 'what' and 'how' of matrix operators but also the 'why'—their profound significance across a multitude of disciplines.

This article is structured to guide you from core theory to practical application. The first chapter, **"Principles and Mechanisms,"** lays the groundwork by exploring how operators become matrices, analyzing their [fundamental subspaces](@entry_id:190076), quantifying their "size" with norms, and delving into the critical concepts of [spectral theory](@entry_id:275351) and operator decompositions. Building on this foundation, the second chapter, **"Applications and Interdisciplinary Connections,"** demonstrates how these mathematical tools are used to solve real-world problems in quantum mechanics, computer science, engineering, and [mathematical biology](@entry_id:268650). Finally, **"Hands-On Practices"** will offer you the opportunity to solidify your understanding by tackling targeted problems. By the end, you will have a robust understanding of matrix operators as both elegant mathematical objects and indispensable tools for modern science and technology.

## Principles and Mechanisms

Having established the foundational concept of vector spaces, we now turn our attention to the mappings between them. This chapter delves into the principles and mechanisms of linear operators, which are the structure-preserving functions that form the bedrock of linear algebra and [functional analysis](@entry_id:146220). We will explore how these abstract transformations can be represented concretely as matrices, analyze their fundamental properties, and uncover the deep structural theorems that allow us to decompose them into simpler, more understandable components.

### From Abstract Operators to Concrete Matrices

A **linear operator** is a function $T: V \to W$ between two vector spaces $V$ and $W$ (over the same field) that preserves the operations of [vector addition and scalar multiplication](@entry_id:151375). While this abstract definition is powerful, for computational and theoretical purposes, we often need a more concrete representation. This is achieved by using matrices.

The key idea is that once we choose an ordered basis for the domain $V$ and the [codomain](@entry_id:139336) $W$, any [linear operator](@entry_id:136520) $T$ can be uniquely represented by a matrix. Let $\mathcal{B} = \{v_1, v_2, \dots, v_n\}$ be a basis for $V$ and $\mathcal{C} = \{w_1, w_2, \dots, w_m\}$ be a basis for $W$. To find the [matrix representation](@entry_id:143451) of $T$ with respect to these bases, we apply $T$ to each basis vector $v_j$ in $\mathcal{B}$. The resulting vector $T(v_j)$ is an element of $W$ and can therefore be written as a unique [linear combination](@entry_id:155091) of the basis vectors in $\mathcal{C}$:

$T(v_j) = a_{1j}w_1 + a_{2j}w_2 + \dots + a_{mj}w_m$

The coefficients of this [linear combination](@entry_id:155091), $(a_{1j}, a_{2j}, \dots, a_{mj})^T$, form the $j$-th column of the [matrix representation](@entry_id:143451) of $T$, denoted $[T]_{\mathcal{C},\mathcal{B}}$. The resulting $m \times n$ matrix allows us to transform the [coordinate vector](@entry_id:153319) of any $v \in V$ to the [coordinate vector](@entry_id:153319) of $T(v) \in W$ through standard [matrix-vector multiplication](@entry_id:140544).

To illustrate this process, consider a less-obvious vector space: the space of $2 \times 2$ real matrices, $V = M_2(\mathbb{R})$. This is a 4-dimensional vector space. Let's define a linear operator $T: V \to V$ by $T(A) = A^T$, the transpose of the matrix $A$. To find the [matrix representation](@entry_id:143451) of this operator, we must first choose a basis for $V$. The standard basis consists of four matrices:

$v_1 = \begin{pmatrix} 1  0 \\ 0  0 \end{pmatrix}, v_2 = \begin{pmatrix} 0  1 \\ 0  0 \end{pmatrix}, v_3 = \begin{pmatrix} 0  0 \\ 1  0 \end{pmatrix}, v_4 = \begin{pmatrix} 0  0 \\ 0  1 \end{pmatrix}$

We now apply the operator $T$ to each [basis vector](@entry_id:199546) and express the result in terms of the same basis [@problem_id:1869191]:

- $T(v_1) = \begin{pmatrix} 1  0 \\ 0  0 \end{pmatrix}^T = \begin{pmatrix} 1  0 \\ 0  0 \end{pmatrix} = 1v_1 + 0v_2 + 0v_3 + 0v_4$. The [coordinate vector](@entry_id:153319) is $(1, 0, 0, 0)^T$.
- $T(v_2) = \begin{pmatrix} 0  1 \\ 0  0 \end{pmatrix}^T = \begin{pmatrix} 0  0 \\ 1  0 \end{pmatrix} = 0v_1 + 0v_2 + 1v_3 + 0v_4$. The [coordinate vector](@entry_id:153319) is $(0, 0, 1, 0)^T$.
- $T(v_3) = \begin{pmatrix} 0  0 \\ 1  0 \end{pmatrix}^T = \begin{pmatrix} 0  1 \\ 0  0 \end{pmatrix} = 0v_1 + 1v_2 + 0v_3 + 0v_4$. The [coordinate vector](@entry_id:153319) is $(0, 1, 0, 0)^T$.
- $T(v_4) = \begin{pmatrix} 0  0 \\ 0  1 \end{pmatrix}^T = \begin{pmatrix} 0  0 \\ 0  1 \end{pmatrix} = 0v_1 + 0v_2 + 0v_3 + 1v_4$. The [coordinate vector](@entry_id:153319) is $(0, 0, 0, 1)^T$.

Arranging these coordinate vectors as columns, we obtain the $4 \times 4$ matrix representation of the transpose operator:

$[T]_{\mathcal{B}} = \begin{pmatrix} 1  0  0  0 \\ 0  0  1  0 \\ 0  1  0  0 \\ 0  0  0  1 \end{pmatrix}$

This matrix now acts on the coordinate vectors of matrices in $M_2(\mathbb{R})$ exactly as the transpose operation acts on the matrices themselves. This example highlights the power of [matrix representations](@entry_id:146025): even an operation on a space of matrices can be encoded as a simple matrix multiplication in a coordinate system.

### Fundamental Subspaces: The Kernel and Range

Every [linear operator](@entry_id:136520) $T: V \to W$ is intrinsically associated with two [fundamental subspaces](@entry_id:190076). The first is the **kernel** (or **null space**) of $T$, denoted $\ker(T)$, which is a subspace of the domain $V$:

$\ker(T) = \{ v \in V \mid T(v) = \mathbf{0}_W \}$

The kernel consists of all vectors in the domain that are mapped to the zero vector in the codomain. It measures the extent to which the operator "collapses" the space; a non-trivial kernel means that distinct vectors are mapped to the same output vector.

The second fundamental subspace is the **range** (or **image**) of $T$, denoted $\text{ran}(T)$, which is a subspace of the [codomain](@entry_id:139336) $W$:

$\text{ran}(T) = \{ w \in W \mid w = T(v) \text{ for some } v \in V \}$

The range consists of all possible outputs of the operator. It describes the "reach" of the transformation.

These two subspaces are linked by the celebrated **[rank-nullity theorem](@entry_id:154441)**, which states that for a [linear operator](@entry_id:136520) on a [finite-dimensional vector space](@entry_id:187130) $V$:

$\dim(V) = \dim(\ker(T)) + \dim(\text{ran}(T))$

The dimension of the kernel is called the **[nullity](@entry_id:156285)**, and the dimension of the range is called the **rank**.

Let's explore these concepts within the [vector space of polynomials](@entry_id:196204). Consider the operator $T: P_3(\mathbb{R}) \to P_2(\mathbb{R})$ acting on polynomials of degree at most 3, defined by $T(p(x)) = p'(x) - x p''(x)$ [@problem_id:1869170]. Let's find the [kernel and range](@entry_id:155506) of this operator. An arbitrary polynomial in $P_3(\mathbb{R})$ has the form $p(x) = ax^3 + bx^2 + cx + d$. Its derivatives are $p'(x) = 3ax^2 + 2bx + c$ and $p''(x) = 6ax + 2b$.

The action of the operator is:
$T(p(x)) = (3ax^2 + 2bx + c) - x(6ax + 2b) = 3ax^2 + 2bx + c - 6ax^2 - 2bx = -3ax^2 + c$

To find the kernel, we set $T(p(x)) = 0$. The polynomial $-3ax^2 + c$ is the zero polynomial if and only if all its coefficients are zero. This requires $a=0$ and $c=0$. The coefficients $b$ and $d$ can be any real numbers. Thus, any polynomial in the kernel must be of the form $p(x) = bx^2 + d$. The kernel is the set of all such polynomials, which is spanned by the basis $\{1, x^2\}$. So, $\ker(T) = \text{span}\{1, x^2\}$.

To find the range, we examine the form of the output, $-3ax^2 + c$. As the coefficients $a$ and $c$ can be chosen freely from $\mathbb{R}$, the output can be any [linear combination](@entry_id:155091) of the polynomials $1$ and $x^2$. Therefore, the range is also spanned by the basis $\{1, x^2\}$, and $\text{ran}(T) = \text{span}\{1, x^2\}$.

In this case, $\dim(\ker(T)) = 2$ and $\dim(\text{ran}(T)) = 2$. The domain is $P_3(\mathbb{R})$, which has dimension 4 (basis $\{1, x, x^2, x^3\}$). The [rank-nullity theorem](@entry_id:154441) is satisfied: $4 = 2 + 2$.

### The Size of an Operator: The Operator Norm

When dealing with [normed vector spaces](@entry_id:274725), we can quantify the "size" or "strength" of a linear operator. The **[induced operator norm](@entry_id:750614)** measures the maximum factor by which an operator can stretch a vector. For a linear operator $T: V \to W$ between two [normed spaces](@entry_id:137032), its norm is defined as:

$\|T\| = \sup \{ \|T(v)\|_W \mid v \in V, \|v\|_V = 1 \}$

This is equivalent to finding the smallest constant $C \ge 0$ such that $\|T(v)\|_W \le C\|v\|_V$ for all $v \in V$. The [operator norm](@entry_id:146227) depends on the choice of norms for the domain and [codomain](@entry_id:139336).

A particularly common and useful norm is the **maximum norm** (or $\ell_{\infty}$-norm) on $\mathbb{R}^n$, defined as $\|v\|_{\infty} = \max_i |v_i|$. Let's determine the [operator norm of a matrix](@entry_id:272193) operator $M: \mathbb{R}^n \to \mathbb{R}^m$ induced by the $\ell_{\infty}$-norm on both spaces.

Let $v \in \mathbb{R}^n$ with $\|v\|_{\infty} = 1$, which means $|v_j| \le 1$ for all $j$. The $i$-th component of the output vector $Mv$ is $(Mv)_i = \sum_{j=1}^n M_{ij}v_j$. Using the triangle inequality, we can bound its magnitude:

$|(Mv)_i| = \left| \sum_{j=1}^n M_{ij}v_j \right| \le \sum_{j=1}^n |M_{ij}||v_j| \le \sum_{j=1}^n |M_{ij}|$

Since this holds for every row $i$, it must also hold for the row where the output magnitude is maximal:

$\|Mv\|_{\infty} = \max_i |(Mv)_i| \le \max_i \sum_{j=1}^n |M_{ij}|$

This inequality shows that the [operator norm](@entry_id:146227) is bounded by the maximum absolute row sum of the matrix. In fact, this bound is always attained. To see this, let $k$ be the row index for which the absolute row sum is maximal. We can construct a vector $v$ with entries $v_j = \text{sgn}(M_{kj})$, where $\text{sgn}$ is the sign function. This vector has $\|v\|_\infty = 1$ (unless the $k$-th row is all zeros, in which case the norm is trivial). For this specific vector, the $k$-th component of the output is:

$(Mv)_k = \sum_{j=1}^n M_{kj}v_j = \sum_{j=1}^n M_{kj} \text{sgn}(M_{kj}) = \sum_{j=1}^n |M_{kj}|$

Therefore, $\|Mv\|_{\infty} \ge |(Mv)_k| = \sum_{j=1}^n |M_{kj}| = \max_i \sum_{j=1}^n |M_{ij}|$. Combining the two inequalities, we arrive at a simple formula for the $\ell_\infty$-[induced norm](@entry_id:148919):

$\|T\|_{\infty} = \max_i \sum_{j=1}^n |M_{ij}|$

For example, consider the operator on $\mathbb{R}^2$ represented by the matrix $M = \begin{pmatrix} 1  -2 \\ 3  -1 \end{pmatrix}$ [@problem_id:1869169]. The absolute row sums are:
- Row 1: $|1| + |-2| = 3$
- Row 2: $|3| + |-1| = 4$

The maximum of these sums is 4. Therefore, the [operator norm](@entry_id:146227) is $\|T\|_{\infty} = 4$. This means that no unit vector (in the max norm sense) can be stretched by a factor greater than 4, and there exists at least one vector for which this maximum stretch is achieved.

### Spectral Theory: Eigenvalues, Eigenvectors, and the Spectrum

Perhaps the most important aspect of an operator is its **spectrum**, which generalizes the concept of eigenvalues. For a [linear operator](@entry_id:136520) $T$ on a vector space $V$, a non-zero vector $v \in V$ is an **eigenvector** of $T$ if applying $T$ to $v$ simply scales $v$ by some scalar $\lambda$. This scalar $\lambda$ is called the corresponding **eigenvalue**.

$T(v) = \lambda v, \quad v \neq \mathbf{0}$

Eigenvectors represent the directions in the space that are invariant under the transformation $T$. For [finite-dimensional spaces](@entry_id:151571), the **spectrum** of $T$, denoted $\sigma(T)$, is simply the set of all its eigenvalues.

A profoundly useful result connecting an operator to functions of that operator is the **Spectral Mapping Theorem**. For a square matrix $A$ and any polynomial $p(t)$, the theorem states that the spectrum of the operator $p(A)$ is given by the set of values $p(\lambda)$ for every eigenvalue $\lambda$ of $A$.

$\sigma(p(A)) = \{ p(\lambda) \mid \lambda \in \sigma(A) \}$

To see why this is true, let $v$ be an eigenvector of $A$ with eigenvalue $\lambda$. Then $Av = \lambda v$. Applying $A$ again gives $A^2v = A(\lambda v) = \lambda(Av) = \lambda^2v$. By induction, $A^k v = \lambda^k v$ for any positive integer $k$. For a polynomial $p(t) = c_k t^k + \dots + c_1 t + c_0$, the operator $p(A)$ is $c_k A^k + \dots + c_1 A + c_0 I$. Applying this to $v$:

$p(A)v = (c_k A^k + \dots + c_1 A + c_0 I)v = c_k(\lambda^k v) + \dots + c_1(\lambda v) + c_0 v = (c_k \lambda^k + \dots + c_1 \lambda + c_0)v = p(\lambda)v$

This shows that if $\lambda$ is an eigenvalue of $A$, then $p(\lambda)$ is an eigenvalue of $p(A)$ [@problem_id:1869198].

Let's consider an operator $T$ constructed as a polynomial of a simpler operator $R$. Let $R$ be the reflection across the line $y=x$ in $\mathbb{R}^2$. The matrix for $R$ is $\begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix}$. Its characteristic equation is $\lambda^2 - 1 = 0$, giving eigenvalues $\lambda = 1$ (for eigenvectors along $y=x$, like $(1,1)^T$) and $\lambda = -1$ (for eigenvectors along $y=-x$, like $(1,-1)^T$). Now, define a new operator $T = aI + bR$ for constants $a, b$. This is a polynomial $p(t) = a+bt$ applied to $R$. According to the [spectral mapping theorem](@entry_id:264489), the eigenvalues of $T$ will be $p(1) = a+b$ and $p(-1) = a-b$. For instance, if $a=1/3$ and $b=5/2$, the eigenvalues of $T$ are $1/3 + 5/2 = 17/6$ and $1/3 - 5/2 = -13/6$ [@problem_id:1869201].

### Operators on Inner Product Spaces: Adjoints and Their Kin

When a vector space is endowed with an **inner product** $\langle \cdot, \cdot \rangle$, we can define new classes of operators based on their interaction with this structure. The most fundamental of these is the **adjoint operator**. For any [linear operator](@entry_id:136520) $T$ on a finite-dimensional [inner product space](@entry_id:138414) $V$, there exists a unique operator $T^*$, called the adjoint of $T$, that satisfies:

$\langle T(u), v \rangle = \langle u, T^*(v) \rangle \quad \text{for all } u, v \in V$

If we work in an **orthonormal basis**, the matrix representation of the adjoint, $[T^*]$, is simply the **[conjugate transpose](@entry_id:147909)** (or Hermitian conjugate) of the matrix of $T$, denoted $[T]^\dagger$ or $[T]^*$. The [conjugate transpose](@entry_id:147909) is found by taking the transpose of the matrix and then taking the complex conjugate of every entry.

For example, consider the operator on $\mathbb{C}^2$ (with the standard inner product) represented by the matrix $A = \begin{pmatrix} 1+2i  4-3i \\ 6  5i \end{pmatrix}$ [@problem_id:1869196]. Its adjoint $A^*$ is found by:
1. Transposing $A$: $A^T = \begin{pmatrix} 1+2i  6 \\ 4-3i  5i \end{pmatrix}$.
2. Taking the [complex conjugate](@entry_id:174888) of each entry: $A^* = \overline{A^T} = \begin{pmatrix} 1-2i  6 \\ 4+3i  -5i \end{pmatrix}$.

The relationship between an operator and its adjoint allows us to define several crucial classes of operators:

- **Self-Adjoint (or Hermitian) Operators**: These are operators for which $T = T^*$. In matrix form, $A = A^\dagger$. This implies that the diagonal entries must be real ($a_{ii} = \overline{a_{ii}}$) and the off-diagonal entries must exhibit [conjugate symmetry](@entry_id:144131) ($a_{ij} = \overline{a_{ji}}$). For example, the matrices $\begin{pmatrix} 2  3i \\ -3i  1 \end{pmatrix}$ and $\begin{pmatrix} 4  2-i \\ 2+i  0 \end{pmatrix}$ are self-adjoint, whereas $\begin{pmatrix} 1  1+i \\ 1+i  2 \end{pmatrix}$ is not [@problem_id:1869174]. Self-adjoint operators are of paramount importance in quantum mechanics, where they represent physical observables, as their eigenvalues (the possible measurement outcomes) are always real.

- **Skew-Adjoint (or Skew-Hermitian) Operators**: These satisfy $T = -T^*$. Their eigenvalues are always purely imaginary or zero. A special case is a real matrix that is **skew-symmetric** ($A^T = -A$). Such operators are intimately connected to rotations. Consider the dynamical system $\frac{d\vec{x}}{dt} = A\vec{x}$ where $A$ is a real $3 \times 3$ [skew-symmetric matrix](@entry_id:155998). This equation describes a steady rotation of the vector $\vec{x}(t)$ around a fixed axis with a constant [angular velocity](@entry_id:192539). The length of the vector, $\|\vec{x}(t)\|$, is conserved over time, which is a hallmark of rotational motion. This is because $\frac{d}{dt}\|\vec{x}\|^2 = \frac{d}{dt}\langle \vec{x}, \vec{x} \rangle = \langle \dot{\vec{x}}, \vec{x} \rangle + \langle \vec{x}, \dot{\vec{x}} \rangle = \langle A\vec{x}, \vec{x} \rangle + \langle \vec{x}, A\vec{x} \rangle$. For real spaces, this is $\vec{x}^T A^T \vec{x} + \vec{x}^T A \vec{x} = \vec{x}^T (-A) \vec{x} + \vec{x}^T A \vec{x} = 0$, confirming that the norm is constant [@problem_id:1869161].

- **Unitary (or Orthogonal) Operators**: These operators preserve the inner product, $\langle T(u), T(v) \rangle = \langle u, v \rangle$. This is equivalent to the condition $T^*T = TT^* = I$, or $T^* = T^{-1}$. They represent [rigid motions](@entry_id:170523) like rotations and reflections.

### The Structure of Operators: Decompositions

A powerful technique in linear algebra is to decompose a complex operator into a product or sum of simpler, more structured operators. These decompositions reveal the operator's underlying geometric action and algebraic properties.

#### The Jordan-Chevalley Decomposition

Not all matrices can be diagonalized. The **Jordan-Chevalley decomposition** provides a [canonical form](@entry_id:140237) for *any* square matrix over an [algebraically closed field](@entry_id:151401) (like $\mathbb{C}$). It states that any matrix $A$ can be uniquely written as a sum:

$A = D + N$

where:
1.  $D$ is a **diagonalizable** (or semisimple) matrix.
2.  $N$ is a **nilpotent** matrix (i.e., $N^k=0$ for some integer $k$).
3.  $D$ and $N$ commute: $DN = ND$.

The matrix $D$ captures the "diagonalizable part" of $A$, containing its eigenvalues, while $N$ captures the "non-diagonalizable part."

Consider the matrix $A = \begin{pmatrix} 4  1 \\ -1  2 \end{pmatrix}$. Its [characteristic polynomial](@entry_id:150909) is $(\lambda-3)^2=0$, so it has a single repeated eigenvalue $\lambda=3$. Since $A - 3I = \begin{pmatrix} 1  1 \\ -1  -1 \end{pmatrix}$ is not the [zero matrix](@entry_id:155836), $A$ is not diagonalizable. The diagonalizable part, $D$, must have the same eigenvalues as $A$. A [diagonalizable matrix](@entry_id:150100) with only the eigenvalue 3 must be $D=3I$. This gives us the decomposition [@problem_id:1869158]:

$D = \begin{pmatrix} 3  0 \\ 0  3 \end{pmatrix}$
$N = A - D = \begin{pmatrix} 4  1 \\ -1  2 \end{pmatrix} - \begin{pmatrix} 3  0 \\ 0  3 \end{pmatrix} = \begin{pmatrix} 1  1 \\ -1  -1 \end{pmatrix}$

We can check that $N$ is nilpotent: $N^2 = \begin{pmatrix} 1  1 \\ -1  -1 \end{pmatrix}\begin{pmatrix} 1  1 \\ -1  -1 \end{pmatrix} = \begin{pmatrix} 0  0 \\ 0  0 \end{pmatrix}$. And since $D$ is a scalar multiple of the identity, it commutes with any matrix, so $DN=ND$ is satisfied. This decomposition uniquely separates the scaling action ($D=3I$) from the shearing action ($N$).

#### The Polar Decomposition

Another fundamental result is the **polar decomposition**, which is a matrix analog of the [polar form](@entry_id:168412) of a complex number $z = re^{i\theta}$. It states that any invertible square matrix $A$ can be uniquely factored as:

$A = UP$

where:
1.  $U$ is a **unitary** matrix.
2.  $P$ is a **positive-semidefinite Hermitian** matrix.

Geometrically, this decomposition separates the action of $A$ into a pure stretching/scaling along orthogonal axes (represented by $P$) followed by a rigid rotation/reflection (represented by $U$). This has profound applications in fields like continuum mechanics (decomposing a deformation into stretch and rotation) and quantum information, where it separates an ideal quantum gate ($U$) from noise and decoherence effects ($P$) [@problem_id:1869187].

The construction is as follows: The matrix $P$ is uniquely defined as the positive-semidefinite square root of the matrix $A^\dagger A$, i.e., $P = \sqrt{A^\dagger A}$. Since $A$ is invertible, $A^\dagger A$ is positive-definite, and $P$ is also invertible. The unitary part $U$ is then found via $U = AP^{-1}$.

Let's decompose the matrix $A = \begin{pmatrix} 1  1 \\ i  0 \end{pmatrix}$.
First, we compute $A^\dagger A$:
$A^\dagger = \begin{pmatrix} 1  -i \\ 1  0 \end{pmatrix}$, so $A^\dagger A = \begin{pmatrix} 1  -i \\ 1  0 \end{pmatrix} \begin{pmatrix} 1  1 \\ i  0 \end{pmatrix} = \begin{pmatrix} 2  1 \\ 1  1 \end{pmatrix}$.
So, $P^2 = \begin{pmatrix} 2  1 \\ 1  1 \end{pmatrix}$. To find $U=AP^{-1}$, we need $P^{-1}$. It is easier to find $(P^2)^{-1}$ first:
$(P^2)^{-1} = (A^\dagger A)^{-1} = \begin{pmatrix} 1  -1 \\ -1  2 \end{pmatrix}$.
$P^{-1}$ is the unique positive-semidefinite square root of this matrix. Through diagonalization or solving a system of equations, one can find that $P^{-1} = \frac{1}{\sqrt{5}}\begin{pmatrix} 2  -1 \\ -1  3 \end{pmatrix}$.
Finally, we compute $U$:
$U = AP^{-1} = \begin{pmatrix} 1  1 \\ i  0 \end{pmatrix} \frac{1}{\sqrt{5}}\begin{pmatrix} 2  -1 \\ -1  3 \end{pmatrix} = \frac{1}{\sqrt{5}} \begin{pmatrix} 1  2 \\ 2i  -i \end{pmatrix}$.
One can verify that this $U$ is indeed unitary ($U^\dagger U = I$). This decomposition cleanly separates the non-unitary effects of the operator, captured in $P$, from its purely unitary part $U$.