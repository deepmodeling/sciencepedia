## Introduction
The [hyperbolic functions](@entry_id:165175), sinh and cosh, are familiar tools from real calculus, defined in terms of the [exponential function](@entry_id:161417). However, their true depth and elegance are fully revealed only when they are extended into the complex plane. This transition is far more than a formal exercise; it uncovers a rich structure of hidden properties and surprising connections, most notably with trigonometric functions, and introduces new behaviors like periodicity that are absent on the real line. This article bridges the gap between the real and complex domains, exploring the fundamental properties and broad utility of hyperbolic functions with complex arguments.

Through three comprehensive chapters, this article will guide you from first principles to practical applications. "Principles and Mechanisms" establishes the foundational definitions, identities, and analytic properties of complex sinh and cosh. "Applications and Interdisciplinary Connections" showcases their power in solving problems in mathematics, physics, and engineering. Finally, "Hands-On Practices" offers a chance to apply and reinforce this knowledge. We will begin by exploring the core definitions and algebraic rules that govern these fascinating functions.

## Principles and Mechanisms

In extending real-valued calculus to the complex plane, we find that familiar functions often reveal richer structures and deeper connections. The hyperbolic [sine and cosine functions](@entry_id:172140), which in [real analysis](@entry_id:145919) are defined in terms of the [exponential function](@entry_id:161417), provide a prime example of this phenomenon. Their generalization to a complex argument $z$ serves not only as a formal extension but also uncovers profound relationships with the trigonometric functions, illuminates the constraints of [analyticity](@entry_id:140716), and introduces new periodic behaviors.

### Definitions and Basic Identities

We begin by defining the complex hyperbolic [sine and cosine functions](@entry_id:172140) in a manner that directly extends their real-valued counterparts. For any complex number $z \in \mathbb{C}$, we define **hyperbolic sine** ($\sinh$) and **hyperbolic cosine** ($\cosh$) as:

$$
\sinh(z) = \frac{\exp(z) - \exp(-z)}{2}
$$

$$
\cosh(z) = \frac{\exp(z) + \exp(-z)}{2}
$$

These definitions retain the fundamental symmetry properties observed on the real line. By substituting $-z$ into the definitions, we can readily verify the parity of these functions. For the hyperbolic cosine:
$$
\cosh(-z) = \frac{\exp(-z) + \exp(-(-z))}{2} = \frac{\exp(-z) + \exp(z)}{2} = \cosh(z)
$$
This demonstrates that **$\cosh(z)$ is an even function**. For the hyperbolic sine:
$$
\sinh(-z) = \frac{\exp(-z) - \exp(-(-z))}{2} = \frac{\exp(-z) - \exp(z)}{2} = - \frac{\exp(z) - \exp(-z)}{2} = -\sinh(z)
$$
Thus, **$\sinh(z)$ is an [odd function](@entry_id:175940)**. These symmetry properties are foundational to their behavior in the complex plane [@problem_id:2245630].

A cornerstone identity for real [hyperbolic functions](@entry_id:165175) is $\cosh^2(x) - \sinh^2(x) = 1$. We can verify that this identity holds for any complex argument $z$. By squaring the exponential definitions:
$$
\cosh^2(z) = \left(\frac{\exp(z) + \exp(-z)}{2}\right)^2 = \frac{\exp(2z) + 2\exp(z)\exp(-z) + \exp(-2z)}{4} = \frac{\exp(2z) + 2 + \exp(-2z)}{4}
$$
$$
\sinh^2(z) = \left(\frac{\exp(z) - \exp(-z)}{2}\right)^2 = \frac{\exp(2z) - 2\exp(z)\exp(-z) + \exp(-2z)}{4} = \frac{\exp(2z) - 2 + \exp(-2z)}{4}
$$
Subtracting the second expression from the first yields:
$$
\cosh^2(z) - \sinh^2(z) = \frac{(\exp(2z) + 2 + \exp(-2z)) - (\exp(2z) - 2 + \exp(-2z))}{4} = \frac{4}{4} = 1
$$
This fundamental Pythagorean-like identity, **$\cosh^2(z) - \sinh^2(z) = 1$**, is therefore valid for all $z \in \mathbb{C}$.

### The Bridge to Trigonometry

One of the most elegant results in complex analysis is the intimate connection between hyperbolic and [trigonometric functions](@entry_id:178918). This relationship becomes transparent when we consider purely imaginary arguments. Let's replace $z$ with $iz$ in the definition of $\cosh(z)$:
$$
\cosh(iz) = \frac{\exp(iz) + \exp(-iz)}{2}
$$
This expression is precisely the exponential definition of the complex cosine function, $\cos(z)$. Thus, we arrive at the remarkable identity:
$$
\cosh(iz) = \cos(z)
$$
Similarly, for the hyperbolic sine:
$$
\sinh(iz) = \frac{\exp(iz) - \exp(-iz)}{2} = i \left( \frac{\exp(iz) - \exp(-iz)}{2i} \right) = i\sin(z)
$$
These two relations, **$\cosh(iz) = \cos(z)$** and **$\sinh(iz) = i\sin(z)$**, form a bridge between the two families of functions [@problem_id:2245602]. They allow us to translate identities from trigonometry into the language of [hyperbolic functions](@entry_id:165175), and vice versa. For example, the trigonometric identity $\cos^2(z) + \sin^2(z) = 1$ can be seen as a direct consequence of the hyperbolic identity. By substituting $z$ with $iz$ in $\cosh^2(z) - \sinh^2(z) = 1$, we get:
$$
\cosh^2(iz) - \sinh^2(iz) = 1 \implies (\cos(z))^2 - (i\sin(z))^2 = 1 \implies \cos^2(z) - i^2\sin^2(z) = 1 \implies \cos^2(z) + \sin^2(z) = 1
$$

### Decomposition into Real and Imaginary Components

To understand the behavior of these functions as mappings from $\mathbb{C}$ to $\mathbb{C}$, it is essential to separate them into their real and imaginary parts. Let $z = x + iy$, where $x, y \in \mathbb{R}$. We use the property $\exp(x+iy) = \exp(x)\exp(iy)$ and Euler's formula, $\exp(iy) = \cos(y) + i\sin(y)$.

For $\cosh(z)$:
$$
\cosh(x+iy) = \frac{\exp(x+iy) + \exp(-x-iy)}{2} = \frac{\exp(x)(\cos(y) + i\sin(y)) + \exp(-x)(\cos(y) - i\sin(y))}{2}
$$
Grouping the real and imaginary terms:
$$
\cosh(x+iy) = \left(\frac{\exp(x) + \exp(-x)}{2}\right)\cos(y) + i\left(\frac{\exp(x) - \exp(-x)}{2}\right)\sin(y)
$$
Recognizing the definitions of the real hyperbolic functions, we obtain the standard decomposition [@problem_id:2245607]:
$$
\cosh(x+iy) = \cosh(x)\cos(y) + i\sinh(x)\sin(y)
$$
A similar derivation for $\sinh(z)$ yields [@problem_id:2245631]:
$$
\sinh(x+iy) = \sinh(x)\cos(y) + i\cosh(x)\sin(y)
$$
These formulas are indispensable for computation and analysis. For instance, to find the real and imaginary parts of $\cosh(2z)$, we simply substitute $2x$ and $2y$ into the formula for $\cosh(z)$, yielding $\text{Re}(\cosh(2z)) = \cosh(2x)\cos(2y)$ and $\text{Im}(\cosh(2z)) = \sinh(2x)\sin(2y)$ [@problem_id:2245599].

These decompositions also allow us to investigate the modulus of hyperbolic functions. While $\cosh^2(z) - \sinh^2(z) = 1$, the same is not true for their squared moduli. Using the decompositions, we find:
$$
|\cosh(z)|^2 = (\cosh(x)\cos(y))^2 + (\sinh(x)\sin(y))^2 = \cosh^2(x)\cos^2(y) + \sinh^2(x)\sin^2(y)
$$
$$
|\sinh(z)|^2 = (\sinh(x)\cos(y))^2 + (\cosh(x)\sin(y))^2 = \sinh^2(x)\cos^2(y) + \cosh^2(x)\sin^2(y)
$$
Subtracting the second from the first and regrouping terms gives:
$$
|\cosh(z)|^2 - |\sinh(z)|^2 = (\cosh^2(x) - \sinh^2(x))\cos^2(y) - (\cosh^2(x) - \sinh^2(x))\sin^2(y)
$$
Using the real identity $\cosh^2(x) - \sinh^2(x) = 1$, this simplifies to:
$$
|\cosh(z)|^2 - |\sinh(z)|^2 = \cos^2(y) - \sin^2(y) = \cos(2y)
$$
This elegant result shows that the difference in squared moduli depends only on the imaginary part of $z$, a non-obvious property that follows directly from the function's structure [@problem_id:2245640].

### Analyticity and Harmonic Nature

The functions $\exp(z)$ and $\exp(-z)$ are **entire**, meaning they are analytic on the entire complex plane. Since $\sinh(z)$ and $\cosh(z)$ are [linear combinations](@entry_id:154743) of these two [entire functions](@entry_id:176232), they are themselves entire. This is a profound property, which implies that they are infinitely differentiable and can be represented by a Taylor series that converges everywhere.

A direct consequence of [analyticity](@entry_id:140716) is that the real and imaginary parts of the function must satisfy the **Cauchy-Riemann equations**. Let $f(z) = u(x,y) + iv(x,y)$. The equations are $\frac{\partial u}{\partial x} = \frac{\partial v}{\partial y}$ and $\frac{\partial u}{\partial y} = -\frac{\partial v}{\partial x}$. Let's verify this for $f(z) = \cosh(z)$, where $u(x,y) = \cosh(x)\cos(y)$ and $v(x,y) = \sinh(x)\sin(y)$. We compute the [partial derivatives](@entry_id:146280):
$$
\frac{\partial u}{\partial x} = \sinh(x)\cos(y) \quad , \quad \frac{\partial v}{\partial y} = \sinh(x)\cos(y)
$$
$$
\frac{\partial u}{\partial y} = -\cosh(x)\sin(y) \quad , \quad \frac{\partial v}{\partial x} = \cosh(x)\sin(y)
$$
The equations $\frac{\partial u}{\partial x} = \frac{\partial v}{\partial y}$ and $\frac{\partial u}{\partial y} = -\frac{\partial v}{\partial x}$ are satisfied for all $(x,y)$, confirming the [analyticity](@entry_id:140716) of $\cosh(z)$ [@problem_id:2245629].

Furthermore, the real and imaginary parts of any [analytic function](@entry_id:143459) must be **harmonic**, meaning they satisfy the two-dimensional **Laplace's equation**, $\nabla^2 \phi = \frac{\partial^2 \phi}{\partial x^2} + \frac{\partial^2 \phi}{\partial y^2} = 0$. Let's test this for $u(x,y) = \text{Re}(\cosh(z))$. We compute the second-order partial derivatives:
$$
\frac{\partial^2 u}{\partial x^2} = \frac{\partial}{\partial x}(\sinh(x)\cos(y)) = \cosh(x)\cos(y)
$$
$$
\frac{\partial^2 u}{\partial y^2} = \frac{\partial}{\partial y}(-\cosh(x)\sin(y)) = -\cosh(x)\cos(y)
$$
Adding these together gives:
$$
\nabla^2 u = \frac{\partial^2 u}{\partial x^2} + \frac{\partial^2 u}{\partial y^2} = \cosh(x)\cos(y) - \cosh(x)\cos(y) = 0
$$
Thus, $u(x,y) = \cosh(x)\cos(y)$ is indeed a harmonic function, as expected for the real part of an [analytic function](@entry_id:143459) [@problem_id:2245586].

### Periodicity and Invertibility

While the real functions $\sinh(x)$ and $\cosh(x)$ are not periodic, their complex extensions are. This [periodicity](@entry_id:152486) is purely imaginary and stems from the $2\pi i$ [periodicity](@entry_id:152486) of the [exponential function](@entry_id:161417), $\exp(z+2\pi i) = \exp(z)$.
$$
\cosh(z + 2\pi i) = \frac{\exp(z+2\pi i) + \exp(-(z+2\pi i))}{2} = \frac{\exp(z) + \exp(-z)\exp(-2\pi i)}{2} = \frac{\exp(z) + \exp(-z)}{2} = \cosh(z)
$$
A similar calculation shows $\sinh(z + 2\pi i) = \sinh(z)$. Both functions are periodic with a [fundamental period](@entry_id:267619) of $2\pi i$.

This [periodicity](@entry_id:152486) implies that the hyperbolic functions are not one-to-one (injective) in the complex plane, which complicates the notion of an inverse. To find all complex numbers $w$ such that $\sinh(w) = \sinh(z_0)$ for a given $z_0$, we must solve the equation $\frac{\exp(w) - \exp(-w)}{2} = \frac{\exp(z_0) - \exp(-z_0)}{2}$. Letting $Y = \exp(w)$ and $C = \exp(z_0) - \exp(-z_0)$, this is equivalent to solving the quadratic equation $Y^2 - CY - 1 = 0$. The two solutions are $Y = \exp(z_0)$ and $Y = -\exp(-z_0)$. This leads to two families of solutions for $w$:
1. $\exp(w) = \exp(z_0) \implies w = z_0 + 2n\pi i$ for $n \in \mathbb{Z}$.
2. $\exp(w) = -\exp(-z_0) = \exp(i\pi)\exp(-z_0) = \exp(i\pi - z_0) \implies w = i\pi - z_0 + 2n\pi i$ for $n \in \mathbb{Z}$.

This analysis reveals a richer structure than simple [periodicity](@entry_id:152486) might suggest. For any given value in the range of $\sinh$, there are two distinct series of preimages in the domain [@problem_id:2245588].

### Inverse Hyperbolic Functions and their Logarithmic Forms

The multi-valued nature of the complex [hyperbolic functions](@entry_id:165175) necessitates a careful definition of their inverses. We define the **inverse hyperbolic sine**, $\text{arsinh}(w)$, as the set of all complex numbers $z$ such that $\sinh(z) = w$. To find an explicit formula, we solve for $z$:
$$
w = \frac{\exp(z) - \exp(-z)}{2}
$$
Multiplying by $2\exp(z)$ gives $2w\exp(z) = \exp(2z) - 1$. Let $U = \exp(z)$, this is a quadratic equation:
$$
U^2 - 2wU - 1 = 0
$$
The quadratic formula gives $U = \frac{2w \pm \sqrt{4w^2 + 4}}{2} = w \pm \sqrt{w^2 + 1}$. Since $\exp(z)$ cannot be zero, and the product of the roots is $-1$, we can write this compactly. Taking the logarithm gives the solutions for $z$:
$$
z = \text{arsinh}(w) = \ln(w + \sqrt{w^2+1})
$$
This expression is multi-valued due to both the complex square root (which has two branches) and the [complex logarithm](@entry_id:174857) (which is infinitely valued). The two branches of the square root, $\pm\sqrt{w^2+1}$, are related because $(w+\sqrt{w^2+1})(w-\sqrt{w^2+1}) = w^2 - (w^2+1) = -1$. Taking logs, $\ln(w+\sqrt{w^2+1}) + \ln(w-\sqrt{w^2+1}) = \ln(-1) = i\pi + 2k\pi i$. This connects the two solution families found in the previous section.

To work with a single-valued function, we define the **[principal value](@entry_id:192761)**, $\text{Arsinh}(w)$, by choosing the [principal values](@entry_id:189577) of both the square root and the logarithm.

As an example, let's find the [principal value](@entry_id:192761) of $z$ that solves $\sinh(z) = 2i$ [@problem_id:2245610]. Using the formula for the [principal value](@entry_id:192761):
$$
z = \text{Arsinh}(2i) = \text{Log}(2i + \sqrt{(2i)^2 + 1})
$$
First, we compute the term inside the square root: $(2i)^2 + 1 = -4 + 1 = -3$. The [principal value](@entry_id:192761) of the square root of $-3$ is $\sqrt{-3} = i\sqrt{3}$. Substituting this back:
$$
z = \text{Log}(2i + i\sqrt{3}) = \text{Log}(i(2+\sqrt{3}))
$$
To compute the [principal logarithm](@entry_id:195969) $\text{Log}(W) = \ln|W| + i\text{Arg}(W)$, we find the modulus and [principal argument](@entry_id:171517) of $W = i(2+\sqrt{3})$:
$$
|W| = |i(2+\sqrt{3})| = 2+\sqrt{3}
$$
$$
\text{Arg}(W) = \frac{\pi}{2} \quad (\text{since } 2+\sqrt{3} > 0)
$$
Therefore, the principal solution is:
$$
z = \ln(2+\sqrt{3}) + i\frac{\pi}{2}
$$
This example illustrates the complete process of inverting a complex hyperbolic function, requiring careful application of the definitions of principal branches for multi-valued operations.