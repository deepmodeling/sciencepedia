## Introduction
The reflection of a point across a plane is a fundamental transformation in [analytic geometry](@entry_id:164266), serving as a conceptual and computational cornerstone in numerous scientific and technical fields. From creating realistic virtual environments in [computer graphics](@entry_id:148077) to understanding [wave propagation](@entry_id:144063) in physics and crystal structures in materials science, the ability to mathematically describe a mirror image is essential. This article addresses the core problem of how to precisely define and calculate the coordinates of a reflected point, bridging the gap between intuitive geometric ideas and their rigorous algebraic formulations.

This article will guide you through the complete theory and application of planar reflection. In "Principles and Mechanisms," you will learn the foundational geometric rules and derive the powerful vector and coordinate-based formulas for reflection. Next, "Applications and Interdisciplinary Connections" will demonstrate how this single operation solves practical problems in optics, provides deep insights into physical laws via the method of images, and describes [fundamental symmetries](@entry_id:161256) in the material world. Finally, the "Hands-On Practices" section will allow you to solidify your understanding by working through targeted computational exercises.

## Principles and Mechanisms

The reflection of a point across a plane is a fundamental transformation in [analytic geometry](@entry_id:164266) with profound implications in fields ranging from computer graphics and robotics to physics and materials science. This chapter delves into the principles governing this transformation, establishing its geometric foundations, deriving its algebraic and vector formulations, and exploring its properties and applications.

### The Fundamental Geometry of Reflection

At its core, a [geometric reflection](@entry_id:635628) is an operation that creates a mirror image. For any point $P$ in three-dimensional space and a given plane of reflection $\Pi$, its reflection is a unique point $P'$. The relationship between $P$, $P'$, and $\Pi$ is defined by two simple yet powerful geometric rules:

1.  The line segment connecting the point $P$ and its reflection $P'$ is **perpendicular** to the plane of reflection $\Pi$.
2.  The **midpoint** of the line segment $PP'$ lies on the plane of reflection $\Pi$.

These two conditions are sufficient to uniquely determine the reflection of a point, or conversely, to define the plane of reflection if a point and its image are known. For instance, in optical engineering or robotics simulations, one might need to determine the precise location and orientation of a mirror. If a control point $P$ is at a known location and its [virtual image](@entry_id:175248) $P'$ is observed at another location, these two principles allow us to find the equation of the mirror plane [@problem_id:2153799] [@problem_id:2153854].

Let us formalize this. The first principle implies that the vector $\vec{PP'} = P' - P$ is parallel to the **[normal vector](@entry_id:264185)** $\vec{n}$ of the plane $\Pi$. The [normal vector](@entry_id:264185) is a vector perpendicular to the plane, and its components $(a, b, c)$ are the coefficients in the plane's standard equation, $ax + by + cz = d$. The second principle states that the midpoint $M = \frac{P+P'}{2}$ must satisfy the equation of the plane.

Consider an example where a point light source is at $P_1 = (3, 5, 2)$ and its [virtual image](@entry_id:175248) in a mirror is at $P_2 = (-5, -11, 18)$. To find the equation of the [mirror plane](@entry_id:148117):
-   A [normal vector](@entry_id:264185) $\vec{n}$ to the plane is given by the [displacement vector](@entry_id:262782) $\vec{P_1P_2}$:
    $\vec{n} = P_2 - P_1 = (-5-3, -11-5, 18-2) = (-8, -16, 16)$. We can simplify this vector by dividing by its [greatest common divisor](@entry_id:142947), $-8$, to get a parallel vector $(1, 2, -2)$, which also serves as a normal vector.
-   The midpoint $M$ of the segment $P_1P_2$ must lie on the plane:
    $M = \frac{P_1+P_2}{2} = \left(\frac{3-5}{2}, \frac{5-11}{2}, \frac{2+18}{2}\right) = (-1, -3, 10)$.
-   The [equation of a plane](@entry_id:151332) with normal $\vec{n}=(a,b,c)$ passing through a point $M=(x_0, y_0, z_0)$ is $a(x-x_0) + b(y-y_0) + c(z-z_0) = 0$. Using $\vec{n}=(1, 2, -2)$ and $M=(-1, -3, 10)$, we have:
    $1(x - (-1)) + 2(y - (-3)) - 2(z - 10) = 0$
    $x + 1 + 2y + 6 - 2z + 20 = 0$
    $x + 2y - 2z = -27$.
This equation precisely defines the mirror plane.

### A Vector-Based Approach to Reflection

While the geometric approach is intuitive, a more powerful and generalizable method uses vector algebra. Let's first consider the case of a plane passing through the origin, which simplifies the analysis. Such a plane is defined by the equation $\vec{r} \cdot \vec{n} = 0$, where $\vec{n}$ is the normal vector and $\vec{r}$ is the [position vector](@entry_id:168381) of any point on the plane.

Any vector $\vec{p}$ (representing the position of a point $P$) can be decomposed into two orthogonal components: one parallel to the [normal vector](@entry_id:264185) $\vec{n}$, and one perpendicular to it (i.e., lying in the plane).
Let $\vec{p}_{\parallel}$ be the component of $\vec{p}$ parallel to $\vec{n}$, and $\vec{p}_{\perp}$ be the component perpendicular to $\vec{n}$. Then, $\vec{p} = \vec{p}_{\parallel} + \vec{p}_{\perp}$.

The component parallel to $\vec{n}$ is found using the vector [projection formula](@entry_id:152164):
$$ \vec{p}_{\parallel} = \text{proj}_{\vec{n}}(\vec{p}) = \frac{\vec{p} \cdot \vec{n}}{\vec{n} \cdot \vec{n}} \vec{n} $$
The component perpendicular to $\vec{n}$ is then simply:
$$ \vec{p}_{\perp} = \vec{p} - \vec{p}_{\parallel} $$
The act of reflection preserves the component lying within the plane ($\vec{p}_{\perp}$) and inverts the component that is normal to the plane ($\vec{p}_{\parallel}$). Therefore, the position vector of the reflected point, $\vec{p}'$, is given by:
$$ \vec{p}' = \vec{p}_{\perp} - \vec{p}_{\parallel} $$
Substituting the expression for $\vec{p}_{\perp}$, we get:
$$ \vec{p}' = (\vec{p} - \vec{p}_{\parallel}) - \vec{p}_{\parallel} = \vec{p} - 2\vec{p}_{\parallel} $$
This leads to the elegant and fundamental formula for reflection across a plane through the origin [@problem_id:2153827]:
$$ \vec{p}' = \vec{p} - 2 \frac{\vec{p} \cdot \vec{n}}{\vec{n} \cdot \vec{n}} \vec{n} $$
Note that if $\vec{n}$ is a **[unit normal vector](@entry_id:178851)** (i.e., $\|\vec{n}\| = \sqrt{\vec{n} \cdot \vec{n}} = 1$), the formula simplifies to $\vec{p}' = \vec{p} - 2(\vec{p} \cdot \vec{n})\vec{n}$.

### The General Formula for Reflection

We can extend this vector-based approach to any arbitrary plane, not just those passing through the origin. Consider a general plane defined by the equation $ax + by + cz + d = 0$. The normal vector is $\vec{n} = (a, b, c)$. Let the point to be reflected be $P(x_0, y_0, z_0)$.

The line connecting $P$ to its reflection $P'(x', y', z')$ must be parallel to the [normal vector](@entry_id:264185) $\vec{n}$. This means the position vector of $P'$ can be expressed as:
$$ \vec{P'} = \vec{P} + k\vec{n} $$
for some scalar $k$. In coordinate form, this is:
$$ x' = x_0 + ka, \quad y' = y_0 + kb, \quad z' = z_0 + kc $$

The midpoint $M$ of the segment $PP'$ must lie on the plane. The coordinates of $M$ are:
$$ M = \frac{P+P'}{2} = \left( \frac{x_0+x'}{2}, \frac{y_0+y'}{2}, \frac{z_0+z'}{2} \right) = \left( x_0+\frac{ka}{2}, y_0+\frac{kb}{2}, z_0+\frac{kc}{2} \right) $$
Since $M$ is on the plane, its coordinates must satisfy the plane's equation:
$$ a\left(x_0+\frac{ka}{2}\right) + b\left(y_0+\frac{kb}{2}\right) + c\left(z_0+\frac{kc}{2}\right) + d = 0 $$
Solving for $k$, we rearrange the terms:
$$ (ax_0 + by_0 + cz_0 + d) + \frac{k}{2}(a^2+b^2+c^2) = 0 $$
$$ k = -2 \frac{ax_0 + by_0 + cz_0 + d}{a^2+b^2+c^2} $$
The quantity $ax_0 + by_0 + cz_0 + d$ is proportional to the signed distance from the point $P$ to the plane, and $a^2+b^2+c^2 = \|\vec{n}\|^2$ is the squared magnitude of the normal vector.

Substituting this value of $k$ back into the equations for $x', y', z'$ gives the complete coordinate-based formula for reflection [@problem_id:2153842]:
$$ x' = x_0 - 2a \frac{ax_0 + by_0 + cz_0 + d}{a^2+b^2+c^2} $$
$$ y' = y_0 - 2b \frac{ax_0 + by_0 + cz_0 + d}{a^2+b^2+c^2} $$
$$ z' = z_0 - 2c \frac{ax_0 + by_0 + cz_0 + d}{a^2+b^2+c^2} $$

This formula is indispensable in applications such as satellite tracking, where the position of a virtual signal source must be calculated. For a satellite at $P=(10, -5, 8)$ reflecting off a plane $2x+y-2z=15$ (or $2x+y-2z-15=0$), we have $\vec{n}=(2, 1, -2)$, $d=-15$, and $\|\vec{n}\|^2 = 2^2+1^2+(-2)^2=9$. The scalar quantity $ax_0+by_0+cz_0+d$ is $2(10)+1(-5)-2(8)-15 = -16$. Thus, $k = -2(-16)/9 = 32/9$. The virtual source $P'$ is located at $P' = P + \frac{32}{9}\vec{n} = (10, -5, 8) + \frac{32}{9}(2, 1, -2) = (\frac{154}{9}, -\frac{13}{9}, \frac{8}{9})$ [@problem_id:2153820].

### Core Properties and Applications of Reflection

#### Isometry and the Reflection Principle

A key property of reflection is that it is an **isometry**, meaning it preserves distances. For any two points $P_1$ and $P_2$, the distance between them is equal to the distance between their reflections, $P'_1$ and $P'_2$. That is, $d(P_1, P_2) = d(P'_1, P'_2)$ [@problem_id:2153819].

A more specific consequence, which gives rise to a powerful problem-solving technique known as the **reflection principle**, is that for any point $Q$ on the plane of reflection $\Pi$, the distance from $Q$ to a point $P$ is equal to the distance from $Q$ to its reflection $P'$.
$$ d(Q, P) = d(Q, P') \quad \text{for all } Q \in \Pi $$
This can be proven by considering the two right triangles formed by the points $P, P'$, their midpoint $M$, and any point $Q$ on the plane. Both triangles share a side $QM$, and the sides $PM$ and $P'M$ are equal in length. The angles at $M$ are right angles, so by the Pythagorean theorem, $\|QP\|^2 = \|QM\|^2 + \|MP\|^2 = \|QM\|^2 + \|MP'\|^2 = \|QP'\|^2$.

#### The Principle of Minimum Path Length

This property is the foundation for solving a class of optimization problems involving path length minimization. It is the geometric basis for **Fermat's Principle of Least Time** in optics, which states that light traveling between two points takes the path that requires the shortest time. For reflection from a flat surface, this corresponds to the shortest distance.

Consider a light ray traveling from a source $P$ to a point $R$ by reflecting off a [mirror plane](@entry_id:148117) $\Pi$ at some point $Q$. The total path length is $L = d(P, Q) + d(Q, R)$. Using the [reflection principle](@entry_id:148504), we can replace $d(Q, R)$ with $d(Q, R')$, where $R'$ is the reflection of $R$ across the plane. The path length becomes $L = d(P, Q) + d(Q, R')$. The [shortest distance between two points](@entry_id:162983) ($P$ and $R'$) is a straight line. Therefore, the minimum path length is achieved when the reflection point $Q$ lies on the straight line segment connecting $P$ and $R'$. This minimum path length is simply the Euclidean distance $d(P, R')$. The actual point of reflection on the mirror is the intersection of the line segment $PR'$ with the plane $\Pi$ [@problem_id:2153863].

This "unfolding" technique is remarkably effective and can be applied sequentially to problems involving multiple reflections. For a path from point $S$ to $D$ reflecting first off plane $\Pi_1$ and then off plane $\Pi_2$, the path length is minimized by first reflecting $D$ across $\Pi_2$ to get $D'$, and then reflecting this new point $D'$ across $\Pi_1$ to get $D''$. The minimum total path length is the straight-line distance $d(S, D'')$.

### Reflection as a Linear Transformation

When the plane of reflection passes through the origin, the reflection mapping $T(\vec{p}) = \vec{p}'$ is a **[linear transformation](@entry_id:143080)**. This allows us to analyze it using the powerful tools of linear algebra, such as [eigenvalues and eigenvectors](@entry_id:138808). An **eigenvector** of a linear transformation is a non-zero vector that changes by only a scalar factor when that [linear transformation](@entry_id:143080) is applied to it. This factor is known as the **eigenvalue**. The equation for an eigenvector $\vec{v}$ and its corresponding eigenvalue $\lambda$ is $T(\vec{v}) = \lambda\vec{v}$.

For a reflection across a plane $P$ through the origin, we can identify the eigenvalues and their corresponding **eigenspaces** (the set of all eigenvectors for a given eigenvalue, plus the zero vector) by geometric reasoning [@problem_id:2153850]:

1.  **Eigenvalue $\lambda = 1$**: Any vector $\vec{v}$ that lies *within* the plane of reflection $P$ is unchanged by the reflection. For such a vector, $T(\vec{v}) = \vec{v}$. This means it is an eigenvector with an eigenvalue of $1$. The set of all such vectors is the plane $P$ itself. Thus, the reflection transformation has an eigenvalue of $1$, and its corresponding eigenspace is the two-dimensional plane of reflection.

2.  **Eigenvalue $\lambda = -1$**: Any vector $\vec{v}$ that is *normal* to the plane of reflection (i.e., parallel to the [normal vector](@entry_id:264185) $\vec{n}$) is exactly reversed in direction. For such a vector, $T(\vec{v}) = -\vec{v}$. This means it is an eigenvector with an eigenvalue of $-1$. The set of all such vectors forms the one-dimensional line passing through the origin and parallel to $\vec{n}$. Thus, the transformation also has an eigenvalue of $-1$, with its corresponding eigenspace being the one-dimensional line normal to the plane.

These two [eigenspaces](@entry_id:147356) span the entire $\mathbb{R}^3$ space ($\mathbb{R}^3 = P \oplus P^{\perp}$), providing a complete and intuitive geometric characterization of the reflection transformation.

### Composition of Reflections: From Mirrors to Rotations

A fascinating result emerges when we compose transformations. What is the net effect of performing one reflection followed by another? While a single reflection is an orientation-reversing isometry, the composition of two reflections is an orientation-preserving isometry, which in three dimensions corresponds to a rotation or a translation.

Consider the case of two distinct planes, $\Pi_1$ and $\Pi_2$, that intersect and pass through the origin. Let their respective normal vectors be $\vec{n}_1$ and $\vec{n}_2$. A reflection across $\Pi_1$ followed by a reflection across $\Pi_2$ is equivalent to a single rotation [@problem_id:2153828]. The properties of this rotation are determined by the geometry of the two planes:

-   **Axis of Rotation**: The axis of the equivalent rotation is the line of intersection of the two planes, $\Pi_1 \cap \Pi_2$. Any vector lying on this line is in both planes, so it remains unchanged by both reflections. It is therefore invariant under the composite transformation, defining the rotation axis. The direction vector for this axis can be found by taking the cross product of the normal vectors: $\vec{u} = \vec{n}_1 \times \vec{n}_2$.

-   **Angle of Rotation**: The angle of rotation, $\theta$, is twice the angle, $\phi$, between the two planes. The angle $\phi$ between the planes is defined as the acute angle between their normal vectors, which can be found using the dot product: $\cos(\phi) = \frac{|\vec{n}_1 \cdot \vec{n}_2|}{\|\vec{n}_1\| \|\vec{n}_2\|}$. The rotation angle is then $\theta = 2\phi$.

For example, if two planes are orthogonal ($\phi = \frac{\pi}{2}$), the composite transformation is a rotation by $\theta = \pi$, which is a half-turn or point reflection through the axis of rotation. This powerful principle connects two fundamental geometric operations and is a cornerstone of the study of [symmetry groups](@entry_id:146083) and [geometric algebra](@entry_id:201205).