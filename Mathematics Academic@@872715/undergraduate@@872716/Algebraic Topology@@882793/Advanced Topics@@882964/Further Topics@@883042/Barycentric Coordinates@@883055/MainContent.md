## Introduction
In geometry and its many applications, describing the position of a point is a fundamental task. While the familiar Cartesian system relies on a global origin and axes, it can be inefficient for problems concerning the intrinsic properties of shapes. Barycentric coordinates offer a powerful alternative, defining a point's location not by external axes, but as a weighted average of a set of reference vertices. This approach provides an elegant, intrinsic coordinate system that simplifies many problems in geometry and computation. This article bridges the gap between the abstract definition of barycentric coordinates and their concrete utility. In the following chapters, you will first delve into the core "Principles and Mechanisms," exploring their algebraic foundation, geometric interpretations as area ratios, and key properties like [affine invariance](@entry_id:275782). Next, "Applications and Interdisciplinary Connections" will reveal how these principles are applied across diverse fields, from creating realistic computer graphics and modeling complex physical systems with the Finite Element Method to representing compositions in chemistry. Finally, the "Hands-On Practices" section will allow you to solidify your understanding by solving practical problems. This journey will equip you with a deep appreciation for barycentric coordinates as a versatile tool in both theoretical and [applied mathematics](@entry_id:170283).

## Principles and Mechanisms

Barycentric coordinates offer a powerful and elegant system for describing the position of points relative to a set of reference vertices. This system moves beyond a dependence on a global Cartesian framework, instead defining location through a set of weights that are intrinsic to the geometry of the vertices themselves. In this chapter, we will explore the fundamental principles of barycentric coordinates, from their algebraic definition to their profound geometric and physical interpretations, and establish their key properties.

### The Algebraic Foundation: Affine Combinations and Independence

The concept of barycentric coordinates is rooted in the idea of an **[affine combination](@entry_id:276726)**. Given a set of points $\{v_0, v_1, \ldots, v_n\}$ in a Euclidean space $\mathbb{R}^d$, a linear combination $P = \sum_{i=0}^{n} \lambda_i v_i$ is called an [affine combination](@entry_id:276726) if the coefficients sum to one, i.e., $\sum_{i=0}^{n} \lambda_i = 1$. The set of all possible affine combinations of these points forms their **[affine hull](@entry_id:637696)**, which is the smallest affine subspace (such as a point, line, or plane) containing all the vertices.

For barycentric coordinates to be a well-defined and unique system, the reference vertices must be **affinely independent**. This means that no vertex $v_k$ can be expressed as an [affine combination](@entry_id:276726) of the other vertices. Geometrically, for points in $\mathbb{R}^2$, this means three points cannot be collinear; for points in $\mathbb{R}^3$, it means four points cannot be coplanar, and so on.

The necessity of this condition becomes clear when we consider a set of affinely dependent vertices, such as three collinear points $v_0, v_1, v_2$. Any point $p$ on the line passing through them can be expressed as an [affine combination](@entry_id:276726), but this representation is not unique. For instance, if one is asked to find the coordinates $(t_0, t_1, t_2)$ for a point $p$ on the line defined by $v_0, v_1, v_2$, the system of equations derived from $p = t_0v_0 + t_1v_1 + t_2v_2$ and $t_0 + t_1 + t_2 = 1$ will be underdetermined, yielding infinite solutions. Only by imposing an additional, arbitrary constraint (e.g., fixing one of the coordinate values) can a unique solution be found for that specific case [@problem_id:1633404].

When the $n+1$ vertices $\{v_0, v_1, \ldots, v_n\}$ are affinely independent, they form the vertices of an **[n-simplex](@entry_id:264768)**. A 2-simplex is a triangle, and a 3-simplex is a tetrahedron. For any point $P$ within the [affine hull](@entry_id:637696) of these vertices, there exists a unique set of scalars $(\lambda_0, \lambda_1, \ldots, \lambda_n)$ such that:
$$
P = \sum_{i=0}^{n} \lambda_i v_i \quad \text{and} \quad \sum_{i=0}^{n} \lambda_i = 1
$$
These unique scalars $\lambda_i$ are the **barycentric coordinates** of $P$ with respect to the ordered vertices $(v_0, v_1, \ldots, v_n)$.

To calculate these coordinates, we can directly solve the system of linear equations formed by the definitional relationship. For a point $P=(p_x, p_y)$ in $\mathbb{R}^2$ and a triangle with vertices $v_0=(x_0, y_0)$, $v_1=(x_1, y_1)$, and $v_2=(x_2, y_2)$, the vector equation $P = \lambda_0 v_0 + \lambda_1 v_1 + \lambda_2 v_2$ and the summation constraint lead to a system of three [linear equations](@entry_id:151487) for the three unknown coordinates $(\lambda_0, \lambda_1, \lambda_2)$ [@problem_id:1633365].
$$
\begin{cases}
\lambda_0 x_0 + \lambda_1 x_1 + \lambda_2 x_2  = p_x \\
\lambda_0 y_0 + \lambda_1 y_1 + \lambda_2 y_2  = p_y \\
\lambda_0 + \lambda_1 + \lambda_2  = 1
\end{cases}
$$
This system can be written in matrix form, which provides a direct computational pathway:
$$
\begin{pmatrix}
x_0 & x_1 & x_2 \\
y_0 & y_1 & y_2 \\
1 & 1 & 1
\end{pmatrix}
\begin{pmatrix}
\lambda_0 \\
\lambda_1 \\
\lambda_2
\end{pmatrix}
=
\begin{pmatrix}
p_x \\
p_y \\
1
\end{pmatrix}
$$
The [affine independence](@entry_id:262726) of the vertices ensures that the matrix on the left is invertible, guaranteeing a unique solution for $(\lambda_0, \lambda_1, \lambda_2)$. For instance, for a point $P=(3,3)$ and vertices $v_0=(1,1)$, $v_1=(4,2)$, and $v_2=(2,5)$, solving this system yields the barycentric coordinates $(\frac{1}{11}, \frac{6}{11}, \frac{4}{11})$ [@problem_id:1633365].

### Geometric Interpretation: Location, Faces, and Area Ratios

Barycentric coordinates provide a powerful geometric map. The simplex itself, defined as the **[convex hull](@entry_id:262864)** of its vertices, corresponds to the set of points for which all barycentric coordinates are non-negative, i.e., $\lambda_i \ge 0$ for all $i$.

The boundaries of the [simplex](@entry_id:270623) are neatly described using these coordinates. A **face** of the simplex is formed by the subset of points where one or more barycentric coordinates are equal to zero. Specifically, the face opposite to vertex $v_k$ is the set of all points within the [simplex](@entry_id:270623) for which $\lambda_k = 0$. These points are convex combinations of the remaining $n$ vertices and thus form an $(n-1)$-simplex. For a tetrahedron (a 3-[simplex](@entry_id:270623)) with vertices $\{v_0, v_1, v_2, v_3\}$, the subset of points where $\lambda_3 = 0$ constitutes the triangular face spanned by $\{v_0, v_1, v_2\}$ [@problem_id:1633387].

The signs of the coordinates reveal the location of a point $P$ relative to the simplex. The [affine hull](@entry_id:637696) of the simplex's vertices is partitioned into distinct regions, each characterized by a unique sign pattern for $(\lambda_0, \ldots, \lambda_n)$.
*   If all $\lambda_i \ge 0$, $P$ is inside or on the boundary of the [simplex](@entry_id:270623).
*   If one coordinate, say $\lambda_k$, is negative, $P$ lies outside the [simplex](@entry_id:270623) on the other side of the face opposite to $v_k$.
*   If a point lies on the line passing through vertices $v_i$ and $v_j$, all other coordinates $\lambda_k$ (for $k \neq i,j$) must be zero. The specific values of $\lambda_i$ and $\lambda_j$ determine its position along this line. For example, a point $P$ with barycentric coordinates $(2, -1, 0)$ with respect to vertices $(A, B, C)$ must lie on the line through $A$ and $B$ because $\lambda_C=0$. The relationship $\vec{P} = 2\vec{A} - \vec{B}$ reveals that $A$ is the midpoint of the segment connecting $B$ and $P$ [@problem_id:2109635].
*   A point located in the region "behind" a vertex $v_k$ (opposite the rest of the triangle) will have $\lambda_k > 1$ and all other $\lambda_i  0$ (for $i \neq k$). For a triangle with vertices $v_0, v_1, v_2$, a point in the region vertically opposite the interior at vertex $v_0$ will exhibit coordinates where $\lambda_0 > 1$, while $\lambda_1  0$ and $\lambda_2  0$ [@problem_id:1633364].

For a 2-[simplex](@entry_id:270623) (triangle), there is a particularly elegant geometric interpretation of the coordinates as **ratios of areas**. The barycentric coordinates $(\lambda_0, \lambda_1, \lambda_2)$ of a point $P$ inside a triangle with vertices $(v_0, v_1, v_2)$ are given by:
$$
\lambda_0 = \frac{\text{Area}(\triangle(P, v_1, v_2))}{\text{Area}(\triangle(v_0, v_1, v_2))}, \quad
\lambda_1 = \frac{\text{Area}(\triangle(P, v_0, v_2))}{\text{Area}(\triangle(v_0, v_1, v_2))}, \quad
\lambda_2 = \frac{\text{Area}(\triangle(P, v_0, v_1))}{\text{Area}(\triangle(v_0, v_1, v_2))}
$$
Here, the sub-triangle for $\lambda_i$ is formed by the point $P$ and the two vertices other than $v_i$. This relationship provides a visual and computational tool. As $P$ approaches a vertex, say $v_0$, the area of the sub-triangle $\triangle(P, v_1, v_2)$ approaches the total area of $\triangle(v_0, v_1, v_2)$, causing $\lambda_0$ to approach 1, while the other two areas (and thus coordinates) approach 0. This method, often implemented using the determinant-based [shoelace formula](@entry_id:175960) for calculating signed areas, is a mainstay in computational geometry and computer graphics [@problem_id:1633416].

### Physical Intuition and Invariance Properties

The term "barycentric" originates from the Greek *barys*, meaning "heavy," and hints at a deep connection to the physical concept of a center of mass, or **[barycenter](@entry_id:170655)**. If we imagine placing masses $m_0, m_1, \ldots, m_n$ at the vertices $v_0, v_1, \ldots, v_n$, the center of mass of this system is given by:
$$
P_{cm} = \frac{\sum_{i=0}^{n} m_i v_i}{\sum_{i=0}^{n} m_i} = \sum_{i=0}^{n} \left(\frac{m_i}{\sum_{j=0}^{n} m_j}\right) v_i
$$
By comparing this to the definition of barycentric coordinates, we see that the normalized barycentric coordinates of the center of mass are precisely the ratios of the individual masses to the total mass: $\lambda_i = m_i / (\sum m_j)$ [@problem_id:1633410]. The unnormalized, or **homogeneous barycentric coordinates**, can be seen simply as the masses $(m_0, m_1, \ldots, m_n)$ themselves. Any such triplet of coordinates $(c_0, c_1, \ldots, c_n)$ that are not all zero can be converted to normalized coordinates $(\lambda_i)$ by dividing by their sum: $\lambda_i = c_i / \sum c_j$. The resulting point is the same [@problem_id:2109642]. A direct consequence is that the **geometric [centroid](@entry_id:265015)** of a [simplex](@entry_id:270623), the average of its vertex positions, corresponds to placing equal masses at each vertex. Its barycentric coordinates are therefore $(\frac{1}{n+1}, \frac{1}{n+1}, \ldots, \frac{1}{n+1})$.

Perhaps the most significant property of barycentric coordinates, especially for applications in computer graphics and geometric modeling, is their **invariance under affine transformations**. An affine transformation $T(\vec{x}) = A\vec{x} + \vec{b}$ is a [linear transformation](@entry_id:143080) followed by a translation. It preserves collinearity and ratios of distances along a line.

If a point $P$ is an [affine combination](@entry_id:276726) of vertices $\{v_i\}$ with coefficients $\{\lambda_i\}$, then the transformed point $P' = T(P)$ is the *same* [affine combination](@entry_id:276726) of the transformed vertices $\{v'_i = T(v_i)\}$. The proof is straightforward, leveraging the properties of affine maps and the fact that the coordinates sum to one:
$$
\begin{align*}
P' = T(P) = T\left(\sum_{i=0}^{n} \lambda_i v_i\right) \\
= A\left(\sum_{i=0}^{n} \lambda_i v_i\right) + \vec{b} \\
= \sum_{i=0}^{n} \lambda_i (A v_i) + \left(\sum_{i=0}^{n} \lambda_i\right) \vec{b} \quad (\text{since } \sum \lambda_i = 1) \\
= \sum_{i=0}^{n} \lambda_i (A v_i + \vec{b}) \\
= \sum_{i=0}^{n} \lambda_i T(v_i) = \sum_{i=0}^{n} \lambda_i v'_i
\end{align*}
$$
This means that the barycentric coordinates of a point with respect to a set of vertices do not change when the entire system is rotated, scaled, sheared, or translated. This property is invaluable; for example, if one defines color at a point inside a triangle by interpolating the vertex colors using barycentric coordinates, this color will remain correctly mapped even if the triangle is moved or deformed by an affine transformation [@problem_id:1633386] [@problem_id:2109680]. This invariance establishes barycentric coordinates as a fundamental, intrinsic coordinate system that captures the geometry of a configuration independent of its embedding in a larger space.