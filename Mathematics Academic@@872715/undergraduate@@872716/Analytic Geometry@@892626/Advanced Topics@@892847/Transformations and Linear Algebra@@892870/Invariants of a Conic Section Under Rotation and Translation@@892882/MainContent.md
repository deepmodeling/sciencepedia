## Introduction
The [general second-degree equation](@entry_id:177618), $Ax^2 + Bxy + Cy^2 + Dx + Ey + F = 0$, can describe any [conic section](@entry_id:164211)—an ellipse, parabola, or hyperbola. However, the specific values of its coefficients are highly dependent on the chosen coordinate system; a simple rotation or shift of the axes can alter the equation dramatically. This variability poses a fundamental problem: how can we identify the true, unchanging geometric nature of a conic from an equation that is so sensitive to its frame of reference? The answer lies in the study of **invariants**—algebraic quantities derived from the coefficients that remain constant regardless of [coordinate transformations](@entry_id:172727). This article provides a comprehensive exploration of these powerful tools.

Across the following chapters, you will build a complete understanding of [conic section invariants](@entry_id:166825).
- **Principles and Mechanisms** will deconstruct the effects of translation and rotation on the general equation, rigorously deriving the key invariants such as the trace ($A+C$) and the discriminant ($B^2-4AC$).
- **Applications and Interdisciplinary Connections** will demonstrate how these invariants are used to classify conics, directly calculate geometric properties like area and [eccentricity](@entry_id:266900), and solve problems in fields ranging from physics to engineering.
- **Hands-On Practices** will offer a series of guided problems to solidify your ability to apply these concepts computationally.

By exploring the principles, applications, and practical exercises, you will learn to look beyond the superficial coefficients and understand the deep, invariant geometry of conic sections.

## Principles and Mechanisms

The geometric form of a conic section—whether it is an ellipse, a parabola, or a hyperbola—is an intrinsic property of the curve itself. However, its algebraic representation, the [general second-degree equation](@entry_id:177618), is dependent on the chosen coordinate system. A simple shift (translation) or rotation of the coordinate axes can dramatically alter the coefficients of the equation. This raises a fundamental question: which algebraic quantities within the general equation are independent of the coordinate system, and what do these **invariants** tell us about the underlying geometry of the conic?

The general equation of a conic section in a Cartesian coordinate system $(x,y)$ is given by:
$$ Ax^2 + Bxy + Cy^2 + Dx + Ey + F = 0 $$
where $A, B, C, D, E, F$ are real coefficients. Our analysis will focus on how these coefficients transform under rigid motions—translations and rotations—and which combinations of them remain constant.

### Transformations and Their Effects

A rigid motion in a plane is composed of a translation and a rotation. Understanding how the conic's equation changes under each transformation separately is key to identifying the invariants.

#### Translation

A **translation** establishes a new coordinate system $(x', y')$ by shifting the origin of the $(x, y)$ system to a new point $(h, k)$. The relationship between the coordinates is given by:
$$ x = x' + h, \quad y = y' + k $$

Substituting these into the general conic equation reveals the structure of the transformed equation. The quadratic part becomes:
$$ A(x' + h)^2 + B(x' + h)(y' + k) + C(y' + k)^2 = A(x')^2 + Bx'y' + C(y')^2 + \dots $$
Notice that when expanded, the coefficients of the second-degree terms—$(x')^2$, $x'y'$, and $(y')^2$—are identical to the original coefficients $A$, $B$, and $C$. This is a crucial first observation: **The coefficients of the quadratic terms, $A, B,$ and $C$, are invariant under translation** [@problem_id:2141626]. Consequently, any quantity derived solely from these coefficients will also be a translational invariant.

The linear and constant terms, however, do change. The new equation is of the form $A'(x')^2 + B'x'y' + C'(y')^2 + D'x' + E'y' + F' = 0$, where:
- $A' = A, B' = B, C' = C$
- $D' = 2Ah + Bk + D$
- $E' = Bh + 2Ck + E$
- $F' = Ah^2 + Bhk + Ck^2 + Dh + Ek + F$

This transformation property has a profound application. For many conics, it is possible to choose the translation vector $(h, k)$ specifically to eliminate the linear terms in the new coordinate system. That is, we can find $(h, k)$ such that $D' = 0$ and $E' = 0$. This special point $(h, k)$ is called the **center** of the conic.

#### The Center of a Conic

For a conic to have its linear terms vanish under translation to a point $(h, k)$, the following [system of linear equations](@entry_id:140416) must be satisfied:
$$ 2Ah + Bk = -D $$
$$ Bh + 2Ck = -E $$

This system has a unique solution for $(h, k)$ if and only if the determinant of the [coefficient matrix](@entry_id:151473) is non-zero:
$$ \det \begin{pmatrix} 2A  B \\ B  2C \end{pmatrix} = 4AC - B^2 \neq 0 $$

This condition, conventionally written as $B^2 - 4AC \neq 0$, defines a **central conic** (an ellipse or a hyperbola). If a conic satisfies this condition, it possesses a unique center of symmetry. By translating the coordinate system to this center, the equation simplifies to the centered form $A(x')^2 + Bx'y' + C(y')^2 + F' = 0$ [@problem_id:2141611].

For example, consider the conic $5x^2 + 4xy + 2y^2 - 22x - 4y + 41 = 0$. The center $(h,k)$ is found by solving $10h+4k-22=0$ and $4h+4k-4=0$, which yields $(h, k) = (3, -2)$. The new constant term $F'$ is the value of the original polynomial evaluated at the center: $F' = 5(3)^2 + 4(3)(-2) + 2(-2)^2 - 22(3) - 4(-2) + 41 = 12$. The centered equation is $5(x')^2 + 4x'y' + 2(y')^2 + 12 = 0$ [@problem_id:2141611].

Conversely, if $B^2 - 4AC = 0$, the system for the center either has no solution or infinitely many solutions. Such a conic, a **parabola**, lacks a unique center [@problem_id:2141617]. This algebraic condition directly corresponds to a fundamental geometric distinction.

It is important to recognize that while some algebraic properties are invariant, geometric properties defined relative to the coordinate system are not. For instance, if we have two different equations for the same ellipse, obtained by translating the coordinate system, the distance from the origin to the center of the ellipse will be different in each system [@problem_id:2141618]. Invariants are special quantities that capture the intrinsic nature of the conic, independent of its position.

#### Rotation

A **rotation** establishes a new coordinate system $(x', y')$ by rotating the $(x, y)$ axes counter-clockwise by an angle $\theta$ about the origin. The coordinates are related by:
$$ x = x'\cos\theta - y'\sin\theta $$
$$ y = x'\sin\theta + y'\cos\theta $$

Substituting these expressions into the general conic equation is algebraically intensive. Unlike translation, rotation mixes the $x^2$, $xy$, and $y^2$ terms. The new coefficients $A', B', C'$ are complex combinations of the old coefficients and the angle $\theta$. Similarly, the linear coefficients $D'$ and $E'$ are new combinations of $D, E,$ and $\theta$. For example, rotating the circle $(x-2)^2+y^2=1$ (or $x^2+y^2-4x+3=0$) by $90^\circ$ yields the equation $x'^2+y'^2+4y'+3=0$. The original linear coefficients $(D, E) = (-4, 0)$ become $(D', E') = (0, 4)$, demonstrating that they are not rotational invariants [@problem_id:2141661]. The constant term $F$, however, remains unchanged under a rotation about the origin.

Since the individual quadratic coefficients $A, B, C$ are not rotational invariants, we must look for specific combinations of them that are.

### Invariants of the Quadratic Form

The quadratic part of the conic's equation, $Ax^2 + Bxy + Cy^2$, is known as the **[quadratic form](@entry_id:153497)**. Its properties determine the type of the conic. We can represent this form using [matrix multiplication](@entry_id:156035):
$$ Ax^2 + Bxy + Cy^2 = \begin{pmatrix} x  y \end{pmatrix} \begin{pmatrix} A  B/2 \\ B/2  C \end{pmatrix} \begin{pmatrix} x \\ y \end{pmatrix} = \mathbf{x}^T Q \mathbf{x} $$
where $\mathbf{x} = \begin{pmatrix} x \\ y \end{pmatrix}$ and $Q$ is the symmetric matrix of the [quadratic form](@entry_id:153497).

Under a rotation, the [coordinate vector](@entry_id:153319) transforms as $\mathbf{x} = R \mathbf{x'}$, where $R = \begin{pmatrix} \cos\theta  -\sin\theta \\ \sin\theta  \cos\theta \end{pmatrix}$ is the orthogonal rotation matrix. The [quadratic form](@entry_id:153497) in the new coordinates becomes:
$$ (R\mathbf{x'})^T Q (R\mathbf{x'}) = (\mathbf{x'})^T (R^T Q R) \mathbf{x'} = (\mathbf{x'})^T Q' \mathbf{x'} $$
The new matrix of the quadratic form is $Q' = R^T Q R$. The new coefficients $A'$ and $C'$ are the diagonal elements of $Q'$. We can now use properties of matrix operations to find invariants.

#### The Trace Invariant: $A+C$

The sum of the diagonal elements of a square matrix is its **trace**, denoted $\operatorname{tr}(\cdot)$. The trace has a cyclic property: $\operatorname{tr}(XYZ) = \operatorname{tr}(ZXY)$. Using this property and the fact that $R$ is orthogonal ($R^T R = I$, the identity matrix), we find:
$$ A' + C' = \operatorname{tr}(Q') = \operatorname{tr}(R^T Q R) = \operatorname{tr}(Q R R^T) = \operatorname{tr}(Q) = A + C $$
This proves that the quantity **$I_1 = A+C$ is an invariant under rotation** [@problem_id:2141658], [@problem_id:2141641]. Since $A$ and $C$ are also invariant under translation, $A+C$ is an invariant under all [rigid motions](@entry_id:170523).

#### The Discriminant Invariant: $B^2-4AC$

The [determinant of a matrix product](@entry_id:152524) is the product of the [determinants](@entry_id:276593). Since $\det(R) = \cos^2\theta - (-\sin^2\theta) = 1$ and $\det(R^T) = \det(R) = 1$, we have:
$$ \det(Q') = \det(R^T Q R) = \det(R^T) \det(Q) \det(R) = \det(Q) $$
The determinant of the matrix $Q$ is also a rotational invariant. Let's calculate it:
$$ \det(Q) = \det \begin{pmatrix} A  B/2 \\ B/2  C \end{pmatrix} = AC - \frac{B^2}{4} = -\frac{1}{4}(B^2 - 4AC) $$
Since $\det(Q)$ is an invariant, any constant multiple of it is also an invariant. The quantity $I_2 = B^2 - 4AC$, known as the **discriminant** of the conic, is therefore a rotational invariant. As it depends only on $A, B, C$, it is also a translational invariant.

The [invariance of the discriminant](@entry_id:170103) is immensely powerful. It allows us to classify any [conic section](@entry_id:164211) from its general equation, regardless of how the coordinate system is oriented or positioned [@problem_id:2141620].
- If $I_2 > 0$, the conic is a **hyperbola**.
- If $I_2 = 0$, the conic is a **parabola**.
- If $I_2  0$, the conic is an **ellipse**.

### Deeper Interpretations and Advanced Invariants

The invariants $A+C$ and $B^2-4AC$ have deeper connections to the principles of linear algebra and can be extended to identify more subtle geometric properties.

#### Eigenvalues of the Quadratic Form

The invariants of the [quadratic form](@entry_id:153497) are directly related to the **eigenvalues** $\lambda_1, \lambda_2$ of the matrix $Q$. For any $2 \times 2$ matrix, the trace is the sum of its eigenvalues, and the determinant is the product of its eigenvalues.
$$ I_1 = A+C = \operatorname{tr}(Q) = \lambda_1 + \lambda_2 $$
$$ \det(Q) = AC - \frac{B^2}{4} = \lambda_1 \lambda_2 $$
From this, we can express the [discriminant](@entry_id:152620) in terms of eigenvalues:
$$ I_2 = B^2 - 4AC = -4 \left(AC - \frac{B^2}{4}\right) = -4 \det(Q) = -4 \lambda_1 \lambda_2 $$
This confirms the relationship from problem [@problem_id:2141647], which asks for the value of $\frac{B^2 - 4AC}{\lambda_1 \lambda_2} = -4$.

This perspective provides a clear geometric interpretation. A [rotation of axes](@entry_id:178802) that eliminates the $Bxy$ term is equivalent to diagonalizing the matrix $Q$. In such a rotated system, the new matrix $Q'$ is diagonal, and its diagonal entries, $A'$ and $C'$, are precisely the eigenvalues $\lambda_1$ and $\lambda_2$. The classification of the conic is then determined by the signs of its eigenvalues.

#### The Invariant for Degeneracy

The invariants discussed so far classify the type of a non-[degenerate conic](@entry_id:167498). However, an equation like $x^2 - y^2 = 0$ represents two intersecting lines, a **degenerate hyperbola**. To distinguish between non-degenerate and [degenerate conics](@entry_id:171197), we need a higher-order invariant.

This is achieved by representing the entire conic equation in [homogeneous coordinates](@entry_id:154569) $(x, y, w)$, where the Cartesian plane corresponds to $w=1$. The general conic equation can be written as:
$$ \begin{pmatrix} x  y  1 \end{pmatrix} \begin{pmatrix} A  B/2  D/2 \\ B/2  C  E/2 \\ D/2  E/2  F \end{pmatrix} \begin{pmatrix} x \\ y \\ 1 \end{pmatrix} = 0 $$
The $3 \times 3$ matrix, let's call it $M$, is the characteristic matrix of the conic. It can be shown that its determinant, **$I_3 = \det(M)$, is an invariant under both [rotation and translation](@entry_id:175994)**.

The significance of this invariant is that **a conic is degenerate if and only if $\det(M) = 0$**. A non-zero determinant, as seen in the two equivalent conic equations from problem [@problem_id:2141643], indicates a non-degenerate curve. The fact that both equations, despite their different coefficients, yield the same determinant value of $-64$ is a concrete illustration of this invariance.

#### Complex Variable Representation

An elegant and powerful perspective on these invariants emerges when we use complex numbers. By setting $z = x+iy$ and its conjugate $\bar{z} = x-iy$, we can express the Cartesian coordinates as $x = (z+\bar{z})/2$ and $y = (z-\bar{z})/(2i)$. Substituting these into the quadratic form $Ax^2+Bxy+Cy^2$ and regrouping terms yields an expression of the form $\alpha z^2 + \beta \bar{z}^2 + \gamma z\bar{z}$.

By matching coefficients, we can find the relationships [@problem_id:2141609]:
- $A = \gamma + (\alpha+\beta)$
- $B = 2i(\alpha-\beta)$
- $C = \gamma - (\alpha+\beta)$

Now we can express our Cartesian invariants in terms of these complex coefficients.
The [trace invariant](@entry_id:183000) is:
$$ I_1 = A+C = (\gamma + \alpha + \beta) + (\gamma - \alpha - \beta) = 2\gamma $$
The [discriminant](@entry_id:152620) is:
$$ I_2 = B^2 - 4AC = (2i(\alpha-\beta))^2 - 4(\gamma + \alpha + \beta)(\gamma - \alpha - \beta) $$
$$ I_2 = -4(\alpha-\beta)^2 - 4(\gamma^2 - (\alpha+\beta)^2) = 4 [(\alpha+\beta)^2 - (\alpha-\beta)^2] - 4\gamma^2 $$
Using the identity $(\alpha+\beta)^2 - (\alpha-\beta)^2 = 4\alpha\beta$, we arrive at:
$$ I_2 = 4(4\alpha\beta) - 4\gamma^2 = 16\alpha\beta - 4\gamma^2 $$
This formulation compactly encodes the rotational invariants in the coefficients of the [complex representation](@entry_id:183096), highlighting the deep synergy between geometry and complex analysis.

In summary, the study of invariants provides a systematic method for peering through the veil of [coordinate systems](@entry_id:149266) to understand the true, unchanging geometric nature of [conic sections](@entry_id:175122). From the simple trace and discriminant to the more abstract eigenvalue and [complex representations](@entry_id:144331), these constant quantities form the bedrock of the classification and analysis of second-degree curves.