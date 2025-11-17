## Introduction
The [general second-degree equation](@entry_id:177618), $Ax^2 + Bxy + Cy^2 + Dx + Ey + F = 0$, is the algebraic key to understanding all [conic sections](@entry_id:175122). While most terms are straightforward to interpret, the presence of the [cross-product term](@entry_id:148190), $Bxy$, complicates the picture, rotating the familiar shapes of ellipses, hyperbolas, and parabolas away from their standard orientations. This rotation obscures their true geometric properties, creating a gap between the complex equation and a clear visual understanding. This article provides a comprehensive guide to bridging that gap by mastering the technique of axis rotation to eliminate the $xy$-term.

In the first chapter, **Principles and Mechanisms**, we will delve into the core mathematics of [coordinate rotation](@entry_id:164444), deriving the fundamental formula to find the necessary angle and exploring the powerful concepts of [rotation invariants](@entry_id:170459) and the elegant linear algebra approach using eigenvalues. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate how this geometric tool is applied not only to classify conics but also to solve real-world problems in physics and engineering, from analyzing the [principal axes of inertia](@entry_id:167151) to simplifying complex dynamical systems. Finally, **Hands-On Practices** will allow you to solidify your understanding by working through guided problems, transforming challenging equations into their standard forms. We begin by establishing the foundational principles of the coordinate transformation that will unlock the geometry hidden within the algebra.

## Principles and Mechanisms

The [general second-degree equation](@entry_id:177618) in two variables, $Ax^2 + Bxy + Cy^2 + Dx + Ey + F = 0$, provides a comprehensive algebraic description of all [conic sections](@entry_id:175122). While terms involving $x^2$, $y^2$, $x$, and $y$ correspond to scaling, orientation, and translation, the presence of a non-zero **[cross-product term](@entry_id:148190)**, $Bxy$, signifies that the principal axes of the conic—its axes of symmetry—are rotated with respect to the standard Cartesian coordinate axes. To simplify the analysis and understand the true geometry of the conic, our primary goal is to perform a coordinate transformation that eliminates this $xy$-term. This is achieved through a rotation of the coordinate system.

### The Transformation of Coordinates by Rotation

Let us consider a Cartesian coordinate system $(x, y)$. We can introduce a new coordinate system $(x', y')$ that shares the same origin but is rotated by a counter-clockwise angle $\theta$ relative to the original system. The relationship between the coordinates of a point in the original system and the new system is given by the rotation equations:

$x = x'\cos\theta - y'\sin\theta$

$y = x'\sin\theta + y'\cos\theta$

Our objective is to find a specific angle $\theta$ such that when these expressions for $x$ and $y$ are substituted into the [general second-degree equation](@entry_id:177618), the resulting equation in terms of $x'$ and $y'$ has no [cross-product term](@entry_id:148190) (i.e., the coefficient of $x'y'$ is zero).

### Determining the Angle of Rotation

Let's focus on the quadratic part of the equation, $Q(x, y) = Ax^2 + Bxy + Cy^2$, as the linear terms and the constant do not affect the rotation angle required to align the axes. Substituting the rotation equations into this [quadratic form](@entry_id:153497), we can expand each term and collect the coefficients of $(x')^2$, $(y')^2$, and $x'y'$. The coefficient of the new [cross-product term](@entry_id:148190), $B'$, is the result of contributions from all three original quadratic terms:

$B' = -2A\sin\theta\cos\theta + B(\cos^2\theta - \sin^2\theta) + 2C\sin\theta\cos\theta$

Using the double-angle identities $\sin(2\theta) = 2\sin\theta\cos\theta$ and $\cos(2\theta) = \cos^2\theta - \sin^2\theta$, we can simplify this expression to:

$B' = (C - A)\sin(2\theta) + B\cos(2\theta)$

To eliminate the cross-term, we must set its coefficient $B'$ to zero:

$(C - A)\sin(2\theta) + B\cos(2\theta) = 0$

Assuming $A \neq C$, we can rearrange this to obtain the fundamental formula for the angle of rotation:

$\tan(2\theta) = \frac{B}{A - C}$

This equation allows us to determine the angle $2\theta$, and subsequently $\theta$, that aligns the coordinate system with the axes of the conic.

For instance, consider the path of a celestial object described by the equation $x^2 - 2\sqrt{3} xy - y^2 + 10x - 10y - 20 = 0$ [@problem_id:2123200]. Here, $A=1$, $B=-2\sqrt{3}$, and $C=-1$. Applying the formula gives:

$\tan(2\theta) = \frac{-2\sqrt{3}}{1 - (-1)} = \frac{-2\sqrt{3}}{2} = -\sqrt{3}$

The [principal value](@entry_id:192761) for $2\theta$ would be $-\frac{\pi}{3}$. However, since the tangent function has a period of $\pi$, possible values for $2\theta$ are $-\frac{\pi}{3} + k\pi$ for any integer $k$. To find the smallest positive angle $\theta$, we can choose $k=1$, which gives $2\theta = \frac{2\pi}{3}$, and thus $\theta = \frac{\pi}{3}$ or $60^\circ$. Once this angle is found, the explicit transformation equations can be written. For an ellipse given by $7x^2 - 6\sqrt{3}xy + 13y^2 = 64$ [@problem_id:2123172], the required angle is $\theta=\frac{\pi}{6}$, leading to the transformation $x = \frac{\sqrt{3}x' - y'}{2}$ and $y = \frac{x' + \sqrt{3}y'}{2}$.

It is important to note that if $\theta_0$ is a valid angle of rotation, then so is $\theta_0 + \frac{\pi}{2}$. Geometrically, this corresponds to simply swapping the $x'$ and $y'$ axes, which naturally also results in an equation with no cross-term. This property arises from the $\pi$-[periodicity](@entry_id:152486) of $\tan(2\theta)$ [@problem_id:2123147].

A particularly insightful special case occurs when $A=C$. The formula for $\tan(2\theta)$ becomes undefined. Returning to the condition for $B'=0$, if $A=C$, the equation simplifies to $B\cos(2\theta) = 0$. Assuming $B \neq 0$, this implies $\cos(2\theta) = 0$. The smallest positive solution for $2\theta$ is $\frac{\pi}{2}$, which means $\theta = \frac{\pi}{4}$ or $45^\circ$. This means that any conic section whose $x^2$ and $y^2$ coefficients are equal is simply rotated by $45^\circ$ from its standard orientation [@problem_id:2123144].

### Invariants Under Rotation

While the coefficients $A, B, C$ change under rotation, certain combinations of these coefficients remain constant. These **invariants** are powerful tools for analysis, as they reveal properties of the conic that are independent of the coordinate system's orientation.

The most important invariant is the **[discriminant](@entry_id:152620)**, defined as $B^2 - 4AC$. It can be shown that for any rotation, $(B')^2 - 4A'C' = B^2 - 4AC$ [@problem_id:2123199]. In our simplified system, we have specifically chosen the rotation such that $B' = 0$. This leads to a crucial relationship:

$B^2 - 4AC = -4A'C'$

The sign of the [discriminant](@entry_id:152620) is therefore determined by the product $A'C'$. This allows us to classify the conic section *before* performing any rotation:
- If $B^2 - 4AC  0$, then $A'C' > 0$, meaning $A'$ and $C'$ have the same sign. This corresponds to an **ellipse** (or a circle if $A'=C'$).
- If $B^2 - 4AC = 0$, then $A'C' = 0$, meaning either $A'$ or $C'$ is zero. This corresponds to a **parabola**.
- If $B^2 - 4AC > 0$, then $A'C'  0$, meaning $A'$ and $C'$ have opposite signs. This corresponds to a **hyperbola**.

For the celestial object path in [@problem_id:2123200], with $A=1$, $B=-2\sqrt{3}$, and $C=-1$, the [discriminant](@entry_id:152620) is $B^2 - 4AC = (-2\sqrt{3})^2 - 4(1)(-1) = 12 + 4 = 16$. Since $16 > 0$, the trajectory is a hyperbola.

Another important invariant is the **trace** of the quadratic part, $A+C$. Under rotation, the sum of the coefficients of the squared terms is preserved:

$A' + C' = A + C$

This provides a quick check on calculations. For example, for an elliptical film described by $13x^2 + 10xy + 13y^2 = 72$ [@problem_id:2123208], we immediately know that in the rotated system $A'(x')^2 + C'(y')^2 = 72$, the sum of the new coefficients must be $A' + C' = 13 + 13 = 26$.

### The Linear Algebra Perspective: Eigenvalues and Eigenvectors

The process of eliminating the $xy$-term can be framed most elegantly using linear algebra. The quadratic form $Ax^2 + Bxy + Cy^2$ can be written in matrix notation as $\mathbf{x}^T M \mathbf{x}$, where $\mathbf{x} = \begin{pmatrix} x \\ y \end{pmatrix}$ and $M$ is a [symmetric matrix](@entry_id:143130):

$M = \begin{pmatrix} A  B/2 \\ B/2  C \end{pmatrix}$

A rotation of coordinates is a [change of basis](@entry_id:145142), $\mathbf{x} = R \mathbf{x}'$, where $R$ is an orthogonal [rotation matrix](@entry_id:140302). The [quadratic form](@entry_id:153497) in the new coordinates becomes $(\mathbf{x}')^T (R^T M R) \mathbf{x}'$. The task of eliminating the cross-term is precisely the task of diagonalizing the matrix $M$. The Spectral Theorem guarantees that any real [symmetric matrix](@entry_id:143130) can be diagonalized by an [orthogonal matrix](@entry_id:137889).

The resulting diagonal matrix, $M' = R^T M R = \begin{pmatrix} A'  0 \\ 0  C' \end{pmatrix}$, contains the coefficients of the simplified equation. The entries on the diagonal, $A'$ and $C'$, are the **eigenvalues** of the original matrix $M$.

This provides a direct method to find the simplified equation without calculating the rotation angle. One must simply find the eigenvalues of the matrix $M$ by solving the characteristic equation, $\det(M - \lambda I) = 0$.

Consider a stress potential function $\sigma(x, y) = 11x^2 - 24xy + 4y^2$ [@problem_id:2123143]. The associated matrix is $M = \begin{pmatrix} 11  -12 \\ -12  4 \end{pmatrix}$. Its [characteristic equation](@entry_id:149057) is $(11-\lambda)(4-\lambda) - (-12)^2 = \lambda^2 - 15\lambda - 100 = 0$. Solving for $\lambda$ yields the eigenvalues $\lambda = 20$ and $\lambda = -5$. These are the [principal stress](@entry_id:204375) magnitudes, $A'$ and $C'$. The rotated equation is thus $\sigma(x', y') = 20(x')^2 - 5(y')^2$. Similarly, for an equipotential contour $7x^2 + 2\sqrt{6}xy + 8y^2 = 30$ [@problem_id:2123195], the eigenvalues of the associated matrix $M = \begin{pmatrix} 7  \sqrt{6} \\ \sqrt{6}  8 \end{pmatrix}$ are found to be $10$ and $5$. The simplified equation is $10(x')^2 + 5(y')^2 = 30$.

The [rotation invariants](@entry_id:170459) are also beautifully explained in this framework. The trace $A+C$ is the trace of $M$, which is equal to the sum of its eigenvalues, $A'+C'$. The expression $AC - B^2/4$ is the determinant of $M$, which is equal to the product of its eigenvalues, $A'C'$. This confirms the invariance of trace and determinant under rotation.

### Incorporating Translations and Completing the Analysis

When the [general second-degree equation](@entry_id:177618) includes linear terms $Dx + Ey$, the conic is not centered at the origin. A complete simplification requires both a rotation and a translation. For [central conics](@entry_id:168814) (ellipses and hyperbolas), one can first find the center $(x_c, y_c)$ by solving the [system of linear equations](@entry_id:140416) obtained by setting the partial derivatives of the equation with respect to $x$ and $y$ to zero:

$2Ax + By + D = 0$
$Bx + 2Cy + E = 0$

For instance, the center of the ellipse $5x^2 + 6xy + 5y^2 - 12\sqrt{2}x - 20\sqrt{2}y + 24 = 0$ [@problem_id:2123191] is found by solving the system $10x+6y-12\sqrt{2}=0$ and $6x+10y-20\sqrt{2}=0$, which yields the center $(0, 2\sqrt{2})$.

Once the center is found, a translation to this point eliminates the linear terms. A subsequent rotation, as described above, eliminates the cross-term, resulting in a standard form equation.

To perform a full [geometric analysis](@entry_id:157700), such as finding the foci of an ellipse [@problem_id:2123190], one must combine these concepts.
1. Represent the quadratic part with matrix $M$ and find its eigenvalues, $\lambda_1, \lambda_2$, to get the rotated equation form $\lambda_1(x')^2 + \lambda_2(y')^2 = F$.
2. From this, identify the semi-major ($a$) and semi-minor ($b$) axes and calculate the focal distance $c$.
3. Find the **eigenvector** corresponding to the eigenvalue associated with the major axis. This eigenvector gives the direction of the major axis in the original $(x, y)$ coordinate system.
4. The foci are located at a distance $\pm c$ from the center along the direction of this eigenvector.

This multi-step process, integrating [eigenvalue analysis](@entry_id:273168) for rotation with vector calculations for orientation, demonstrates the full power of these techniques in transforming a complex algebraic equation into a clear geometric picture.