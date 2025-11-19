## Introduction
In the study of [analytic geometry](@entry_id:164266), [conic sections](@entry_id:175122)—circles, ellipses, parabolas, and hyperbolas—form a cornerstone of analysis. A frequently encountered problem is determining the equation of a chord that passes through these curves. While many methods exist, the specific case of finding a chord's equation when only its midpoint is known presents a unique challenge that can be solved with a remarkably elegant and unified approach. This article moves beyond solving this problem on a case-by-case basis and introduces a powerful general formula that applies to any conic section.

This article is structured to build your understanding progressively. In the first section, **Principles and Mechanisms**, we will derive this central formula, starting with the intuitive geometric properties of a circle and advancing to a robust algebraic proof for general conics, culminating in the concise expression $T=S_1$. Next, in **Applications and Interdisciplinary Connections**, we will unleash the power of this formula, using it to solve a wide variety of locus problems and explore its deep connections to advanced concepts like poles, polars, and director circles. Finally, the **Hands-On Practices** section will provide a set of guided problems to help you master the application of these principles and solidify your skills in solving complex geometric challenges.

## Principles and Mechanisms

In the introduction, we outlined the fundamental properties of [conic sections](@entry_id:175122). We now delve into a more specialized yet powerful concept: determining the equation of a chord within a conic section when its midpoint is known. This problem arises in various scientific and engineering contexts, from analyzing the trajectory of a probe through a gravitational field to designing optical systems. While it can be solved using first principles for any given case, a remarkable and elegant general formula simplifies this task considerably. This chapter will derive this formula, explore its geometric underpinnings, and demonstrate its utility.

### The Foundational Case: Chords of a Circle

We begin our investigation with the simplest [conic section](@entry_id:164211): the circle. The unique symmetries of the circle provide a clear geometric intuition that will serve as a foundation for more general cases.

Consider a circle centered at the origin $O(0,0)$ with radius $R$, described by the equation $x^2 + y^2 = R^2$. Let there be a chord whose midpoint is the point $M(h,k)$. A fundamental theorem of Euclidean geometry states that the radius that passes through the midpoint of a chord is perpendicular to that chord. Therefore, the line segment $OM$ is perpendicular to the chord in question.

The vector from the origin to the midpoint is $\vec{OM} = \langle h, k \rangle$. Since the chord is a line passing through $M(h,k)$ and is perpendicular to $\vec{OM}$, this vector $\langle h, k \rangle$ serves as a **[normal vector](@entry_id:264185)** to the line. The [equation of a line](@entry_id:166789) passing through $(x_0, y_0)$ with a normal vector $\langle A, B \rangle$ is $A(x-x_0) + B(y-y_0) = 0$. Applying this, the equation of our chord is:

$h(x-h) + k(y-k) = 0$

Expanding this equation, we arrive at a concise form:

$hx + ky = h^2 + k^2$

This equation elegantly defines the chord based solely on the coordinates of its midpoint. For instance, in a RADAR system with a detection circle $x^2+y^2=R^2$, if a target's flight path has a midpoint $(h,k)$, the path length can be found by constructing a right triangle with the origin, the midpoint, and one endpoint of the chord. The Pythagorean theorem gives the half-length of the chord as $\sqrt{R^2 - (h^2+k^2)}$, so the total visible path length is $2\sqrt{R^2 - h^2 - k^2}$ [@problem_id:2123924].

To pave the way for generalization, let us introduce a standard notation. Let the equation of the circle be written as $S(x,y) = x^2 + y^2 - R^2 = 0$. We define two related expressions:
1.  $S_1 = S(x_1, y_1) = x_1^2 + y_1^2 - R^2$, which is the result of evaluating the conic's function at a point $(x_1, y_1)$.
2.  $T = xx_1 + yy_1 - R^2$, which is the expression for the tangent line to the circle at a point $(x_1, y_1)$ on the circle.

Using this notation with the midpoint $(h,k)$, the chord equation $hx + ky = h^2 + k^2$ can be rewritten by subtracting $R^2$ from both sides:

$xh + yk - R^2 = h^2 + k^2 - R^2$

This is precisely **$T = S_1$**.

This formulation reveals a beautiful connection between chords, midpoints, and tangents. The equation for a tangent at a point $(x_1, y_1)$ on the circle is $T=0$. The equation for the chord whose midpoint is $(x_1, y_1)$ is $T=S_1$. The lines are parallel, differing only by a constant. The [perpendicular distance](@entry_id:176279) between a chord with midpoint $(h,k)$ and a parallel tangent can be found by calculating the distance between the lines $xh+yk - (h^2+k^2) = 0$ and $xh+yk - R\sqrt{h^2+k^2} = 0$. This distance simplifies to the intuitive result $R - \sqrt{h^2+k^2}$, which is the radius minus the distance of the midpoint from the center [@problem_id:2123899].

### The Algebraic Approach: The Method of the Midpoint

The simple perpendicularity argument used for the circle does not generally apply to ellipses or hyperbolas, as their centers do not maintain a constant distance to their peripheries. A more robust, algebraic approach is required. This technique, which we shall call the **method of the midpoint**, leverages the relationship between the roots of a polynomial and its coefficients.

Let's illustrate this method for an elliptical mirror described by $\frac{x^2}{a^2} + \frac{y^2}{b^2} = 1$, where we need to find the equation of a chord with a given midpoint $P_1(x_1, y_1)$ [@problem_id:2123894].

1.  Assume the chord lies on a line passing through $P_1(x_1, y_1)$ with an unknown slope $m$. The equation of this line is $y - y_1 = m(x - x_1)$.

2.  To find the endpoints of the chord, we substitute this [line equation](@entry_id:177883) into the ellipse equation:
    $$\frac{x^2}{a^2} + \frac{(y_1 + m(x-x_1))^2}{b^2} = 1$$

3.  Expanding and collecting terms in powers of $x$ yields a quadratic equation of the form $K_2 x^2 + K_1 x + K_0 = 0$.

4.  Let the roots of this quadratic be $x_A$ and $x_B$, corresponding to the x-coordinates of the chord's endpoints. Since $P_1(x_1, y_1)$ is the midpoint, its x-coordinate must be the average of the endpoints' x-coordinates: $\frac{x_A + x_B}{2} = x_1$.

5.  According to **Viète's formulas**, the sum of the roots of the quadratic is $x_A + x_B = -\frac{K_1}{K_2}$.

6.  Combining these facts gives the crucial constraint: $2x_1 = -\frac{K_1}{K_2}$. This equation allows us to solve for the unknown slope $m$.

For the ellipse, this procedure yields the slope $m = -\frac{b^2 x_1}{a^2 y_1}$. Once the slope is known, the equation of the chord is fully determined using the [point-slope form](@entry_id:165105). This same method applies equally well to other conics, such as finding the line of sight for an instrument observing a probe on a hyperbolic path [@problem_id:2123911].

A particularly elegant result emerges for the [rectangular hyperbola](@entry_id:165798) $xy = c^2$. If a chord has intercepts $(a,0)$ and $(0,b)$, its midpoint can be shown to be $(\frac{a}{2}, \frac{b}{2})$. Therefore, if a chord has a given midpoint of $(5,3)$ on the hyperbola $xy=16$, we can immediately deduce that the intercepts of the line containing the chord are $a=10$ and $b=6$ [@problem_id:2123913].

### The General Formula for Conic Sections: $T = S_1$

While the method of the midpoint is fundamental, performing the algebra for a general conic section with [rotation and translation](@entry_id:175994) can be tedious. Fortunately, these individual results are all manifestations of a single, unifying formula.

Consider the general equation of a second-degree curve:
$$S(x,y) = Ax^2 + 2Hxy + By^2 + 2Gx + 2Fy + C = 0$$

Let $P_1(x_1, y_1)$ be the given midpoint of a chord. We define the expression $S_1$ as the evaluation of $S$ at this point:
$$S_1 = S(x_1, y_1) = Ax_1^2 + 2Hx_1y_1 + By_1^2 + 2Gx_1 + 2Fy_1 + C$$

We also define a linear expression $T$ by a process of symmetrization on the quadratic terms of $S$:
$$T = Axx_1 + H(xy_1 + yx_1) + Byy_1 + G(x+x_1) + F(y+y_1) + C$$

The central theorem states that the equation of the chord of the conic $S=0$ bisected at the point $(x_1, y_1)$ is given by the remarkably compact equation:
**$T = S_1$**

To prove this powerful result, we use a parametric approach [@problem_id:2123914]. Consider a line passing through $P_1(x_1, y_1)$ with direction vector $\langle \cos\theta, \sin\theta \rangle$. Any point on this line can be written as $(x_1 + r\cos\theta, y_1 + r\sin\theta)$, where $r$ is the signed distance from $P_1$. Substituting these coordinates into the conic equation $S(x,y)=0$ yields a quadratic equation in $r$:

$K_2 r^2 + K_1 r + S_1 = 0$

The roots of this equation, $r_A$ and $r_B$, represent the distances from the midpoint $P_1$ to the two endpoints of the chord. For $P_1$ to be the midpoint, the endpoints must be equidistant in opposite directions, meaning $r_A = -r_B$. This implies that the sum of the roots is zero: $r_A + r_B = 0$. From Viète's formulas, this requires the coefficient of the linear term, $K_1$, to be zero.

The coefficient $K_1$ can be shown to be:
$$K_1 = (2Ax_1 + 2Hy_1 + 2G)\cos\theta + (2Hx_1 + 2By_1 + 2F)\sin\theta = 0$$

This equation provides a condition on the angle $\theta$, and thus the slope of the chord. The equation of the line passing through $(x_1, y_1)$ that satisfies this condition is precisely:
$(x - x_1)(Ax_1 + Hy_1 + G) + (y - y_1)(Hx_1 + By_1 + F) = 0$

While this equation is correct, it is not immediately obvious how it relates to $T=S_1$. However, with careful algebraic manipulation, the equation $T=S_1$ can be shown to be identical to the one above. This confirms that $T=S_1$ is not just a mnemonic device, but a valid and profound statement about the geometry of [conic sections](@entry_id:175122).

For example, to find the chord of $3x^2 - 2xy + 3y^2 - 16x - 16y + 32 = 0$ with midpoint $(3, 2)$, we can simply apply the formula. Here $A=3, H=-1, B=3, G=-8, F=-8, C=32$.
First, calculate $S_1 = S(3,2) = 3(9) - 2(3)(2) + 3(4) - 16(3) - 16(2) + 32 = 27 - 12 + 12 - 48 - 32 + 32 = -21$.
Next, write down $T = 3x(3) - (x(2)+y(3)) + 3y(2) - 8(x+3) - 8(y+2) + 32$.
$T = 9x - 2x - 3y + 6y - 8x - 24 - 8y - 16 + 32 = -x - 5y - 8$.
Setting $T = S_1$ gives $-x - 5y - 8 = -21$, which simplifies to $x + 5y = 13$ [@problem_id:2123914].

### Geometric Interpretation and Advanced Applications

The derivation of the general formula provides a deeper geometric insight. The condition that the linear coefficient $K_1$ is zero can be written using vector notation. The gradient of the function $S(x,y)$ at the point $(x_1, y_1)$ is the vector $\nabla S(x_1, y_1) = \langle \frac{\partial S}{\partial x_1}, \frac{\partial S}{\partial y_1} \rangle$, where $\frac{\partial S}{\partial x_1} = 2Ax_1 + 2Hy_1 + 2G$ and $\frac{\partial S}{\partial y_1} = 2Hx_1 + 2By_1 + 2F$. The direction vector of the chord is $\vec{v} = \langle \cos\theta, \sin\theta \rangle$. The condition $K_1 = 0$ is exactly the statement that the dot product is zero:

$$\nabla S(x_1, y_1) \cdot \vec{v} = 0$$

This means that **the chord bisected at a point $P_1$ is always perpendicular to the [gradient vector](@entry_id:141180) of the conic's implicit function evaluated at $P_1$**. This is the generalization of our starting observation for the circle, where the gradient vector points along the radius. This principle extends to three dimensions, as seen in modeling atom clouds with ellipsoidal boundaries. A laser beam passing through such a cloud with a given midpoint will have a direction vector orthogonal to the gradient of the ellipsoid's function at that midpoint [@problem_id:2123901].

The formula $T=S_1$ is also a powerful tool for solving more complex locus and envelope problems. For example, consider a scenario where the midpoints of a series of chords are constrained to lie on a specific curve, such as a straight line. We might ask for the shape of the **envelope** formed by this family of chords. By using the $T=S_1$ formula, we can write the equation of a generic chord in terms of the coordinates of its midpoint, $(h,k)$. Then, by substituting the constraint equation (e.g., $k=h+2$), we obtain a one-parameter [family of lines](@entry_id:169519). Standard calculus techniques can then be used to find the envelope of this family, revealing the curve that is tangent to every chord in the set [@problem_id:2123906].

In summary, the relationship $T=S_1$ provides a unified, efficient, and insightful method for determining the equation of a chord with a given midpoint for any [conic section](@entry_id:164211). It connects algebraic manipulation with profound geometric principles, offering a glimpse into the deep and elegant structure underlying [analytic geometry](@entry_id:164266).