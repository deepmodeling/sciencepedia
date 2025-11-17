## Introduction
In the realm of linear algebra, eigenvectors and their corresponding eigenvalues represent the foundational elements that describe how a [linear transformation](@entry_id:143080) acts. These special vectors maintain their direction under the transformation, being merely scaled by a factor—the eigenvalue. While analyzing individual eigenvectors is insightful, the true power of this concept is unlocked when we consider the collective structure they form. This structure, known as an eigenspace, is not just a simple collection of vectors but a fundamental subspace that reveals the invariant properties and geometric character of the transformation itself. This article addresses the need to move beyond single eigenvectors to understand these richer, more structured mathematical objects.

Across the following chapters, you will embark on a comprehensive exploration of [eigenspaces](@entry_id:147356). The journey begins with **Principles and Mechanisms**, where you will learn the formal definition of an eigenspace, understand why it forms a subspace, and discover its crucial connection to the null space, which provides a direct method for its computation. Next, in **Applications and Interdisciplinary Connections**, you will see how this abstract concept finds concrete utility in diverse fields such as quantum mechanics, data science, and dynamical systems, serving as the bedrock for describing equilibrium states and principal modes of behavior. Finally, the **Hands-On Practices** chapter will allow you to solidify your understanding by applying these theoretical concepts to solve practical problems, from verifying eigenvectors to constructing matrices from their eigen-properties.

## Principles and Mechanisms

In the study of [linear transformations](@entry_id:149133), certain vectors stand out due to their remarkable simplicity of behavior. When acted upon by a linear transformation represented by a matrix $A$, these vectors are merely scaled, without any change in their direction. Such a non-zero vector $\mathbf{v}$ is called an **eigenvector**, and the scaling factor $\lambda$ is its corresponding **eigenvalue**. This relationship is captured by the fundamental equation $A\mathbf{v} = \lambda\mathbf{v}$. While individual eigenvectors are insightful, the collective structure they form reveals deeper properties of the transformation itself. This chapter explores the concept of the **eigenspace**, the [vector subspace](@entry_id:151815) associated with each eigenvalue.

### From Eigenvectors to Eigenspaces: A Formal Definition

The definition of an eigenvector explicitly requires it to be a **non-zero** vector. This is a crucial convention; if the zero vector were allowed, any scalar $\lambda$ would satisfy $A\mathbf{0} = \lambda\mathbf{0} = \mathbf{0}$, making every scalar an eigenvalue, which would be a trivial and uninformative situation. However, the set consisting only of the non-zero eigenvectors for a given eigenvalue $\lambda$ does not form a [vector subspace](@entry_id:151815). For a set to be a subspace, it must satisfy three conditions: it must contain the [zero vector](@entry_id:156189), it must be closed under vector addition, and it must be closed under scalar multiplication. The set of eigenvectors fails the first condition by definition. It can also fail the others; for instance, if $\mathbf{v}$ is an eigenvector, then $-\mathbf{v}$ is also an eigenvector, but their sum $\mathbf{v} + (-\mathbf{v}) = \mathbf{0}$ is not an eigenvector.

To remedy this and harness the powerful tools of vector space theory, we introduce a slightly more inclusive set. The **[eigenspace](@entry_id:150590)** corresponding to an eigenvalue $\lambda$ of a matrix $A$, denoted $E_{\lambda}$, is the set of *all* vectors $\mathbf{v}$ (including the [zero vector](@entry_id:156189)) that satisfy the equation $A\mathbf{v} = \lambda\mathbf{v}$.

$$E_{\lambda} = \{\mathbf{v} \in \mathbb{R}^n \mid A\mathbf{v} = \lambda\mathbf{v}\}$$

This simple inclusion of the [zero vector](@entry_id:156189) is the critical step that elevates a mere collection of special vectors into a structured mathematical object with profound implications [@problem_id:1394453].

### The Eigenspace as a Subspace

The primary importance of the eigenspace $E_{\lambda}$ is that it is, in fact, a **subspace** of the larger vector space $\mathbb{R}^n$. To verify this, we must confirm the three subspace axioms:

1.  **Presence of the Zero Vector:** The [zero vector](@entry_id:156189) $\mathbf{0}$ is always in $E_{\lambda}$ because $A\mathbf{0} = \mathbf{0}$ and $\lambda\mathbf{0} = \mathbf{0}$, so $A\mathbf{0} = \lambda\mathbf{0}$ is always true.

2.  **Closure under Addition:** Let $\mathbf{v}_1$ and $\mathbf{v}_2$ be any two vectors in $E_{\lambda}$. By definition, this means $A\mathbf{v}_1 = \lambda\mathbf{v}_1$ and $A\mathbf{v}_2 = \lambda\mathbf{v}_2$. Now consider their sum, $\mathbf{v}_1 + \mathbf{v}_2$. Using the linearity of matrix multiplication, we have:
    $$A(\mathbf{v}_1 + \mathbf{v}_2) = A\mathbf{v}_1 + A\mathbf{v}_2 = \lambda\mathbf{v}_1 + \lambda\mathbf{v}_2 = \lambda(\mathbf{v}_1 + \mathbf{v}_2)$$
    This result shows that the vector $\mathbf{v}_1 + \mathbf{v}_2$ also satisfies the defining equation for $E_{\lambda}$, so it is also in the eigenspace.

3.  **Closure under Scalar Multiplication:** Let $\mathbf{v}$ be a vector in $E_{\lambda}$ and let $c$ be any scalar. We know $A\mathbf{v} = \lambda\mathbf{v}$. Consider the vector $c\mathbf{v}$:
    $$A(c\mathbf{v}) = c(A\mathbf{v}) = c(\lambda\mathbf{v}) = \lambda(c\mathbf{v})$$
    Thus, $c\mathbf{v}$ is also in $E_{\lambda}$.

Since $E_{\lambda}$ satisfies all three conditions, it is a subspace of $\mathbb{R}^n$ [@problem_id:1394412]. This means that any [linear combination](@entry_id:155091) of eigenvectors corresponding to the same eigenvalue $\lambda$ will also be an eigenvector for $\lambda$ (or the [zero vector](@entry_id:156189)). For example, if $\mathbf{v}_1$ and $\mathbf{v}_2$ are [linearly independent](@entry_id:148207) eigenvectors for $\lambda$, then vectors such as $\mathbf{v}_1 + \mathbf{v}_2$ and $4\mathbf{v}_1 - 7\mathbf{v}_2$ are also guaranteed to be in $E_\lambda$.

### The Fundamental Connection: Eigenspaces and Null Spaces

The definition of the eigenspace can be rewritten in a way that connects it directly to another fundamental concept in linear algebra: the null space. The defining equation is:
$$A\mathbf{v} = \lambda\mathbf{v}$$

We can introduce the identity matrix $I$ (where $I\mathbf{v}=\mathbf{v}$) to rewrite the right side:
$$A\mathbf{v} = \lambda I \mathbf{v}$$

Rearranging the terms gives:
$$A\mathbf{v} - \lambda I \mathbf{v} = \mathbf{0}$$

Factoring out the vector $\mathbf{v}$ yields:
$$(A - \lambda I)\mathbf{v} = \mathbf{0}$$

This equation reveals a profound identity: the eigenspace $E_{\lambda}$ is precisely the **null space** (or **kernel**) of the matrix $(A - \lambda I)$.
$$E_{\lambda} = \ker(A - \lambda I)$$

This connection is incredibly useful. Since the null space of any matrix is always a subspace, this provides an alternative proof that $E_{\lambda}$ is a subspace. More importantly, it gives us a direct computational method for finding the eigenspace.

A particularly noteworthy special case occurs when $\lambda = 0$ is an eigenvalue. In this situation, the [eigenspace](@entry_id:150590) $E_0$ is defined by the equation $A\mathbf{v} = 0\mathbf{v}$, which simplifies to $A\mathbf{v} = \mathbf{0}$. This is the definition of the [null space](@entry_id:151476) of the matrix $A$ itself. Therefore, the [eigenspace](@entry_id:150590) corresponding to the eigenvalue zero is identical to the null space of the matrix: $E_0 = \ker(A)$ [@problem_id:1394445]. This implies that a matrix has an eigenvalue of 0 if and only if it is singular (i.e., not invertible), as a non-trivial null space is the defining characteristic of a singular matrix.

### Computing a Basis for an Eigenspace

The identification of $E_{\lambda}$ with $\ker(A - \lambda I)$ provides a concrete algorithm for determining the [eigenspace](@entry_id:150590) associated with a known eigenvalue $\lambda$. The process involves solving a homogeneous [system of [linear equation](@entry_id:140416)s](@entry_id:151487).

Let's illustrate this with an example. Consider the matrix and eigenvalue [@problem_id:1394454]:
$$A = \begin{pmatrix} 5  -1  0 \\ 1  4  3 \\ 3  0  6 \end{pmatrix}, \quad \lambda = 3$$

1.  **Form the matrix $A - \lambda I$**:
    We subtract $\lambda=3$ from the diagonal entries of $A$:
    $$A - 3I = \begin{pmatrix} 5-3  -1  0 \\ 1  4-3  3 \\ 3  0  6-3 \end{pmatrix} = \begin{pmatrix} 2  -1  0 \\ 1  1  3 \\ 3  0  3 \end{pmatrix}$$

2.  **Set up the [homogeneous system](@entry_id:150411) $(A - \lambda I)\mathbf{v} = \mathbf{0}$**:
    Let $\mathbf{v} = \begin{pmatrix} x \\ y \\ z \end{pmatrix}$. The matrix equation becomes:
    $$\begin{pmatrix} 2  -1  0 \\ 1  1  3 \\ 3  0  3 \end{pmatrix} \begin{pmatrix} x \\ y \\ z \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \\ 0 \end{pmatrix}$$
    This corresponds to the [system of linear equations](@entry_id:140416):
    $$\begin{cases} 2x - y + 0z = 0 \\ x + y + 3z = 0 \\ 3x + 0y + 3z = 0 \end{cases}$$

3.  **Solve the system**:
    From the third equation, $3x + 3z = 0$, we get $z = -x$.
    From the first equation, $2x - y = 0$, we get $y = 2x$.
    Substituting these into the second equation confirms consistency: $x + (2x) + 3(-x) = 3x - 3x = 0$.
    The system is dependent, with one free variable. Let's choose $x=t$ as the free parameter. The solution vector is:
    $$\mathbf{v} = \begin{pmatrix} x \\ y \\ z \end{pmatrix} = \begin{pmatrix} t \\ 2t \\ -t \end{pmatrix} = t \begin{pmatrix} 1 \\ 2 \\ -1 \end{pmatrix}$$

4.  **Describe the [eigenspace](@entry_id:150590)**:
    The [solution set](@entry_id:154326), which is the eigenspace $E_3$, consists of all scalar multiples of the vector $\begin{pmatrix} 1 \\ 2 \\ -1 \end{pmatrix}$. This means the eigenspace is a one-dimensional subspace of $\mathbb{R}^3$, and a **basis** for $E_3$ is given by the single vector $\left\{\begin{pmatrix} 1 \\ 2 \\ -1 \end{pmatrix}\right\}$.

The dimension of an [eigenspace](@entry_id:150590) $E_\lambda$ is called the **[geometric multiplicity](@entry_id:155584)** of the eigenvalue $\lambda$. In the example above, the [geometric multiplicity](@entry_id:155584) of $\lambda=3$ is 1.

### The Geometry of Eigenspaces

Since eigenspaces are subspaces of $\mathbb{R}^n$, they have clear geometric interpretations. The dimension of the [eigenspace](@entry_id:150590) determines the nature of this geometry.

*   A **1-dimensional [eigenspace](@entry_id:150590)** in $\mathbb{R}^2$ or $\mathbb{R}^3$ corresponds to a **line** passing through the origin. All vectors on this line are eigenvectors (or the zero vector). The transformation $A$ acts on this line by stretching or compressing all vectors along it by the factor $\lambda$.
*   A **2-dimensional [eigenspace](@entry_id:150590)** in $\mathbb{R}^3$ corresponds to a **plane** passing through the origin. Any non-zero vector lying in this plane is an eigenvector with eigenvalue $\lambda$. The transformation $A$ scales this entire plane by the factor $\lambda$.
*   A **3-dimensional eigenspace** in $\mathbb{R}^3$ is the entire space $\mathbb{R}^3$. This occurs only if the matrix $A$ is a scalar multiple of the identity matrix, $A = \lambda I$. In this case, every vector in $\mathbb{R}^3$ is an eigenvector with eigenvalue $\lambda$.

Consider the matrix [@problem_id:1394429]:
$$A = \begin{pmatrix} 3  0  0 \\ 2  1  -2 \\ 2  -2  1 \end{pmatrix}$$
The characteristic polynomial is $\det(A-\lambda I) = -(3-\lambda)^2(1+\lambda)$. The eigenvalues are $\lambda_1 = 3$ (with **[algebraic multiplicity](@entry_id:154240)** 2) and $\lambda_2 = -1$ (with algebraic multiplicity 1). Let's find the eigenspace for $\lambda=3$. We solve $(A-3I)\mathbf{x}=\mathbf{0}$:
$$A-3I = \begin{pmatrix} 0  0  0 \\ 2  -2  -2 \\ 2  -2  -2 \end{pmatrix}$$
The system reduces to the single equation $2x - 2y - 2z = 0$, or more simply, $x - y - z = 0$. This is the [equation of a plane](@entry_id:151332) passing through the origin. The [geometric multiplicity](@entry_id:155584) of $\lambda=3$ is 2, which matches its algebraic multiplicity in this case. The normal vector to this plane is $\begin{pmatrix} 1 \\ -1 \\ -1 \end{pmatrix}$. Geometrically, the transformation $A$ acts by scaling every vector in this plane by a factor of 3.

### Core Properties of Eigenspaces

Eigenspaces possess several fundamental properties that are central to their role in linear algebra and its applications.

#### Invariance Under Transformation

An eigenspace $E_\lambda$ is an **invariant subspace** under the transformation $A$. This means that if you take any vector $\mathbf{v}$ from $E_\lambda$ and apply the transformation $A$ to it, the resulting vector $A\mathbf{v}$ will also be in $E_\lambda$. This is immediately clear from the definition: $A\mathbf{v} = \lambda\mathbf{v}$. Since $E_\lambda$ is closed under scalar multiplication, the vector $\lambda\mathbf{v}$ is guaranteed to be in $E_\lambda$.

This invariance extends to any polynomial of the matrix $A$. Let $p(t) = c_k t^k + \dots + c_1 t + c_0$ be a polynomial. Then for any $\mathbf{v} \in E_\lambda$:
$$A^2\mathbf{v} = A(A\mathbf{v}) = A(\lambda\mathbf{v}) = \lambda(A\mathbf{v}) = \lambda(\lambda\mathbf{v}) = \lambda^2\mathbf{v}$$
By induction, $A^m\mathbf{v} = \lambda^m\mathbf{v}$ for any non-negative integer $m$. Therefore,
$$p(A)\mathbf{v} = (c_k A^k + \dots + c_1 A + c_0 I)\mathbf{v} = (c_k\lambda^k + \dots + c_1\lambda + c_0)\mathbf{v} = p(\lambda)\mathbf{v}$$
This shows that if $\mathbf{v}$ is an eigenvector of $A$ with eigenvalue $\lambda$, then $\mathbf{v}$ is also an eigenvector of the matrix $p(A)$ with eigenvalue $p(\lambda)$. As an example, if $\mathbf{v} \in E_3$ for some matrix $A$, and we form the vector $\mathbf{w} = (2A^2 - 11A + 10I)\mathbf{v}$, we can immediately find the scaling factor $k$ such that $\mathbf{w}=k\mathbf{v}$ by evaluating the polynomial at $\lambda=3$: $k = 2(3)^2 - 11(3) + 10 = 18 - 33 + 10 = -5$ [@problem_id:1394447].

#### Interaction of Distinct Eigenspaces

While [linear combinations](@entry_id:154743) of eigenvectors *within* a single eigenspace remain in that [eigenspace](@entry_id:150590), combining eigenvectors from *different* [eigenspaces](@entry_id:147356) generally does not produce another eigenvector [@problem_id:1394412]. In fact, [eigenspaces](@entry_id:147356) corresponding to distinct eigenvalues are almost entirely separate.

A fundamental theorem states that **eigenvectors corresponding to distinct eigenvalues are linearly independent**. A direct consequence of this is that the intersection of two [eigenspaces](@entry_id:147356) for distinct eigenvalues contains only the zero vector. Let $\lambda_1 \neq \lambda_2$ be two distinct eigenvalues of $A$. Suppose a vector $\mathbf{w}$ lies in both [eigenspaces](@entry_id:147356), i.e., $\mathbf{w} \in E_{\lambda_1}$ and $\mathbf{w} \in E_{\lambda_2}$.
- Since $\mathbf{w} \in E_{\lambda_1}$, we have $A\mathbf{w} = \lambda_1\mathbf{w}$.
- Since $\mathbf{w} \in E_{\lambda_2}$, we have $A\mathbf{w} = \lambda_2\mathbf{w}$.

Equating these gives $\lambda_1\mathbf{w} = \lambda_2\mathbf{w}$, which can be rearranged to $(\lambda_1 - \lambda_2)\mathbf{w} = \mathbf{0}$. Because $\lambda_1 \neq \lambda_2$, the scalar $(\lambda_1 - \lambda_2)$ is non-zero. The only way for a non-zero scalar to multiply a vector and yield the [zero vector](@entry_id:156189) is if the vector itself is the zero vector. Therefore, $\mathbf{w} = \mathbf{0}$.
This proves that the only vector shared by two distinct [eigenspaces](@entry_id:147356) is the [zero vector](@entry_id:156189): $E_{\lambda_1} \cap E_{\lambda_2} = \{\mathbf{0}\}$ [@problem_id:1394451].

The sum of these eigenspaces, $E_{\lambda_1} + E_{\lambda_2}$, is also a subspace, known as a [direct sum](@entry_id:156782), denoted $E_{\lambda_1} \oplus E_{\lambda_2}$ [@problem_id:1394453].

#### Eigenspaces of Shifted and Transposed Matrices

The structure of eigenspaces also behaves predictably with respect to simple matrix operations.
Consider a **shifted matrix** $B = A - kI$ for some scalar $k$. If $\mathbf{v}$ is an eigenvector of $A$ with eigenvalue $\lambda$, then $A\mathbf{v} = \lambda\mathbf{v}$. Let's see how $B$ acts on $\mathbf{v}$:
$$B\mathbf{v} = (A - kI)\mathbf{v} = A\mathbf{v} - kI\mathbf{v} = \lambda\mathbf{v} - k\mathbf{v} = (\lambda - k)\mathbf{v}$$
This shows that $\mathbf{v}$ is also an eigenvector of $B$, but with the eigenvalue $\lambda - k$. This relationship is bidirectional, meaning the eigenspaces themselves are identical: $E_{\lambda}(A) = E_{\lambda-k}(A-kI)$. The eigenvectors do not change, only their corresponding eigenvalues are shifted [@problem_id:1394417].

Another important relationship involves the **transpose matrix**, $A^T$. The eigenvalues of $A^T$ are the same as the eigenvalues of $A$. However, their corresponding eigenvectors (called **left eigenvectors** of $A$) are generally different, unless $A$ is symmetric ($A=A^T$). There is a remarkable orthogonality relationship between the [eigenspaces](@entry_id:147356) of $A$ (right [eigenspaces](@entry_id:147356)) and $A^T$ (left [eigenspaces](@entry_id:147356)).

Let $\mathbf{u}$ be an eigenvector of $A$ for eigenvalue $\lambda$, and let $\mathbf{w}$ be an eigenvector of $A^T$ for eigenvalue $\mu$, where $\lambda \neq \mu$. We have $A\mathbf{u} = \lambda\mathbf{u}$ and $A^T\mathbf{w} = \mu\mathbf{w}$. Consider the scalar quantity $\mathbf{w}^T A \mathbf{u}$. We can evaluate this in two ways:
1.  $\mathbf{w}^T (A\mathbf{u}) = \mathbf{w}^T (\lambda\mathbf{u}) = \lambda(\mathbf{w}^T \mathbf{u})$
2.  $(\mathbf{w}^T A)\mathbf{u} = (A^T \mathbf{w})^T \mathbf{u} = (\mu\mathbf{w})^T \mathbf{u} = \mu(\mathbf{w}^T \mathbf{u})$

Equating the two results gives $\lambda(\mathbf{w}^T \mathbf{u}) = \mu(\mathbf{w}^T \mathbf{u})$, or $(\lambda - \mu)(\mathbf{w}^T \mathbf{u}) = 0$. Since $\lambda \neq \mu$, we must conclude that $\mathbf{w}^T \mathbf{u} = 0$. This means the vectors are orthogonal. In other words, any eigenvector of $A$ with eigenvalue $\lambda$ is orthogonal to any eigenvector of $A^T$ with a different eigenvalue $\mu$. This implies that the entire [eigenspace](@entry_id:150590) $E_\lambda(A)$ is orthogonal to the [eigenspace](@entry_id:150590) $E_\mu(A^T)$ when $\lambda \neq \mu$ [@problem_id:1394419].

### Beyond Eigenspaces: A Note on Generalized Eigenspaces

For many matrices, the sum of the dimensions of all their [eigenspaces](@entry_id:147356) (the sum of the geometric multiplicities) equals the dimension of the matrix, $n$. Such matrices are called **diagonalizable**. For these matrices, one can form a basis for the entire space $\mathbb{R}^n$ using only eigenvectors.

However, some matrices are **defective**, meaning the [geometric multiplicity](@entry_id:155584) of at least one eigenvalue is strictly less than its algebraic multiplicity. For such matrices, the eigenvectors are not numerous enough to form a basis for the whole space. To build a complete basis, one must introduce the concept of **[generalized eigenvectors](@entry_id:152349)**.

A [generalized eigenvector](@entry_id:154062) of order $m$ corresponding to eigenvalue $\lambda$ is a non-zero vector $\mathbf{v}$ such that $(A - \lambda I)^m \mathbf{v} = \mathbf{0}$ but $(A - \lambda I)^{m-1} \mathbf{v} \neq \mathbf{0}$. Standard eigenvectors are [generalized eigenvectors](@entry_id:152349) of order 1. The set of all vectors satisfying $(A - \lambda I)^m \mathbf{v} = \mathbf{0}$ for a fixed $m$ forms the **generalized eigenspace** of order $m$, denoted $K_\lambda^{(m)} = \ker((A - \lambda I)^m)$.

These generalized [eigenspaces](@entry_id:147356) form a nested sequence of subspaces:
$$E_\lambda = K_\lambda^{(1)} \subseteq K_\lambda^{(2)} \subseteq \dots$$

For [defective matrices](@entry_id:194492), this sequence grows until it stabilizes. The full set of [generalized eigenvectors](@entry_id:152349) for an eigenvalue does provide a subspace of the "correct" dimension (equal to the algebraic multiplicity). These concepts are critical in the study of the Jordan normal form of a matrix and in solving [systems of differential equations](@entry_id:148215), particularly when dealing with operators on more [abstract vector spaces](@entry_id:155811), such as spaces of matrices or functions [@problem_id:1394460].