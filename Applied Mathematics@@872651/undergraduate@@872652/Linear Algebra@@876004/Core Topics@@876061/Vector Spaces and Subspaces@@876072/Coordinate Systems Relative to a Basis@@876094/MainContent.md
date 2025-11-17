## Introduction
In linear algebra, vectors are often treated as abstract objects. To perform concrete computations, we need a way to represent them with numbers. Coordinate systems provide this crucial link, translating abstract vectors into ordered lists of scalars relative to a chosen frame of reference, known as a basis. This framework is essential for bridging the gap between geometric intuition and numerical calculation.

While we know a basis spans a vector space, how do we systematically assign a unique numerical "address" to every vector? And how do we translate these addresses between different [frames of reference](@entry_id:169232)? This article addresses these questions by formalizing the concept of a [coordinate vector](@entry_id:153319) and the process of changing bases.

You will begin by exploring the fundamental **Principles and Mechanisms** of [coordinate mapping](@entry_id:156506), understanding why a basis guarantees a unique coordinate representation for any vector. Next, in **Applications and Interdisciplinary Connections**, you will discover the power of this concept in diverse fields like physics, robotics, and signal processing, where changing perspective is key to solving complex problems. Finally, you will solidify your understanding through a series of **Hands-On Practices** designed to test your computational and conceptual skills.

## Principles and Mechanisms

In our exploration of [vector spaces](@entry_id:136837), we have established that a basis provides a minimal set of building blocks for constructing every vector in the space. Now, we delve deeper to formalize the relationship between a vector and its constituent basis elements. This leads to the concept of a **coordinate system**, a powerful framework for translating abstract vector relationships into the concrete language of numerical arrays and linear equations. A coordinate system allows us to label and manipulate vectors using an ordered set of scalars, bridging the gap between abstract vector algebra and numerical computation.

### The Coordinate Mapping: A New Perspective on Vectors

The fundamental purpose of a basis is to provide a unique reference frame for a vector space. Just as latitude and longitude provide unique coordinates for any point on the Earth's surface, a basis allows us to assign a unique set of coordinates to any vector within a vector space.

#### The Definition of Coordinates

Let $V$ be a vector space and let $B = \{b_1, b_2, \dots, b_n\}$ be an ordered basis for $V$. The **Coordinate Mapping Theorem** states that for any vector $v \in V$, there exists a unique set of scalars $c_1, c_2, \dots, c_n$ such that:

$$ v = c_1 b_1 + c_2 b_2 + \dots + c_n b_n $$

This unique set of scalars forms the **[coordinate vector](@entry_id:153319)** of $v$ relative to the basis $B$. We denote this [coordinate vector](@entry_id:153319) as $[v]_B$:

$$ [v]_B = \begin{pmatrix} c_1 \\ c_2 \\ \vdots \\ c_n \end{pmatrix} $$

It is crucial to distinguish between the vector $v$ itself, which is an abstract geometric or algebraic object, and its [coordinate vector](@entry_id:153319) $[v]_B$, which is an ordered list of numbers representing $v$ in a specific reference frame. The basis vectors are the "grid lines" of this frame, and the coordinates are the instructions for how far to travel along each grid line to reach the point corresponding to $v$.

#### The Uniqueness Theorem and Linear Independence

The "uniqueness" in the definition of coordinates is not a trivial matter; it is a direct consequence of the linear independence of the basis vectors. If a set of vectors $S = \{v_1, v_2, \dots, v_n\}$ is used to represent other vectors, but $S$ is not [linearly independent](@entry_id:148207), then representations are not unique.

Consider a scenario where a vector $w$ can be represented by two different coordinate vectors with respect to a set $S = \{v_1, v_2, v_3\}$. For instance, suppose we find that $w$ can be expressed as both:

$$ w = 5v_1 + 2v_2 - v_3 $$
$$ w = 3v_1 + 3v_2 + v_3 $$

Since both expressions equal $w$, we can set them equal to each other and rearrange the terms:

$$ (5v_1 + 2v_2 - v_3) - (3v_1 + 3v_2 + v_3) = \vec{0} $$
$$ (5-3)v_1 + (2-3)v_2 + (-1-1)v_3 = \vec{0} $$
$$ 2v_1 - v_2 - 2v_3 = \vec{0} $$

This is a non-trivial linear combination of the vectors in $S$ that equals the [zero vector](@entry_id:156189) (the coefficients are $2, -1, -2$, which are not all zero). By definition, this means the set $S$ is **linearly dependent**. Therefore, the uniqueness of a coordinate representation for every vector is inextricably linked to the linear independence of the basis set [@problem_id:1356113].

#### Existence and Span

The other cornerstone of a basis is that it must **span** the entire vector space. This property guarantees the *existence* of a [coordinate vector](@entry_id:153319) for any vector $v$ in the space. If a set of vectors $S$ does not span the space $V$, then there will be vectors in $V$ that cannot be expressed as a linear combination of the vectors in $S$.

Attempting to find the coordinates of such a vector will lead to an inconsistent [system of linear equations](@entry_id:140416). For example, if we are trying to find the coefficients $c_i$ for the equation $c_1 v_1 + \dots + c_k v_k = u$, we might set up an [augmented matrix](@entry_id:150523) $[v_1 \ v_2 \ \dots \ v_k \ | \ u]$. If, after [row reduction](@entry_id:153590), we obtain a row of the form $[0 \ 0 \ \dots \ 0 \ | \ b]$ where $b \neq 0$, this represents the impossible equation $0 = b$. This inconsistency is definitive proof that no solution for the coefficients exists, which means the vector $u$ is not in the subspace spanned by the set $S$ [@problem_id:1356067]. When $S$ is a basis for $V$, this situation can never occur for a vector $u \in V$.

#### The Linearity of the Coordinate Mapping

The mapping from a vector $v$ to its [coordinate vector](@entry_id:153319) $[v]_B$ is a [linear transformation](@entry_id:143080). This means it respects the operations of [vector addition and scalar multiplication](@entry_id:151375). For any vectors $u, v \in V$ and any scalar $k$:

1.  $[u+v]_B = [u]_B + [v]_B$
2.  $[kv]_B = k[v]_B$

This property is immensely useful. For example, if we know the [coordinate vector](@entry_id:153319) of $x$ is $[x]_B = \begin{pmatrix} 3 \\ -2 \\ 5 \end{pmatrix}$ relative to a basis $B=\{v_1, v_2, v_3\}$, this means $x = 3v_1 - 2v_2 + 5v_3$. Now, consider a new vector $y = x + v_2$. Instead of re-deriving the [linear combination](@entry_id:155091) for $y$ from scratch, we can use the linearity of the [coordinate mapping](@entry_id:156506).

We first note that the [coordinate vector](@entry_id:153319) of a basis vector itself is simple: $[v_2]_B = \begin{pmatrix} 0 \\ 1 \\ 0 \end{pmatrix}$, since $v_2 = 0v_1 + 1v_2 + 0v_3$. Using linearity:

$$ [y]_B = [x + v_2]_B = [x]_B + [v_2]_B = \begin{pmatrix} 3 \\ -2 \\ 5 \end{pmatrix} + \begin{pmatrix} 0 \\ 1 \\ 0 \end{pmatrix} = \begin{pmatrix} 3 \\ -1 \\ 5 \end{pmatrix} $$

This confirms that $y = 3v_1 - 1v_2 + 5v_3$. This simple algebraic manipulation of coordinate vectors mirrors the more complex addition of the abstract vectors themselves, which is the foundational power of using coordinate systems [@problem_id:1356080].

### Computational Frameworks for Coordinate Transformations

While the theoretical underpinnings are important, the practical utility of coordinate systems lies in our ability to compute coordinates and translate between different systems. Typically, we operate within a **standard basis**, such as $E = \{e_1, e_2, \dots, e_n\}$ in $\mathbb{R}^n$, where $e_i$ is the vector with a 1 in the $i$-th position and zeros elsewhere. A vector's representation in the standard basis is simply the vector itself, i.e., $v = [v]_E$. The core computational tasks involve converting between this standard representation and the representation in some other basis $B = \{b_1, b_2, \dots, b_n\}$.

#### The Change-of-Coordinates Matrix

The bridge between the standard basis and a custom basis $B$ is the **[change-of-coordinates matrix](@entry_id:151446)**, denoted $P_B$. This matrix is formed by simply using the basis vectors of $B$ (expressed in standard coordinates) as its columns:

$$ P_B = \begin{pmatrix} |  |   | \\ b_1  b_2  \dots  b_n \\ |  |   | \end{pmatrix} $$

This matrix allows us to translate from the "language" of basis $B$ to the standard basis.

#### From Basis Coordinates to Standard Coordinates

If we know a vector's representation in basis $B$, say $[v]_B = \begin{pmatrix} c_1 \\ \vdots \\ c_n \end{pmatrix}$, we can find its standard representation $v$ using the definition of coordinates and the [change-of-coordinates matrix](@entry_id:151446). The definition $v = c_1 b_1 + c_2 b_2 + \dots + c_n b_n$ is equivalent to the [matrix-vector product](@entry_id:151002):

$$ v = P_B [v]_B $$

This provides a direct computational recipe. For example, a drone's internal navigation might use a basis $B = \{b_1, b_2, b_3\}$. If its sensors locate an object at $[v]_B = \begin{pmatrix} 5 \\ 2 \\ -1 \end{pmatrix}$ relative to its own basis, and the basis vectors are known in the lab's standard coordinate system, we can find the object's lab coordinates $v$ by direct computation: $v = 5b_1 + 2b_2 - 1b_3$. This is a straightforward [linear combination](@entry_id:155091) performed column by column [@problem_id:1356083].

#### From Standard Coordinates to Basis Coordinates

The more common and slightly more involved task is to find a vector's coordinates in a new basis $B$, given its standard representation $v$. This requires us to find the unknown coefficients $c_i$ in the equation $v = c_1 b_1 + \dots + c_n b_n$. Using our [change-of-coordinates matrix](@entry_id:151446), this becomes the matrix equation:

$$ P_B [v]_B = v $$

Here, $P_B$ and $v$ are known, and the [coordinate vector](@entry_id:153319) $[v]_B$ is the unknown we must solve for. Since $B$ is a basis, its vectors are linearly independent, which means the matrix $P_B$ is invertible. Therefore, we can find the coordinates by solving this linear system, or equivalently, by using the inverse matrix:

$$ [v]_B = P_B^{-1} v $$

For instance, to command a plotter whose actuators move along directions $b_1 = \begin{pmatrix} 3 \\ 2 \end{pmatrix}$ and $b_2 = \begin{pmatrix} -1 \\ 4 \end{pmatrix}$, a desired displacement of $e_1 = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$ requires finding the coefficients $c_1$ and $c_2$ such that $c_1 b_1 + c_2 b_2 = e_1$. This is precisely the problem of finding $[e_1]_B$, which involves setting up and solving the system $\begin{pmatrix} 3  -1 \\ 2  4 \end{pmatrix} \begin{pmatrix} c_1 \\ c_2 \end{pmatrix} = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$ [@problem_id:1356109].

#### Coordinate Systems in Abstract Vector Spaces

The power of this framework extends beyond vectors in $\mathbb{R}^n$. The same principle applies to any [finite-dimensional vector space](@entry_id:187130), such as the space of polynomials $P_n$. To find the coordinates of a polynomial $q(t)$ with respect to a given [basis of polynomials](@entry_id:148579) $\mathcal{B} = \{p_1(t), p_2(t), \dots, p_n(t)\}$, we set up an equation for the unknown coefficients $c_i$:

$$ q(t) = c_1 p_1(t) + c_2 p_2(t) + \dots + c_n p_n(t) $$

By collecting terms of like powers of $t$ on both sides, we can equate their coefficients. This generates a system of linear equations for the $c_i$, which can be solved using [standard matrix](@entry_id:151240) methods. This process effectively translates a problem about abstract objects (polynomials) into a concrete numerical problem in $\mathbb{R}^n$ [@problem_id:1356070].

### The Geometric Significance of Orthonormal Bases

While any basis can define a coordinate system, some bases are far more convenient and geometrically intuitive than others. The most important of these are **[orthonormal bases](@entry_id:753010)**. An [orthonormal basis](@entry_id:147779) $B = \{u_1, u_2, \dots, u_n\}$ is one where all basis vectors are mutually orthogonal and have a length (norm) of 1. That is:

$$ u_i \cdot u_j = \begin{cases} 1  \text{if } i = j \\ 0  \text{if } i \neq j \end{cases} $$

#### Orthogonality and the Simplification of Coordinates

The primary advantage of an [orthonormal basis](@entry_id:147779) is that it dramatically simplifies the process of finding coordinates. Instead of solving a [system of linear equations](@entry_id:140416), we can find each coordinate independently using a simple dot product.

To find the coordinates $[v]_B = (c_1, \dots, c_n)^T$ of a vector $v$ in an [orthonormal basis](@entry_id:147779) $B$, we start with the defining equation:

$$ v = c_1 u_1 + c_2 u_2 + \dots + c_n u_n $$

Now, take the dot product of both sides with a [basis vector](@entry_id:199546), say $u_i$:

$$ v \cdot u_i = (c_1 u_1 + c_2 u_2 + \dots + c_n u_n) \cdot u_i $$

Using the linearity of the dot product and the [orthogonality property](@entry_id:268007) ($u_j \cdot u_i = 0$ for $j \neq i$):

$$ v \cdot u_i = c_1(u_1 \cdot u_i) + \dots + c_i(u_i \cdot u_i) + \dots + c_n(u_n \cdot u_i) = 0 + \dots + c_i(1) + \dots + 0 $$

This leaves us with a beautifully simple formula for each coordinate:

$$ c_i = v \cdot u_i $$

Each coordinate is simply the [scalar projection](@entry_id:148823) of the vector $v$ onto the corresponding basis vector. This is computationally efficient and provides clear geometric insight. A practical application is finding an object's position relative to a character in a video game. The character's "forward" and "rightward" directions can form a local [orthonormal basis](@entry_id:147779). To find an item's coordinates in this local frame, we simply take the dot product of the [relative position](@entry_id:274838) vector with the character's forward and rightward unit vectors [@problem_id:1356046].

#### Isometry: The Preservation of Geometric Structure

Orthonormal bases have a deeper geometric property: they preserve length and angles. A [coordinate transformation](@entry_id:138577) involving an orthonormal basis is an **[isometry](@entry_id:150881)**. This means the geometric properties of a vector in its original space are identical to the geometric properties of its [coordinate vector](@entry_id:153319). Specifically, for an orthonormal basis $B$, the [norm of a vector](@entry_id:154882) $v$ is equal to the norm of its [coordinate vector](@entry_id:153319) $[v]_B$:

$$ \|v\| = \|[v]_B\| $$

This can be proven by examining the squared norm of $v = \sum c_i u_i$:

$$ \|v\|^2 = v \cdot v = \left(\sum_{i=1}^{n} c_i u_i\right) \cdot \left(\sum_{j=1}^{n} c_j u_j\right) = \sum_{i,j} c_i c_j (u_i \cdot u_j) $$

Due to [orthonormality](@entry_id:267887), $u_i \cdot u_j$ is 1 if $i=j$ and 0 otherwise. The double summation collapses:

$$ \|v\|^2 = \sum_{i=1}^{n} c_i^2 (u_i \cdot u_i) = \sum_{i=1}^{n} c_i^2 $$

The right-hand side is precisely the definition of the squared Euclidean norm of the [coordinate vector](@entry_id:153319) $[v]_B = (c_1, \dots, c_n)^T$. Thus, $\|v\|^2 = \|[v]_B\|^2$. This remarkable property holds if and only if the basis is orthonormal, making such bases fundamental in fields where geometry must be preserved, such as physics and computer graphics [@problem_id:1356069].

### Geometric Interpretations in General Bases

What happens to geometry when our basis is not orthonormal? The simple correspondence between dot products and coordinates, and between [vector norms](@entry_id:140649) and coordinate norms, breaks down. This reveals the change-of-basis operation as a geometric transformation that can stretch, shear, and rotate space.

#### The Metric Tensor and Inner Products

In a general (non-orthogonal) basis $B = \{b_1, \dots, b_n\}$, the dot product of two vectors $v$ and $w$ can no longer be computed by simply taking the dot product of their coordinate vectors. Let $[v]_B = (\alpha_1, \dots, \alpha_n)^T$ and $[w]_B = (\beta_1, \dots, \beta_n)^T$. Then:

$$ v \cdot w = \left(\sum_{i=1}^{n} \alpha_i b_i\right) \cdot \left(\sum_{j=1}^{n} \beta_j b_j\right) = \sum_{i,j} \alpha_i \beta_j (b_i \cdot b_j) $$

The dot product now depends on a matrix of values $G_{ij} = b_i \cdot b_j$, which captures the geometric relationships between the basis vectors themselves. This matrix $G$, known as the **metric tensor**, dictates how to measure lengths and angles in the skewed coordinate system defined by $B$. For example, the dot product of a vector $v = \alpha b_1 + \beta b_2$ with the basis vector $b_1$ is not simply $\alpha$, but rather $v \cdot b_1 = \alpha (b_1 \cdot b_1) + \beta (b_2 \cdot b_1) = \alpha G_{11} + \beta G_{12}$ [@problem_id:1356079]. The simplicity of the orthonormal case is recovered when $G$ is the identity matrix.

#### Change of Basis as a Geometric Transformation

The equation $v = P_B [v]_B$ can be viewed as a linear transformation that maps a [coordinate vector](@entry_id:153319) $[v]_B$ from the "coordinate space" to the actual vector $v$ in the standard "world space." Let's consider the set of all vectors whose coordinates in basis $B$ lie on the unit circle, i.e., $c_1^2 + c_2^2 = 1$. What geometric shape do these vectors form in the standard Cartesian plane?

The set of coordinate vectors forms a unit circle in the $c_1$-$c_2$ plane. The transformation $P_B$ maps this circle into the $x$-$y$ plane. As [linear transformations](@entry_id:149133) map lines to lines and preserve [parallelism](@entry_id:753103), the image of the circle under $P_B$ is an **ellipse**. This illustrates how a [non-orthogonal basis](@entry_id:154908) distorts geometry: what is a simple circle in the coordinate representation becomes a stretched and rotated ellipse in the standard view [@problem_id:1356075].

Furthermore, the area of this ellipse is related to the area of the original unit circle (which is $\pi$) by a scaling factor. This factor is the absolute value of the determinant of the transformation matrix, $|\det(P_B)|$. For a basis $B = \left\{ \begin{pmatrix} 2 \\ 1 \end{pmatrix}, \begin{pmatrix} 1 \\ 2 \end{pmatrix} \right\}$, the [change-of-coordinates matrix](@entry_id:151446) is $P_B = \begin{pmatrix} 2  1 \\ 1  2 \end{pmatrix}$, with $\det(P_B) = 3$. Therefore, the unit circle in the $B$-coordinate space is mapped to an ellipse of area $3\pi$ in the standard space. The determinant of the [change-of-coordinates matrix](@entry_id:151446) measures the factor by which volume (or area in 2D) is scaled by the transformation from the coordinate grid to the standard grid.