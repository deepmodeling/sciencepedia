## Introduction
In three-dimensional geometry, precisely locating points and understanding their relationships is essential. While vectors allow us to define points and directions, a common challenge is to find the coordinates of a point that lies along a specific path between two other points. This article addresses this fundamental problem by developing the [section formula](@entry_id:163285), an algebraic tool for dividing a line segment in a given ratio. This powerful concept serves as a bridge between simple geometry and complex applications in physics and engineering.

This article is structured to build your understanding progressively. In "Principles and Mechanisms," you will learn the derivation of the [section formula](@entry_id:163285) for both internal and [external division](@entry_id:165030), explore its connection to the [parametric equation of a line](@entry_id:178852), and see its generalization to physical concepts like the center of mass. Next, "Applications and Interdisciplinary Connections" will demonstrate the formula's utility in solving real-world problems, from finding the centroids of geometric figures to determining the intersection points of lines with planes and [quadric surfaces](@entry_id:264390). Finally, "Hands-On Practices" will allow you to solidify your knowledge by working through guided problems that reinforce these core concepts.

## Principles and Mechanisms

In our exploration of three-dimensional geometry, the ability to describe and analyze the relationships between points is fundamental. Having established the use of vectors to represent points in space, we now turn to a foundational concept: the [division of a line segment](@entry_id:165429). This chapter develops the **[section formula](@entry_id:163285)**, a powerful tool for determining the coordinates of a point that divides a line segment in a given ratio. We will see that this simple idea has profound implications, connecting to the [parametric representation](@entry_id:173803) of lines, the physical concept of the center of mass, and even the fundamental properties of geometric transformations.

### The Vector Parametrization of a Line Segment

Consider two distinct points in three-dimensional space, $A$ and $B$, with [position vectors](@entry_id:174826) $\vec{p}_A = (x_A, y_A, z_A)$ and $\vec{p}_B = (x_B, y_B, z_B)$, respectively. The straight line segment connecting these two points can be thought of as a path from $A$ to $B$. The direction and length of this path are captured by the [displacement vector](@entry_id:262782), $\vec{p}_B - \vec{p}_A$.

Any point $P$ on the infinite line passing through $A$ and $B$ can be reached by starting at $A$ and moving some distance along the direction of the [displacement vector](@entry_id:262782). This intuition is formalized by the **parametric [vector equation of a line](@entry_id:172383)**:

$$ \vec{r}(t) = \vec{p}_A + t(\vec{p}_B - \vec{p}_A) $$

Here, $\vec{r}(t)$ is the position vector of a point on the line, and $t$ is a scalar parameter. The value of $t$ determines the position of the point along the line relative to $A$ and $B$. We can rewrite the equation as $\vec{r}(t) = (1-t)\vec{p}_A + t\vec{p}_B$. This form, known as a **[linear interpolation](@entry_id:137092)** or an **[affine combination](@entry_id:276726)**, elegantly expresses any point on the line as a weighted average of the endpoints.

The parameter $t$ has a direct geometric interpretation:
- If $t=0$, $\vec{r}(0) = \vec{p}_A$, so we are at point $A$.
- If $t=1$, $\vec{r}(1) = \vec{p}_B$, so we are at point $B$.
- If $0 \lt t \lt 1$, the point lies on the **line segment** between $A$ and $B$. The value of $t$ represents the fraction of the distance covered when moving from $A$ to $B$.

For example, consider a 3D printing process where a print head moves from a starting point $A$ to an ending point $B$ [@problem_id:2156611]. If the controller determines that the head has completed exactly 40% of its linear path, its position corresponds to $t=0.40$. Its coordinates can be calculated directly using the parametric equation: $\vec{p} = (1-0.4)\vec{p}_A + 0.4\vec{p}_B = 0.6\vec{p}_A + 0.4\vec{p}_B$.

### The Section Formula for Internal Division

While the parameter $t$ is useful, it is often more intuitive to describe the position of a point by the **ratio** in which it divides a segment. Let's say a point $P$ lies on the segment $AB$ and divides it in the ratio $m:n$. This means the ratio of the length of segment $AP$ to the length of segment $PB$ is $m/n$.

$$ \frac{|\vec{AP}|}{|\vec{PB}|} = \frac{m}{n} $$

Since $P$ is between $A$ and $B$, the vectors $\vec{AP}$ and $\vec{PB}$ are in the same direction. We can therefore write the vector relationship $n\vec{AP} = m\vec{PB}$. Expressing this in terms of [position vectors](@entry_id:174826) $\vec{p}_A$, $\vec{p}_B$, and $\vec{p}$:

$$ n(\vec{p} - \vec{p}_A) = m(\vec{p}_B - \vec{p}) $$

Rearranging this equation to solve for $\vec{p}$ gives the celebrated **[section formula](@entry_id:163285)** for internal division:

$$ \vec{p} = \frac{n\vec{p}_A + m\vec{p}_B}{m+n} $$

This formula expresses the [position vector](@entry_id:168381) of the dividing point $P$ as a weighted average of the endpoint vectors, where the weights are determined by the division ratio. In coordinate form, the coordinates $(x, y, z)$ of point $P$ are:

$$ x = \frac{nx_A + mx_B}{m+n}, \quad y = \frac{ny_A + my_B}{m+n}, \quad z = \frac{nz_A + mz_B}{m+n} $$

A common and important special case of internal division is finding the **midpoint** of a segment. Here, the point divides the segment into two equal halves, so the ratio is $1:1$. Substituting $m=1$ and $n=1$ into the [section formula](@entry_id:163285) yields the [midpoint formula](@entry_id:166676):

$$ \vec{p}_M = \frac{\vec{p}_A + \vec{p}_B}{2} $$

For instance, the geometric center of a cube is the midpoint of any of its space diagonals. Given two opposite vertices $A$ and $B$, the center's coordinates can be found instantly using this formula [@problem_id:2156585].

The connection between the [parametric form](@entry_id:176887) and the ratio-based [section formula](@entry_id:163285) is direct. By setting the parameter $t = \frac{m}{m+n}$, the parametric equation $\vec{r}(t) = (1-t)\vec{p}_A + t\vec{p}_B$ becomes identical to the [section formula](@entry_id:163285). This confirms that a point dividing a segment in the ratio $m:n$ is located a fractional distance $t = m/(m+n)$ from the starting point. This is useful in problems where ratios are given implicitly, such as by time intervals for constant-velocity travel [@problem_id:2156587].

The [section formula](@entry_id:163285) can also be used in reverse. If we know the coordinates of three collinear points $A$, $P$, and $B$, we can determine the ratio in which $P$ divides the segment $AB$. By equating one of the coordinate formulas, say for $x$, with the known coordinate of $P$, we can solve for the ratio $m:n$ (or more simply, the value $k = m/n$) [@problem_id:2156625]. Verifying this ratio holds for the other coordinates confirms the calculation.

### External Division, Collinearity, and a Unified Framework

The concept of dividing a line can be extended to points that lie on the infinite line passing through $A$ and $B$, but *outside* the segment $AB$. This is called **[external division](@entry_id:165030)**.

If a point $P$ divides the segment $AB$ externally in the ratio $m:n$, it means that $P$ lies on the line such that the ratio of its distances from $A$ and $B$ is still $|\vec{AP}|/|\vec{PB}| = m/n$. However, if $P$ is on the side of $B$, the vector $\vec{AP}$ is in the same direction as $\vec{PB}$, but longer. If $P$ is on the side of $A$, $\vec{AP}$ is in the opposite direction. A careful derivation for the external point leads to a similar formula, but with a crucial sign change:

$$ \vec{p} = \frac{m\vec{p}_B - n\vec{p}_A}{m-n} $$

This formula can be used to find the coordinates of an external dividing point given a ratio, for example, $5:3$ as in problem [@problem_id:2156602].

The existence of two separate formulas for internal and [external division](@entry_id:165030) can be cumbersome. We can unify them using the [parametric representation](@entry_id:173803) $\vec{r}(t) = (1-t)\vec{p}_A + t\vec{p}_B$. As we've seen, $t \in (0,1)$ corresponds to internal division. What about other values of $t$?
- If $t > 1$, the point $P$ lies on the line beyond $B$.
- If $t  0$, the point $P$ lies on the line beyond $A$.
In both cases, $P$ is an external point.

This leads to a more sophisticated and unified view of the division ratio. Let's define a single ratio $k$ such that $\vec{AP} = k\vec{PB}$. This vector equation accounts for both magnitude and direction.
- If $P$ is between $A$ and $B$, $\vec{AP}$ and $\vec{PB}$ have the same direction, so $k > 0$. The ratio is $k:1$.
- If $P$ is outside the segment $AB$, $\vec{AP}$ and $\vec{PB}$ have opposite directions, so $k  0$.

Solving $\vec{p} - \vec{p}_A = k(\vec{p}_B - \vec{p})$ for $\vec{p}$ yields a single, universal [section formula](@entry_id:163285):

$$ \vec{p} = \frac{\vec{p}_A + k\vec{p}_B}{1+k} $$

This formula holds for both internal ($k > 0$) and external ($k  0$) division. The parameter $t$ from our original vector equation and this ratio $k$ are related by $k = \frac{t}{1-t}$ and $t = \frac{k}{1+k}$ [@problem_id:2156628].

This unified framework provides a powerful test for **collinearity**. Three distinct points $P, Q, R$ are collinear if and only if one divides the segment formed by the other two. For example, to check if $Q$ lies on the line through $P$ and $R$, we can assume it does and solve for the ratio $k$ in which $Q$ divides $PR$. If we find a consistent value of $k$ that satisfies the equation for all three coordinates, the points are indeed collinear [@problem_id:2156575].

### Physical and Geometric Generalizations

The [section formula](@entry_id:163285) is not just an abstract geometric tool; it is the mathematical backbone for important physical concepts and reveals deep geometric truths.

#### Center of Mass

In physics, the **center of mass** of a [system of particles](@entry_id:176808) is the unique point where the weighted average of the [position vectors](@entry_id:174826) of the particles is zero. For a simple system of two point masses, $m_A$ at position $\vec{p}_A$ and $m_B$ at position $\vec{p}_B$, the position vector of the center of mass, $\vec{r}_{CM}$, is given by:

$$ \vec{r}_{CM} = \frac{m_A\vec{p}_A + m_B\vec{p}_B}{m_A + m_B} $$

This formula is mathematically identical to the [section formula](@entry_id:163285) [@problem_id:2156607]. By comparing the two, we see that the center of mass divides the line segment connecting the two masses in the ratio $m_B : m_A$. That is, the center of mass is closer to the heavier object. This provides a tangible, physical interpretation of the abstract concept of a weighted average.

This principle extends from discrete masses to continuous objects. For a rigid rod with non-uniform [linear mass density](@entry_id:276685) $\lambda$, the summations in the center of mass formula become integrals. The position of the center of mass is found by integrating the position vector $\vec{r}$ weighted by the mass element $dm = \lambda ds$ over the entire length of the rod:

$$ \vec{r}_{CM} = \frac{\int \vec{r} \, dm}{\int dm} = \frac{\int \vec{r}(t) \lambda(t) \, L \, dt}{\int \lambda(t) \, L \, dt} $$

where $t$ is the fractional distance along the rod. Solving this integral for a given density function, such as an exponential variation, yields the precise location of the center of mass, generalizing the [section formula](@entry_id:163285) to a continuous domain [@problem_id:2156626].

#### Affine Invariance

Perhaps the most profound property of the [section formula](@entry_id:163285) is its invariance under a class of [geometric transformations](@entry_id:150649) known as **affine transformations**. An affine transformation $T$ is a combination of a [linear transformation](@entry_id:143080) (represented by a matrix $A$) and a translation (represented by a vector $\vec{c}$): $T(\vec{v}) = A\vec{v} + \vec{c}$. Such transformations can rotate, scale, shear, and translate space, but they preserve two key properties: [collinearity](@entry_id:163574) (points on a line remain on a line) and, crucially, ratios of distances along a line.

Consider a point $Q_a$ that divides a segment $P_1P_2$ with a parameter $a$, such that $\vec{q}_a = (1-a)\vec{p}_1 + a\vec{p}_2$. If we apply an affine transformation $T$ to all points, the new [position vector](@entry_id:168381) $\vec{q}'_a$ is:

$$ \vec{q}'_a = T(\vec{q}_a) = A((1-a)\vec{p}_1 + a\vec{p}_2) + \vec{c} $$
$$ \vec{q}'_a = (1-a)(A\vec{p}_1 + \vec{c}) + a(A\vec{p}_2 + \vec{c}) = (1-a)\vec{p}'_1 + a\vec{p}'_2 $$

This remarkable result shows that the transformed point $\vec{q}'_a$ is related to the transformed endpoints $\vec{p}'_1$ and $\vec{p}'_2$ by the exact same [barycentric weights](@entry_id:168528) $(1-a)$ and $a$. This means that the ratio in which a segment is divided is an **[affine invariant](@entry_id:173351)**—it does not change under any affine transformation. Consequently, ratios of lengths of sub-segments along a line are also preserved [@problem_id:2156581]. This invariance highlights that the [section formula](@entry_id:163285) captures a fundamental structural property of Euclidean space, one that is more general than properties that depend on absolute distances or angles, which are only preserved by the more restrictive set of rigid motions (isometries).