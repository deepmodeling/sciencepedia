## Introduction
In the study of [analytic geometry](@entry_id:164266), geometric objects are not merely static figures but can be subjected to dynamic transformations that alter their position and orientation. Among the most fundamental of these transformations is the reflection, an operation that creates a perfect mirror image of an object across a line. Understanding reflections is crucial as it bridges the gap between visual geometric intuition and rigorous algebraic formulation. This article provides a comprehensive exploration of reflections over axes, moving from foundational rules to advanced applications.

You will begin by learning the core **Principles and Mechanisms** of reflection, including how to transform coordinates, equations of functions, and entire geometric figures. We will then delve into the powerful consequences of these principles in the **Applications and Interdisciplinary Connections** chapter, discovering how reflections solve [optimization problems](@entry_id:142739), define symmetry in abstract algebra, and find use in fields like physics and engineering. Finally, the **Hands-On Practices** section will offer you the opportunity to apply these concepts to concrete problems, solidifying your understanding. Let's begin our journey by establishing the fundamental principles of reflection in the Cartesian plane.

## Principles and Mechanisms

In our study of [analytic geometry](@entry_id:164266), we move from the static description of objects to the dynamic analysis of their transformations. Among the most fundamental transformations are reflections. A reflection is an operation that "flips" an object across a line, known as the axis of reflection, creating a mirror image. This chapter will systematically develop the principles of reflection, beginning with their coordinate definitions and culminating in their representation as linear operators.

### Defining Reflections in the Cartesian Plane

The most intuitive way to understand a reflection is to see how it acts on a single point in the Cartesian plane. We will begin by defining reflections across the primary coordinate axes and the line $y=x$.

Let $P(x, y)$ be an arbitrary point in the plane.

- **Reflection across the x-axis:** When a point is reflected across the horizontal x-axis, its horizontal position remains unchanged, while its vertical position is inverted. The reflected point, let's call it $P_x$, will have coordinates $(x, -y)$. The transformation rule is $(x, y) \mapsto (x, -y)$.

- **Reflection across the y-axis:** Similarly, a reflection across the vertical y-axis inverts the point's horizontal position while preserving its vertical position. The reflected point, $P_y$, will have coordinates $(-x, y)$. The transformation rule is $(x, y) \mapsto (-x, y)$.

- **Reflection across the line $y=x$:** Reflection across the line $y=x$ is a special case where the roles of the $x$ and $y$ coordinates are interchanged. The reflected point, $P_{y=x}$, has coordinates $(y, x)$. The transformation rule is $(x, y) \mapsto (y, x)$. This is equivalent to finding the inverse of a function or relation.

These basic rules can be applied in sequence. For instance, consider a problem where a point $P_0(x_0, y_0)$ is first reflected across the y-axis to $P_1$, then across the x-axis to $P_2$, and finally across the line $y=x$ to $P_3$. We can trace the coordinates through this sequence [@problem_id:2154054]:
1. Reflection of $P_0(x_0, y_0)$ across the y-axis yields $P_1(-x_0, y_0)$.
2. Reflection of $P_1(-x_0, y_0)$ across the x-axis yields $P_2(-x_0, -y_0)$.
3. Reflection of $P_2(-x_0, -y_0)$ across the line $y=x$ yields $P_3(-y_0, -x_0)$.
If we are given that the final point is $P_3(7, -11)$, we can reverse the process by equating the coordinates: $-y_0 = 7$ and $-x_0 = -11$. This immediately gives us the original coordinates as $P_0(11, -7)$.

### The Effect of Reflection on Geometric Figures and Functions

The power of [analytic geometry](@entry_id:164266) lies in its ability to describe geometric figures using algebraic equations. A reflection transforms not just single points but the entire figure. The principle for transforming an equation is to substitute the variables with their expressions from the inverse transformation.

Consider a curve defined by an equation $E(x, y) = 0$.
- To reflect this curve across the x-axis, we note that a point $(x', y')$ on the new curve corresponds to a point $(x, y)$ on the original curve where $x' = x$ and $y' = -y$. To find the equation for the new curve, we express the original coordinates in terms of the new ones: $x = x'$ and $y = -y'$. Substituting these into the original equation gives $E(x', -y') = 0$. Dropping the primes for notational simplicity, the equation for the reflected curve is $E(x, -y) = 0$.

- Similarly, reflecting across the y-axis involves the substitution $x \to -x$, yielding the new equation $E(-x, y) = 0$.

This principle applies to any geometric figure. Let's examine its effect on functions, lines, and circles.

For a function defined by $y = f(x)$, a reflection across the x-axis transforms the equation to $-y = f(x)$, which is more commonly written as $y = -f(x)$ [@problem_id:2154025]. A reflection across the y-axis transforms the equation to $y = f(-x)$.

Let's consider a line $L_1$ with the equation $y = mx + c$, where $m \neq 0$ and $c \neq 0$.
If we reflect $L_1$ across the y-axis to obtain a new line $L_2$, we replace $x$ with $-x$ in the equation:
$y = m(-x) + c \implies y = -mx + c$.
The new slope is $-m$, and the y-intercept remains $c$ [@problem_id:2154070].
If we reflect $L_1$ across the x-axis, we replace $y$ with $-y$:
$-y = mx + c \implies y = -mx - c$.
The new slope is again $-m$, but the [y-intercept](@entry_id:168689) becomes $-c$.
A notable observation emerges: for a non-horizontal, non-vertical line, reflection across either the x-axis or the y-axis negates its slope [@problem_id:2154036]. If $m_0$ is the original slope, the slope after x-axis reflection, $m_x$, is $-m_0$, and the slope after y-axis reflection, $m_y$, is also $-m_0$.

Now, let's consider a circle. A circle is defined by its center and radius. Consider a circle $C_1$ with equation $(x-h)^2 + (y-k)^2 = r^2$, having center $(h, k)$ and radius $r$. Reflecting this circle across the x-axis transforms each point $(x, y)$ on the circle to $(x, -y)$. The center $(h, k)$ is transformed to $(h, -k)$. The radius, being a measure of distance, remains unchanged. Therefore, the equation of the reflected circle, $C_2$, is $(x-h)^2 + (y - (-k))^2 = r^2$, or $(x-h)^2 + (y+k)^2 = r^2$.
This property can be used to solve geometric problems. For example, if we are given the equation $x^2 + y^2 - 10x - 8y + 16 = 0$, we can complete the square to find the standard form: $(x-5)^2 + (y-4)^2 = 25$. This circle has its center at $(5, 4)$ and a radius of $5$. Reflecting it across the x-axis gives a new circle with center $(5, -4)$ and radius $5$. To find their intersection points, one would solve the system of two circle equations, which reveals that the intersection points must lie on the axis of reflection itself, i.e., where $y=0$ [@problem_id:2154063].

### Isometry: The Preservation of Distance

An essential characteristic of reflection is that it is an **isometry** (from Greek *isos*, "equal," and *metron*, "measure"). An isometry is a transformation that preserves distances between points. This means that the shape and size of a figure remain unchanged after a reflection; only its orientation may change.

We can prove this formally. Let $P_1 = (x_1, y_1)$ and $P_2 = (x_2, y_2)$ be two distinct points. The square of the Euclidean distance between them is $d^2 = (x_2 - x_1)^2 + (y_2 - y_1)^2$.

Now, let's reflect these points across the x-axis to get $P'_1 = (x_1, -y_1)$ and $P'_2 = (x_2, -y_2)$. The square of the new distance is:
$(d')^2 = (x_2 - x_1)^2 + ((-y_2) - (-y_1))^2 = (x_2 - x_1)^2 + (-y_2 + y_1)^2 = (x_2 - x_1)^2 + (y_1 - y_2)^2$.
Since $(y_1 - y_2)^2 = (y_2 - y_1)^2$, we see that $(d')^2 = d^2$. Thus, the distance is preserved. A similar proof holds for reflection across the y-axis and the line $y=x$.

Since reflections are isometries, any [composition of reflections](@entry_id:173247) must also be an [isometry](@entry_id:150881). This means that any transformation built from a sequence of reflections will preserve the distance between any two points. For example, if a composite transformation $\mathcal{T}$ is defined by applying reflection across the x-axis ($R_x$), then the y-axis ($R_y$), then the x-axis again ($\mathcal{T} = R_x \circ R_y \circ R_x$), the distance between any two transformed points will be the same as the distance between the original points [@problem_id:2154023].

### The Algebra of Composed Reflections

The sequential application of transformations, or composition, reveals a deep algebraic structure. Composing reflections can lead to other fundamental transformations, such as rotations and translations.

A striking result appears when we compose two reflections across [perpendicular lines](@entry_id:174147). Let's first reflect a point $P(a, b)$ across the vertical line $x = k$, and then reflect the resulting point $P'$ across the horizontal line $y=h$.
1. Reflection of $P(a, b)$ across $x=k$: The x-coordinate $a$ is mapped to a point that is equidistant from the line $x=k$ on the opposite side. This new coordinate is $k + (k-a) = 2k-a$. The y-coordinate is unchanged. So, $P' = (2k-a, b)$.
2. Reflection of $P'(2k-a, b)$ across $y=h$: The x-coordinate is unchanged, while the y-coordinate is mapped to $h + (h-b) = 2h-b$. So, the final point is $P'' = (2k-a, 2h-b)$.

This composite transformation $T(a,b) = (2k-a, 2h-b)$ is not a reflection. Instead, it is precisely a **rotation of 180 degrees** about the point of intersection of the two axes, $(k, h)$ [@problem_id:2154033]. A 180-degree rotation of $(a, b)$ around $(k, h)$ maps the vector from $(k, h)$ to $(a, b)$, which is $(a-k, b-h)$, to its negative, $(-a+k, -b+h)$. The new point is $(k, h) + (-a+k, -b+h) = (2k-a, 2h-b)$, which matches our result. A reflection across the y-axis followed by a reflection across the x-axis is a special case of this, with $k=0$ and $h=0$, resulting in a 180-degree rotation about the origin.

The order of transformations matters. In general, geometric transformations are **non-commutative**. For example, a rotation followed by a reflection is not necessarily the same as the reflection followed by the rotation. We can demonstrate this using [matrix representations](@entry_id:146025). A counter-clockwise rotation by an angle $\theta$ is given by the matrix $R(\theta) = \begin{pmatrix} \cos\theta & -\sin\theta \\ \sin\theta & \cos\theta \end{pmatrix}$, and a reflection across the x-axis is $F_x = \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix}$.
The composition $F_x \circ R(\theta)$ (rotation first) corresponds to the matrix product $F_x R(\theta) = \begin{pmatrix} \cos\theta & -\sin\theta \\ -\sin\theta & -\cos\theta \end{pmatrix}$.
The composition $R(\theta) \circ F_x$ (reflection first) corresponds to $R(\theta) F_x = \begin{pmatrix} \cos\theta & \sin\theta \\ \sin\theta & -\cos\theta \end{pmatrix}$.
For these two operations to be commutative, the resulting matrices must be identical. Equating them, we find the condition $-\sin\theta = \sin\theta$, which implies $\sin\theta = 0$. This occurs when $\theta = n\pi$ for any integer $n$. Thus, rotation and x-axis reflection commute only when the rotation is by a multiple of 180 degrees, which effectively leaves the x-axis invariant [@problem_id:2154027].

### An Advanced View: Symmetry, Functions, and Linear Transformations

The concept of reflection is deeply connected to the mathematical ideas of symmetry, functions, and linear algebra.

A geometric object is said to be symmetric with respect to a line if it is invariant under reflection across that line. For a **level set** of a function, defined by $f(x, y) = c$, this [geometric symmetry](@entry_id:189059) translates into an algebraic property of the function $f$. A [level set](@entry_id:637056) is symmetric with respect to the x-axis if, for every point $(x, y)$ on the curve, the point $(x, -y)$ is also on the curve. This means that if $f(x, y) = c$, then we must also have $f(x, -y) = c$. For this to hold for *any* [level set](@entry_id:637056), the function itself must satisfy the property $f(x, y) = f(x, -y)$ for all $(x, y)$ in its domain. Such a function is called an **[even function](@entry_id:164802)** with respect to the variable $y$.

We can systematically construct functions with this symmetry property from an arbitrary function $g(x, y)$. For example, the functions $f(x, y) = g(x, y) \cdot g(x, -y)$ and $f(x, y) = g(x, y) + g(x, -y)$ are always even in $y$, and thus their [level sets](@entry_id:151155) will always be symmetric with respect to the x-axis [@problem_id:2154065].

In the language of linear algebra, transformations in the plane that fix the origin can be represented by $2 \times 2$ matrices. Reflections across lines through the origin are [linear transformations](@entry_id:149133).
- Reflection across x-axis: $R_x = \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix}$
- Reflection across y-axis: $R_y = \begin{pmatrix} -1 & 0 \\ 0 & 1 \end{pmatrix}$
- Reflection across a line making an angle $\theta$ with the positive x-axis: $T = \begin{pmatrix} \cos(2\theta) & \sin(2\theta) \\ \sin(2\theta) & -\cos(2\theta) \end{pmatrix}$

The [composition of linear transformations](@entry_id:149867) corresponds to [matrix multiplication](@entry_id:156035). The composition of two reflections is particularly revealing. Let's analyze the composition $S = T \circ R_x$, where $R_x$ is reflection across the x-axis and $T$ is reflection across a line at angle $\theta$ [@problem_id:2154061]. The resulting matrix is:
$S = T R_x = \begin{pmatrix} \cos(2\theta) & \sin(2\theta) \\ \sin(2\theta) & -\cos(2\theta) \end{pmatrix} \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix} = \begin{pmatrix} \cos(2\theta) & -\sin(2\theta) \\ \sin(2\theta) & \cos(2\theta) \end{pmatrix}$
This resulting matrix is the [standard matrix](@entry_id:151240) for a counter-clockwise rotation by an angle of $2\theta$. This confirms a fundamental theorem of geometry: the composition of two reflections across intersecting lines is a rotation about their intersection point by twice the angle between them.

The **eigenvalues** and **eigenvectors** of a transformation matrix reveal its intrinsic geometric properties. An eigenvector is a vector whose direction is unchanged by the transformation, and its corresponding eigenvalue is the factor by which it is scaled. For a reflection matrix, vectors lying on the axis of reflection are unchanged (eigenvalue $\lambda = 1$), while vectors perpendicular to the axis are inverted (eigenvalue $\lambda = -1$). For the rotation matrix $S$ we derived above, the eigenvalues are the roots of the [characteristic equation](@entry_id:149057) $\lambda^2 - 2\lambda\cos(2\theta) + 1 = 0$. The solutions are $\lambda = \cos(2\theta) \pm i \sin(2\theta)$, or $\exp(\pm i 2\theta)$ in complex notation. The fact that the eigenvalues are complex and not real indicates that the transformation (a rotation) does not have any invariant lines in the real plane, unless the rotation is by a multiple of $180^\circ$. This linear algebraic perspective provides a powerful, abstract framework for understanding the deep geometric truths governing reflections and their compositions.