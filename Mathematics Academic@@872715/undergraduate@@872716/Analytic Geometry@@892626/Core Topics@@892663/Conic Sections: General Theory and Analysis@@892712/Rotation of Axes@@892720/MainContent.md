## Introduction
In [analytic geometry](@entry_id:164266), the appearance of a curve is deeply tied to the coordinate system used to describe it. A complex, tilted [conic section](@entry_id:164211) can often be understood more clearly by simply changing our perspective. The rotation of axes is a fundamental transformation technique that allows us to do just that, turning cumbersome equations into their simpler, standard forms.

The [general second-degree equation](@entry_id:177618), $Ax^2 + Bxy + Cy^2 + Dx + Ey + F = 0$, can represent any conic section. However, the presence of the $Bxy$ "cross-product" term indicates that the conic is rotated, making it difficult to identify its properties—like its vertices or foci—directly. This article addresses how to systematically eliminate this term to reveal the conic's true nature.

We will embark on a comprehensive exploration of this powerful tool. The journey begins in the "Principles and Mechanisms" chapter, where we will derive the rotation formulas from first principles and apply them to eliminate the [cross-product term](@entry_id:148190). Next, in "Applications and Interdisciplinary Connections," we will broaden our perspective, revealing how rotation of axes is a manifestation of a deeper concept from linear algebra with far-reaching implications in physics and engineering. Finally, the "Hands-On Practices" section will provide you with the opportunity to apply these concepts to solve concrete problems, solidifying your understanding.

## Principles and Mechanisms

In our study of [analytic geometry](@entry_id:164266), we frequently encounter equations that represent geometric figures. The complexity of these equations often depends on the choice of the coordinate system. A strategic change of coordinates can transform a cumbersome equation into a much simpler, more insightful form. One of the most powerful techniques for such simplification is the **rotation of axes**. This chapter delves into the principles governing this transformation, the mechanisms for applying it, and its profound implications for analyzing conic sections.

### The Geometry of Coordinate Rotation

Imagine a standard Cartesian plane with axes denoted by $x$ and $y$. Now, let's establish a new coordinate system, with axes $x'$ and $y'$, by rotating the original axes counterclockwise about the origin by an angle $\theta$. Any point $P$ in the plane is fixed, but its coordinates will change depending on which system we use to describe its position. If $P$ has coordinates $(x, y)$ in the original system, what are its coordinates $(x', y')$ in the new system?

#### Deriving the Transformation Equations

We can answer this question from first principles using vector projections. Let the position vector of the point $P$ be $\vec{r}$, and let $\hat{i}$ and $\hat{j}$ be the unit vectors along the original $x$ and $y$ axes, respectively. Thus, we can write $\vec{r} = x\hat{i} + y\hat{j}$.

The new $x'$-axis is rotated by an angle $\theta$ from the $x$-axis. The [unit vector](@entry_id:150575) along this new axis, which we call $\hat{i}'$, can be expressed in terms of the original basis vectors using trigonometry as:
$$
\hat{i}' = (\cos\theta)\hat{i} + (\sin\theta)\hat{j}
$$
The new coordinate $x'$ is, by definition, the [scalar projection](@entry_id:148823) of the position vector $\vec{r}$ onto the direction of the new $x'$-axis. This projection is computed using the dot product:
$$
x' = \vec{r} \cdot \hat{i}' = (x\hat{i} + y\hat{j}) \cdot ((\cos\theta)\hat{i} + (\sin\theta)\hat{j})
$$
By expanding the dot product and using the [orthonormality](@entry_id:267887) of the basis vectors ($\hat{i} \cdot \hat{i} = 1$, $\hat{j} \cdot \hat{j} = 1$, and $\hat{i} \cdot \hat{j} = 0$), we arrive at the first transformation formula [@problem_id:2119958]:
$$
x' = x\cos\theta + y\sin\theta
$$

Similarly, the new $y'$-axis is perpendicular to the $x'$-axis, rotated by $\theta$ from the $y$-axis. The unit vector $\hat{j}'$ along the $y'$-axis is:
$$
\hat{j}' = \cos(\theta + \frac{\pi}{2})\hat{i} + \sin(\theta + \frac{\pi}{2})\hat{j} = (-\sin\theta)\hat{i} + (\cos\theta)\hat{j}
$$
The new coordinate $y'$ is the [scalar projection](@entry_id:148823) of $\vec{r}$ onto $\hat{j}'$ [@problem_id:2155620]:
$$
y' = \vec{r} \cdot \hat{j}' = (x\hat{i} + y\hat{j}) \cdot ((-\sin\theta)\hat{i} + (\cos\theta)\hat{j})
$$
This simplifies to the second transformation formula:
$$
y' = -x\sin\theta + y\cos\theta
$$

Together, these two equations allow us to find the coordinates of any point in the rotated system, given its original coordinates and the angle of rotation.

For instance, if we rotate the axes by $\theta = \frac{\pi}{4}$ and wish to find the new coordinates of a point $P$ at $(x, y) = (3, -1)$, we use $\cos(\frac{\pi}{4}) = \frac{\sqrt{2}}{2}$ and $\sin(\frac{\pi}{4}) = \frac{\sqrt{2}}{2}$.
$$
x' = (3)\left(\frac{\sqrt{2}}{2}\right) + (-1)\left(\frac{\sqrt{2}}{2}\right) = \frac{2\sqrt{2}}{2} = \sqrt{2}
$$
$$
y' = -(3)\left(\frac{\sqrt{2}}{2}\right) + (-1)\left(\frac{\sqrt{2}}{2}\right) = \frac{-4\sqrt{2}}{2} = -2\sqrt{2}
$$
The new coordinates are $(\sqrt{2}, -2\sqrt{2})$ [@problem_id:2155618].

### A Matrix Formulation

The linear relationship between the coordinate pairs $(x, y)$ and $(x', y')$ suggests a more compact and powerful representation using linear algebra.

#### Rotation of Points versus Rotation of Axes

It is crucial to distinguish between two closely related concepts: the rotation of a point (or vector) within a fixed coordinate system, and the rotation of the coordinate axes themselves while the point remains fixed.

1.  **Rotation of a Point:** When a point $P(x, y)$ is rotated counterclockwise by an angle $\theta$ to a new position $P'(x', y')$, the transformation is given by:
    $$
    \begin{pmatrix} x' \\ y' \end{pmatrix} = \begin{pmatrix} \cos\theta & -\sin\theta \\ \sin\theta & \cos\theta \end{pmatrix} \begin{pmatrix} x \\ y \end{pmatrix}
    $$
    The matrix $R(\theta) = \begin{pmatrix} \cos\theta & -\sin\theta \\ \sin\theta & \cos\theta \end{pmatrix}$ is the standard **rotation matrix**. Its columns are the images of the [standard basis vectors](@entry_id:152417) $\hat{i}=\begin{pmatrix}1 \\ 0\end{pmatrix}$ and $\hat{j}=\begin{pmatrix}0 \\ 1\end{pmatrix}$ after rotation [@problem_id:2119924].

2.  **Rotation of Axes:** This is the transformation we derived geometrically. A point $P$ is fixed, but its representation changes from $(x, y)$ to $(x', y')$. The formulas are:
    $$
    \begin{pmatrix} x' \\ y' \end{pmatrix} = \begin{pmatrix} \cos\theta & \sin\theta \\ -\sin\theta & \cos\theta \end{pmatrix} \begin{pmatrix} x \\ y \end{pmatrix}
    $$
    Notice that the matrix for rotating axes by $\theta$ is $\begin{pmatrix} \cos\theta & \sin\theta \\ -\sin\theta & \cos\theta \end{pmatrix} = \begin{pmatrix} \cos(-\theta) & -\sin(-\theta) \\ \sin(-\theta) & \cos(-\theta) \end{pmatrix} = R(-\theta)$. This makes intuitive sense: describing a fixed point in a coordinate system rotated by $\theta$ is equivalent to rotating the point itself by $-\theta$ in the original, fixed system.

Often, we need to express the original coordinates $(x,y)$ in terms of the new ones $(x',y')$. This is known as the **inverse transformation**. We can derive it by solving the system of equations for $x$ and $y$, or more elegantly, by noting it is equivalent to rotating the axes by an angle of $-\theta$. This yields the equations:
$$
x = x'\cos\theta - y'\sin\theta
$$
$$
y = x'\sin\theta + y'\cos\theta
$$
In matrix form, this is $\begin{pmatrix} x \\ y \end{pmatrix} = R(\theta) \begin{pmatrix} x' \\ y' \end{pmatrix}$, which is the inverse of the axis rotation transformation.

### Application to Conic Sections

The primary motivation for rotating axes in [analytic geometry](@entry_id:164266) is to simplify the [general second-degree equation](@entry_id:177618):
$$
Ax^2 + Bxy + Cy^2 + Dx + Ey + F = 0
$$
The presence of the **[cross-product term](@entry_id:148190)** $Bxy$ indicates that the [conic section](@entry_id:164211) it represents (an ellipse, parabola, or hyperbola) is "tilted" with respect to the coordinate axes. By rotating the axes to align with the conic's own axes of symmetry, we can eliminate this term, making the equation much easier to analyze and graph.

#### Eliminating the Cross-Product Term

Our goal is to find an angle of rotation $\theta$ such that in the new $(x', y')$ system, the equation has the form $A'(x')^2 + C'(y')^2 + D'x' + E'y' + F' = 0$, where the new cross-product coefficient $B'$ is zero.

To find the condition on $\theta$, we substitute the inverse transformation formulas for $x$ and $y$ into the original equation. The algebra can be extensive, but focusing on the terms that produce $x'y'$ is sufficient. After substitution and collection of terms, the new coefficient $B'$ is found to be [@problem_id:2119934]:
$$
B' = B(\cos^2\theta - \sin^2\theta) + 2(C-A)\sin\theta\cos\theta
$$
Using the double-angle identities $\cos(2\theta) = \cos^2\theta - \sin^2\theta$ and $\sin(2\theta) = 2\sin\theta\cos\theta$, this simplifies to:
$$
B' = B\cos(2\theta) + (C-A)\sin(2\theta)
$$
To eliminate the [cross-product term](@entry_id:148190), we set $B' = 0$:
$$
B\cos(2\theta) = -(C-A)\sin(2\theta) = (A-C)\sin(2\theta)
$$
Assuming $B \neq 0$ and $\sin(2\theta) \neq 0$, we can rearrange this to find the fundamental condition for the rotation angle:
$$
\cot(2\theta) = \frac{A-C}{B}
$$
This single equation gives us the necessary angle $\theta$ to align our coordinate system with the [conic section](@entry_id:164211).

#### Worked Examples of Simplification

Let's apply this method. Consider the [conic section](@entry_id:164211) described by $5x^2 + 2\sqrt{3}xy + 7y^2 = 24$ [@problem_id:2155656]. Here, $A=5$, $B=2\sqrt{3}$, and $C=7$.
$$
\cot(2\theta) = \frac{5 - 7}{2\sqrt{3}} = \frac{-2}{2\sqrt{3}} = -\frac{1}{\sqrt{3}}
$$
This implies that $2\theta = 120^\circ$, or $\frac{2\pi}{3}$ radians, as we seek a positive acute angle $\theta$. Therefore, the required angle of rotation is $\theta = 60^\circ$. A rotation by this angle will produce an equation with no [cross-product term](@entry_id:148190).

As another example, consider the equation $x^2 - 4xy + y^2 = 6$ [@problem_id:2155635]. Here, $A=1$, $B=-4$, and $C=1$. The condition becomes:
$$
\cot(2\theta) = \frac{1 - 1}{-4} = 0
$$
This gives $2\theta = \frac{\pi}{2}$, so $\theta = \frac{\pi}{4}$ [radians](@entry_id:171693), or $45^\circ$. Substituting the transformation formulas for this angle ($x = \frac{1}{\sqrt{2}}(x' - y')$, $y = \frac{1}{\sqrt{2}}(x' + y')$) into the equation yields:
$$
\frac{1}{2}(x' - y')^2 - 4\left(\frac{1}{2}(x'^2 - y'^2)\right) + \frac{1}{2}(x' + y')^2 = 6
$$
$$
\frac{1}{2}(x'^2 - 2x'y' + y'^2) - 2(x'^2 - y'^2) + \frac{1}{2}(x'^2 + 2x'y' + y'^2) = 6
$$
$$
x'^2 + y'^2 - 2x'^2 + 2y'^2 = 6
$$
$$
-x'^2 + 3y'^2 = 6 \quad \text{or} \quad \frac{y'^2}{2} - \frac{x'^2}{6} = 1
$$
The simplified equation clearly represents a hyperbola. Its vertices in the $(x', y')$ system are at $(0, \pm\sqrt{2})$. The distance between them is $2\sqrt{2}$. Since rotation is an [isometry](@entry_id:150881) (it preserves distances), this is the true distance between the vertices of the hyperbola in any coordinate system.

### Invariants Under Rotation

While coordinates of points and coefficients of equations change under rotation, some fundamental properties remain unchanged. These are known as **invariants**.

#### Properties that Endure Transformation

The most fundamental invariant is **distance**. The distance between any two points is the same whether measured in the $(x, y)$ system or the rotated $(x', y')$ system. This is why we can confidently calculate geometric quantities like the distance between vertices [@problem_id:2155635] or the distance between the foci of an ellipse [@problem_id:2155639] in the simplified rotated system.

Beyond this geometric invariant, there are also algebraic invariants related to the coefficients of the quadratic equation. For the quadratic part $Ax^2 + Bxy + Cy^2$, two expressions are invariant under any rotation:
1.  **The Trace Invariant:** The sum of the coefficients of the squared terms, $A+C$.
2.  **The Discriminant:** The expression $B^2 - 4AC$.

Let's prove the invariance of $A+C$. The new coefficients $A'$ and $C'$ in terms of the old ones are:
$$
A' = A\cos^2\theta + B\cos\theta\sin\theta + C\sin^2\theta
$$
$$
C' = A\sin^2\theta - B\cos\theta\sin\theta + C\cos^2\theta
$$
Adding these two equations gives:
$$
A' + C' = A(\cos^2\theta + \sin^2\theta) + C(\sin^2\theta + \cos^2\theta) = A(1) + C(1) = A+C
$$
This demonstrates that $A'+C' = A+C$ for any angle of rotation $\theta$ [@problem_id:2155633]. For the equation $7x^2 + 4xy + 4y^2 - \dots = 0$, the sum of the new coefficients $A'+C'$ must be $7+4=11$, regardless of the rotation.

The [discriminant](@entry_id:152620), $B^2-4AC$, is also invariant. This particular invariant is extremely useful because its sign determines the type of [conic section](@entry_id:164211), a property that cannot be changed by rotation.
-   If $B^2 - 4AC  0$, the conic is an ellipse or a circle.
-   If $B^2 - 4AC = 0$, the conic is a parabola.
-   If $B^2 - 4AC > 0$, the conic is a hyperbola.

#### A Powerful Shortcut for Analysis

These invariants provide a remarkable shortcut. In the rotated system, the equation is $A'(x')^2 + C'(y')^2 + \dots = 0$, which means the new [cross-product term](@entry_id:148190) $B'$ is zero. The invariants then become:
$$
A+C = A'+C'
$$
$$
B^2 - 4AC = (B')^2 - 4A'C' = -4A'C'
$$
This gives us a system of two equations for the two unknowns $A'$ and $C'$, allowing us to find them without ever calculating the rotation angle $\theta$.

Let's analyze the ellipse $17x^2 - 12xy + 8y^2 = 80$ [@problem_id:2155639]. Here $A=17, B=-12, C=8$.
Using the invariants:
$$
A'+C' = A+C = 17+8 = 25
$$
$$
-4A'C' = B^2 - 4AC = (-12)^2 - 4(17)(8) = 144 - 544 = -400 \implies A'C' = 100
$$
We need to find two numbers whose sum is 25 and whose product is 100. These are the roots of the quadratic equation $z^2 - 25z + 100 = 0$. Solving gives $z = \frac{25 \pm \sqrt{625-400}}{2} = \frac{25 \pm 15}{2}$, so the roots are $20$ and $5$. Thus, the new coefficients are $\{A', C'\} = \{5, 20\}$. The rotated equation is $5(x')^2 + 20(y')^2 = 80$, which simplifies to the standard form:
$$
\frac{(x')^2}{16} + \frac{(y')^2}{4} = 1
$$
From this, we can immediately identify the semi-major axis $a = \sqrt{16} = 4$ and the semi-minor axis $b = \sqrt{4} = 2$. The distance from the center to each focus is $c = \sqrt{a^2-b^2} = \sqrt{16-4} = \sqrt{12} = 2\sqrt{3}$. The total distance between the foci is $2c = 4\sqrt{3}$.

### The Principal Axes Theorem and Linear Algebra

The process of rotating axes to simplify a conic is deeply connected to the concepts of eigenvalues and eigenvectors in linear algebra. This connection provides the theoretical foundation for what we have observed.

The quadratic part of the conic's equation, $Ax^2 + Bxy + Cy^2$, can be represented using a [symmetric matrix](@entry_id:143130):
$$
\begin{pmatrix} x  y \end{pmatrix} \begin{pmatrix} A  B/2 \\ B/2  C \end{pmatrix} \begin{pmatrix} x \\ y \end{pmatrix}
$$
The directions in which the conic is not "sheared" or "tilted"—its axes of symmetry—are called its **principal axes**. Finding these axes is equivalent to diagonalizing the matrix $Q = \begin{pmatrix} A  B/2 \\ B/2  C \end{pmatrix}$.

The directions of the principal axes are given by the **eigenvectors** of this matrix. The coefficients of the squared terms in the simplified, rotated equation, $A'$ and $C'$, are precisely the **eigenvalues** of the matrix $Q$. This is why the characteristic equation for the eigenvalues, $\lambda^2 - (A+C)\lambda + (AC - B^2/4) = 0$, is directly related to our invariants.

Furthermore, the slope $m$ of a principal axis corresponds to an eigenvector $\begin{pmatrix} 1 \\ m \end{pmatrix}$. The eigenvector equation $Qv = \lambda v$ leads to a quadratic equation for the slopes of the principal axes [@problem_id:2123153]:
$$
B m^2 + 2(A-C)m - B = 0
$$
For the conic $2x^2 + 12xy - 3y^2 - 42 = 0$, we have $A=2, B=12, C=-3$. The sum of the slopes of its principal axes, $m_1+m_2$, can be found using Vieta's formulas on this quadratic equation:
$$
m_1 + m_2 = -\frac{2(A-C)}{B} = \frac{2(C-A)}{B} = \frac{2(-3-2)}{12} = -\frac{10}{12} = -\frac{5}{6}
$$
This result is obtained without finding the individual slopes or the rotation angle, showcasing the power of this deeper algebraic perspective.

In summary, the rotation of axes is more than a mere algebraic manipulation. It is a geometric transformation that allows us to view a conic section in its natural orientation. This process, rooted in trigonometry, is elegantly expressed in the language of linear algebra, where it reveals itself as a search for the principal directions of a quadratic form—an eigenvalue problem. By understanding these principles, we gain a powerful tool for simplifying complexity and revealing the inherent beauty and structure of geometric forms.