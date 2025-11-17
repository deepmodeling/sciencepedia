## Introduction
In linear algebra, transformations are fundamental rules that map vectors from one space to another. While the idea of a mapping is intuitive, a deeper analysis requires a precise understanding of its core components: the domain (the space of inputs), the codomain (the space of potential outputs), and the range (the set of actual outputs). This article bridges the gap between the general concept of a transformation and the detailed characterization of its structure and capabilities. By dissecting these three elements, we unlock the ability to analyze a transformation's behavior, determine its expressive power, and solve a wide array of problems in mathematics and science.

The following sections will guide you through this exploration. In **Principles and Mechanisms**, we will establish the formal definitions of domain, [codomain](@entry_id:139336), and range, and prove the critical theorem that the range of a linear transformation is always a subspace. Next, **Applications and Interdisciplinary Connections** will demonstrate the utility of these concepts, from visualizing geometric transformations to characterizing operators in abstract spaces of polynomials and matrices. Finally, **Hands-On Practices** will provide you with opportunities to solidify your understanding by solving targeted problems.

## Principles and Mechanisms

In the study of linear algebra, transformations are the dynamic elements that describe relationships between [vector spaces](@entry_id:136837). Having introduced the general notion of a transformation, we now dissect its fundamental components: the domain, the [codomain](@entry_id:139336), and the range. Understanding these concepts is crucial for analyzing the behavior of transformations, [solving systems of linear equations](@entry_id:136676), and grasping the geometric and algebraic consequences of mapping one space to another.

### Fundamental Definitions: Domain, Codomain, and Range

A **transformation** (or map) $T$ from a vector space $V$ to a vector space $W$, denoted $T: V \to W$, is a rule that assigns to each vector $\mathbf{v}$ in $V$ a unique vector $\mathbf{w}$ in $W$.

The three key sets associated with any transformation are:

1.  The **Domain**: The starting vector space $V$ is called the **domain** of the transformation. It is the set of all possible input vectors.

2.  The **Codomain**: The target vector space $W$ is called the **[codomain](@entry_id:139336)** of the transformation. It is the space in which all output vectors reside.

3.  The **Range**: The **range** of $T$, also known as the **image** of $T$ and denoted $\text{range}(T)$ or $\text{im}(T)$, is the subset of the [codomain](@entry_id:139336) $W$ consisting of all actual output vectors. Formally,
    $$
    \text{range}(T) = \{ T(\mathbf{v}) \mid \mathbf{v} \in V \}
    $$

It is essential to distinguish between the codomain and the range. The [codomain](@entry_id:139336) is the space of *potential* outputs, whereas the range is the set of *actual* outputs. The range is always a subset of the codomain, i.e., $\text{range}(T) \subseteq W$, but it is not always equal to it.

A common and highly illustrative class of [linear transformations](@entry_id:149133) arises from [matrix multiplication](@entry_id:156035). If $A$ is an $m \times n$ matrix, it defines a [linear transformation](@entry_id:143080) $T: \mathbb{R}^n \to \mathbb{R}^m$ by the rule $T(\mathbf{x}) = A\mathbf{x}$. Here, the input vectors $\mathbf{x}$ must be in $\mathbb{R}^n$ for the [matrix-vector product](@entry_id:151002) $A\mathbf{x}$ to be defined, and the resulting output vectors are in $\mathbb{R}^m$.

Consider a transformation $T$ from $\mathbb{R}^2$ to $\mathbb{R}^4$ defined by multiplication with a $4 \times 2$ matrix $A$ [@problem_id:1359043]. For such a transformation, the domain is explicitly $\mathbb{R}^2$, the space of inputs, and the [codomain](@entry_id:139336) is $\mathbb{R}^4$, the space where the outputs lie. The range is the set of all vectors $\mathbf{y} \in \mathbb{R}^4$ that can be written as $A\mathbf{x}$ for some $\mathbf{x} \in \mathbb{R}^2$. This set is precisely the collection of all possible [linear combinations](@entry_id:154743) of the columns of $A$, a concept we will explore next.

### The Range as a Fundamental Subspace

One of the most elegant and powerful properties of [linear transformations](@entry_id:149133) is that their ranges are not just arbitrary subsets of the codomain; they possess a rich structure of their own.

**Theorem:** For any linear transformation $T: V \to W$ between two [vector spaces](@entry_id:136837) $V$ and $W$, the range of $T$ is a **subspace** of the [codomain](@entry_id:139336) $W$.

*Proof:* To prove that $\text{range}(T)$ is a subspace of $W$, we must verify three conditions:

1.  **Contains the Zero Vector:** Since $T$ is a [linear transformation](@entry_id:143080), it must map the zero vector of the domain to the [zero vector](@entry_id:156189) of the [codomain](@entry_id:139336): $T(\mathbf{0}_V) = \mathbf{0}_W$. Therefore, $\mathbf{0}_W$ is in the range of $T$.

2.  **Closure under Addition:** Let $\mathbf{w}_1$ and $\mathbf{w}_2$ be any two vectors in $\text{range}(T)$. By the definition of the range, there exist vectors $\mathbf{v}_1, \mathbf{v}_2 \in V$ such that $T(\mathbf{v}_1) = \mathbf{w}_1$ and $T(\mathbf{v}_2) = \mathbf{w}_2$. We must show that their sum, $\mathbf{w}_1 + \mathbf{w}_2$, is also in the range. Using the linearity of $T$:
    $$
    \mathbf{w}_1 + \mathbf{w}_2 = T(\mathbf{v}_1) + T(\mathbf{v}_2) = T(\mathbf{v}_1 + \mathbf{v}_2)
    $$
    Since $\mathbf{v}_1 + \mathbf{v}_2$ is a vector in the domain $V$, its image $T(\mathbf{v}_1 + \mathbf{v}_2)$ is, by definition, in the range of $T$. Thus, the range is closed under addition.

3.  **Closure under Scalar Multiplication:** Let $\mathbf{w}$ be any vector in $\text{range}(T)$ and let $c$ be any scalar. There exists a vector $\mathbf{v} \in V$ such that $T(\mathbf{v}) = \mathbf{w}$. We must show that $c\mathbf{w}$ is also in the range. Again, using linearity:
    $$
    c\mathbf{w} = cT(\mathbf{v}) = T(c\mathbf{v})
    $$
    Since $c\mathbf{v}$ is a vector in $V$, its image $T(c\mathbf{v})$ is in the range of $T$. Thus, the range is closed under scalar multiplication.

Because the range contains the [zero vector](@entry_id:156189) and is closed under both addition and [scalar multiplication](@entry_id:155971), it is a subspace of the codomain $W$ [@problem_id:1359030].

This subspace property is a strict requirement for the range of any [linear transformation](@entry_id:143080). For instance, consider several subsets of $\mathbb{R}^3$. A set like $S_1 = \{(x, y, z) \in \mathbb{R}^3 \mid 2x - y + z = 5\}$ cannot be the range of a [linear transformation](@entry_id:143080) because it is an affine plane that does not contain the origin $(0, 0, 0)$ [@problem_id:1877815]. Similarly, a set defined by a non-linear constraint, such as $S_2 = \{(x, y, z) \in \mathbb{R}^3 \mid z = |x+y|\}$, is not a subspace because it fails [closure under scalar multiplication](@entry_id:153275) (e.g., $(1, 0, 1)$ is in $S_2$, but $-1 \cdot (1, 0, 1) = (-1, 0, -1)$ is not). In contrast, a set like $S_3 = \{(x, y, z) \in \mathbb{R}^3 \mid x = 3y \text{ and } z = -2y\}$, which describes a line through the origin, is a valid subspace and is a plausible candidate for the range of a linear transformation.

The requirement of linearity is critical. For a non-linear transformation, the range may not be a subspace. Consider the transformation $T: V \to W$ from the space of $3 \times 3$ [skew-symmetric matrices](@entry_id:195119) to the space of $3 \times 3$ [symmetric matrices](@entry_id:156259), defined by $T(A) = A^2$ [@problem_id:1359071]. The set of all output matrices $\{A^2\}$ is not a subspace. However, the set of all finite linear combinations of these output matrices, known as the **span of the range**, does form a subspace.

### Characterizing and Computing the Range

Identifying the range is a central task in linear algebra. The method depends on how the transformation is defined.

#### For Matrix Transformations: The Column Space

For a [linear transformation](@entry_id:143080) $T(\mathbf{x}) = A\mathbf{x}$ where $A$ is an $m \times n$ matrix with columns $\mathbf{c}_1, \mathbf{c}_2, \dots, \mathbf{c}_n$, any output vector can be written as:
$$
T(\mathbf{x}) = A\mathbf{x} = x_1\mathbf{c}_1 + x_2\mathbf{c}_2 + \dots + x_n\mathbf{c}_n
$$
This equation reveals that the range of $T$ is precisely the set of all linear combinations of the columns of $A$. This subspace is so fundamental that it has its own name: the **column space** of $A$, denoted $\text{Col}(A)$.
$$
\text{range}(T) = \text{Col}(A) = \text{span}\{\mathbf{c}_1, \mathbf{c}_2, \dots, \mathbf{c}_n\}
$$
The **dimension of the range** is the dimension of the column space, which is equal to the number of linearly independent columns of $A$. This number is the **rank** of the matrix $A$. For the transformation $T: \mathbb{R}^2 \to \mathbb{R}^4$ with the $4 \times 2$ matrix from before, one can verify that its two columns are linearly independent, so the dimension of its range is 2 [@problem_id:1359043].

This connection between the range and the [column space](@entry_id:150809) provides a powerful link to [solving systems of linear equations](@entry_id:136676). A system $A\mathbf{x} = \mathbf{b}$ has a solution if and only if the vector $\mathbf{b}$ can be expressed as a linear combination of the columns of $A$. In other words:

A [system of linear equations](@entry_id:140416) $A\mathbf{x} = \mathbf{b}$ is consistent if and only if $\mathbf{b}$ is in the range of the transformation $T(\mathbf{x}) = A\mathbf{x}$.

To determine if $\mathbf{b}$ is in the range, we can try to solve the system. If a solution exists, $\mathbf{b}$ is in the range. Often, this process reveals one or more [linear constraints](@entry_id:636966) on the components of $\mathbf{b}$ that must be satisfied. These constraints are the implicit equations that define the range as a subspace. For example, for a transformation $T: \mathbb{R}^3 \to \mathbb{R}^4$ defined by a specific $4 \times 3$ matrix $A$, solving the system $A\mathbf{x} = \mathbf{b}$ for an arbitrary $\mathbf{b} = [b_1, b_2, b_3, b_4]^T$ might lead to a condition like $b_1 - b_2 - b_3 + b_4 = 0$. This single equation defines the 3-dimensional subspace of $\mathbb{R}^4$ that constitutes the range of $T$ [@problem_id:1359029].

#### For Abstract Vector Spaces

When dealing with transformations between more abstract spaces like polynomials or matrices, the same principle applies. A general method to find the range is to apply the transformation to a basis for the domain. The span of the resulting set of vectors in the codomain will be the range of the transformation.

Let's consider a linear transformation $T: P_2 \to M_{2 \times 2}$ from the space of polynomials of degree at most 2 to the space of $2 \times 2$ matrices, defined by $T(p(t)) = \begin{pmatrix} p(1) - p(-1)  p'(0) \\ p''(0)  p(0) \end{pmatrix}$ [@problem_id:1359060]. To characterize the range, we can take a general polynomial $p(t) = \alpha t^2 + \beta t + \gamma$ from the domain $P_2$. We then compute the components required for the transformation:
*   $p(1) - p(-1) = (\alpha + \beta + \gamma) - (\alpha - \beta + \gamma) = 2\beta$
*   $p'(t) = 2\alpha t + \beta \implies p'(0) = \beta$
*   $p''(t) = 2\alpha \implies p''(0) = 2\alpha$
*   $p(0) = \gamma$

Substituting these into the definition of $T$ gives the form of any matrix in the range:
$$
T(p(t)) = \begin{pmatrix} 2\beta  \beta \\ 2\alpha  \gamma \end{pmatrix}
$$
By inspecting this output matrix, we see that for any choice of $\alpha, \beta, \gamma$, the top-left entry is always twice the top-right entry. Any such matrix can be produced by choosing appropriate polynomial coefficients. Therefore, the range of $T$ is the subspace of $M_{2 \times 2}$ consisting of all matrices $\begin{pmatrix} a  b \\ c  d \end{pmatrix}$ that satisfy the condition $a = 2b$. This is a 3-dimensional subspace of the 4-dimensional space $M_{2 \times 2}$.

### Dimensionality, Surjectivity, and the Rank-Nullity Theorem

The dimension of the range, known as the **rank** of the transformation, is a measure of the "size" of the output set. A transformation $T: V \to W$ is called **surjective** (or **onto**) if its range fills the entire codomain, i.e., $\text{range}(T) = W$. This means that for every vector $\mathbf{w} \in W$, there is at least one vector $\mathbf{v} \in V$ such that $T(\mathbf{v}) = \mathbf{w}$.

The concept of [surjectivity](@entry_id:148931) is equivalent to several other conditions, which is a hallmark of a deep mathematical idea. In the context of a [matrix transformation](@entry_id:151622) $T: \mathbb{R}^n \to \mathbb{R}^m$ given by $T(\mathbf{u}) = A\mathbf{u}$, the following statements are equivalent to $T$ being surjective [@problem_id:1359075]:

*   The range of $T$ is $\mathbb{R}^m$.
*   The columns of the matrix $A$ span $\mathbb{R}^m$.
*   The rank of $A$ is equal to $m$, the dimension of the [codomain](@entry_id:139336).
*   The reduced [row-echelon form](@entry_id:199986) of $A$ has a [pivot position](@entry_id:156455) in every row.
*   The system $A\mathbf{u} = \mathbf{b}$ has a solution for every $\mathbf{b} \in \mathbb{R}^m$.

A fundamental relationship connects the dimension of the domain, the dimension of the range (rank), and the dimension of the kernel ([nullity](@entry_id:156285)). This is the **Rank-Nullity Theorem**:

For a [linear transformation](@entry_id:143080) $T: V \to W$ on a finite-dimensional domain $V$,
$$
\dim(V) = \dim(\ker T) + \dim(\text{range } T)
$$

This theorem places strong constraints on what a [linear transformation](@entry_id:143080) can do. Since the range is a subspace of the codomain, its dimension cannot exceed the dimension of the [codomain](@entry_id:139336): $\dim(\text{range } T) \le \dim(W)$. Combining this with the [rank-nullity theorem](@entry_id:154441) yields a profound consequence: a [linear transformation](@entry_id:143080) from a larger space to a smaller space cannot be injective.

Consider a transformation $T: P_4(\mathbb{R}) \to P_2(\mathbb{R})$ [@problem_id:1359067]. Here, the dimension of the domain is $\dim(P_4) = 5$ and the dimension of the [codomain](@entry_id:139336) is $\dim(P_2) = 3$. The dimension of the range is at most 3. From the [rank-nullity theorem](@entry_id:154441):
$$
\dim(\ker T) = \dim(P_4) - \dim(\text{range } T) = 5 - \dim(\text{range } T)
$$
Since $\dim(\text{range } T) \le 3$, we must have $\dim(\ker T) \ge 5 - 3 = 2$. A kernel of dimension 2 or greater is non-trivial, meaning it contains non-zero vectors. Therefore, the transformation $T$ cannot be injective (one-to-one), as multiple input vectors map to the same output vector.

### Advanced Topics: Range of Composite and Adjoint Transformations

The concept of the range also behaves predictably under more complex operations.

#### Composition of Transformations

Let $T: V \to W$ and $S: W \to Z$ be two linear transformations. The range of their composition, $S \circ T: V \to Z$, is intimately related to the ranges of $S$ and $T$.

First, it is always true that the range of the composite map is a subspace of the range of the outer map: $\text{range}(S \circ T) \subseteq \text{range}(S)$ [@problem_id:1359051]. This is because any output of $S \circ T$ is of the form $S(T(\mathbf{v}))$. Since $T(\mathbf{v})$ is some vector in $W$, the output $S(T(\mathbf{v}))$ must lie in the range of $S$.

Equality, $\text{range}(S \circ T) = \text{range}(S)$, occurs if the inner transformation $T$ is surjective. If $\text{range}(T) = W$, then the inputs to $S$ (which come from the range of $T$) cover all of $W$, so the output of the composition will cover all of the range of $S$.

The dimensions of the ranges are related by the elegant formula:
$$
\dim(\text{range}(S \circ T)) = \dim(\text{range}(T)) - \dim(\ker(S) \cap \text{range}(T))
$$
This equation tells us that the dimension of the range of $T$ is "shrunk" by the composition with $S$. The amount of shrinkage is precisely the dimension of the part of $T$'s range that lies in the kernel of $S$—that is, the part of $T$'s output that $S$ maps to zero [@problem_id:1359051]. If $S$ is injective, then its kernel is trivial, the intersection is trivial, and $\dim(\text{range}(S \circ T)) = \dim(\text{range}(T))$.

#### Adjoint Transformations and Orthogonality

In the context of [inner product spaces](@entry_id:271570), there is a deep and surprising connection between the [range of a transformation](@entry_id:155277) $T$ and the kernel of its **adjoint**, $T^*$. The [adjoint operator](@entry_id:147736) $T^*: W \to V$ is uniquely defined by the relation $\langle T(\mathbf{v}), \mathbf{w} \rangle_W = \langle \mathbf{v}, T^*(\mathbf{w}) \rangle_V$ for all $\mathbf{v} \in V, \mathbf{w} \in W$.

One of the cornerstones of linear algebra, often called the **Fundamental Theorem of Linear Algebra**, states that the range of $T$ is the [orthogonal complement](@entry_id:151540) of the kernel of its adjoint:
$$
\text{range}(T) = (\ker(T^*))^\perp
$$
This means that the set of all outputs of $T$ is precisely the set of all vectors in $W$ that are orthogonal to every vector that $T^*$ sends to zero. This theorem provides a powerful way to characterize the range without having to compute it directly. For example, for a linear operator $T: P_1(\mathbb{R}) \to P_1(\mathbb{R})$ defined by $T(a+bx) = a$, we can see that its range is the set of all constant polynomials, $\text{span}\{1\}$. By the theorem, we can immediately deduce that the [orthogonal complement](@entry_id:151540) of the kernel of its adjoint, $(\ker(T^*))^\perp$, is also equal to $\text{span}\{1\}$ [@problem_id:1359038]. This reveals a fundamental [geometric duality](@entry_id:204458) between these [four fundamental subspaces](@entry_id:154834): the range and kernel of $T$ and its adjoint $T^*$.