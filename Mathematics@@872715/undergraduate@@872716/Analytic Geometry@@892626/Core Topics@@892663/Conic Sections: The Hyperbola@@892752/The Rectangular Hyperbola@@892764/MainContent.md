## Introduction
Among the family of conic sections, the [rectangular hyperbola](@entry_id:165798) stands out for its unique symmetry and elegant properties. Also known as the equilateral hyperbola, its perpendicular asymptotes give rise to a simple yet powerful algebraic form that appears in surprisingly diverse fields, from physics to advanced mathematics. However, connecting its intuitive geometric definition to its signature within the general conic equation, and appreciating its role beyond the classroom, can be a challenge. This article aims to bridge that gap by providing a clear and structured exploration of this fascinating curve.

The journey begins in **"Principles and Mechanisms,"** where we derive the [rectangular hyperbola](@entry_id:165798)'s canonical equations ($x^2 - y^2 = a^2$ and $xy = k$) from its geometric foundation and establish the definitive algebraic test ($A+C=0$) for its identification. Next, **"Applications and Interdisciplinary Connections"** reveals its manifestations in celestial mechanics, [differential geometry](@entry_id:145818), and complex analysis, showcasing the curve's practical and theoretical significance. Finally, **"Hands-On Practices"** offers a curated set of problems designed to solidify your understanding and analytical skills. Through this progression, you will gain a comprehensive grasp of the [rectangular hyperbola](@entry_id:165798), from its core theory to its real-world relevance.

## Principles and Mechanisms

This chapter delves into the fundamental principles that define a [rectangular hyperbola](@entry_id:165798) and the algebraic mechanisms used to identify and analyze it. We will bridge the intuitive geometric definition of a [rectangular hyperbola](@entry_id:165798) with its specific algebraic signatures within the general framework of conic sections.

### Geometric Foundation: Perpendicular Asymptotes

A hyperbola is geometrically defined as the set of all points in a plane, the difference of whose distances from two fixed points (the **foci**) is a constant. This geometric property gives rise to its characteristic two-branched curve. A key feature of any hyperbola is its pair of **asymptotes**—straight lines that the curve approaches infinitely closely but never touches.

For a hyperbola centered at the origin with its principal axis along the x-axis, its standard equation is:
$$ \frac{x^2}{a^2} - \frac{y^2}{b^2} = 1 $$
Here, $a$ and $b$ are the semi-major and semi-minor axes, respectively. The equations for the asymptotes of this hyperbola are given by:
$$ y = \pm \frac{b}{a}x $$
The slopes of these two lines are $m_1 = \frac{b}{a}$ and $m_2 = -\frac{b}{a}$.

A **[rectangular hyperbola](@entry_id:165798)** is a special case of a hyperbola where its asymptotes are perpendicular to each other. For two lines to be perpendicular, the product of their slopes must be $-1$. Applying this condition to the asymptotes, we find:
$$ m_1 \cdot m_2 = \left(\frac{b}{a}\right) \left(-\frac{b}{a}\right) = -1 $$
$$ -\frac{b^2}{a^2} = -1 $$
$$ b^2 = a^2 $$
This implies that $b=a$ (since $a$ and $b$ represent positive lengths). Thus, in a [rectangular hyperbola](@entry_id:165798), the lengths of the semi-major and semi-minor axes are equal. For this reason, it is also sometimes referred to as an **equilateral hyperbola**.

Substituting $b=a$ into the standard hyperbola equation gives the canonical equation for a [rectangular hyperbola](@entry_id:165798) whose axes of symmetry are the coordinate axes:
$$ x^2 - y^2 = a^2 $$

### A Canonical Form: The Hyperbola as $xy = k$

While the form $x^2 - y^2 = a^2$ is fundamental, one of the most elegant and useful representations of a [rectangular hyperbola](@entry_id:165798) arises when we rotate the coordinate system such that the asymptotes themselves become the coordinate axes. This occurs after a rotation of $45^\circ$ or $\frac{\pi}{4}$ radians.

Let's perform this transformation. The equations for a counter-clockwise rotation of the coordinate system by an angle $\theta$ are:
$$ x = x'\cos\theta - y'\sin\theta $$
$$ y = x'\sin\theta + y'\cos\theta $$
Setting $\theta = 45^\circ$, we have $\cos(45^\circ) = \sin(45^\circ) = \frac{1}{\sqrt{2}}$. The transformation equations become:
$$ x = \frac{x' - y'}{\sqrt{2}} $$
$$ y = \frac{x' + y'}{\sqrt{2}} $$
Substituting these into the standard [rectangular hyperbola](@entry_id:165798) equation $x^2 - y^2 = a^2$:
$$ \left(\frac{x' - y'}{\sqrt{2}}\right)^2 - \left(\frac{x' + y'}{\sqrt{2}}\right)^2 = a^2 $$
$$ \frac{(x')^2 - 2x'y' + (y')^2}{2} - \frac{(x')^2 + 2x'y' + (y')^2}{2} = a^2 $$
Combining the terms, we see that the $(x')^2$ and $(y')^2$ terms cancel out:
$$ \frac{-2x'y' - 2x'y'}{2} = a^2 $$
$$ -2x'y' = a^2 $$
$$ x'y' = -\frac{a^2}{2} $$
By setting the constant $k = -\frac{a^2}{2}$, we arrive at the remarkably simple equation $x'y' = k$. This equation represents a [rectangular hyperbola](@entry_id:165798) whose asymptotes are the $x'$ and $y'$ axes. This form is particularly prevalent in applications, such as in physics where it describes inverse relationships (e.g., Boyle's Law, $PV = \text{constant}$).

### The Algebraic Signature in the General Conic Equation

The true power of [analytic geometry](@entry_id:164266) lies in its ability to classify and analyze curves from their general algebraic form, even when they are not in a standard orientation. The general equation of a second-degree [plane curve](@entry_id:271353), or [conic section](@entry_id:164211), is given by:
$$ Ax^2 + Bxy + Cy^2 + Dx + Ey + F = 0 $$
where $A, B, C, D, E, F$ are real constants. The presence of the $Bxy$ term indicates that the conic's axes are rotated with respect to the coordinate axes.

To classify a conic from this general equation, we can use certain quantities, known as **invariants**, which do not change their value when the coordinate system is rotated or translated. For a [rectangular hyperbola](@entry_id:165798), the most important invariant is the **trace** of the quadratic part, defined as $I_1 = A+C$.

Let us prove that $A+C$ is invariant under rotation. After rotating the axes by an angle $\theta$, the new equation will have coefficients $A', B', C'$. The new coefficients of the quadratic terms are related to the old ones by:
$$ A' = A\cos^2\theta + B\sin\theta\cos\theta + C\sin^2\theta $$
$$ C' = A\sin^2\theta - B\sin\theta\cos\theta + C\cos^2\theta $$
Summing these two expressions yields:
$$ A' + C' = A(\cos^2\theta + \sin^2\theta) + C(\sin^2\theta + \cos^2\theta) $$
Using the fundamental trigonometric identity $\sin^2\theta + \cos^2\theta = 1$, we get:
$$ A' + C' = A + C $$
This confirms that the quantity $A+C$ is a rotational invariant.

Now, consider a general [rectangular hyperbola](@entry_id:165798). We can always rotate the coordinate system to align with the hyperbola's principal axes, resulting in an equation of the form $A'(x')^2 + C'(y')^2 + \dots = 0$. In this orientation, we know that the hyperbola is rectangular if $|A'| = |C'|$. Since for a hyperbola the coefficients $A'$ and $C'$ must have opposite signs, this implies $A' = -C'$, or $A' + C' = 0$. Because $A+C$ is an invariant, if $A'+C'=0$ in the rotated system, it must be that $A+C=0$ in the original, un-rotated system.

This gives us a simple, powerful, and necessary condition: **a non-[degenerate conic](@entry_id:167498) section given by the general equation is a [rectangular hyperbola](@entry_id:165798) if and only if $A+C=0$.**

### Applying the Principles: Identification and Analysis

The condition $A+C=0$ provides an immediate method for identifying a [rectangular hyperbola](@entry_id:165798) from its general equation. Let's consider a practical application of this principle.

Suppose we are given the equation of a [conic section](@entry_id:164211) that includes an unknown parameter, $k$:
$$ k x^2 + 8xy + (k-4)y^2 - 10x + 2y - 5 = 0 $$
and we are told that this equation represents a [rectangular hyperbola](@entry_id:165798) [@problem_id:2141660]. To find the value of $k$, we do not need to perform complex transformations. We can directly apply the invariant condition.

By comparing the given equation to the general form $Ax^2 + Bxy + Cy^2 + Dx + Ey + F = 0$, we identify the coefficients of the quadratic terms:
$A = k$
$C = k-4$

Applying the condition for a [rectangular hyperbola](@entry_id:165798), $A+C=0$:
$$ k + (k-4) = 0 $$
$$ 2k - 4 = 0 $$
$$ k = 2 $$
Thus, the equation must be $2x^2 + 8xy - 2y^2 - 10x + 2y - 5 = 0$. This demonstrates the utility of the invariant property for quickly determining the nature of a conic.

### The Mechanism of Coordinate Transformation

Once we have identified a conic as a [rectangular hyperbola](@entry_id:165798), we may wish to analyze it further by transforming it into a standard form without the cross-product ($xy$) term. This is accomplished by rotating the coordinate axes by a specific angle $\theta$. The goal is to find the angle that makes the new cross-product coefficient, $B'$, equal to zero.

The formula that provides this angle is:
$$ \cot(2\theta) = \frac{A-C}{B} $$

Let's continue with the example from before [@problem_id:2141660], where the equation for the [rectangular hyperbola](@entry_id:165798) was determined to be:
$$ 2x^2 + 8xy - 2y^2 - 10x + 2y - 5 = 0 $$
Here, the coefficients are $A=2$, $B=8$, and $C=-2$. We can now calculate the angle of rotation needed to eliminate the $xy$ term.

$$ \cot(2\theta) = \frac{2 - (-2)}{8} = \frac{4}{8} = \frac{1}{2} $$

To find the angle $\theta$, we first solve for $2\theta$. A positive value for $\cot(2\theta)$ implies that $2\theta$ is in the first or third quadrant. By convention, we choose the smallest positive angle of rotation, so we take $2\theta$ to be in the first quadrant ($0^\circ  2\theta  90^\circ$).
$$ 2\theta = \arccot\left(\frac{1}{2}\right) $$
This is equivalent to $2\theta = \arctan(2)$. Using a calculator, we find:
$$ 2\theta \approx 63.43^\circ $$
Therefore, the required angle of rotation is:
$$ \theta = \frac{2\theta}{2} \approx 31.7^\circ $$
Rotating the coordinate system by approximately $31.7^\circ$ would transform the equation into a new one in terms of $x'$ and $y'$, where the $x'y'$ term is absent, revealing the orientation of the hyperbola's principal axes.

In summary, the principle $A+C=0$ serves as a definitive algebraic signature for a [rectangular hyperbola](@entry_id:165798), while the rotation formula provides the mechanism to reorient the coordinate system for simplified analysis. These tools, rooted in the properties of rotational invariants, are cornerstones of the study of [conic sections](@entry_id:175122).