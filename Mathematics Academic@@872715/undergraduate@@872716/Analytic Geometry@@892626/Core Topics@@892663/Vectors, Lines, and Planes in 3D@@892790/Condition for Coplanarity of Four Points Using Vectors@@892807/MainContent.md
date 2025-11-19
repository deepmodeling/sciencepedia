## Introduction
In the study of three-dimensional space, understanding the relationships between points, lines, and planes is fundamental. While three non-collinear points uniquely define a plane, a fourth point typically introduces a third dimension, forming a volume. The critical question then arises: under what specific condition do four points lie on the same plane? This property, known as coplanarity, is not just a geometric puzzle but a foundational concept with far-reaching implications in science and engineering. This article addresses this question by providing a rigorous, vector-based framework for determining coplanarity.

In the chapters that follow, you will gain a comprehensive understanding of this topic. The first chapter, **Principles and Mechanisms**, delves into the core mathematical concepts, starting with linear dependence and building up to the powerful scalar triple product test. It establishes the computational tools, such as determinants, for applying this condition. The second chapter, **Applications and Interdisciplinary Connections**, explores the practical significance of coplanarity, showcasing its role in solving problems in fields from classical mechanics and computer vision to materials science. Finally, the **Hands-On Practices** chapter allows you to solidify your knowledge by working through targeted problems that apply these principles in various contexts. By the end, you will be equipped to both understand and apply the condition for coplanarity in theoretical and practical settings.

## Principles and Mechanisms

In our study of [analytic geometry](@entry_id:164266), moving from one and two dimensions into three-dimensional space introduces a new level of complexity and geometric richness. A foundational concept in 3D space is the idea of a **plane**. While two points define a line, and three non-collinear points define a plane, what can be said about four points? Four points chosen randomly in space will generally not lie on the same plane; they will instead define a three-dimensional volume, such as a tetrahedron. The condition under which four points do lie on the same plane, a property known as **coplanarity**, is a fundamental question with significant applications across science and engineering. This chapter elucidates the vector-based principles and mechanisms used to test for and enforce coplanarity.

### The Geometric Condition of Linear Dependence

The most intuitive way to understand coplanarity is by building upon the concept of collinearity. Three distinct points $A$, $B$, and $C$ are **collinear** if they lie on a single straight line. In vector terms, this means the displacement vector from one point to another, say $\vec{AB}$, is parallel to the [displacement vector](@entry_id:262782) from the first point to the third, $\vec{AC}$. This parallelism implies that one vector is a scalar multiple of the other:
$$ \vec{AC} = k \vec{AB} $$
for some scalar $k$.

We extend this logic to planes. Let us consider four points, $A$, $B$, $C$, and $D$. To start, we assume that the first three points, $A$, $B$, and $C$, are not collinear, as they must define a unique plane. For the fourth point, $D$, to be coplanar with $A$, $B$, and $C$, it must lie on this plane.

A plane can be defined by a point and two non-parallel direction vectors. Let us choose $A$ as our reference point. The plane is then spanned by the vectors $\vec{AB}$ and $\vec{AC}$. Any vector originating at $A$ and lying in this plane can be expressed as a linear combination of these two basis vectors. Therefore, for point $D$ to be on the plane, the vector $\vec{AD}$ must be expressible as:
$$ \vec{AD} = s \vec{AB} + t \vec{AC} $$
for some real scalars $s$ and $t$.

This equation represents the core principle of coplanarity: the three vectors originating from a common reference point, $\vec{AB}$, $\vec{AC}$, and $\vec{AD}$, must be **linearly dependent**. If they were linearly independent, they would span a three-dimensional volume, and the point $D$ would necessarily lie outside the plane defined by $A$, $B$, and $C$. This condition provides a direct algebraic test for coplanarity.

A simple, illustrative case arises if the point $D$ lies on the line segment connecting $A$ and $B$. In this situation, the vectors $\vec{AD}$ and $\vec{AB}$ are collinear, so $\vec{AD} = s\vec{AB}$ for some scalar $s$. This fits our general condition with $t=0$, confirming that if four points include a collinear subset of three, the four points must be coplanar [@problem_id:2113927].

### The Scalar Triple Product and Geometric Volume

While the [linear dependence](@entry_id:149638) condition is conceptually clear, a more direct and computationally powerful test for coplanarity arises from the geometric interpretation of the **[scalar triple product](@entry_id:152997)**. For three vectors $\vec{u}$, $\vec{v}$, and $\vec{w}$, the [scalar triple product](@entry_id:152997) is defined as $\vec{u} \cdot (\vec{v} \times \vec{w})$.

Geometrically, the magnitude of the [cross product](@entry_id:156749), $|\vec{v} \times \vec{w}|$, gives the area of the parallelogram formed by vectors $\vec{v}$ and $\vec{w}$. The subsequent dot product with $\vec{u}$ projects $\vec{u}$ onto the normal of the parallelogram's plane and multiplies this projected height by the base area. The result, $|\vec{u} \cdot (\vec{v} \times \vec{w})|$, is the volume of the **parallelepiped** spanned by the three vectors $\vec{u}$, $\vec{v}$, and $\vec{w}$.

This insight provides a definitive test for coplanarity. If the three vectors $\vec{AB}$, $\vec{AC}$, and $\vec{AD}$ are coplanar, the "parallelepiped" they define is a flattened, two-dimensional figure with zero volume. Conversely, if the volume of the parallelepiped is zero, the three vectors must lie in the same plane.

Thus, the condition for four points $A$, $B$, $C$, and $D$ to be coplanar is:
$$ [\vec{AB}, \vec{AC}, \vec{AD}] = \vec{AB} \cdot (\vec{AC} \times \vec{AD}) = 0 $$

It is important to note that the order of the vectors in the scalar triple product only affects the sign of the result (a consequence of the properties of cross products and [determinants](@entry_id:276593)), and the choice of the common reference point (e.g., using $\vec{BA}, \vec{BC}, \vec{BD}$) does not alter the zero-volume condition.

An interesting implication arises when we consider vectors that are all confined to a single plane, such as the $xy$-plane. For instance, if we have beacons on a flat ground plane at positions $B_1, B_2, B_3, B_4$, any vectors formed between them, like $\vec{B_1B_2}$ and $\vec{B_1B_3}$, will have a zero $z$-component. Their [cross product](@entry_id:156749), $\vec{B_1B_2} \times \vec{B_1B_3}$, will be perpendicular to the $xy$-plane, pointing purely in the $\vec{k}$ direction. This geometric property is a direct consequence of the definition of the [cross product](@entry_id:156749) and can be useful in specialized calculations, such as determining the orientation of a surface from measurements taken in a plane [@problem_id:2113905].

### Computational Frameworks for Coplanarity

The [scalar triple product](@entry_id:152997) condition is most effectively implemented using [determinants](@entry_id:276593). Given three vectors in Cartesian coordinates, $\vec{u} = \langle u_x, u_y, u_z \rangle$, $\vec{v} = \langle v_x, v_y, v_z \rangle$, and $\vec{w} = \langle w_x, w_y, w_z \rangle$, their [scalar triple product](@entry_id:152997) is equivalent to the determinant of the matrix formed by these vectors as its rows (or columns):
$$ \vec{u} \cdot (\vec{v} \times \vec{w}) = \begin{vmatrix} u_x & u_y & u_z \\ v_x & v_y & v_z \\ w_x & w_y & w_z \end{vmatrix} $$

This transforms the geometric problem of coplanarity into a straightforward algebraic calculation.

**Worked Example: Calibrating Sensor Positions**

Consider a scenario in materials science where the positions of atoms in a crystal lattice are mapped. Three atoms, $A$, $B$, and $C$, define a crystallographic plane, and we need to determine if an impurity atom, $D$, lies on this same plane. Let the coordinates be $A=(3, -1, 2)$, $B=(1, 1, 1)$, $C=(5, 0, -2)$, and $D=(2, 2, z_D)$. To ensure [structural integrity](@entry_id:165319), all four atoms must be coplanar [@problem_id:2113943].

1.  **Form Displacement Vectors:** We select $A$ as the reference point and form the vectors:
    $$ \vec{AB} = B - A = \langle 1-3, 1-(-1), 1-2 \rangle = \langle -2, 2, -1 \rangle $$
    $$ \vec{AC} = C - A = \langle 5-3, 0-(-1), -2-2 \rangle = \langle 2, 1, -4 \rangle $$
    $$ \vec{AD} = D - A = \langle 2-3, 2-(-1), z_D-2 \rangle = \langle -1, 3, z_D-2 \rangle $$

2.  **Apply the Determinant Condition:** The coplanarity condition is $[\vec{AB}, \vec{AC}, \vec{AD}] = 0$. We set up the determinant:
    $$ \begin{vmatrix} -2 & 2 & -1 \\ 2 & 1 & -4 \\ -1 & 3 & z_D-2 \end{vmatrix} = 0 $$

3.  **Evaluate the Determinant:** Expanding along the first row:
    $$ -2 \begin{vmatrix} 1 & -4 \\ 3 & z_D-2 \end{vmatrix} - 2 \begin{vmatrix} 2 & -4 \\ -1 & z_D-2 \end{vmatrix} + (-1) \begin{vmatrix} 2 & 1 \\ -1 & 3 \end{vmatrix} = 0 $$
    $$ -2((z_D-2) - (-12)) - 2(2(z_D-2) - 4) - 1(6 - (-1)) = 0 $$
    $$ -2(z_D + 10) - 2(2z_D - 8) - 7 = 0 $$
    $$ -2z_D - 20 - 4z_D + 16 - 7 = 0 $$
    $$ -6z_D - 11 = 0 $$

4.  **Solve for the Unknown:**
    $$ z_D = -\frac{11}{6} $$

Thus, the impurity atom $D$ is coplanar with atoms $A, B,$ and $C$ if its $z$-coordinate is precisely $-\frac{11}{6}$. This method is broadly applicable in fields like structural engineering [@problem_id:2113960], quality control [@problem_id:2113946], and 3D scanning calibration [@problem_id:2113911].

#### Special Case: Coplanarity with the Origin

A frequent and important special case occurs when one of the four points is the origin $O(0,0,0)$. Let the other three points be $A, B, C$ with [position vectors](@entry_id:174826) $\vec{a}, \vec{b}, \vec{c}$ respectively. The displacement vectors from the origin are simply the [position vectors](@entry_id:174826) themselves: $\vec{OA} = \vec{a}$, $\vec{OB} = \vec{b}$, and $\vec{OC} = \vec{c}$.

The coplanarity condition simplifies elegantly: four points $O, A, B, C$ are coplanar if and only if their [position vectors](@entry_id:174826) are linearly dependent, which means the scalar triple product of the [position vectors](@entry_id:174826) is zero [@problem_id:2113920].
$$ [\vec{a}, \vec{b}, \vec{c}] = \vec{a} \cdot (\vec{b} \times \vec{c}) = \begin{vmatrix} a_x & a_y & a_z \\ b_x & b_y & b_z \\ c_x & c_y & c_z \end{vmatrix} = 0 $$
This provides the condition for three vectors to lie on a single plane passing through the origin.

### Equivalent Formulations and Advanced Perspectives

The [scalar triple product](@entry_id:152997) provides a robust computational tool, but alternative formulations of the coplanarity condition offer deeper conceptual insights and connections to other areas of mathematics.

#### The Planar Equation Approach

Another way to frame the problem is to first find the equation of the plane defined by three points ($A, B, C$) and then check if the fourth point ($D$) satisfies this equation. The normal vector $\vec{n}$ to the plane is perpendicular to any vector lying within it. We can find $\vec{n}$ by taking the cross product of two vectors in the plane, for example:
$$ \vec{n} = \vec{AB} \times \vec{AC} $$
The equation of the plane is then given by $\vec{n} \cdot (\vec{r} - \vec{a}) = 0$, where $\vec{r}$ is the [position vector](@entry_id:168381) of any point on the plane and $\vec{a}$ is the position vector of point $A$. For point $D$ to lie on this plane, its [position vector](@entry_id:168381) $\vec{d}$ must satisfy the equation:
$$ \vec{n} \cdot (\vec{d} - \vec{a}) = 0 \quad \implies \quad (\vec{AB} \times \vec{AC}) \cdot \vec{AD} = 0 $$
This result is precisely the [scalar triple product](@entry_id:152997) condition, but the derivation emphasizes the geometric relationship between the point $D$ and the plane's normal vector. This approach is particularly useful in problems where a point's position is a variable parameter, such as tracking a drone relative to fixed beacons [@problem_id:2113976].

#### Affine Combinations

A particularly elegant and powerful formulation comes from the concept of **affine combinations**. A point $D$ is coplanar with non-collinear points $A, B, C$ if and only if its [position vector](@entry_id:168381) $\vec{d}$ can be expressed as a specific weighted average of the [position vectors](@entry_id:174826) $\vec{a}, \vec{b}, \vec{c}$:
$$ \vec{d} = c_1 \vec{a} + c_2 \vec{b} + c_3 \vec{c}, \quad \text{where} \quad c_1 + c_2 + c_3 = 1 $$
This can be derived directly from our [linear dependence](@entry_id:149638) condition, $\vec{AD} = s \vec{AB} + t \vec{AC}$:
$$ \vec{d} - \vec{a} = s(\vec{b} - \vec{a}) + t(\vec{c} - \vec{a}) $$
$$ \vec{d} = \vec{a} - s\vec{a} - t\vec{a} + s\vec{b} + t\vec{c} $$
$$ \vec{d} = (1 - s - t)\vec{a} + s\vec{b} + t\vec{c} $$
By setting $c_1 = 1 - s - t$, $c_2 = s$, and $c_3 = t$, we obtain the [affine combination](@entry_id:276726), as the sum of the coefficients is $c_1+c_2+c_3 = (1-s-t)+s+t = 1$. The coefficients $(c_1, c_2, c_3)$ are known as the **[barycentric coordinates](@entry_id:155488)** of $D$ with respect to the triangle $ABC$.

This formulation is invaluable in fields like [computer graphics](@entry_id:148077) for texture mapping and physics for interpolating fields. For example, if a scalar property like temperature or stress is known at points $A, B, C$, its value at any coplanar point $D$ can be estimated by the same [linear interpolation](@entry_id:137092) [@problem_id:2113910]:
$$ \Psi_D = c_1 \Psi_A + c_2 \Psi_B + c_3 \Psi_C $$

#### Basis-Independent Nature of Coplanarity

Finally, it is crucial to recognize that coplanarity is an intrinsic geometric property, independent of the chosen coordinate system. The condition of [linear dependence](@entry_id:149638) is fundamental. This can be highlighted by considering a problem in an [abstract vector space](@entry_id:188875). Suppose we have four points $A, B, C, D$ defined relative to a reference point $P$ by vectors expressed in terms of a non-standard, mutually [orthogonal basis](@entry_id:264024) $\{\vec{u}, \vec{v}, \vec{w}\}$ [@problem_id:2113966].

The test for coplanarity remains the same: we form the vectors $\vec{AB}$, $\vec{AC}$, and $\vec{AD}$ and check if their scalar triple product is zero. When these vectors are expressed as linear combinations of the basis vectors, the scalar triple product can be calculated as the determinant of their coefficients multiplied by the scalar triple product of the basis vectors, $[\vec{u}, \vec{v}, \vec{w}]$.
$$ [\vec{AB}, \vec{AC}, \vec{AD}] = \begin{vmatrix} c_{11} & c_{12} & c_{13} \\ c_{21} & c_{22} & c_{23} \\ c_{31} & c_{32} & c_{33} \end{vmatrix} [\vec{u}, \vec{v}, \vec{w}] $$
Since the basis vectors are non-zero and mutually orthogonal, they are [linearly independent](@entry_id:148207), so $[\vec{u}, \vec{v}, \vec{w}] \neq 0$. Therefore, the coplanarity condition reduces to the determinant of the [coefficient matrix](@entry_id:151473) being zero. This demonstrates that the algebraic mechanism for testing coplanarity holds true regardless of the coordinate system, underscoring the universal power of vector methods.