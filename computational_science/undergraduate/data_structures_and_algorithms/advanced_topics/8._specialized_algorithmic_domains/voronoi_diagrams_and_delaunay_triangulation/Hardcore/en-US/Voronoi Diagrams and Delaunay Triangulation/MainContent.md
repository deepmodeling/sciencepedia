## Introduction
How do we systematically organize a collection of points in space to understand proximity and neighborhood relationships? In the field of computational geometry, two elegant and powerful structures provide the answer: the Voronoi diagram and the Delaunay triangulation. These constructs address the fundamental challenge of partitioning space and connecting points in a meaningful way, transforming raw coordinate data into insightful spatial information. This article provides a comprehensive exploration of these two concepts. We will begin in "Principles and Mechanisms" by dissecting their geometric definitions, from the [perpendicular bisectors](@entry_id:163148) that form Voronoi cells to the [empty circumcircle property](@entry_id:635047) that defines Delaunay triangles, ultimately revealing their profound dual relationship. Following this, "Applications and Interdisciplinary Connections" will showcase their real-world impact across diverse fields like machine learning, GIS, and [scientific simulation](@entry_id:637243). Finally, "Hands-On Practices" will offer opportunities to apply this knowledge to concrete problems. Our journey starts with the foundational geometric principles that give these structures their power and elegance.

## Principles and Mechanisms

This chapter delves into the foundational principles and geometric mechanisms that govern Voronoi diagrams and Delaunay triangulations. We will dissect these structures, starting from their most basic components and building towards their profound dual relationship. Our exploration will be grounded in geometric intuition and formalized with precise mathematical definitions, revealing the elegance and utility of these constructs in computational geometry.

### The Voronoi Diagram: A Partition of Proximity

At its core, a **Voronoi diagram** is a spatial partitioning based on the intuitive concept of proximity. Given a finite set of distinct points $P = \{p_1, p_2, \dots, p_n\}$ in a plane, which we call **sites**, the Voronoi diagram divides the plane into $n$ regions, or **cells**. Each cell, denoted $V(p_i)$, is associated with a single site $p_i$ and consists of every point in the plane that is closer to or equidistant to $p_i$ than to any other site $p_j$ in the set.

This concept finds direct application in numerous real-world scenarios, such as defining service areas for hospitals, districting for schools, or, as we will explore, allocating responsibility to community centers or infrastructure hubs.

#### The Building Blocks: Edges and Vertices

The boundaries of Voronoi cells are composed of two fundamental geometric elements: Voronoi edges and Voronoi vertices.

A **Voronoi edge** is the set of points in the plane that are equidistant to exactly two sites, say $p_i$ and $p_j$, and closer to this pair than to any other site. Geometrically, the locus of all points equidistant from two distinct points is the **[perpendicular bisector](@entry_id:176427)** of the line segment connecting them.

For instance, consider two community centers, $C_1 = (-4, 7)$ and $C_2 = (2, -3)$ . The boundary separating their service regions is the [perpendicular bisector](@entry_id:176427) of the segment $\overline{C_1C_2}$. The midpoint of this segment is $M = (\frac{-4+2}{2}, \frac{7-3}{2}) = (-1, 2)$. The slope of the segment is $m_{C} = \frac{-3-7}{2-(-4)} = -\frac{10}{6} = -\frac{5}{3}$. The slope of the [perpendicular bisector](@entry_id:176427) is the negative reciprocal, $m = -\frac{1}{-5/3} = \frac{3}{5}$. Using the [point-slope form](@entry_id:165105), the equation of this Voronoi edge is $y - 2 = \frac{3}{5}(x + 1)$, which simplifies to $y = \frac{3}{5}x + \frac{13}{5}$. This line represents the complete set of locations that have no preference between $C_1$ and $C_2$.

A **Voronoi vertex** is a point where three or more Voronoi edges meet. Consequently, a Voronoi vertex is a point that is equidistant from three or more sites. In the general case, where no four sites are concyclic, each vertex is equidistant from exactly three sites. Such a point is the **[circumcenter](@entry_id:174510)** of the triangle formed by those three sites.

As a practical illustration, imagine placing a public art installation equidistant from three landmarks $A=(-4, -2)$, $B=(6, 0)$, and $C=(2, 8)$ . The desired location $(x,y)$ must satisfy $|P-A| = |P-B| = |P-C|$, where $P=(x,y)$. This is equivalent to finding the intersection of two [perpendicular bisectors](@entry_id:163148). The bisector of $\overline{AB}$ is found by setting $(x+4)^2 + (y+2)^2 = (x-6)^2 + y^2$, which simplifies to the linear equation $5x+y=4$. The bisector of $\overline{AC}$ is found from $(x+4)^2 + (y+2)^2 = (x-2)^2 + (y-8)^2$, which simplifies to $3x+5y=12$. Solving this system of two linear equations yields the coordinates of the Voronoi vertex: $(\frac{4}{11}, \frac{24}{11})$. This is the unique point that serves as the [circumcenter](@entry_id:174510) of $\triangle ABC$.

#### Formal Definition and the Convexity Property

Formally, the Voronoi cell $V(p_i)$ for a site $p_i$ is defined by the intersection of half-planes. For every other site $p_j$ in the set, the [perpendicular bisector](@entry_id:176427) of $\overline{p_ip_j}$ divides the plane into two half-planes. The half-plane containing $p_i$ consists of all points closer to $p_i$ than to $p_j$. The cell $V(p_i)$ is the intersection of all such half-planes for $j \neq i$.
Mathematically, if $H(p_i, p_j)$ is the half-plane containing $p_i$ bounded by the [perpendicular bisector](@entry_id:176427) of $\overline{p_ip_j}$, then:
$$
V(p_i) = \bigcap_{j \neq i} H(p_i, p_j)
$$
Each half-plane is described by a [linear inequality](@entry_id:174297). For two sites $A=(x_1, y_1)$ and $B=(x_2, y_2)$, the condition that a point $P=(x,y)$ is closer to $A$ than $B$ is $|P-A|^2 \le |P-B|^2$. Expanding this yields a [linear inequality](@entry_id:174297):
$$
(x-x_1)^2 + (y-y_1)^2 \le (x-x_2)^2 + (y-y_2)^2
$$
$$
-2x x_1 + x_1^2 - 2y y_1 + y_1^2 \le -2x x_2 + x_2^2 - 2y y_2 + y_2^2
$$
$$
2(x_2 - x_1)x + 2(y_2 - y_1)y \le x_2^2 + y_2^2 - x_1^2 - y_1^2
$$
As an example, to begin constructing the Voronoi cell for a site $A=(1,1)$ relative to sites $B=(5,3)$ and $C=(3,7)$ , we would derive two such inequalities. The boundary with $B$ yields $2x+y \le 8$, and the boundary with $C$ yields $x+3y \le 14$. The final cell for $A$ would be the intersection of these two half-planes along with others for any additional sites.

An essential property that follows directly from this definition is that **every Voronoi cell is a [convex set](@entry_id:268368)**. A set is convex if for any two points within the set, the line segment connecting them is also entirely contained within the set. Since each half-plane is a convex set, and the intersection of any number of [convex sets](@entry_id:155617) is also a convex set, it follows that every Voronoi cell must be convex. In a 2D plane, this means each cell is a [convex polygon](@entry_id:165008), which may be bounded or unbounded.

This property has direct practical consequences. Consider an autonomous vehicle traveling between two points $A$ and $B$ that are both located within the Voronoi cell of a depot $S_1$ . Due to the convexity of $V(S_1)$, the entire straight-line path $\overline{AB}$ is also within $V(S_1)$. This means that for any point on its journey, including the midpoint $M$, the closest depot remains $S_1$.

#### Unbounded Cells and the Convex Hull

Voronoi cells are not always bounded polygons. A cell $V(p_i)$ is unbounded if and only if the site $p_i$ is a vertex of the **[convex hull](@entry_id:262864)** of the point set $P$. The convex hull is the smallest [convex polygon](@entry_id:165008) that encloses all the sites. Intuitively, if a site is on the "outer edge" of the point configuration, one can move infinitely far away from the entire set of points in a certain direction while still remaining closest to that specific site. The boundary of an unbounded cell consists of two infinite rays connected to a sequence of finite edges.

For example, consider stations at $S_1=(1,1)$, $S_2=(4,5)$, $S_3=(7,2)$, and $S_4=(3,3)$ . The [convex hull](@entry_id:262864) is the triangle formed by $S_1$, $S_2$, and $S_3$. Therefore, the Voronoi cells for these three sites will be unbounded, while the cell for the interior site $S_4$ will be a bounded polygon. The unbounded Voronoi edge separating the cells of two adjacent convex hull vertices, say $S_1$ and $S_2$, is a ray lying on their [perpendicular bisector](@entry_id:176427), extending outwards from the Voronoi diagram.

### The Delaunay Triangulation: A Triangulation of Neighbors

Given the same set of sites $P$, a **triangulation** connects them to form a set of non-overlapping triangles that completely cover the [convex hull](@entry_id:262864) of $P$. While many such triangulations are possible, the **Delaunay triangulation**, denoted $DT(P)$, is a specific construction with remarkable properties.

#### The Empty Circumcircle Property

The defining characteristic of a Delaunay triangulation is the **[empty circumcircle property](@entry_id:635047)**. This states that for any triangle $\triangle p_i p_j p_k$ in $DT(P)$, its unique [circumcircle](@entry_id:165300) (the circle passing through its three vertices $p_i, p_j, p_k$) must contain no other site from the set $P$ in its interior.

This single, elegant condition has profound implications. One of the most celebrated is that the Delaunay [triangulation](@entry_id:272253) tends to avoid "skinny" triangles—those with very small interior angles . In fact, among all possible triangulations of a point set, the Delaunay triangulation maximizes the minimum angle. This "angle optimality" makes Delaunay triangulations exceptionally valuable in applications like [finite element analysis](@entry_id:138109) and [mesh generation](@entry_id:149105), where poorly-shaped triangles can lead to [numerical instability](@entry_id:137058). The [empty circumcircle property](@entry_id:635047) is the fundamental geometric principle from which this angle-maximizing behavior arises.

#### The In-Circle Test

To computationally construct a Delaunay triangulation, one needs a robust method to check the [empty circumcircle property](@entry_id:635047). This is commonly done with the **in-circle test**, which can be formulated as the sign of a determinant. For a triangle with vertices $A=(A_x, A_y)$, $B=(B_x, B_y)$, and $C=(C_x, C_y)$, we can test if a fourth point $P=(P_x, P_y)$ lies inside its [circumcircle](@entry_id:165300) by evaluating the following determinant :
$$
\Delta = \det\begin{pmatrix}
A_x  & A_y  & A_x^2 + A_y^2  & 1 \\
B_x  & B_y  & B_x^2 + B_y^2  & 1 \\
C_x  & C_y  & C_x^2 + C_y^2  & 1 \\
P_x  & P_y  & P_x^2 + P_y^2  & 1
\end{pmatrix}
$$
The sign of $\Delta$ reveals the position of $P$ relative to the [circumcircle](@entry_id:165300) of $\triangle ABC$. Assuming the vertices $A, B, C$ are ordered counter-clockwise:
*   If $\Delta > 0$, $P$ is inside the [circumcircle](@entry_id:165300).
*   If $\Delta < 0$, $P$ is outside the [circumcircle](@entry_id:165300).
*   If $\Delta = 0$, $P$ is on the [circumcircle](@entry_id:165300).

For instance, given stations $A=(0,3)$, $B=(-2,-1)$, $C=(4,1)$ and a potential new station $P=(1,0)$, we can compute this determinant. The calculation yields $\Delta = 200$ . Since the value is positive, we conclude that point $P$ lies inside the [circumcircle](@entry_id:165300) of $\triangle ABC$. Therefore, the triangle $\triangle ABC$ could not be part of a Delaunay triangulation of the set $\{A, B, C, P\}$.

#### Special Case: Concyclic Points

The case where $\Delta=0$ is of special interest. This occurs when four or more points are **concyclic**, meaning they all lie on the same circle. In this "degenerate" configuration, the Delaunay [triangulation](@entry_id:272253) is not unique.

Consider four seismic stations $A, B, C, D$ that lie on a circle . These points form a convex quadrilateral. A [triangulation](@entry_id:272253) of this quadrilateral requires choosing one of two diagonals: $\overline{AC}$ or $\overline{BD}$. If we consider the triangle $\triangle ABD$, its [circumcircle](@entry_id:165300) passes through $C$. Because $C$ is *on* the circle and not strictly inside, the empty [circumcircle](@entry_id:165300) condition is met (in its relaxed form). This means the edge $\overline{BD}$ is a valid Delaunay edge. Symmetrically, the [circumcircle](@entry_id:165300) of $\triangle ABC$ passes through $D$, making the edge $\overline{AC}$ also a valid Delaunay edge. Consequently, two distinct Delaunay triangulations exist: one using the diagonal $\overline{AC}$ (forming triangles $\triangle ABC$ and $\triangle ADC$) and another using the diagonal $\overline{BD}$ (forming triangles $\triangle ABD$ and $\triangle BCD$).

### The Duality of Voronoi and Delaunay

The Voronoi diagram and the Delaunay [triangulation](@entry_id:272253) are not independent structures; they are **geometric duals** of one another. This deep and beautiful connection provides a powerful lens for understanding both. The duality can be summarized as follows:

*   Each **site** $p_i$ (a Delaunay vertex) corresponds to a **Voronoi cell** $V(p_i)$.
*   An **edge** connects two sites $p_i$ and $p_j$ in the Delaunay [triangulation](@entry_id:272253) if and only if their Voronoi cells $V(p_i)$ and $V(p_j)$ share a common **Voronoi edge**.
*   Each **triangle** in the Delaunay [triangulation](@entry_id:272253) corresponds to a **Voronoi vertex**. Specifically, the [circumcenter](@entry_id:174510) of a Delaunay triangle is a Voronoi vertex.

This duality provides powerful insights and properties.

#### Adjacency and the Closest Pair Property

The dual relationship means that the concept of "adjacency" is consistent across both structures. Two sites whose Voronoi cells share a boundary are considered neighbors in the Delaunay [triangulation](@entry_id:272253) . Conversely, if two cells do not share a boundary, their corresponding sites are not connected by a Delaunay edge.

A significant consequence of this is the **closest pair property**: The pair of points in the set $P$ that are closest to each other must be connected by an edge in the Delaunay triangulation . To see why, let $p_i$ and $p_j$ be the closest pair of sites. Consider a circle whose diameter is the segment $\overline{p_i p_j}$. This circle passes through $p_i$ and $p_j$. Because they are the closest pair, no other site $p_k$ can be inside this circle, as that would imply $|p_i p_k|  |p_i p_j|$ or $|p_j p_k|  |p_i p_j|$. Since there exists a circle passing through $p_i$ and $p_j$ with an empty interior, the edge $\overline{p_i p_j}$ must be in the Delaunay [triangulation](@entry_id:272253).

#### Orthogonality and Geometric Relationships

The duality also manifests as a precise geometric relationship: every edge in the Delaunay [triangulation](@entry_id:272253) is orthogonal to its dual edge in the Voronoi diagram.

Let $\overline{p_i p_j}$ be a Delaunay edge. Its dual is the Voronoi edge separating $V(p_i)$ and $V(p_j)$. This Voronoi edge is a segment of the [perpendicular bisector](@entry_id:176427) of $\overline{p_i p_j}$. Therefore, the Delaunay edge and its dual Voronoi edge are perpendicular. This relationship can be leveraged to solve geometric problems. For example, if we know the locations of the two Voronoi vertices $V_1$ and $V_2$ that form a Voronoi edge, we can deduce information about the dual Delaunay edge $\overline{P_1P_2}$ . Since $V_1$ and $V_2$ are on the [perpendicular bisector](@entry_id:176427) of $\overline{P_1P_2}$, the vector $\vec{P_1 P_2}$ must be orthogonal to the vector $\vec{V_1 V_2}$. Furthermore, because $V_1$ and $V_2$ are Voronoi vertices (circumcenters of Delaunay triangles), they are equidistant from $P_1$ and $P_2$. These geometric constraints are often sufficient to fully determine the properties of one structure from the other.

In summary, the principles of proximity and empty circles give rise to the Voronoi diagram and Delaunay [triangulation](@entry_id:272253), respectively. While seemingly different, they are inextricably linked through the powerful concept of duality, forming a cornerstone of computational geometry with far-reaching applications.