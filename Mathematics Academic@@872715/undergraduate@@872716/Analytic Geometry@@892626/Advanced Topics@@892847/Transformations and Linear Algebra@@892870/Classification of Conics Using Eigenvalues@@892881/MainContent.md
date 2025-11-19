## Introduction
The study of conic sections—ellipses, hyperbolas, and parabolas—is a fundamental topic in [analytic geometry](@entry_id:164266), representing the beautiful interplay between algebraic equations and geometric forms. Any conic can be described by a [general second-degree equation](@entry_id:177618), but the presence of a cross-term often obscures its true nature and orientation. This article addresses the challenge of systematically classifying and analyzing these curves by introducing a powerful method from linear algebra. By representing the conic's quadratic terms with a [symmetric matrix](@entry_id:143130), we can unlock its geometric secrets through the analysis of eigenvalues and eigenvectors.

This article will guide you through this elegant approach in three parts. First, in **Principles and Mechanisms**, we will establish the foundational theory, explaining how the Principal Axis Theorem allows us to eliminate the cross-term and how the eigenvalues of the associated matrix definitively classify the conic. Next, in **Applications and Interdisciplinary Connections**, we will explore how this method extends beyond pure mathematics, providing crucial insights in fields like physics, chemistry, and engineering. Finally, in **Hands-On Practices**, you will have the opportunity to solidify your understanding by working through targeted problems. By the end, you will not only be able to classify any conic section but also appreciate the deep connection between [matrix algebra](@entry_id:153824) and geometric structure.

## Principles and Mechanisms

The study of conic sections—ellipses, hyperbolas, and parabolas—represents a cornerstone of [analytic geometry](@entry_id:164266), bridging the gap between algebraic equations and geometric shapes. While these curves can be defined by the intersection of a plane and a double cone, their representation as second-degree polynomial equations in two variables,
$$ Ax^2 + Bxy + Cy^2 + Dx + Ey + F = 0 $$
provides a powerful framework for analysis. The classification of a conic depends fundamentally on its **quadratic part**, $Ax^2 + Bxy + Cy^2$. By leveraging the tools of linear algebra, specifically eigenvalues and eigenvectors, we can develop a systematic and insightful method for identifying and understanding the properties of any [conic section](@entry_id:164211).

### The Matrix of a Quadratic Form

At the heart of this algebraic approach is the ability to represent the quadratic part of the conic's equation using [matrix multiplication](@entry_id:156035). Any [quadratic form](@entry_id:153497) $Q(x,y) = Ax^2 + Bxy + Cy^2$ can be expressed as $\mathbf{x}^T M \mathbf{x}$, where $\mathbf{x}$ is the [coordinate vector](@entry_id:153319) and $M$ is a [symmetric matrix](@entry_id:143130).

$$ \mathbf{x} = \begin{pmatrix} x \\ y \end{pmatrix}, \quad M = \begin{pmatrix} A & B/2 \\ B/2 & C \end{pmatrix} $$

This representation is not merely a notational convenience; the properties of the matrix $M$ are intrinsically linked to the geometry of the [conic section](@entry_id:164211). The symmetric nature of $M$ is crucial, as it guarantees that the matrix is diagonalizable and possesses real eigenvalues.

For instance, consider a curve defined by the equation $13x^2 - 10xy + 13y^2 = 72$. The quadratic part is $Q(x,y) = 13x^2 - 10xy + 13y^2$. By matching the coefficients with the general form $Ax^2 + Bxy + Cy^2$, we have $A=13$, $B=-10$, and $C=13$. The corresponding [symmetric matrix](@entry_id:143130) $M$ is:
$$ M = \begin{pmatrix} A & B/2 \\ B/2 & C \end{pmatrix} = \begin{pmatrix} 13 & -5 \\ -5 & 13 \end{pmatrix} $$
The analysis of this matrix, as we will see, reveals everything we need to know about the shape and orientation of the curve [@problem_id:2112480].

### The Principal Axis Theorem: Aligning Geometry with Algebra

The presence of a cross-term $Bxy$ in the conic's equation indicates that its axes of symmetry (its **principal axes**) are not aligned with the standard Cartesian coordinate axes. A primary goal is to find a new coordinate system $(x', y')$ in which the equation has no cross-term, thereby simplifying its form and revealing its nature. This transformation is achieved by a rotation of the coordinate axes.

The **Principal Axis Theorem** provides the theoretical foundation for this procedure. It states that for any symmetric matrix $M$, there exists an [orthogonal matrix](@entry_id:137889) $P$ (representing a rotation or reflection) such that $P^T M P$ is a diagonal matrix, $D$. The diagonal entries of $D$ are the **eigenvalues** of $M$, and the columns of $P$ are the corresponding orthonormal **eigenvectors**.

If we perform a change of variables $\mathbf{x} = P\mathbf{x}'$, where $\mathbf{x}' = \begin{pmatrix} x' \\ y' \end{pmatrix}$, the quadratic form becomes:
$$ \mathbf{x}^T M \mathbf{x} = (P\mathbf{x}')^T M (P\mathbf{x}') = (\mathbf{x}')^T (P^T M P) \mathbf{x}' = (\mathbf{x}')^T D \mathbf{x}' $$

Letting the eigenvalues of $M$ be $\lambda_1$ and $\lambda_2$, the diagonal matrix is $D = \begin{pmatrix} \lambda_1 & 0 \\ 0 & \lambda_2 \end{pmatrix}$. The [quadratic form](@entry_id:153497) in the new coordinates is simply:
$$ \lambda_1 (x')^2 + \lambda_2 (y')^2 $$

This transformed equation is profoundly revealing. First, the absence of a cross-term confirms that the new coordinate axes, $(x', y')$, are the principal axes of the conic. Second, the directions of these new axes are given by the eigenvectors of the original matrix $M$ [@problem_id:2112501]. This establishes a direct link between an algebraic property of the matrix (its eigenvectors) and a geometric feature of the curve (its axes of symmetry).

### Invariants under Rotation

A key consequence of this analysis is that the eigenvalues of the matrix $M$ are **invariant** under rotation. No matter how we rotate the coordinate system, the eigenvalues associated with the conic's [quadratic form](@entry_id:153497) remain the same. They are intrinsic properties of the curve itself. This is because the process of changing coordinates from $\mathbf{x}$ to $\mathbf{x}'$ via a rotation matrix $P$ transforms the matrix $M$ to $P^T M P$, which is a similarity transformation. The eigenvalues of $P^T M P$ are the same as the eigenvalues of $M$.

This invariance is a powerful computational tool. For a conic $Kx^2 - 12xy + 10y^2 = 20$, if we know that in a rotated frame its equation is $4(x')^2 + \beta(y')^2 = 20$, we can immediately conclude that the eigenvalues of the original matrix $M = \begin{pmatrix} K & -6 \\ -6 & 10 \end{pmatrix}$ are $\lambda_1 = 4$ and $\lambda_2 = \beta$ [@problem_id:2112492].

Other matrix properties are also invariant under rotation, such as the trace and the determinant.
- The **trace** of $M$, $\text{tr}(M) = A+C$, is equal to the sum of the eigenvalues, $\lambda_1 + \lambda_2$.
- The **determinant** of $M$, $\det(M) = AC - (B/2)^2$, is equal to the product of the eigenvalues, $\lambda_1 \lambda_2$.

The invariance of the trace, for example, implies that if a conic's equation is transformed by rotation from $Ax^2+Bxy+Cy^2=F$ to $A'(x')^2+B'x'y'+C'(y')^2=F$, then it must be that $A'+C' = A+C$ [@problem_id:2112459]. These invariants provide checks and shortcuts for calculation.

### Classification of Conics via Eigenvalues

The signs of the eigenvalues provide a complete and unambiguous classification of the conic section's type. This method is more robust than relying solely on the traditional [discriminant](@entry_id:152620) ($B^2-4AC$), as it also reveals information about the shape's orientation and scale. The classification hinges on the product of the eigenvalues, $\lambda_1 \lambda_2 = \det(M)$.

#### Ellipses: $\det(M) = \lambda_1 \lambda_2 > 0$

If the determinant is positive, the eigenvalues $\lambda_1$ and $\lambda_2$ must have the same sign (both positive or both negative). The equation in the principal axis system is $\lambda_1 (x')^2 + \lambda_2 (y')^2 = k$. If $k$ has the same sign as the eigenvalues, the equation describes an **ellipse**. If the signs differ, the equation has no real solution (the empty set). An ellipse is a **bounded** set, meaning it can be enclosed within a circle of finite radius. A [quadratic form](@entry_id:153497) will define a bounded set if and only if its matrix is [positive definite](@entry_id:149459) (or [negative definite](@entry_id:154306)), which means both its eigenvalues are positive (or both negative) [@problem_id:2112455]. For example, a conic described by $kx^2 + 8xy + y^2 + \dots = 0$ will be an ellipse when the determinant of its matrix $M=\begin{pmatrix} k & 4 \\ 4 & 1 \end{pmatrix}$, which is $k-16$, is positive. Thus, for $k > 16$, the conic is an ellipse [@problem_id:2112457].

#### Hyperbolas: $\det(M) = \lambda_1 \lambda_2  0$

If the determinant is negative, the eigenvalues must have opposite signs. The equation $\lambda_1 (x')^2 + \lambda_2 (y')^2 = k$ becomes the standard equation of a **hyperbola**. A hyperbola is an **unbounded** set. In the previous example, the conic becomes a hyperbola when $k-16  0$, or $k  16$ [@problem_id:2112457].

#### Parabolas: $\det(M) = \lambda_1 \lambda_2 = 0$

If the determinant is zero, at least one of the eigenvalues must be zero. If only one eigenvalue is zero (e.g., $\lambda_2 = 0$ and $\lambda_1 \neq 0$), the quadratic part in the rotated frame becomes $\lambda_1(x')^2$. The full equation, including linear terms, cannot be simplified by translation alone to eliminate all linear terms. This leads to the characteristic form of a **parabola**, such as $\lambda_1(x')^2 + E'y' = 0$. Like a hyperbola, a parabola is an **unbounded** set.

The condition $\det(M)=0$ is equivalent to the classical [discriminant](@entry_id:152620) test for parabolas.
$$ \det(M) = AC - \frac{B^2}{4} = 0 \iff B^2 - 4AC = 0 $$
For a conic defined by $9x^2 + \beta xy + 4y^2 + \dots = 0$ to be a parabola, we must have $\beta^2 - 4(9)(4) = 0$, which for $\beta>0$ yields $\beta=12$. The matrix $M = \begin{pmatrix} 9  6 \\ 6  4 \end{pmatrix}$ has $\det(M) = 36-36=0$, confirming a zero eigenvalue. The other eigenvalue can be found from the trace: $\text{tr}(M) = 9+4 = 13 = \lambda_1 + \lambda_2$. Since one eigenvalue is 0, the other must be 13 [@problem_id:2112512].

### Geometric Significance of Eigenvalues and Eigenvectors

The power of the eigenvalue method extends beyond mere classification. The values themselves carry direct geometric meaning.

For an ellipse or hyperbola centered at the origin, whose equation in the principal axis frame is $\lambda_1 (x')^2 + \lambda_2 (y')^2 = k$, we can rewrite it in standard form:
$$ \frac{(x')^2}{k/\lambda_1} + \frac{(y')^2}{k/\lambda_2} = 1 $$
The quantities $k/\lambda_1$ and $k/\lambda_2$ are the squares of the semi-axis lengths. If the curve is an ellipse, the lengths of the semi-axes are $a = \sqrt{k/\lambda_{\text{min}}}$ and $b = \sqrt{k/\lambda_{\text{max}}}$. This reveals that the eigenvalues are inversely proportional to the squares of the semi-axis lengths along their corresponding eigenvector directions.

This relationship allows for direct computation of geometric properties. For example, the area of the ellipse defined by $\mathbf{x}^T M \mathbf{x} = k$ is given by $\text{Area} = \pi ab$. Substituting the expressions for $a$ and $b$:
$$ \text{Area} = \pi \sqrt{\frac{k}{\lambda_1}} \sqrt{\frac{k}{\lambda_2}} = \frac{\pi k}{\sqrt{\lambda_1 \lambda_2}} = \frac{\pi k}{\sqrt{\det(M)}} $$
For the ellipse $7x^2 + 6\sqrt{3}xy + 13y^2 = 16$, the matrix $M=\begin{pmatrix} 7  3\sqrt{3} \\ 3\sqrt{3}  13 \end{pmatrix}$ has $\det(M) = 91 - 27 = 64$. The area is therefore $\frac{16\pi}{\sqrt{64}} = 2\pi$ [@problem_id:2112478].

Furthermore, the [eccentricity](@entry_id:266900) $e$ of an ellipse depends on the ratio of its semi-axes, and thus on the ratio of the eigenvalues:
$$ e = \sqrt{1 - \frac{b^2}{a^2}} = \sqrt{1 - \frac{k/\lambda_{\text{max}}}{k/\lambda_{\text{min}}}} = \sqrt{1 - \frac{\lambda_{\min}}{\lambda_{\text{max}}}} $$
This shows that the more "stretched" an ellipse is (higher [eccentricity](@entry_id:266900)), the greater the disparity between its corresponding eigenvalues [@problem_id:2112501].

### Degenerate Conics

The classification above assumes the conic is non-degenerate. However, for specific combinations of coefficients, the equation can represent a **[degenerate conic](@entry_id:167498)**: a pair of intersecting lines, a pair of parallel lines, a single line, a single point, or the empty set.

A [conic section](@entry_id:164211) $Ax^2 + Bxy + Cy^2 + Dx + Ey + F = 0$ is degenerate if and only if the determinant of its $3 \times 3$ [augmented matrix](@entry_id:150523) is zero:
$$ \det \begin{pmatrix} A  B/2  D/2 \\ B/2  C  E/2 \\ D/2  E/2  F \end{pmatrix} = 0 $$

For instance, consider a conic of the parabolic type ($\det(M)=0$). This can degenerate into a pair of parallel lines. The equation $x^2 + 4xy + cy^2 - 6x - 12y + 5 = 0$ is of the parabolic type when $c=4$. Substituting $c=4$, the $3 \times 3$ determinant is indeed zero. The equation can be factored as $(x+2y-1)(x+2y-5)=0$, which represents two distinct parallel lines [@problem_id:2112468].

Similarly, a conic of the hyperbolic type ($\det(M)0$) can degenerate into two intersecting lines. This occurs when the constant term of the equation takes a specific value that makes the $3 \times 3$ determinant zero [@problem_id:2112489].

In conclusion, the [eigenvalue analysis](@entry_id:273168) of the [quadratic form](@entry_id:153497) matrix provides a comprehensive and unifying framework for the study of [conic sections](@entry_id:175122). It not only classifies the conics into their fundamental types but also reveals their orientation, dimensions, and geometric properties through the direct interpretation of eigenvalues and eigenvectors.