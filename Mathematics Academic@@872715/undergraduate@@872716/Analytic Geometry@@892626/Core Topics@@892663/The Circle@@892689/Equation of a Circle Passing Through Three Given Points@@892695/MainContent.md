## Introduction
In [analytic geometry](@entry_id:164266), the circle stands as a figure of fundamental importance. While often defined by its center and radius, a circle can also be uniquely determined by the points it passes through. This article addresses a classic and practical question: how do we find the [equation of a circle](@entry_id:167379) that passes through three given, non-collinear points? This problem bridges the gap between abstract geometric principles and concrete algebraic computation, offering a powerful tool for solving problems across various scientific disciplines.

Over the course of this article, you will gain a comprehensive understanding of this topic. The first chapter, "Principles and Mechanisms," will lay the theoretical groundwork, explaining why three non-collinear points define a unique circle and detailing two robust methods—one algebraic and one geometric—for finding its equation. The second chapter, "Applications and Interdisciplinary Connections," will broaden our perspective, showcasing how this concept is applied in advanced geometry, vector analysis, physics, and complex analysis. Finally, "Hands-On Practices" will provide opportunities to apply these techniques to concrete problems, solidifying your knowledge and building practical skills. We begin by exploring the core principles that govern the existence and uniqueness of such a circle.

## Principles and Mechanisms

In the preceding chapter, we established the circle as a fundamental locus of points in Euclidean geometry. We now transition from its definition to its specification. A central question in [analytic geometry](@entry_id:164266) is: what information is necessary and sufficient to uniquely define a circle? While a center and a radius provide the most direct definition, a circle can also be determined by a set of points through which it must pass. This chapter explores the principles and mechanisms for determining the [equation of a circle](@entry_id:167379) that passes through three given points.

A foundational theorem of geometry states that **a unique circle passes through any three non-collinear points**. This principle is the bedrock of our investigation. The uniqueness arises from the geometric properties of points and distances. The center of any such circle must be equidistant from all three points. The locus of points equidistant from two distinct points, say $P_1$ and $P_2$, is the [perpendicular bisector](@entry_id:176427) of the line segment $\overline{P_1P_2}$. Given three non-collinear points $P_1$, $P_2$, and $P_3$, the circle's center must lie on the [perpendicular bisector](@entry_id:176427) of $\overline{P_1P_2}$ and also on the [perpendicular bisector](@entry_id:176427) of $\overline{P_2P_3}$. Since the points are not collinear, these two bisectors are not parallel and will intersect at exactly one point. This unique intersection point is the **[circumcenter](@entry_id:174510)** of the triangle formed by $P_1$, $P_2$, and $P_3$, and it serves as the center of the unique circle passing through them. The distance from this center to any of the three points is the circle's radius, known as the **circumradius**.

This chapter will detail two primary methods for finding the circle's equation: a direct algebraic substitution method and a more geometric approach based on [perpendicular bisectors](@entry_id:163148). We will also examine special configurations that permit elegant shortcuts and explore the degenerate case of three collinear points.

### The Algebraic Approach: A System of Equations

The most direct method for finding a circle's equation from three points is purely algebraic. We begin with the center-radius form of a circle's equation:
$$(x - h)^2 + (y - k)^2 = r^2$$
where $(h, k)$ are the coordinates of the center and $r$ is the radius. If a circle passes through three given points $(x_1, y_1)$, $(x_2, y_2)$, and $(x_3, y_3)$, then each point's coordinates must satisfy the equation. This yields a system of three equations with three unknowns: $h$, $k$, and $r^2$.

$$(x_1 - h)^2 + (y_1 - k)^2 = r^2$$
$$(x_2 - h)^2 + (y_2 - k)^2 = r^2$$
$$(x_3 - h)^2 + (y_3 - k)^2 = r^2$$

Although this system involves squared terms, it can be readily solved. By setting the left-hand sides of the first two equations equal to each other, we eliminate $r^2$. The same can be done with the first and third equations. This process results in a system of two [linear equations](@entry_id:151487) in the variables $h$ and $k$, which can be solved straightforwardly.

Let us illustrate this with a concrete example. Suppose we must find the center and radius of a circular path traced by a drone, which is known to pass through the points $P_1(-2, 1)$, $P_2(5, 8)$, and $P_3(6, 1)$ [@problem_id:2124123]. Substituting these into the center-radius form gives:

1.  $(-2 - h)^2 + (1 - k)^2 = r^2$
2.  $(5 - h)^2 + (8 - k)^2 = r^2$
3.  $(6 - h)^2 + (1 - k)^2 = r^2$

Equating the expressions for $r^2$ from equations (1) and (3) gives:
$$(-2 - h)^2 + (1 - k)^2 = (6 - h)^2 + (1 - k)^2$$
The $(1 - k)^2$ terms cancel, leaving:
$$(-2 - h)^2 = (6 - h)^2$$
$$4 + 4h + h^2 = 36 - 12h + h^2$$
$$16h = 32 \implies h = 2$$
This simplification occurred because points $P_1$ and $P_3$ have the same $y$-coordinate, meaning the center must lie on their [perpendicular bisector](@entry_id:176427), the vertical line $x = \frac{-2+6}{2} = 2$.

Now, we equate expressions (1) and (2) and substitute $h=2$:
$$(-2 - 2)^2 + (1 - k)^2 = (5 - 2)^2 + (8 - k)^2$$
$$(-4)^2 + (1 - 2k + k^2) = (3)^2 + (64 - 16k + k^2)$$
$$16 + 1 - 2k + k^2 = 9 + 64 - 16k + k^2$$
$$17 - 2k = 73 - 16k$$
$$14k = 56 \implies k = 4$$
The center of the circle is $(h, k) = (2, 4)$. To find the radius squared, we substitute these coordinates back into any of the initial equations. Using equation (3):
$$r^2 = (6 - 2)^2 + (1 - 4)^2 = 4^2 + (-3)^2 = 16 + 9 = 25$$
Thus, the equation of the circle is $(x - 2)^2 + (y - 4)^2 = 25$.

### The Geometric Approach: Perpendicular Bisectors

While the algebraic method is robust, the geometric approach often provides deeper insight and can be computationally simpler, especially when the points exhibit symmetry. This method directly implements the principle that the circle's center is the [circumcenter](@entry_id:174510) of the triangle formed by the three points.

The procedure is as follows:
1.  Select two pairs of the three points (e.g., $P_1, P_2$ and $P_2, P_3$). These form two chords of the circle.
2.  For each chord, determine the equation of its [perpendicular bisector](@entry_id:176427). The [perpendicular bisector](@entry_id:176427) of a segment passes through its midpoint and has a slope that is the negative reciprocal of the segment's slope.
3.  Solve the system of two [linear equations](@entry_id:151487) representing the two [perpendicular bisectors](@entry_id:163148). Their intersection is the center $(h, k)$ of the circle.
4.  Calculate the radius $r$ by finding the distance from the center $(h, k)$ to any of the original three points.

Consider a scenario with seismic sensors at symmetric locations $A(-p, 0)$, $B(p, 0)$, and $C(0, q)$ [@problem_id:2124157]. We seek the coordinates of an epicenter equidistant from all three.
The chord $\overline{AB}$ is horizontal. Its midpoint is $(\frac{-p+p}{2}, \frac{0+0}{2}) = (0, 0)$. The [perpendicular bisector](@entry_id:176427) is a vertical line passing through this midpoint, so its equation is simply $x = 0$. This immediately tells us that the center of the circle has an $x$-coordinate $h=0$.

Next, we find the [perpendicular bisector](@entry_id:176427) of chord $\overline{BC}$. The midpoint of $\overline{BC}$ is $(\frac{p+0}{2}, \frac{0+q}{2}) = (\frac{p}{2}, \frac{q}{2})$. The slope of $\overline{BC}$ is $m_{BC} = \frac{q-0}{0-p} = -\frac{q}{p}$. The slope of the [perpendicular bisector](@entry_id:176427) is therefore $m_{\perp} = \frac{p}{q}$. The equation of this bisector is:
$$y - \frac{q}{2} = \frac{p}{q}\left(x - \frac{p}{2}\right)$$
Since we already know the center lies on the line $x=0$, we substitute $h=0$ into this equation to find $k$:
$$k - \frac{q}{2} = \frac{p}{q}\left(0 - \frac{p}{2}\right) = -\frac{p^2}{2q}$$
$$k = \frac{q}{2} - \frac{p^2}{2q} = \frac{q^2 - p^2}{2q}$$
So the center is $(h, k) = (0, \frac{q^2-p^2}{2q})$. The radius $r$ is the distance from this center to any point, for instance $C(0, q)$:
$$r = \sqrt{(0-0)^2 + \left(q - \frac{q^2-p^2}{2q}\right)^2} = \left|q - \frac{q^2-p^2}{2q}\right| = \left|\frac{2q^2 - (q^2-p^2)}{2q}\right| = \left|\frac{q^2+p^2}{2q}\right|$$
Since $p$ and $q$ are typically positive constants in such problems, $r = \frac{p^2+q^2}{2q}$.

This method's power is also evident in problems with different constraints. For instance, if we know a circle passes through two points $P_1(1, 5)$ and $P_2(7, -1)$ and that its center lies on the line $y=2x$, we can find the center by intersecting the given line with the [perpendicular bisector](@entry_id:176427) of $\overline{P_1P_2}$ [@problem_id:2124111]. The intersection of these two constraints uniquely determines the center, from which the radius is easily found.

### Special Configurations and Efficient Solutions

While the general methods are always applicable for non-collinear points, experienced practitioners learn to recognize special geometric arrangements that allow for significantly faster solutions.

A prominent example is when the three points form a **right-angled triangle**. According to a corollary of Thales's Theorem, the [circumcenter](@entry_id:174510) of a right-angled triangle is always the midpoint of its hypotenuse. The circumradius is half the length of the hypotenuse.

Consider a circle passing through the origin $O(0,0)$, a point on the x-axis $A(a,0)$, and a point on the y-axis $B(0,b)$, where $a, b \neq 0$ [@problem_id:2132620]. The segments $\overline{OA}$ and $\overline{OB}$ lie on the coordinate axes and are thus perpendicular. The triangle $\triangle OAB$ is a right-angled triangle with the right angle at the origin. The hypotenuse is the segment $\overline{AB}$.
The length of the hypotenuse is $\sqrt{(a-0)^2 + (0-b)^2} = \sqrt{a^2+b^2}$.
The radius $r$ of the [circumcircle](@entry_id:165300) is half this length:
$$r = \frac{1}{2}\sqrt{a^2+b^2}$$
The center is the midpoint of the hypotenuse: $(\frac{a}{2}, \frac{b}{2})$. This elegant shortcut avoids the need to set up and solve a full system of equations. For example, if one wanted the area of the circle passing through $(0,0)$, $(L,0)$, and $(0,H)$, the radius would be $r = \frac{1}{2}\sqrt{L^2+H^2}$, and the area would be $\pi r^2 = \frac{\pi}{4}(L^2+H^2)$ [@problem_id:2124172].

For triangles that are not right-angled, another powerful tool from geometry is the **extended sine rule**, which relates the side lengths of a triangle to its circumradius $R$:
$$\frac{a}{\sin A} = \frac{b}{\sin B} = \frac{c}{\sin C} = 2R$$
This can be combined with the formula for the area of a triangle, $\Delta = \frac{1}{2}bc \sin A$, to derive a direct formula for the circumradius:
$$R = \frac{abc}{4\Delta}$$
where $a, b, c$ are the lengths of the triangle's sides and $\Delta$ is its area. This formula is particularly useful in applied contexts, such as locating an earthquake's epicenter, where the distances between stations (the side lengths) might be the primary data [@problem_id:2124180].

### The Degenerate Case: Collinear Points

Our entire discussion has been predicated on the three points being non-collinear. What happens if we attempt to find a circle passing through three points that lie on the same straight line?

Geometrically, the answer is clear. The [perpendicular bisectors](@entry_id:163148) of any two segments on the same line will be parallel to each other. Since [parallel lines](@entry_id:169007) never intersect (in Euclidean geometry), there is no finite [circumcenter](@entry_id:174510), and thus no circle of finite radius can pass through the three points. One might intuitively describe the line itself as a "circle of infinite radius."

Algebra reveals this degeneracy in a formal and elegant way. Let us consider the most [general second-degree equation](@entry_id:177618) for a [conic section](@entry_id:164211) that can represent a circle:
$$A(x^2+y^2) + Dx + Ey + F = 0$$
For this to represent a circle, we require $A \neq 0$. If we divide by $A$, we recover the standard general form $x^2+y^2 + (D/A)x + (E/A)y + (F/A) = 0$.

Suppose we attempt to fit this equation to three collinear points, for example $P_1(-2, 7)$, $P_2(1, 1)$, and $P_3(3, -3)$ [@problem_id:2124133]. Substituting these points into the equation generates a system of three [linear equations](@entry_id:151487) in the four variables $A, D, E, F$. Analysis of this system reveals that the only way for a non-[trivial solution](@entry_id:155162) (i.e., not all coefficients being zero) to exist is if $A=0$.
When $A=0$, the equation degenerates to:
$$Dx + Ey + F = 0$$
This is the [equation of a line](@entry_id:166789). For the specific points given, the solution forces the coefficients to be proportional to $D=2$, $E=1$, $F=-3$, yielding the line $2x+y-3=0$. We can easily verify that all three points lie on this line. Therefore, the algebraic process does not fail; rather, it correctly identifies that the geometric object containing the three points is not a circle ($A \neq 0$) but a line ($A=0$).

This concept can be further illuminated by examining a limiting case. Consider the three points $P_1(0,0)$, $P_2(a,0)$, and $P_3(0,\epsilon)$ for some small, non-zero $\epsilon$ [@problem_id:2124145]. As we saw previously, the center of the circle through these points is $(h, k) = (\frac{a}{2}, \frac{\epsilon}{2})$ and its radius is $r = \frac{1}{2}\sqrt{a^2 + \epsilon^2}$.
Now, let us observe what happens as $\epsilon \to 0$. The point $P_3$ slides down the y-axis toward the origin, making the three points approach [collinearity](@entry_id:163574).
$$\lim_{\epsilon \to 0} (h, k) = \left(\frac{a}{2}, 0\right)$$
$$\lim_{\epsilon \to 0} r = \lim_{\epsilon \to 0} \frac{1}{2}\sqrt{a^2 + \epsilon^2} = \frac{1}{2}\sqrt{a^2} = \frac{a}{2}$$
In the limit, the circle does not vanish or become infinite. It becomes the circle with center $(\frac{a}{2}, 0)$ and radius $\frac{a}{2}$. This is precisely the circle that has the line segment connecting the two distinct [limiting points](@entry_id:163060), $(0,0)$ and $(a,0)$, as its diameter. This limiting behavior provides a sophisticated understanding of the transition between the non-collinear and collinear cases, bridging the gap between a well-defined circle and its ultimate degeneration into a line. It also highlights an important numerical consideration: when three points are nearly collinear, the circumradius can be extremely large, making computations sensitive to small errors in the points' coordinates.