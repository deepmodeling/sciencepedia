## Introduction
In the study of [vector spaces](@entry_id:136837), a basis provides a coordinate system that allows us to work with abstract vectors. While the standard basis is a convenient starting point, it is often not the most insightful perspective for understanding a linear transformation or a physical system. The ability to switch from one basis to another—to change our frame of reference—is a fundamental skill that transforms complex problems into simpler ones. This article addresses the core question of how to systematically translate between different coordinate systems and why this is one of the most powerful ideas in linear algebra.

Across the following chapters, you will gain a complete understanding of this crucial concept. The journey begins with **Principles and Mechanisms**, where we will build the mathematical machinery for changing bases for both vectors and [linear transformations](@entry_id:149133). Next, in **Applications and Interdisciplinary Connections**, we will see this machinery in action, exploring how a strategic change of perspective simplifies problems in geometry, physics, and quantum computing. Finally, **Hands-On Practices** will allow you to solidify your understanding by applying these techniques to concrete problems. Let us begin by exploring the foundational principles and mechanisms that govern the change of basis.

## Principles and Mechanisms

In our study of vector spaces, the concept of a basis is paramount. A basis provides a frame of reference, a "coordinate system" that allows us to represent abstract vectors as concrete lists of numbers—their coordinates. However, the choice of basis is often a matter of convenience or perspective. The standard basis in $\mathbb{R}^n$, with its vectors of ones and zeros, is simple for initial computation, but it is not always the most insightful for understanding a particular problem or a [linear transformation](@entry_id:143080). A physicist might choose a basis aligned with the principal axes of a rotating body; a data scientist might choose a basis of principal components to capture the directions of greatest variance in a dataset.

This chapter explores the principles and mechanisms of changing from one basis to another. We will develop a systematic framework for translating the coordinates of vectors and the matrices of [linear transformations](@entry_id:149133) between different bases. This is not merely a technical exercise; it is a powerful tool for simplifying problems, revealing underlying structures, and understanding which properties of a vector or transformation are intrinsic and which are dependent on the chosen frame of reference.

### From One Coordinate System to Another

Let us begin with the fundamental task: given a vector, how do we find its coordinates in a new basis? Consider a vector space $V$ and an "old" basis, which we will often take to be the standard basis $\mathcal{E} = \{\mathbf{e}_1, \dots, \mathbf{e}_n\}$ for familiarity. Let $\mathbf{v}$ be a vector in $V$, represented by its standard [coordinate vector](@entry_id:153319) $[\mathbf{v}]_{\mathcal{E}} = \begin{pmatrix} x_1 \\ \vdots \\ x_n \end{pmatrix}$.

Now, suppose we introduce a new basis $\mathcal{B} = \{\mathbf{b}_1, \dots, \mathbf{b}_n\}$. Since $\mathcal{B}$ is a basis, any vector $\mathbf{v}$ can be written as a unique [linear combination](@entry_id:155091) of its vectors:
$$
\mathbf{v} = c_1 \mathbf{b}_1 + c_2 \mathbf{b}_2 + \dots + c_n \mathbf{b}_n
$$
The scalars $c_1, \dots, c_n$ are the **coordinates of $\mathbf{v}$ relative to the basis $\mathcal{B}$**. We assemble them into the [coordinate vector](@entry_id:153319) $[\mathbf{v}]_{\mathcal{B}} = \begin{pmatrix} c_1 \\ \vdots \\ c_n \end{pmatrix}$.

To find these new coordinates, we can express the equation above in the language of the old basis $\mathcal{E}$. Each new basis vector $\mathbf{b}_j$ has its own representation in the standard basis. If we arrange these coordinate vectors as columns in a matrix, we form the **[change-of-basis matrix](@entry_id:184480) from $\mathcal{B}$ to $\mathcal{E}$**:
$$
P_{\mathcal{E} \leftarrow \mathcal{B}} = \begin{pmatrix} [\mathbf{b}_1]_{\mathcal{E}}  [\mathbf{b}_2]_{\mathcal{E}}  \dots  [\mathbf{b}_n]_{\mathcal{E}} \end{pmatrix}
$$
The fundamental relationship between the coordinate vectors is then given by:
$$
[\mathbf{v}]_{\mathcal{E}} = P_{\mathcal{E} \leftarrow \mathcal{B}} [\mathbf{v}]_{\mathcal{B}}
$$
This equation elegantly states that the standard representation of $\mathbf{v}$ is found by taking a linear combination of the standard representations of the new basis vectors, with the weights given by the new coordinates.

To find the new coordinates $[\mathbf{v}]_{\mathcal{B}}$ from the old ones $[\mathbf{v}]_{\mathcal{E}}$, we must solve this matrix equation. Since the columns of $P_{\mathcal{E} \leftarrow \mathcal{B}}$ are basis vectors, they are [linearly independent](@entry_id:148207), which guarantees that the matrix is invertible. Therefore, we can write:
$$
[\mathbf{v}]_{\mathcal{B}} = (P_{\mathcal{E} \leftarrow \mathcal{B}})^{-1} [\mathbf{v}]_{\mathcal{E}}
$$

**Example: Finding New Coordinates in $\mathbb{R}^2$** [@problem_id:2093]

Consider a vector $\mathbf{v} = \begin{pmatrix} x \\ y \end{pmatrix}$ in the standard basis $\mathcal{E}$ of $\mathbb{R}^2$. Let a new basis be $\mathcal{B} = \{\mathbf{b}_1, \mathbf{b}_2\}$, where $[\mathbf{b}_1]_{\mathcal{E}} = \begin{pmatrix} a \\ c \end{pmatrix}$ and $[\mathbf{b}_2]_{\mathcal{E}} = \begin{pmatrix} b \\ d \end{pmatrix}$. We seek the new coordinates $[\mathbf{v}]_{\mathcal{B}} = \begin{pmatrix} k_1 \\ k_2 \end{pmatrix}$.

The [change-of-basis matrix](@entry_id:184480) from $\mathcal{B}$ to $\mathcal{E}$ is $P_{\mathcal{E} \leftarrow \mathcal{B}} = \begin{pmatrix} a  b \\ c  d \end{pmatrix}$. The relationship is:
$$
\begin{pmatrix} x \\ y \end{pmatrix} = \begin{pmatrix} a  b \\ c  d \end{pmatrix} \begin{pmatrix} k_1 \\ k_2 \end{pmatrix}
$$
To solve for the coordinates $k_1$ and $k_2$, we invert the matrix. Assuming the vectors are [linearly independent](@entry_id:148207), the determinant $ad-bc \neq 0$. The inverse is:
$$
(P_{\mathcal{E} \leftarrow \mathcal{B}})^{-1} = \frac{1}{ad-bc} \begin{pmatrix} d  -b \\ -c  a \end{pmatrix}
$$
Thus, the new [coordinate vector](@entry_id:153319) is:
$$
[\mathbf{v}]_{\mathcal{B}} = \begin{pmatrix} k_1 \\ k_2 \end{pmatrix} = \frac{1}{ad-bc} \begin{pmatrix} d  -b \\ -c  a \end{pmatrix} \begin{pmatrix} x \\ y \end{pmatrix} = \begin{pmatrix} \frac{dx - by}{ad-bc} \\ \frac{ay - cx}{ad-bc} \end{pmatrix}
$$
This provides a general formula for converting coordinates in $\mathbb{R}^2$. In practice, for higher dimensions, one typically solves the linear system directly rather than calculating the inverse matrix explicitly [@problem_id:1351877].

### The General Change-of-Basis Matrix

The matrix that converts coordinates from a basis $\mathcal{B}$ to a basis $\mathcal{C}$ is denoted $P_{\mathcal{C} \leftarrow \mathcal{B}}$. This notation is descriptive: it indicates the "destination" basis $\mathcal{C}$ on the left and the "source" basis $\mathcal{B}$ on the right. The core relationship is:
$$
[\mathbf{v}]_{\mathcal{C}} = P_{\mathcal{C} \leftarrow \mathcal{B}} [\mathbf{v}]_{\mathcal{B}}
$$
A crucial insight into constructing this matrix is to consider what happens when we apply it to the [coordinate vector](@entry_id:153319) of a basis element from $\mathcal{B}$. The [coordinate vector](@entry_id:153319) of $\mathbf{b}_j$ in its own basis is simply a standard basis vector, e.g., $[\mathbf{b}_1]_{\mathcal{B}} = \begin{pmatrix} 1 \\ 0 \\ \vdots \\ 0 \end{pmatrix}$. Applying the transformation:
$$
P_{\mathcal{C} \leftarrow \mathcal{B}} [\mathbf{b}_1]_{\mathcal{B}} = P_{\mathcal{C} \leftarrow \mathcal{B}} \begin{pmatrix} 1 \\ 0 \\ \vdots \\ 0 \end{pmatrix} = (\text{first column of } P_{\mathcal{C} \leftarrow \mathcal{B}})
$$
But from the definition, we also know that $P_{\mathcal{C} \leftarrow \mathcal{B}} [\mathbf{b}_1]_{\mathcal{B}} = [\mathbf{b}_1]_{\mathcal{C}}$. This reveals the fundamental construction rule:

**The $j$-th column of the [change-of-basis matrix](@entry_id:184480) $P_{\mathcal{C} \leftarrow \mathcal{B}}$ is the [coordinate vector](@entry_id:153319) of the $j$-th old [basis vector](@entry_id:199546) $\mathbf{b}_j$ expressed in the new basis $\mathcal{C}$, i.e., $[\mathbf{b}_j]_{\mathcal{C}}$.**

This principle applies to any [finite-dimensional vector space](@entry_id:187130), including spaces of polynomials or functions [@problem_id:1351845]. To find the matrix $P_{\mathcal{C} \leftarrow \mathcal{B}}$, one must systematically take each vector in $\mathcal{B}$, find its coordinates in $\mathcal{C}$, and use these coordinate vectors as the columns of the matrix [@problem_id:1351894].

### Algebraic Properties of Change-of-Basis Matrices

Change-of-basis matrices have a rich algebraic structure that mirrors the logic of changing perspectives.

#### Inversion
If we can change from basis $\mathcal{B}$ to basis $\mathcal{C}$, we must be able to change back. The matrix that reverses the process, changing from $\mathcal{C}$ to $\mathcal{B}$, is $P_{\mathcal{B} \leftarrow \mathcal{C}}$. It logically follows that this matrix must be the inverse of the original.
$$
(P_{\mathcal{C} \leftarrow \mathcal{B}})^{-1} = P_{\mathcal{B} \leftarrow \mathcal{C}}
$$
This identity is immensely useful. For instance, if it is easy to express the vectors of basis $\mathcal{C}$ in terms of basis $\mathcal{B}$, we can construct $P_{\mathcal{B} \leftarrow \mathcal{C}}$ directly. Then, by taking its inverse, we can find $P_{\mathcal{C} \leftarrow \mathcal{B}}$ without having to solve a system of linear equations for each vector in $\mathcal{B}$ [@problem_id:1351888].

#### Composition
Imagine three different coordinate systems, corresponding to bases $\mathcal{B}$, $\mathcal{C}$, and $\mathcal{D}$. If we know how to convert from $\mathcal{B}$ to $\mathcal{C}$ and from $\mathcal{C}$ to $\mathcal{D}$, we can combine these operations to convert directly from $\mathcal{B}$ to $\mathcal{D}$. This composition corresponds to matrix multiplication.

For any vector $\mathbf{v}$:
$$
[\mathbf{v}]_{\mathcal{D}} = P_{\mathcal{D} \leftarrow \mathcal{C}} [\mathbf{v}]_{\mathcal{C}} \quad \text{and} \quad [\mathbf{v}]_{\mathcal{C}} = P_{\mathcal{C} \leftarrow \mathcal{B}} [\mathbf{v}]_{\mathcal{B}}
$$
Substituting the second equation into the first yields:
$$
[\mathbf{v}]_{\mathcal{D}} = P_{\mathcal{D} \leftarrow \mathcal{C}} (P_{\mathcal{C} \leftarrow \mathcal{B}} [\mathbf{v}]_{\mathcal{B}}) = (P_{\mathcal{D} \leftarrow \mathcal{C}} P_{\mathcal{C} \leftarrow \mathcal{B}}) [\mathbf{v}]_{\mathcal{B}}
$$
This gives us the composition rule:
$$
P_{\mathcal{D} \leftarrow \mathcal{B}} = P_{\mathcal{D} \leftarrow \mathcal{C}} P_{\mathcal{C} \leftarrow \mathcal{B}}
$$
Note the order of the matrices and their indices. The transformation from $\mathcal{B}$ to $\mathcal{C}$ is on the right, as it acts first on the [coordinate vector](@entry_id:153319) $[\mathbf{v}]_{\mathcal{B}}$. This chaining property is essential in applications involving multiple [frames of reference](@entry_id:169232), such as robotics or navigation [@problem_id:1351838]. Combining this rule with the inversion property allows for great flexibility. For instance, given $P_{\mathcal{D} \leftarrow \mathcal{C}}$ and $P_{\mathcal{B} \leftarrow \mathcal{C}}$, one can find $P_{\mathcal{D} \leftarrow \mathcal{B}}$ via the relation $P_{\mathcal{D} \leftarrow \mathcal{B}} = P_{\mathcal{D} \leftarrow \mathcal{C}} P_{\mathcal{C} \leftarrow \mathcal{B}} = P_{\mathcal{D} \leftarrow \mathcal{C}} (P_{\mathcal{B} \leftarrow \mathcal{C}})^{-1}$.

### Change of Basis for Linear Transformations

One of the most important applications of changing basis is to find a simpler representation for a linear transformation. A linear transformation $T: V \to V$ is an object that exists independently of any coordinate system. However, to compute with it, we represent it as a matrix. This matrix representation, $[T]_{\mathcal{B}}$, depends entirely on the chosen basis $\mathcal{B}$.

Suppose we know the matrix $[T]_{\mathcal{A}}$ of a transformation $T$ in a basis $\mathcal{A}$, and we wish to find its matrix $[T]_{\mathcal{B}}$ in a new basis $\mathcal{B}$. Let $P$ be the [change-of-basis matrix](@entry_id:184480) that converts coordinates from our new basis $\mathcal{B}$ to the old basis $\mathcal{A}$, i.e., $P = P_{\mathcal{A} \leftarrow \mathcal{B}}$.

The process can be visualized as a three-step journey for a vector $\mathbf{v}$ whose coordinates $[\mathbf{v}]_{\mathcal{B}}$ are known:
1.  **Convert to the old basis:** Find the coordinates of $\mathbf{v}$ in basis $\mathcal{A}$ using $P$: $[\mathbf{v}]_{\mathcal{A}} = P [\mathbf{v}]_{\mathcal{B}}$.
2.  **Apply the transformation:** Apply the known matrix $[T]_{\mathcal{A}}$ to find the coordinates of the transformed vector, $T(\mathbf{v})$, in the $\mathcal{A}$ basis: $[T(\mathbf{v})]_{\mathcal{A}} = [T]_{\mathcal{A}} [\mathbf{v}]_{\mathcal{A}} = [T]_{\mathcal{A}} P [\mathbf{v}]_{\mathcal{B}}$.
3.  **Convert back to the new basis:** Convert this result back to the $\mathcal{B}$ basis using the inverse matrix $P^{-1} = P_{\mathcal{B} \leftarrow \mathcal{A}}$: $[T(\mathbf{v})]_{\mathcal{B}} = P^{-1} [T(\mathbf{v})]_{\mathcal{A}} = P^{-1} [T]_{\mathcal{A}} P [\mathbf{v}]_{\mathcal{B}}$.

By definition, the matrix $[T]_{\mathcal{B}}$ is the matrix that directly maps $[\mathbf{v}]_{\mathcal{B}}$ to $[T(\mathbf{v})]_{\mathcal{B}}$. By comparing with the result above, we arrive at the celebrated **[similarity transformation](@entry_id:152935)** formula:
$$
[T]_{\mathcal{B}} = P^{-1} [T]_{\mathcal{A}} P, \quad \text{where } P = P_{\mathcal{A} \leftarrow \mathcal{B}}
$$
Two matrices $A$ and $B$ are said to be **similar** if there exists an invertible matrix $P$ such that $B = P^{-1}AP$. Our derivation shows that matrices representing the same linear transformation in different bases are similar. This is a profound connection between a geometric concept (a single transformation viewed from different angles) and an algebraic one (an equivalence class of matrices).

This formula is a cornerstone of linear algebra. It allows us to switch to a basis where a transformation's matrix becomes much simpler, for example, a diagonal matrix. Such a basis is called an **[eigenbasis](@entry_id:151409)**, and the process of finding it is **diagonalization** [@problem_id:1351874]. If we can find a basis $\mathcal{B}$ of eigenvectors for $T$, then the matrix $[T]_{\mathcal{B}}$ will be a [diagonal matrix](@entry_id:637782) $D$ whose diagonal entries are the eigenvalues. The [standard matrix](@entry_id:151240) of the transformation, $A = [T]_{\mathcal{E}}$, can then be found using the reverse transformation: $A = PDP^{-1}$, where $P = P_{\mathcal{E} \leftarrow \mathcal{B}}$ is the matrix whose columns are the eigenvectors. Conversely, if we have a [complex matrix](@entry_id:194956) in the standard basis, we can find its representation in a more convenient, custom basis to simplify analysis or computation [@problem_id:1351855].

### Invariants Under Change of Basis

While the matrix representation of a transformation changes with the basis, its essential, geometric properties do not. These are the **invariants** of the transformation. One of the most important invariants is the set of **eigenvalues**.

Let $A = [T]_{\mathcal{A}}$ and $B = [T]_{\mathcal{B}}$ be two [matrix representations](@entry_id:146025) of the same transformation $T$. We know they are similar, so $B = P^{-1}AP$ for some invertible matrix $P$. Let's examine the characteristic equation for $B$:
$$
\det(B - \lambda I) = \det(P^{-1}AP - \lambda I)
$$
We can cleverly write $\lambda I = \lambda P^{-1}P = P^{-1}(\lambda I)P$. Substituting this gives:
$$
\det(P^{-1}AP - P^{-1}(\lambda I)P) = \det(P^{-1}(A - \lambda I)P)
$$
Using the property that $\det(XYZ) = \det(X)\det(Y)\det(Z)$, we get:
$$
\det(P^{-1})\det(A - \lambda I)\det(P) = \det(P^{-1})\det(P)\det(A - \lambda I) = \frac{1}{\det(P)}\det(P)\det(A - \lambda I) = \det(A - \lambda I)
$$
Thus, $\det(B - \lambda I) = \det(A - \lambda I)$. The matrices $A$ and $B$ have the exact same characteristic polynomial. Consequently, they must have the same eigenvalues.

This is a critical result. It confirms that eigenvalues are an intrinsic property of the linear operator $T$, not an artifact of its representation. In physics, for example, [observables](@entry_id:267133) like energy or momentum are represented by operators. The possible outcomes of a measurement are the eigenvalues of that operator. These physical quantities cannot depend on the mathematical coordinate system chosen by the physicist, and this principle provides the mathematical justification [@problem_id:2084052]. Other invariants under similarity transformations include the determinant, the trace, and the rank of the matrix.

### Change of Basis for Dual Spaces

For a more advanced perspective, we can consider how a change of basis in a vector space $V$ affects the coordinates in its **[dual space](@entry_id:146945)** $V^*$. The dual space is the space of all [linear functionals](@entry_id:276136) on $V$.

Let $\mathcal{B} = \{\mathbf{b}_1, \dots, \mathbf{b}_n\}$ be a basis for $V$. The corresponding **[dual basis](@entry_id:145076)** is $\mathcal{B}^* = \{f^1, \dots, f^n\}$, where each $f^i$ is a linear functional defined by its action on the basis vectors of $V$: $f^i(\mathbf{b}_j) = \delta_{ij}$ (the Kronecker delta).

Suppose we change from basis $\mathcal{B}$ to basis $\mathcal{C}$ in $V$, with the [coordinate transformation](@entry_id:138577) $[v]_{\mathcal{C}} = P_{\mathcal{C} \leftarrow \mathcal{B}} [v]_{\mathcal{B}}$. How do the coordinates of a linear functional $f \in V^*$ transform between the [dual bases](@entry_id:151162) $\mathcal{B}^*$ and $\mathcal{C}^*$?

The evaluation of a functional on a vector, $f(v)$, is a scalar and thus independent of any basis choice. In coordinates, this evaluation can be written as a dot product:
$$
f(v) = [f]_{\mathcal{B}^*}^\mathsf{T} [v]_{\mathcal{B}} = [f]_{\mathcal{C}^*}^\mathsf{T} [v]_{\mathcal{C}}
$$
Substituting the relation for the vector coordinates, we have:
$$
[f]_{\mathcal{B}^*}^\mathsf{T} [v]_{\mathcal{B}} = [f]_{\mathcal{C}^*}^\mathsf{T} (P_{\mathcal{C} \leftarrow \mathcal{B}} [v]_{\mathcal{B}})
$$
Since this must hold for all vectors $v$ (and thus for all coordinate vectors $[v]_{\mathcal{B}}$), we can equate the row vectors:
$$
[f]_{\mathcal{B}^*}^\mathsf{T} = [f]_{\mathcal{C}^*}^\mathsf{T} P_{\mathcal{C} \leftarrow \mathcal{B}}
$$
Taking the transpose of both sides gives a relation for the column vectors of coordinates:
$$
[f]_{\mathcal{B}^*} = (P_{\mathcal{C} \leftarrow \mathcal{B}})^\mathsf{T} [f]_{\mathcal{C}^*}
$$
This equation tells us how to convert coordinates from $\mathcal{C}^*$ to $\mathcal{B}^*$. The matrix that performs this transformation is $(P_{\mathcal{C} \leftarrow \mathcal{B}})^\mathsf{T}$. Therefore, the matrix for the reverse transformation, from $\mathcal{B}^*$ to $\mathcal{C}^*$, must be the inverse of this matrix:
$$
Q_{\mathcal{C}^* \leftarrow \mathcal{B}^*} = ((P_{\mathcal{C} \leftarrow \mathcal{B}})^\mathsf{T})^{-1} = ((P_{\mathcal{C} \leftarrow \mathcal{B}})^{-1})^\mathsf{T} = (P_{\mathcal{B} \leftarrow \mathcal{C}})^\mathsf{T}
$$
This shows that the [change-of-basis matrix](@entry_id:184480) for the [dual space](@entry_id:146945) is the transpose of the inverse of the [change-of-basis matrix](@entry_id:184480) for the primal space. This transformation rule is sometimes referred to as **covariant** for vectors and **contravariant** for functionals, terminology common in physics and differential geometry [@problem_id:1351891].