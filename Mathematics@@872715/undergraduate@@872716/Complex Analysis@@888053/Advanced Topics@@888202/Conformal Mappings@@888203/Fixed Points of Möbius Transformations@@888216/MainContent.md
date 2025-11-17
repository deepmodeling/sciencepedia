## Introduction
In complex analysis, Möbius transformations are fundamental functions that map the [extended complex plane](@entry_id:165233) to itself. To truly understand the geometry and dynamics of these transformations, one must first understand their fixed points—the points that remain unchanged under the mapping. These points are not mere curiosities; they are the anchors that dictate the entire structure and behavior of the transformation, from simple rotations and translations to more complex flows on the Riemann sphere. However, for an arbitrary transformation $T(z) = (az+b)/(cz+d)$, its underlying structure is not immediately obvious. A key question arises: how can we systematically analyze and classify these functions? The answer lies in identifying and characterizing their fixed points.

This article provides a comprehensive guide to this essential concept. The first chapter, **Principles and Mechanisms**, will delve into the core algebraic techniques for finding fixed points, establish the fundamental theorem on their number, and introduce their classification based on local dynamics. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate how this knowledge is applied to construct specific transformations and reveal deep connections to hyperbolic geometry, group theory, and dynamical systems. Finally, the **Hands-On Practices** section offers guided problems to solidify your understanding. By mastering the principles of fixed points, you will gain the tools to deconstruct and comprehend any Möbius transformation. We begin by establishing the foundational methods for their discovery and classification.

## Principles and Mechanisms

In the study of Möbius transformations, the concept of a **fixed point** is of central importance. A fixed point of a transformation $T$ is a point $z_0$ in the domain that is mapped to itself, such that $T(z_0) = z_0$. These points are not merely incidental; they act as anchors that govern the overall geometric and dynamic behavior of the transformation across the [extended complex plane](@entry_id:165233), $\hat{\mathbb{C}} = \mathbb{C} \cup \{\infty\}$. Understanding their existence, number, and nature is the key to unlocking the structure of any given Möbius transformation.

### Finding Fixed Points: The Algebraic Approach

A Möbius transformation is a function of the form $T(z) = \frac{az+b}{cz+d}$, where $a, b, c, d$ are complex numbers satisfying the non-degeneracy condition $ad-bc \neq 0$. To find the finite fixed points (those in $\mathbb{C}$), we set $T(z) = z$ and solve the resulting equation:

$$
\frac{az+b}{cz+d} = z
$$

Assuming $cz+d \neq 0$, we can multiply both sides by the denominator to clear the fraction:

$$
az+b = z(cz+d)
$$

Rearranging this expression gives us a standard quadratic equation:

$$
cz^2 + (d-a)z - b = 0
$$

The roots of this equation are the finite fixed points of the transformation $T(z)$.

As a concrete example, consider a transformation constructed by composing an inversion $I(z) = 1/z$ with a translation $S(w) = w+1$. The resulting transformation is $T(z) = S(I(z)) = 1/z + 1 = (z+1)/z$. To find its fixed points, we solve $T(z)=z$, which yields the equation $z^2 - z - 1 = 0$. Applying the quadratic formula, we find two distinct fixed points: $z = \frac{1 \pm \sqrt{5}}{2}$ [@problem_id:2241308]. These are the famous golden ratio and its conjugate, illustrating how even simple compositions lead to significant mathematical constants as fixed points.

An important structural property of Möbius transformations is that their definition is homogeneous in the coefficients. If we scale all four coefficients $a,b,c,d$ by the same non-zero complex number $\lambda$, the transformation itself remains unchanged:
$$
T(z) = \frac{\lambda(az+b)}{\lambda(cz+d)} = \frac{az+b}{cz+d}
$$
This directly implies that the fixed points are also unchanged. The fixed point equation becomes $\lambda(cz^2 + (d-a)z - b) = 0$, which has the exact same roots as the unscaled equation. For instance, the transformations $T_1(z) = \frac{z + 2 - 2i}{z + 2 + i}$ and $T_2(z) = \frac{(1-i)z - 4i}{(1-i)z + 3-i}$ are in fact identical, since the numerator and denominator of $T_1$ can be multiplied by $(1-i)$ to obtain $T_2$. Consequently, they share the same set of fixed points [@problem_id:2241307]. This shows that a Möbius transformation is uniquely determined by the *ratios* of its coefficients, not their [absolute values](@entry_id:197463).

### The Fundamental Theorem: Counting the Fixed Points

A natural question arises: how many fixed points can a Möbius transformation have? The algebraic approach provides a clear answer. The fixed point equation, $cz^2 + (d-a)z - b = 0$, is a quadratic polynomial.

If $c \neq 0$, the equation is genuinely quadratic and can have at most two distinct roots in the complex plane.

If $c = 0$, the equation becomes linear: $(d-a)z - b = 0$.
*   If $a \neq d$, this linear equation has exactly one solution, $z = b/(d-a)$.
*   If $a = d$, the equation becomes $-b=0$. If $b \neq 0$, there is no solution, meaning there are no finite fixed points. If $b=0$, the equation is $0=0$, which is true for all $z$. In this case, with $c=0$ and $b=0$, the transformation is $T(z) = (a/d)z$. Since $ad-bc=ad \neq 0$, we must have $a \neq 0$ and $d \neq 0$. If $a=d$, then $T(z)=z$, which is the **[identity transformation](@entry_id:264671)**.

So far, we have only considered finite fixed points. We must also account for the **[point at infinity](@entry_id:154537)**, $\infty$. A [point at infinity](@entry_id:154537) is a fixed point if $T(\infty) = \infty$. The value of $T(\infty)$ is defined as the limit:
$$
T(\infty) = \lim_{z \to \infty} \frac{az+b}{cz+d} = \lim_{z \to \infty} \frac{a+b/z}{c+d/z}
$$
If $c \neq 0$, this limit is $a/c$, which is a finite complex number. Thus, for $\infty$ to be a fixed point, it is necessary and sufficient that $c=0$ [@problem_id:2241325].

Combining these observations leads to a cornerstone result:

**A non-identity Möbius transformation has at most two fixed points in the [extended complex plane](@entry_id:165233) $\hat{\mathbb{C}}$.**

Let's summarize the possibilities for a non-[identity transformation](@entry_id:264671) $T(z)$:
1.  **Two distinct fixed points:** This occurs if the quadratic equation has two distinct roots (if $c \neq 0$) or if $c=0$ and $a \neq d$ (one finite fixed point and one at $\infty$).
2.  **One unique fixed point:** This occurs if the quadratic has a repeated root (if $c \neq 0$) or if $c=0$, $a=d$, and $b \neq 0$. The latter case corresponds to a pure translation $T(z)=z+b'$, which has no finite fixed points, leaving $\infty$ as the sole fixed point [@problem_id:2241327].

This theorem has a powerful corollary: **If a Möbius transformation has three or more fixed points, it must be the [identity transformation](@entry_id:264671).** If a transformation fixes three distinct finite points, the quadratic equation $cz^2+(d-a)z-b=0$ must be satisfied by three distinct values, which is only possible if all its coefficients are zero: $c=0$, $d-a=0$, and $b=0$. These conditions, combined with $ad-bc \neq 0$, imply $a=d \neq 0$ and $b=c=0$. The transformation is thus $T(z) = (az/a) = z$, the identity map [@problem_id:2241322]. This principle is so fundamental that it guarantees, for example, that no single non-identity Möbius transformation could possibly have all four vertices of a square as its fixed points [@problem_id:2241352].

### Classifying Fixed Points: A Dynamical Perspective

Beyond simply counting fixed points, we can classify them based on the transformation's behavior in their vicinity. This provides a dynamical picture of how points move under repeated application of the transformation, or iteration. The key tool for this classification is the derivative of the transformation evaluated at the fixed point, $T'(z_0)$, also known as the **multiplier** of the fixed point.

For a fixed point $z_0$ and a point $z$ very close to it, Taylor's theorem gives us a linear approximation:
$$
T(z) - T(z_0) \approx T'(z_0)(z-z_0)
$$
Since $T(z_0) = z_0$, this simplifies to:
$$
T(z) - z_0 \approx T'(z_0)(z-z_0)
$$
This approximation reveals that near a fixed point, a Möbius transformation acts like a simple scaling by the multiplier $T'(z_0)$. The magnitude of this multiplier determines the stability of the fixed point under iteration.

*   If $|T'(z_0)|  1$, the fixed point is **attractive**. Each iteration brings points closer to $z_0$ by a factor of approximately $|T'(z_0)|$. A sequence $z_{n+1} = T(z_n)$ starting sufficiently close to $z_0$ will converge to $z_0$.
*   If $|T'(z_0)| > 1$, the fixed point is **repelling**. Each iteration pushes points away from $z_0$. Nearby sequences will diverge from the fixed point.
*   If $|T'(z_0)| = 1$, the fixed point is **indifferent**. The behavior is more subtle and depends on whether the multiplier is a root of unity.

Consider the transformation $T(z) = \frac{9iz - 9}{z + 9i}$ [@problem_id:2241328]. Its fixed points are the solutions to $z^2 = -9$, which are $z_1 = 3i$ and $z_2 = -3i$. The derivative is $T'(z) = \frac{-72}{(z+9i)^2}$.
*   At $z_1 = 3i$, the derivative is $T'(3i) = \frac{-72}{(12i)^2} = \frac{1}{2}$. Since $|1/2|  1$, the point $3i$ is an [attractive fixed point](@entry_id:181694).
*   At $z_2 = -3i$, the derivative is $T'(-3i) = \frac{-72}{(6i)^2} = 2$. Since $|2| > 1$, the point $-3i$ is a [repelling fixed point](@entry_id:189650).
This example clearly illustrates how the derivative's magnitude dictates the dynamics of the map near its fixed points.

### Advanced Properties of Fixed Points

The fixed points and their multipliers are deeply woven into the fabric of the transformation, leading to several elegant properties.

#### The Multiplier Product Theorem

One such remarkable property relates the multipliers of a transformation with two distinct fixed points.

**Theorem:** If a Möbius transformation $T$ has two distinct fixed points $z_1$ and $z_2$ (which may be finite or infinite), then the product of their multipliers is unity: $T'(z_1)T'(z_2) = 1$.

(Note: If one fixed point, say $z_2$, is at infinity, the derivative $T'(z_2)$ is defined via a coordinate change, e.g., $w=1/z$. The result still holds.)

This theorem provides a powerful consistency check. For example, for a transformation $T(z) = \frac{(2+i)z-2}{z+i-1}$, the fixed points are $z_1=1$ and $z_2=2$. One can compute the derivatives $T'(1) = 1-i$ and $T'(2) = \frac{1+i}{2}$. Their product is $(1-i)\frac{1+i}{2} = \frac{1-i^2}{2} = \frac{2}{2} = 1$, verifying the theorem [@problem_id:2241344]. This implies that if one fixed point is attractive ($|T'(z_1)|  1$), the other must be repelling ($|T'(z_2)| = 1/|T'(z_1)| > 1$), unless both are indifferent.

#### Parabolic Transformations

What happens when a transformation has exactly one fixed point? In this case, the quadratic $cz^2+(d-a)z-b=0$ must have a double root. This happens when its discriminant is zero. A deeper analysis reveals that for a transformation with a single fixed point $z_0$, the multiplier must be unity: $T'(z_0)=1$. Such transformations are called **parabolic**.

The [linear approximation](@entry_id:146101) $T(z)-z_0 \approx 1 \cdot (z-z_0)$ is no longer informative. The dynamics are more subtle, often described as a "flow" towards or away from the fixed point. A key insight is that any [parabolic transformation](@entry_id:178588) is conjugate to a simple translation. This means there exists a conjugating map $S$ such that $T = S^{-1} \circ U \circ S$, where $U(w) = w+t$ is a translation. This allows us to construct parabolic maps with specified properties. For instance, to find a non-[identity transformation](@entry_id:264671) with a single fixed point at $z_0=2$ (which implies $T'(2)=1$), we can conjugate the translation $U(w)=w+t$ by the map $S(z)=\frac{1}{z-2}$. The resulting transformation $T(z) = S^{-1}(S(z)+t)$ will have the desired properties, with the specific form depending on the translation amount $t$ [@problem_id:2241333].

#### Periodic Points and Involutions

Finally, it is useful to generalize the concept of a fixed point to that of a **periodic point**. A point $z_0$ is a periodic point of period $n$ for $T$ if $T^n(z_0) = z_0$ and $T^k(z_0) \neq z_0$ for $1 \le k  n$, where $T^n$ denotes the $n$-th iterate of $T$. A fixed point is simply a periodic point of period 1.

The fixed points of $T^n$ include all fixed points of $T$, but may include other points as well. For example, consider the transformation $T(z) = \frac{3z+4}{2z-3}$. A direct calculation shows that its second iterate is the identity map: $T^2(z) = T(T(z)) = z$ for all $z$. Such a transformation is called an **involution**. For an involution, *every* point in $\hat{\mathbb{C}}$ is a fixed point of $T^2$. However, only two of these points are fixed points of $T$ itself (the solutions to $2z^2-6z-4=0$). Any other point $z_0$ is a period-2 point: $T(z_0) \neq z_0$, but $T(T(z_0))=z_0$ [@problem_id:2241331]. This highlights the richer dynamical structure that emerges when considering iterates of a transformation.