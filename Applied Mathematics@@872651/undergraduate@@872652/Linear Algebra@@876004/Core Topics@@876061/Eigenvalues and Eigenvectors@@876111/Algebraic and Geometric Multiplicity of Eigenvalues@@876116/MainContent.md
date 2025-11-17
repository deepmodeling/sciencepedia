## Introduction
Eigenvalues and eigenvectors are foundational concepts in linear algebra, offering deep insights into the properties of [linear transformations](@entry_id:149133). However, a complete understanding requires moving beyond simply finding eigenvalues to analyzing their *[multiplicity](@entry_id:136466)*. This is where a crucial distinction arises: the difference between an eigenvalue's **[algebraic multiplicity](@entry_id:154240)** and its **geometric multiplicity**. This article addresses the pivotal role this relationship plays in determining the structure of a matrix. In the following chapters, you will gain a comprehensive understanding of this topic. **Principles and Mechanisms** will formally define both multiplicities, establish their fundamental inequality, and link them directly to the critical concept of [diagonalizability](@entry_id:748379) and the structure of the Jordan Normal Form. **Applications and Interdisciplinary Connections** will showcase why this theoretical distinction matters, exploring its consequences in dynamical systems, [numerical analysis](@entry_id:142637), and [spectral graph theory](@entry_id:150398). Finally, **Hands-On Practices** will allow you to apply these principles to concrete problems, solidifying your grasp of this essential linear algebra concept.

## Principles and Mechanisms

The study of [eigenvalues and eigenvectors](@entry_id:138808) provides a profound lens through which to understand the behavior of linear transformations. However, simply identifying the eigenvalues is only the first step. To fully characterize a [linear operator](@entry_id:136520) and predict its long-term behavior, we must understand the *[multiplicity](@entry_id:136466)* of its eigenvalues. This concept is not monolithic; it bifurcates into two distinct yet related ideas: [algebraic multiplicity](@entry_id:154240) and geometric multiplicity. The relationship between these two quantities is one of the most critical concepts in linear algebra, governing whether a matrix can be simplified into a [diagonal form](@entry_id:264850) and, if not, determining its canonical structure.

### Defining Multiplicity: Algebraic vs. Geometric

For a given $n \times n$ matrix $A$, the eigenvalues are the roots of its **characteristic polynomial**, defined as $P_A(\lambda) = \det(A - \lambda I)$. This is a polynomial of degree $n$ in the variable $\lambda$.

The **algebraic multiplicity (AM)** of an eigenvalue $\lambda_i$ is its multiplicity as a root of the characteristic polynomial. It signifies how many times the factor $(\lambda - \lambda_i)$ appears in the factorization of $P_A(\lambda)$. For example, if a $4 \times 4$ matrix $A$ has a characteristic polynomial $P_A(\lambda) = (\lambda - c)^4$, then the eigenvalue $\lambda = c$ is the only eigenvalue, and its [algebraic multiplicity](@entry_id:154240) is 4 [@problem_id:502].

While the [algebraic multiplicity](@entry_id:154240) arises from the polynomial structure of the characteristic equation, the geometric multiplicity is rooted in the spatial structure of the operator itself. For each eigenvalue $\lambda_i$, there exists a corresponding subspace of vectors that are simply scaled by $\lambda_i$ under the transformation $A$. This subspace is called the **eigenspace** of $\lambda_i$, denoted $E_{\lambda_i}$. It is formally defined as the [null space](@entry_id:151476) of the matrix $(A - \lambda_i I)$:

$$
E_{\lambda_i} = \ker(A - \lambda_i I) = \{ \mathbf{v} \in V \mid (A - \lambda_i I)\mathbf{v} = \mathbf{0} \}
$$

The **[geometric multiplicity](@entry_id:155584) (GM)** of an eigenvalue $\lambda_i$ is the dimension of its corresponding [eigenspace](@entry_id:150590), $\text{GM}(\lambda_i) = \dim(E_{\lambda_i})$. This number tells us how many [linearly independent](@entry_id:148207) eigenvectors exist for that eigenvalue.

Returning to our previous example where $P_A(\lambda) = (\lambda - c)^4$, the [algebraic multiplicity](@entry_id:154240) of $\lambda=c$ is 4. However, its [geometric multiplicity](@entry_id:155584) is not determined by the [characteristic polynomial](@entry_id:150909) alone. It depends on the structure of the matrix $A$ itself. If we are given that $\dim(\ker(A - cI)) = 2$, this directly states that the [geometric multiplicity](@entry_id:155584) of the eigenvalue $c$ is 2 [@problem_id:502].

A fundamental theorem in linear algebra establishes a crucial inequality between these two multiplicities: for any eigenvalue $\lambda$ of a matrix $A$, its geometric multiplicity is always less than or equal to its algebraic multiplicity.

$$
1 \le \text{GM}(\lambda) \le \text{AM}(\lambda)
$$

The fact that $\text{GM}(\lambda) \ge 1$ is by definition—an eigenvalue must have at least one corresponding non-zero eigenvector. The upper bound, $\text{GM}(\lambda) \le \text{AM}(\lambda)$, is less trivial but can be understood intuitively. The [algebraic multiplicity](@entry_id:154240) corresponds to the dimension of a larger space, the *generalized [eigenspace](@entry_id:150590)*, of which the standard [eigenspace](@entry_id:150590) is a subspace. Therefore, the dimension of the eigenspace cannot exceed the dimension of the generalized eigenspace. The distinction between these two multiplicities is the key to understanding the [diagonalizability](@entry_id:748379) of a matrix.

### The Role of Multiplicity in Diagonalizability

A square matrix $A$ is said to be **diagonalizable** if it is similar to a diagonal matrix $D$. That is, there exists an [invertible matrix](@entry_id:142051) $P$ such that $A = PDP^{-1}$. This is a highly desirable property, as [diagonal matrices](@entry_id:149228) are exceptionally easy to work with in computations. The condition for [diagonalizability](@entry_id:748379) is directly and completely determined by the multiplicities of the matrix's eigenvalues.

A matrix $A$ is diagonalizable if and only if for every eigenvalue $\lambda$ of $A$, its geometric multiplicity is equal to its algebraic multiplicity.

$$
A \text{ is diagonalizable} \iff \text{GM}(\lambda) = \text{AM}(\lambda) \text{ for all eigenvalues } \lambda
$$

This is equivalent to stating that the matrix possesses a full set of $n$ [linearly independent](@entry_id:148207) eigenvectors that can form a basis for the vector space. When $\text{GM}(\lambda)  \text{AM}(\lambda)$ for any eigenvalue, there is a "deficiency" of eigenvectors, and the matrix cannot be diagonalized.

Consider a $3 \times 3$ matrix $A$ with [characteristic polynomial](@entry_id:150909) $\lambda^3$. The only eigenvalue is $\lambda=0$, with an algebraic multiplicity of 3. For this matrix to be diagonalizable, the [geometric multiplicity](@entry_id:155584) of $\lambda=0$ must also be 3. The [geometric multiplicity](@entry_id:155584) is $\dim(\ker(A - 0I)) = \dim(\ker(A))$. By the [rank-nullity theorem](@entry_id:154441), $\dim(\ker(A)) = 3 - \text{rank}(A)$. So, for $\text{GM}(0)$ to be 3, the rank of $A$ must be 0, which means $A$ must be the [zero matrix](@entry_id:155836). If, for instance, we are told that $\text{rank}(A)=1$, then $\text{GM}(0) = 3-1=2$. Since $\text{GM}(0)=2  \text{AM}(0)=3$, the matrix is not diagonalizable [@problem_id:961146].

This criterion can be used to determine how a matrix's properties depend on its entries. Let's analyze the matrix family:
$$
A = \begin{pmatrix} -1  \alpha  2 \\ 0  -1  -4 \\ 0  0  7 \end{pmatrix}
$$
Since this matrix is upper triangular, its eigenvalues are its diagonal entries: $\lambda_1 = -1$ and $\lambda_2 = 7$. The corresponding algebraic multiplicities are $\text{AM}(-1) = 2$ and $\text{AM}(7) = 1$. Since $\text{AM}(7) = 1$, we are guaranteed that $\text{GM}(7)=1$. The [diagonalizability](@entry_id:748379) of $A$ thus hinges entirely on the eigenvalue $\lambda=-1$. The matrix is diagonalizable if and only if $\text{GM}(-1) = \text{AM}(-1) = 2$. To find $\text{GM}(-1)$, we compute the dimension of the [null space](@entry_id:151476) of $A - (-1)I$:
$$
A + I = \begin{pmatrix} 0  \alpha  2 \\ 0  0  -4 \\ 0  0  8 \end{pmatrix}
$$
The system of equations $(A+I)\mathbf{x} = \mathbf{0}$ forces $x_3=0$. Substituting this into the first equation gives $\alpha x_2 = 0$.
- If $\alpha \neq 0$, then we must have $x_2=0$. Only $x_1$ is free, so the null space is spanned by $\begin{pmatrix} 1  0  0 \end{pmatrix}^T$. The dimension is 1. Thus, $\text{GM}(-1)=1  \text{AM}(-1)=2$, and the matrix is not diagonalizable.
- If $\alpha = 0$, the equation becomes $0=0$. Both $x_1$ and $x_2$ are [free variables](@entry_id:151663). The [null space](@entry_id:151476) is spanned by $\begin{pmatrix} 1  0  0 \end{pmatrix}^T$ and $\begin{pmatrix} 0  1  0 \end{pmatrix}^T$. The dimension is 2. Here, $\text{GM}(-1) = \text{AM}(-1) = 2$, and the matrix is diagonalizable [@problem_id:1355359].

This example highlights that [diagonalizability](@entry_id:748379) can be a sensitive property. In fact, a sequence of diagonalizable matrices can converge to a non-diagonalizable one. Consider the matrix family $M(\delta) = \begin{pmatrix} 2  1 \\ \delta  2 \end{pmatrix}$. For any $\delta > 0$, the characteristic polynomial is $(2-\lambda)^2 - \delta = 0$, which gives two distinct eigenvalues $\lambda = 2 \pm \sqrt{\delta}$. Since the eigenvalues are distinct, their algebraic and geometric multiplicities are both 1, and the matrix $M(\delta)$ is diagonalizable. However, in the limit as $\delta \to 0^+$, the matrix becomes $M_0 = \begin{pmatrix} 2  1 \\ 0  2 \end{pmatrix}$. The eigenvalues coalesce: $\lambda=2$ now has $\text{AM}=2$. But the geometric multiplicity, $\dim(\ker(M_0 - 2I))$, is only 1. The limit matrix is not diagonalizable, demonstrating that the property of [diagonalizability](@entry_id:748379) is not "closed" under limits [@problem_id:1347027].

### Deeper Connections and Invariants

The concepts of multiplicity connect to other [fundamental matrix](@entry_id:275638) properties, providing powerful analytical shortcuts.

#### The Special Case of Eigenvalue Zero

The eigenvalue $\lambda = 0$ holds a special status. Its [eigenspace](@entry_id:150590), $E_0 = \ker(A-0I)$, is simply the [null space](@entry_id:151476) of the matrix $A$. Consequently, the [geometric multiplicity](@entry_id:155584) of the eigenvalue 0 is the nullity of the matrix:
$$
\text{GM}(0) = \dim(\ker(A)) = \text{nullity}(A)
$$
The **Rank-Nullity Theorem** states that for an $n \times n$ matrix, $\text{rank}(A) + \text{nullity}(A) = n$. This provides a direct formula connecting the geometric multiplicity of the zero eigenvalue to the rank of the matrix:
$$
\text{GM}(0) = n - \text{rank}(A)
$$
This relationship is particularly useful. If a [linear operator](@entry_id:136520) on an $n$-dimensional space has an image of dimension $r$ (i.e., its matrix representation has rank $r$), then the [geometric multiplicity](@entry_id:155584) of its zero eigenvalue must be precisely $n-r$ [@problem_id:1347049].

#### Invariance Under Transposition

A matrix $A$ and its transpose $A^T$ share many properties. Critically, they have the same characteristic polynomial, since $\det(M) = \det(M^T)$, which means $\det(A-\lambda I) = \det((A-\lambda I)^T) = \det(A^T - \lambda I)$. Therefore, $A$ and $A^T$ have the same eigenvalues with the same algebraic multiplicities.

A more subtle fact is that they also share the same geometric multiplicities for each eigenvalue. This stems from the fundamental result that the rank of any matrix is equal to the rank of its transpose.
$$
\text{GM}_A(\lambda) = n - \text{rank}(A - \lambda I) = n - \text{rank}((A - \lambda I)^T) = n - \text{rank}(A^T - \lambda I) = \text{GM}_{A^T}(\lambda)
$$
This means that for any eigenvalue $\lambda$, the number of linearly independent eigenvectors for $A$ is the same as the number of linearly independent eigenvectors for $A^T$. The eigenvectors of $A^T$ are sometimes called **left eigenvectors** of $A$, as the eigenvector equation $A^T \mathbf{w} = \lambda \mathbf{w}$ is equivalent to $\mathbf{w}^T A = \lambda \mathbf{w}^T$. This result guarantees that the number of independent left eigenvectors for an eigenvalue always equals the number of independent "right" (standard) eigenvectors [@problem_id:1347028].

#### Annihilating Polynomials and Guaranteed Diagonalizability

The condition $\text{GM}(\lambda) = \text{AM}(\lambda)$ can sometimes be guaranteed by the algebraic structure of the matrix itself. This is often revealed by the **[minimal polynomial](@entry_id:153598)** of a matrix, $m_A(t)$, which is the unique [monic polynomial](@entry_id:152311) of least degree such that $m_A(A) = 0$. A cornerstone theorem of linear algebra states:

A matrix $A$ is diagonalizable if and only if its minimal polynomial $m_A(t)$ has no [repeated roots](@entry_id:151486) (i.e., it is a product of distinct linear factors).

This theorem provides an elegant way to prove [diagonalizability](@entry_id:748379) for entire classes of matrices.
- **Projection Matrices:** A matrix is a projection if it satisfies $A^2 = A$. This means the polynomial $q(t) = t^2 - t = t(t-1)$ is an *[annihilating polynomial](@entry_id:155275)*. The minimal polynomial $m_A(t)$ must divide $q(t)$. The possible minimal polynomials are $t$, $t-1$, or $t(t-1)$. In all cases, the roots are distinct (0 and/or 1). Therefore, any [projection matrix](@entry_id:154479) is diagonalizable. This implies that for a [projection matrix](@entry_id:154479), the [geometric multiplicity](@entry_id:155584) of its eigenvalues (which can only be 0 or 1) must equal their [algebraic multiplicity](@entry_id:154240) [@problem_id:1347029].
- **Roots of Unity Matrices:** Consider a complex matrix $A$ satisfying $A^k = I$ for some integer $k \ge 1$. The polynomial $q(t) = t^k - 1$ annihilates $A$. Over the complex numbers, the roots of this polynomial are the $k$ distinct $k$-th [roots of unity](@entry_id:142597). Since the [minimal polynomial](@entry_id:153598) $m_A(t)$ must divide $t^k-1$, its roots must also be distinct. Consequently, any such matrix is diagonalizable over the complex numbers, ensuring that $\text{GM}(\lambda) = \text{AM}(\lambda)$ for all its eigenvalues [@problem_id:1347041].

### Structural Interpretation via the Jordan Normal Form

When a matrix is not diagonalizable because $\text{GM}(\lambda)  \text{AM}(\lambda)$ for some eigenvalue $\lambda$, it can still be simplified into a nearly [diagonal form](@entry_id:264850) known as the **Jordan Normal Form (JNF)**. The JNF reveals the precise structure of a linear operator and provides the ultimate interpretation of algebraic and geometric multiplicities.

A Jordan Normal Form is a [block diagonal matrix](@entry_id:150207), where each block is a **Jordan block** of the form:
$$
J_k(\lambda) = \begin{pmatrix} \lambda  1  0  \dots  0 \\ 0  \lambda  1  \dots  0 \\ \vdots  \ddots  \ddots  \vdots \\ 0  \dots  \dots  \lambda  1 \\ 0  \dots  \dots  0  \lambda \end{pmatrix}
$$
A $1 \times 1$ Jordan block is just $(\lambda)$. A [diagonalizable matrix](@entry_id:150100) is a special case where all Jordan blocks are $1 \times 1$. The JNF of a matrix is unique up to the ordering of the blocks. The multiplicities directly dictate the structure of the Jordan form:

- The **geometric multiplicity** of an eigenvalue $\lambda$ is equal to the **number of Jordan blocks** associated with $\lambda$.
- The **algebraic multiplicity** of an eigenvalue $\lambda$ is equal to the **sum of the sizes** of all Jordan blocks associated with $\lambda$.

For instance, suppose a $5 \times 5$ matrix has an eigenvalue $\lambda=4$ with $\text{AM}(4)=3$ and $\text{GM}(4)=2$. This tells us there must be exactly two Jordan blocks for $\lambda=4$, and their sizes must sum to 3. The only possible combination of sizes is $2$ and $1$. If another eigenvalue $\lambda=-1$ has $\text{AM}(-1)=2$ and $\text{GM}(-1)=1$, there must be a single Jordan block of size 2 for $\lambda=-1$. The Jordan form of the matrix would therefore be (up to permutation of blocks):
$$
J = \begin{pmatrix} 4  1  0  0  0 \\ 0  4  0  0  0 \\ 0  0  4  0  0 \\ 0  0  0  -1  1 \\ 0  0  0  0  -1 \end{pmatrix}
$$
This structure consists of a $2 \times 2$ block for $\lambda=4$, a $1 \times 1$ block for $\lambda=4$, and a $2 \times 2$ block for $\lambda=-1$ [@problem_id:1361918].

This framework can be made even more precise. The exponent of the factor $(t-\lambda)$ in the [minimal polynomial](@entry_id:153598) $m_A(t)$ corresponds to the size of the *largest* Jordan block for that eigenvalue $\lambda$. Let $a = \text{AM}(\lambda)$, $g = \text{GM}(\lambda)$, and $s$ be the size of the largest Jordan block for $\lambda$. With this information, we can establish strict bounds on the [geometric multiplicity](@entry_id:155584) $g$. Since $g$ is the number of blocks whose sizes sum to $a$, with the largest being $s$:
- To **minimize** $g$, we should use the largest possible blocks. The minimum number of blocks required is thus $g_{\min} = \lceil \frac{a}{s} \rceil$.
- To **maximize** $g$, we must use one block of the required size $s$ and then use as many small blocks as possible (of size 1) for the remainder. This gives $s + (g_{\max}-1) \times 1 = a$, which simplifies to $g_{\max} = a - s + 1$.

For example, if for an eigenvalue $\lambda=3$, we find its algebraic multiplicity is $a=12$ (from the characteristic polynomial) and the size of its largest Jordan block is $s=5$ (from the [minimal polynomial](@entry_id:153598)), then the number of Jordan blocks, $g$, which is the geometric multiplicity, must lie in the range:
$$
g_{\min} = \lceil \frac{12}{5} \rceil = 3 \quad \text{and} \quad g_{\max} = 12 - 5 + 1 = 8
$$
Thus, we can conclude that $3 \le \text{GM}(3) \le 8$ without ever seeing the matrix itself [@problem_id:1347039]. This demonstrates the predictive power embedded within the concepts of algebraic and geometric multiplicity and their relationship to the characteristic and minimal polynomials.