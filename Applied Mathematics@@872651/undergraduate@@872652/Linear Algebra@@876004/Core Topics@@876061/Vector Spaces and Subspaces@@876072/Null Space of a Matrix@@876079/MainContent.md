## Introduction
In the study of linear algebra, a matrix is understood as an operator that transforms vectors from one space to another. A fundamental question that arises from this perspective is: which vectors are mapped to the [zero vector](@entry_id:156189)? The answer to this question lies in the concept of the null space, a foundational structure that reveals deep truths about a matrix and the system of equations it represents. Understanding the null space is essential, as it provides the complete [structure of solutions](@entry_id:152035) to [homogeneous linear systems](@entry_id:153432) and describes the inherent ambiguity in solutions to inhomogeneous systems. This article provides a comprehensive exploration of the null space of a matrix, designed to build both conceptual and computational mastery. Across the following chapters, you will learn the core principles and mechanisms defining the null space, explore its wide-ranging applications and interdisciplinary connections in fields from engineering to data science, and finally, apply your knowledge through guided hands-on practices.

## Principles and Mechanisms

In our study of [linear transformations](@entry_id:149133), two fundamental questions arise for any given matrix $A$: which vectors can be produced as outputs (the column space), and which vectors are mapped to the [zero vector](@entry_id:156189)? This second question leads us to one of the most important concepts in linear algebra: the [null space](@entry_id:151476). Understanding the [null space](@entry_id:151476) is not merely an academic exercise; it provides deep insights into the nature of solutions to systems of linear equations and has profound implications in fields ranging from engineering and physics to computer science and data analysis.

### The Definition and Verification of the Null Space

For any given $m \times n$ matrix $A$, the transformation $T(\mathbf{x}) = A\mathbf{x}$ maps vectors from $\mathbb{R}^n$ to $\mathbb{R}^m$. The **[null space](@entry_id:151476)** of $A$, denoted $\text{Nul}(A)$ or sometimes the **kernel** of $A$, is defined as the set of all vectors $\mathbf{x}$ in the domain $\mathbb{R}^n$ that are mapped to the zero vector $\mathbf{0}$ in the [codomain](@entry_id:139336) $\mathbb{R}^m$.

Formally, the definition is:
$$ \text{Nul}(A) = \{ \mathbf{x} \in \mathbb{R}^n \mid A\mathbf{x} = \mathbf{0} \} $$

This definition reveals that the [null space](@entry_id:151476) is precisely the solution set to the **[homogeneous system](@entry_id:150411)** of [linear equations](@entry_id:151487) $A\mathbf{x} = \mathbf{0}$. Any vector that satisfies this equation is an element of the [null space](@entry_id:151476).

Verifying whether a specific vector belongs to the null space is a straightforward application of this definition. One simply performs the [matrix-vector multiplication](@entry_id:140544) and checks if the result is the zero vector.

For instance, consider a physical system whose constraints are described by the equation $A\mathbf{x} = \mathbf{0}$, where $A$ is a $2 \times 3$ matrix. A non-zero vector $\mathbf{x}$ satisfying this equation represents a non-trivial equilibrium state. Let the matrix be:
$$ A = \begin{pmatrix} 1  -2  3 \\ 2  1  -4 \end{pmatrix} $$
To determine if a vector, say $\mathbf{v} = \begin{pmatrix} 1 \\ 2 \\ 1 \end{pmatrix}$, represents such a state, we compute the product $A\mathbf{v}$ [@problem_id:1379226]:
$$ A\mathbf{v} = \begin{pmatrix} 1  -2  3 \\ 2  1  -4 \end{pmatrix} \begin{pmatrix} 1 \\ 2 \\ 1 \end{pmatrix} = \begin{pmatrix} 1(1) - 2(2) + 3(1) \\ 2(1) + 1(2) - 4(1) \end{pmatrix} = \begin{pmatrix} 1 - 4 + 3 \\ 2 + 2 - 4 \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix} $$
Since the product is the [zero vector](@entry_id:156189) in $\mathbb{R}^2$, we confirm that $\mathbf{v}$ is indeed in the null space of $A$. In contrast, for a vector $\mathbf{u} = \begin{pmatrix} 5 \\ 1 \\ 1 \end{pmatrix}$, the product is $A\mathbf{u} = \begin{pmatrix} 5 - 2 + 3 \\ 10 + 1 - 4 \end{pmatrix} = \begin{pmatrix} 6 \\ 7 \end{pmatrix} \neq \mathbf{0}$, so $\mathbf{u}$ is not in $\text{Nul}(A)$.

### The Null Space as a Vector Subspace

The structure of the null space is not just an arbitrary collection of vectors. It possesses a remarkable and crucial property: the null space of any $m \times n$ matrix $A$ is a **subspace** of $\mathbb{R}^n$. To prove this, we must verify three conditions:

1.  **The Zero Vector:** The [zero vector](@entry_id:156189) $\mathbf{0}$ of $\mathbb{R}^n$ must be in $\text{Nul}(A)$. This is always true because $A\mathbf{0} = \mathbf{0}$ for any matrix $A$.

2.  **Closure under Addition:** If $\mathbf{u}$ and $\mathbf{v}$ are any two vectors in $\text{Nul}(A)$, their sum $\mathbf{u} + \mathbf{v}$ must also be in $\text{Nul}(A)$. Since $\mathbf{u}$ and $\mathbf{v}$ are in the [null space](@entry_id:151476), we know $A\mathbf{u} = \mathbf{0}$ and $A\mathbf{v} = \mathbf{0}$. Using the [distributive property](@entry_id:144084) of matrix multiplication:
    $$ A(\mathbf{u} + \mathbf{v}) = A\mathbf{u} + A\mathbf{v} = \mathbf{0} + \mathbf{0} = \mathbf{0} $$
    Thus, $\mathbf{u} + \mathbf{v}$ is in $\text{Nul}(A)$.

3.  **Closure under Scalar Multiplication:** If $\mathbf{u}$ is in $\text{Nul}(A)$ and $c$ is any scalar, the vector $c\mathbf{u}$ must also be in $\text{Nul}(A)$. We know $A\mathbf{u} = \mathbf{0}$. Using the [properties of matrix multiplication](@entry_id:151556):
    $$ A(c\mathbf{u}) = c(A\mathbf{u}) = c\mathbf{0} = \mathbf{0} $$
    Thus, $c\mathbf{u}$ is in $\text{Nul}(A)$.

Since these three properties hold, $\text{Nul}(A)$ is a subspace of $\mathbb{R}^n$. This fact is fundamental. It implies that any [linear combination](@entry_id:155091) of vectors in the [null space](@entry_id:151476) will also reside within the null space [@problem_id:1379254]. For example, if we know that a one-dimensional [null space](@entry_id:151476) (a line) contains the vector $\mathbf{v} = (3, 3, 3)^T$, then any other vector $\mathbf{w}$ in that null space must be a scalar multiple of $\mathbf{v}$, i.e., $\mathbf{w} = t\mathbf{v}$ for some scalar $t$ [@problem_id:1379231].

The subspace property also serves as a powerful diagnostic tool. Any set of vectors that is *not* a subspace of $\mathbb{R}^n$ *cannot* be the [null space](@entry_id:151476) of any matrix. The most immediate test is to check for the presence of the zero vector. Consider a set described as all vectors of the form $(t, 1, 2t)$ for any real number $t$. To obtain the zero vector $(0,0,0)$, we would need $1=0$, which is impossible. Since this set does not contain the zero vector, it fails the first condition for being a subspace and therefore cannot be the [null space](@entry_id:151476) of any matrix [@problem_id:1379266].

### Computing a Basis for the Null Space

While the definition tells us what the [null space](@entry_id:151476) is, it doesn't give us an explicit description of it. To describe a subspace completely, we find a basis for it—a set of linearly independent vectors that span the subspace. The standard algorithm to find a basis for $\text{Nul}(A)$ is as follows:

1.  Solve the [homogeneous system](@entry_id:150411) $A\mathbf{x} = \mathbf{0}$ by row reducing the [augmented matrix](@entry_id:150523) $[A \mid \mathbf{0}]$ to its **[reduced row echelon form](@entry_id:150479) (RREF)**.
2.  Express each **basic variable** (a variable corresponding to a pivot column) in terms of the **[free variables](@entry_id:151663)** (variables corresponding to non-[pivot columns](@entry_id:148772)).
3.  Write the general solution for $\mathbf{x}$ as a vector whose entries depend on the free variables.
4.  Decompose this vector into a [linear combination](@entry_id:155091) of vectors, where each vector corresponds to one of the [free variables](@entry_id:151663). These vectors form a basis for $\text{Nul}(A)$.

This method works because [elementary row operations](@entry_id:155518) correspond to left-multiplying the matrix $A$ by a sequence of invertible [elementary matrices](@entry_id:154374). If $E$ is an invertible matrix, then $A\mathbf{x} = \mathbf{0}$ if and only if $EA\mathbf{x} = E\mathbf{0} = \mathbf{0}$. This means that [row operations](@entry_id:149765) do not change the solution set of the [homogeneous system](@entry_id:150411), and thus **row equivalent matrices have the same null space** [@problem_id:1379260].

As an example, let's find the null space of the matrix from the robotics problem [@problem_id:1379260]:
$$ J_A = \begin{pmatrix} 1  0  2  -1 \\ -2  1  -3  0 \\ 0  1  1  -2 \end{pmatrix} $$
Row reducing $[J_A \mid \mathbf{0}]$ gives:
$$ \left[ \begin{array}{cccc|c} 1  0  2  -1  0 \\ 0  1  1  -2  0 \\ 0  0  0  0  0 \end{array} \right] $$
The variables $w_1$ and $w_2$ are basic, while $w_3$ and $w_4$ are free. The system becomes:
$$ w_1 + 2w_3 - w_4 = 0 \implies w_1 = -2w_3 + w_4 $$
$$ w_2 + w_3 - 2w_4 = 0 \implies w_2 = -w_3 + 2w_4 $$
Let's set the [free variables](@entry_id:151663) as parameters, $w_3 = s$ and $w_4 = t$. The solution vector is:
$$ \mathbf{w} = \begin{pmatrix} w_1 \\ w_2 \\ w_3 \\ w_4 \end{pmatrix} = \begin{pmatrix} -2s + t \\ -s + 2t \\ s \\ t \end{pmatrix} = s \begin{pmatrix} -2 \\ -1 \\ 1 \\ 0 \end{pmatrix} + t \begin{pmatrix} 1 \\ 2 \\ 0 \\ 1 \end{pmatrix} $$
The set of vectors $\left\{ \begin{pmatrix} -2 \\ -1 \\ 1 \\ 0 \end{pmatrix}, \begin{pmatrix} 1 \\ 2 \\ 0 \\ 1 \end{pmatrix} \right\}$ is a basis for $\text{Nul}(J_A)$. The dimension of the [null space](@entry_id:151476) is 2.

### The Null Space, Invertibility, and the Rank-Nullity Theorem

The nature of the null space is intimately connected to fundamental properties of the matrix itself, particularly for square matrices. If the null space of an $n \times n$ matrix $A$ contains only the zero vector, $\text{Nul}(A) = \{\mathbf{0}\}$, it is called the **trivial [null space](@entry_id:151476)**. This occurs if and only if the equation $A\mathbf{x} = \mathbf{0}$ has only the [trivial solution](@entry_id:155162) $\mathbf{x} = \mathbf{0}$. This condition is one of the cornerstones of the Invertible Matrix Theorem. For a square matrix $A$, the following are equivalent:
- $A$ is invertible.
- The null space of $A$ is trivial ($\text{Nul}(A) = \{\mathbf{0}\}$).
- The determinant of $A$ is non-zero ($\det(A) \neq 0$).
- The columns of $A$ are linearly independent.

This means a square matrix has a non-trivial null space (containing at least one non-zero vector) if and only if it is singular, i.e., not invertible [@problem_id:1379228]. This is a powerful computational tool: to check if a system $A\mathbf{x}=\mathbf{0}$ has non-trivial solutions, we can simply calculate the determinant of $A$. If $\det(A)=0$, such solutions exist; if $\det(A)\neq0$, they do not [@problem_id:1379253].

Geometrically, for a $2 \times 2$ matrix, a trivial [null space](@entry_id:151476) is just the origin point in $\mathbb{R}^2$. A non-trivial null space, being a 1-dimensional subspace, is a line passing through the origin [@problem_id:1379239].

For non-square matrices, or more generally, the dimension of the null space is quantified by a pivotal theorem. The **[nullity](@entry_id:156285)** of a matrix $A$, denoted $\text{nullity}(A)$, is the dimension of its null space. This is equal to the number of [free variables](@entry_id:151663) in the solution to $A\mathbf{x}=\mathbf{0}$, which is the number of non-[pivot columns](@entry_id:148772) in the RREF of $A$. The **rank** of $A$, denoted $\text{rank}(A)$, is the dimension of its [column space](@entry_id:150809), which equals the number of [pivot columns](@entry_id:148772). Since every column is either a pivot or a non-pivot column, the sum of these two counts must be the total number of columns. This leads to the **Rank-Nullity Theorem**:

For any $m \times n$ matrix $A$,
$$ \text{rank}(A) + \text{nullity}(A) = n $$

This theorem creates a fixed relationship between the dimension of the output space (rank) and the dimension of the set of vectors mapped to zero (nullity). For example, if a $4 \times 7$ matrix $A$ represents a transformation from $\mathbb{R}^7$ to $\mathbb{R}^4$ and is known to be surjective (its range is all of $\mathbb{R}^4$), then its rank must be 4. The Rank-Nullity Theorem immediately tells us that the dimension of its [null space](@entry_id:151476) is $\text{nullity}(A) = 7 - \text{rank}(A) = 7 - 4 = 3$ [@problem_id:1379212]. This means there is a 3-dimensional subspace of input vectors that are all mapped to the zero vector.

### Orthogonality of the Null Space and Row Space

The Rank-Nullity Theorem provides an algebraic link between [fundamental subspaces](@entry_id:190076). A deeper geometric relationship exists between the null space and another of the [four fundamental subspaces](@entry_id:154834): the [row space](@entry_id:148831). The **row space** of $A$, denoted $\text{Row}(A)$, is the subspace of $\mathbb{R}^n$ spanned by the row vectors of $A$.

A remarkable property connects these two subspaces: the [null space](@entry_id:151476) of a matrix $A$ is the **[orthogonal complement](@entry_id:151540)** of its row space. We write this as $\text{Nul}(A) = (\text{Row}(A))^\perp$.

The proof stems directly from the definition of [matrix multiplication](@entry_id:156035). Let the rows of the $m \times n$ matrix $A$ be $\mathbf{r}_1^T, \mathbf{r}_2^T, \ldots, \mathbf{r}_m^T$. A vector $\mathbf{x} \in \mathbb{R}^n$ is in the null space of $A$ if and only if $A\mathbf{x} = \mathbf{0}$. The product $A\mathbf{x}$ is a column vector whose $i$-th entry is the dot product of the $i$-th row of $A$ with $\mathbf{x}$:
$$ A\mathbf{x} = \begin{pmatrix} \mathbf{r}_1^T \mathbf{x} \\ \mathbf{r}_2^T \mathbf{x} \\ \vdots \\ \mathbf{r}_m^T \mathbf{x} \end{pmatrix} = \begin{pmatrix} \mathbf{r}_1 \cdot \mathbf{x} \\ \mathbf{r}_2 \cdot \mathbf{x} \\ \vdots \\ \mathbf{r}_m \cdot \mathbf{x} \end{pmatrix} $$
For $A\mathbf{x}$ to be the [zero vector](@entry_id:156189), every entry must be zero. This means $\mathbf{r}_i \cdot \mathbf{x} = 0$ for all $i = 1, \ldots, m$. In other words, a vector $\mathbf{x}$ is in the [null space](@entry_id:151476) if and only if it is orthogonal to every row vector of $A$.

If a vector is orthogonal to every vector in a spanning set for a subspace, it is orthogonal to every vector in that subspace. Therefore, any vector $\mathbf{v}$ in the [null space](@entry_id:151476) must be orthogonal to any vector $\mathbf{w}$ in the [row space](@entry_id:148831), meaning their dot product $\mathbf{v} \cdot \mathbf{w}$ is zero. This statement is necessarily true for any matrix $A$ [@problem_id:1379257]. This orthogonal relationship is a cornerstone of the Fundamental Theorem of Linear Algebra and provides a profound geometric picture of the solutions to a [system of linear equations](@entry_id:140416).