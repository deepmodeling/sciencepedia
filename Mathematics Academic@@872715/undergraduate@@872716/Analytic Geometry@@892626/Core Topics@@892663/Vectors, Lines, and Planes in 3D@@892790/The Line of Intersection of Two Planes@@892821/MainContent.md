## Introduction
In the realm of three-dimensional [analytic geometry](@entry_id:164266), the intersection of two planes is a foundational concept with far-reaching implications. While two planes can be parallel or coincident, the most dynamic case is when they intersect to form a single straight line. This line represents the set of all points common to both planes, and being able to precisely define it is crucial for fields ranging from engineering and physics to computer graphics. This article addresses the core problem of how to mathematically determine and represent this line of intersection.

To bridge the gap from geometric intuition to algebraic certainty, this article provides a systematic guide. The reader will first explore the **Principles and Mechanisms** chapter, which details the step-by-step method for finding the line's [direction vector](@entry_id:169562) and a point on it. Following this, the **Applications and Interdisciplinary Connections** chapter will illuminate how these geometric calculations are applied to solve real-world problems in materials science, optics, and advanced mathematics. Finally, the **Hands-On Practices** section offers an opportunity to solidify these concepts through targeted exercises, ensuring a robust understanding of how to describe the [line of intersection of two planes](@entry_id:168327).

## Principles and Mechanisms

In three-dimensional space, two distinct planes can relate to each other in one of three ways: they can be parallel and never meet, they can be identical (coincident), or they can intersect along a single straight line. Our focus in this chapter is on this third case, which is of fundamental importance in fields ranging from computer graphics and engineering design to physics and materials science. We will systematically develop the principles and methods required to define and describe this line of intersection.

### Geometric Conditions for Intersection

A plane in Cartesian space is defined by the linear equation $ax + by + cz = d$. The vector $\vec{n} = \langle a, b, c \rangle$, formed by the coefficients of the variables, is the **normal vector** to the plane. This vector is orthogonal (perpendicular) to every vector lying within the plane. The geometric relationship between two planes, $P_1$ and $P_2$, is entirely determined by the relationship between their respective normal vectors, $\vec{n}_1$ and $\vec{n}_2$.

If the normal vectors are parallel—that is, if $\vec{n}_1$ is a scalar multiple of $\vec{n}_2$ (i.e., $\vec{n}_1 = k\vec{n}_2$ for some scalar $k$)—then the planes themselves are parallel. In this scenario, they either never intersect (if they are distinct) or they are the same plane (if they are coincident). For example, a common design requirement in engineering is to ensure two plates do not intersect [@problem_id:2168838]. Consider two planes $P_1: 4x - 6y + 10z = 7$ and $P_2: -2x + (5k-1)y - 5z = 3$. Their normal vectors are $\vec{n}_1 = \langle 4, -6, 10 \rangle$ and $\vec{n}_2 = \langle -2, 5k-1, -5 \rangle$. For the planes to be parallel, their normals must be proportional. We can see that the first and third components of $\vec{n}_2$ are $-\frac{1}{2}$ times those of $\vec{n}_1$. To maintain this proportionality, the $y$-component must also satisfy this relationship: $5k-1 = -\frac{1}{2}(-6)$, which simplifies to $5k-1=3$, yielding $k = \frac{4}{5}$. When $k = \frac{4}{5}$, the planes are parallel and, since their constant terms are not in the same proportion, they are distinct and will never intersect.

Conversely, if the normal vectors $\vec{n}_1$ and $\vec{n}_2$ are **not parallel**, the planes are guaranteed to intersect. Because the planes are flat and extend infinitely, their intersection cannot be a single point or a curve; it must be a **straight line**.

### Determining the Line of Intersection

To uniquely define a line in three-dimensional space, we need two pieces of information: its **direction** and at least one **point** that lies on it. The task of finding the [line of intersection of two planes](@entry_id:168327) is therefore reduced to finding these two elements.

#### The Direction Vector of the Line

The line of intersection, let us call it $L$, lies within plane $P_1$ and also within plane $P_2$. A fundamental property of a plane is that its [normal vector](@entry_id:264185) is orthogonal to any vector lying in that plane. Therefore, the [direction vector](@entry_id:169562) of our line $L$, which we will denote $\vec{d}$, must be orthogonal to the normal vector $\vec{n}_1$ of plane $P_1$. Simultaneously, since $L$ is also in $P_2$, its direction vector $\vec{d}$ must be orthogonal to the normal vector $\vec{n}_2$ of plane $P_2$.

This provides a powerful geometric constraint: the [direction vector](@entry_id:169562) $\vec{d}$ of the line of intersection is a vector that is simultaneously orthogonal to both $\vec{n}_1$ and $\vec{n}_2$. In vector algebra, the **[cross product](@entry_id:156749)** is the operation that produces a vector orthogonal to two other given vectors. Thus, the [direction vector](@entry_id:169562) $\vec{d}$ must be parallel to the [cross product](@entry_id:156749) of the normal vectors:

$\vec{d} \parallel \vec{n}_1 \times \vec{n}_2$

Let's consider an example from a computer-aided design (CAD) context where two surfaces are modeled by the planes $P_1: 2x + 7y - 4z = 5$ and $P_2: 3x - y + 2z = 11$ [@problem_id:2164166]. The normal vectors are $\vec{n}_1 = \langle 2, 7, -4 \rangle$ and $\vec{n}_2 = \langle 3, -1, 2 \rangle$. The direction vector $\vec{d}$ of their line of intersection is found by calculating the [cross product](@entry_id:156749):

$\vec{d} = \vec{n}_1 \times \vec{n}_2 = \begin{vmatrix} \mathbf{i} & \mathbf{j} & \mathbf{k} \\ 2 & 7 & -4 \\ 3 & -1 & 2 \end{vmatrix} = (7(2) - (-4)(-1))\mathbf{i} - (2(2) - (-4)(3))\mathbf{j} + (2(-1) - 7(3))\mathbf{k}$

$\vec{d} = (14 - 4)\mathbf{i} - (4 + 12)\mathbf{j} + (-2 - 21)\mathbf{k} = 10\mathbf{i} - 16\mathbf{j} - 23\mathbf{k}$

So, a [direction vector](@entry_id:169562) for the line of intersection is $\vec{d} = \langle 10, -16, -23 \rangle$. Any non-zero scalar multiple of this vector is also a valid direction vector.

#### Finding a Point on the Line

Once the direction of the line is known, we must anchor it in space by finding the coordinates $(x_0, y_0, z_0)$ of any single point that lies on it. A point on the line of intersection must, by definition, satisfy the equations of both planes simultaneously. Suppose the planes are given by:

$a_1x + b_1y + c_1z = d_1$
$a_2x + b_2y + c_2z = d_2$

We have a system of two [linear equations](@entry_id:151487) in three variables ($x, y, z$). Because there is one more variable than equations, the system is underdetermined and has infinitely many solutions, which correspond to all the points on the line of intersection. To find just one of these solutions, we can simplify the problem by imposing an additional constraint. A common and effective strategy is to set one of the variables to a constant, typically zero.

For instance, by setting $z=0$, we are effectively seeking the point where the line of intersection pierces the $xy$-plane. The system of equations reduces to:

$a_1x + b_1y = d_1$
$a_2x + b_2y = d_2$

This is now a standard system of two linear equations in two variables ($x, y$), which can be readily solved to find a unique pair of values for $x$ and $y$. This gives us the coordinates of one point on the line.

Let's apply this to a practical scenario of a geological survey mapping two rock strata [@problem_id:1382161]. The planes are $2x - y + 3z = -150$ and $x + y - z = -100$. To find the point where the intersection line passes through the $xy$-plane, we set $z=0$:

$2x - y = -150$
$x + y = -100$

Adding the two equations gives $3x = -250$, so $x = -\frac{250}{3}$. Substituting this back into the second equation gives $y = -100 - x = -100 - (-\frac{250}{3}) = -\frac{50}{3}$. Thus, a point on the line of intersection is $P_0 = (-\frac{250}{3}, -\frac{50}{3}, 0)$.

### Representing the Line of Intersection

With a direction vector $\vec{d} = \langle d_x, d_y, d_z \rangle$ and a point $P_0 = (x_0, y_0, z_0)$ on the line, we can express the line using several standard mathematical forms.

1.  **Vector Form:** This form is concise and geometrically intuitive. A generic point $\vec{r} = \langle x, y, z \rangle$ on the line is reached by starting at the known point $\vec{p}_0 = \langle x_0, y_0, z_0 \rangle$ and moving some distance along the direction vector $\vec{d}$. This is parameterized by a scalar $t$:
    $\vec{r}(t) = \vec{p}_0 + t\vec{d}$

2.  **Parametric Form:** By writing out the components of the vector equation, we get a set of three equations, one for each coordinate:
    $x(t) = x_0 + t d_x$
    $y(t) = y_0 + t d_y$
    $z(t) = z_0 + t d_z$

3.  **Symmetric Form:** If none of the components of the direction vector are zero, we can solve each parametric equation for the parameter $t$ and set them equal to each other:
    $\frac{x - x_0}{d_x} = \frac{y - y_0}{d_y} = \frac{z - z_0}{d_z}$

As an example, suppose we know two planes pass through the point $P_0 = (3, -1, 5)$ and are perpendicular to vectors $\vec{n}_1 = \langle 2, -3, 1 \rangle$ and $\vec{n}_2 = \langle 1, 4, -2 \rangle$ respectively [@problem_id:2168852]. The direction vector of their intersection is $\vec{d} = \vec{n}_1 \times \vec{n}_2 = \langle 2, 5, 11 \rangle$. Since we are given a common point, we do not need to solve for one. We can immediately write the [symmetric equations](@entry_id:175177) for the line:
$\frac{x-3}{2} = \frac{y+1}{5} = \frac{z-5}{11}$

### Verification and Further Topics

Once a line is determined, or proposed, it is often necessary to verify that it is indeed the correct line of intersection.

#### Verifying a Line of Intersection

Suppose we are given the equations of two planes and the [equation of a line](@entry_id:166789), and we must confirm the line is their intersection, as in a quality control check for a surgical laser [@problem_id:2168851]. Let the planes be $P_1: x - 2y + 3z = 1$ and $P_2: 2x + y - z = 7$, and the proposed line be $L: \vec{r}(t) = \langle 3, 1, 0 \rangle + t \langle -1, 7, 5 \rangle$.

There are two primary methods of verification.

1.  **Geometric Verification:** First, confirm the line's direction is correct. The normal vectors are $\vec{n}_1 = \langle 1, -2, 3 \rangle$ and $\vec{n}_2 = \langle 2, 1, -1 \rangle$. Their cross product is $\vec{n}_1 \times \vec{n}_2 = \langle (-2)(-1) - 3(1), 3(2) - 1(-1), 1(1) - (-2)(2) \rangle = \langle -1, 7, 5 \rangle$. This matches the [direction vector](@entry_id:169562) of the line $L$. Second, confirm that the line shares at least one point with both planes. The point on the line corresponding to $t=0$ is $(3, 1, 0)$. Substituting this into the plane equations:
    For $P_1$: $3 - 2(1) + 3(0) = 1$. (True)
    For $P_2$: $2(3) + 1 - 0 = 7$. (True)
    Since the line has the correct direction and passes through a point common to both planes, it must be their line of intersection.

2.  **Algebraic Verification:** Substitute the [parametric equations](@entry_id:172360) for the line, $x = 3-t$, $y = 1+7t$, and $z = 5t$, directly into both plane equations.
    For $P_1$: $(3-t) - 2(1+7t) + 3(5t) = 3 - t - 2 - 14t + 15t = 1$. The equation holds for all $t$.
    For $P_2$: $2(3-t) + (1+7t) - 5t = 6 - 2t + 1 + 7t - 5t = 7$. This equation also holds for all $t$.
    Since the coordinates of every point on the line satisfy both plane equations, the line lies completely within both planes and is therefore their intersection.

#### The Family of Planes through a Line

An elegant and powerful concept arises when we consider the set of all planes that pass through a single line. If a line is defined as the intersection of two planes $P_1: A_1x + B_1y + C_1z - D_1 = 0$ and $P_2: A_2x + B_2y + C_2z - D_2 = 0$, then the equation of *any* other plane passing through this same line can be expressed as a [linear combination](@entry_id:155091) of the two original plane equations:
$(A_1x + B_1y + C_1z - D_1) + k(A_2x + B_2y + C_2z - D_2) = 0$
for some real-valued constant $k$. This is often called a **[pencil of planes](@entry_id:172060)**. Any point $(x,y,z)$ on the line of intersection will, by definition, make both terms in parentheses equal to zero, thus satisfying the composite equation regardless of the value of $k$ [@problem_id:2168865]. This principle is useful in advanced optics and geometry for defining entire families of surfaces that share a common axis.

#### From a Line to its Intersecting Planes

We can also reverse the problem: given a line, find two distinct planes whose intersection is that line. For a line $\vec{r}(t) = \vec{p}_0 + t\vec{v}$, any plane containing this line must have a normal vector $\vec{n}$ that is orthogonal to the line's direction vector $\vec{v}$. This is expressed by the dot product condition $\vec{n} \cdot \vec{v} = 0$.

There are infinitely many vectors $\vec{n}$ that satisfy this condition. To define a unique pair of planes, we need to impose additional constraints. For example, given the line $L: \vec{r}(t) = \langle 2, -1, 3 \rangle + t \langle 1, 4, -2 \rangle$, we could seek one plane whose normal is orthogonal to $\vec{j}=\langle 0,1,0 \rangle$ and another whose normal is orthogonal to $\vec{k}=\langle 0,0,1 \rangle$ [@problem_id:2168831]. By finding two such non-parallel normal vectors and then using the point $\vec{p}_0 = \langle 2,-1,3 \rangle$ to determine the constant term for each [plane equation](@entry_id:152977), we can construct a valid pair of intersecting planes. This exercise reinforces the fundamental relationship between a line's direction and the normal vectors of the planes that contain it.

#### Intersection of Three Planes

When a third plane, $P_3$, is introduced, the system may intersect at a single point, along a line, or not at all. For three distinct planes to intersect along a single common line, a special condition must be met. Algebraically, the system of three [linear equations](@entry_id:151487) must be **consistent** (meaning a solution exists) and **dependent** (meaning there are infinitely many solutions forming a line). This occurs if and only if one of the plane equations can be written as a [linear combination](@entry_id:155091) of the other two. Geometrically, this means the three normal vectors are coplanar, and the planes themselves form a consistent system, like pages of an open book all meeting at the spine [@problem_id:2168862]. Analyzing the rank of the coefficient and augmented matrices of the linear system provides a rigorous method from linear algebra to determine the exact nature of the intersection.