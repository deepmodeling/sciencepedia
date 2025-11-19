## Introduction
The ability to differentiate functions is a cornerstone of calculus, providing the tools to analyze rates of change and local behavior. In complex analysis, while the derivative is defined through a limit process analogous to its real counterpart, relying on this definition for every calculation is impractical and cumbersome. The true power of [complex calculus](@entry_id:167282) is unlocked by a set of elegant and efficient rules for differentiation that mirror those of real-variable calculus, but which are contingent on the crucial property of analyticity.

This article serves as a comprehensive guide to mastering these rules. The first chapter, **Principles and Mechanisms**, establishes the fundamental rules—including the product, quotient, and chain rules—and explores the critical boundary where they no longer apply, delving into non-analytic functions. The second chapter, **Applications and Interdisciplinary Connections**, demonstrates how these rules underpin advanced techniques within complex analysis and serve as foundational tools in fields as diverse as fluid dynamics, [differential geometry](@entry_id:145818), and general relativity. Finally, **Hands-On Practices** provides a set of curated problems to solidify your understanding and apply these concepts to concrete examples, bridging the gap from theory to practical skill.

## Principles and Mechanisms

Having established the definition of the [complex derivative](@entry_id:168773) and the fundamental importance of the Cauchy-Riemann equations in the preceding chapter, we now turn to the practical machinery of differentiation. While the limit definition is the bedrock of the derivative, its direct application for every calculation is cumbersome. Fortunately, a familiar set of rules, analogous to those in real-variable calculus, governs the differentiation of analytic functions. This chapter develops these rules, explores their powerful applications, investigates their limitations, and reveals some of the profound structural consequences they entail for the theory of complex functions.

### The Standard Rules for Analytic Functions

The rules for differentiating sums, products, quotients, and compositions of complex functions are formally identical to their real-variable counterparts. Their validity rests on the assumption that the functions involved are **analytic** in a domain. Analyticity, the property of being complex differentiable in an open neighborhood, is the crucial enabling condition for this powerful calculus to unfold.

The most basic rules are linearity and the power rule.

-   **Linearity**: If $f(z)$ and $g(z)$ are analytic and $\alpha, \beta$ are complex constants, then $\alpha f(z) + \beta g(z)$ is analytic, and its derivative is given by:
    $$
    \frac{d}{dz}(\alpha f(z) + \beta g(z)) = \alpha f'(z) + \beta g'(z)
    $$

-   **The Power Rule**: For any positive integer $n$, the function $f(z) = z^n$ is analytic on the entire complex plane (it is an entire function), and its derivative is given by:
    $$
    \frac{d}{dz}z^n = nz^{n-1}
    $$
    This fundamental result can be derived directly from the limit definition. Consider the [difference quotient](@entry_id:136462) at an arbitrary point $a \in \mathbb{C}$. Using the algebraic factorization $z^n - a^n = (z-a)(z^{n-1} + z^{n-2}a + \dots + a^{n-1})$, we have:
    $$
    f'(a) = \lim_{z \to a} \frac{z^n - a^n}{z-a} = \lim_{z \to a} \sum_{k=0}^{n-1} z^k a^{n-1-k}
    $$
    Since each term in the sum is a continuous function of $z$, we can evaluate the limit by direct substitution, $z=a$:
    $$
    f'(a) = \sum_{k=0}^{n-1} a^k a^{n-1-k} = \sum_{k=0}^{n-1} a^{n-1}
    $$
    The sum consists of $n$ identical terms, yielding $n a^{n-1}$ [@problem_id:2264518]. It is a testament to the consistency of complex analysis that this rule, so familiar from real numbers, holds perfectly. In fact, this rule is valid for any complex exponent $n$, a more general result that we will be equipped to prove after developing the [complex logarithm](@entry_id:174857).

Building upon these, we have the product, quotient, and chain rules.

-   **The Product Rule**: For two analytic functions $f(z)$ and $g(z)$:
    $$
    \frac{d}{dz}(f(z)g(z)) = f'(z)g(z) + f(z)g'(z)
    $$

-   **The Quotient Rule**: For two analytic functions $f(z)$ and $g(z)$, where $g(z) \neq 0$:
    $$
    \frac{d}{dz}\left(\frac{f(z)}{g(z)}\right) = \frac{f'(z)g(z) - f(z)g'(z)}{[g(z)]^2}
    $$

-   **The Chain Rule**: If $g(z)$ is analytic in a domain $D$ and $f(w)$ is analytic in a domain containing the range of $g$, then the composite function $F(z) = f(g(z))$ is analytic in $D$, and its derivative is:
    $$
    F'(z) = f'(g(z)) g'(z)
    $$

These rules, particularly the chain rule, form the cornerstone of practical differentiation, enabling us to differentiate complex polynomials, [rational functions](@entry_id:154279), and compositions involving [elementary functions](@entry_id:181530) like $\exp(z)$, $\sin(z)$, and $\cos(z)$ with the same procedural ease as in real calculus.

### Techniques and Applications

With the basic rules established, we can explore several powerful techniques that they unlock.

#### Implicit Differentiation

Sometimes, a functional relationship is given implicitly by an equation that is not easily solved for one variable in terms of the other. If we can assume that the equation implicitly defines an analytic function, we can differentiate the entire equation to find its derivative.

Consider a function $w(z)$ defined implicitly by the relation $e^{w(z)} - w(z)z = 0$. To find $\frac{dw}{dz}$, we differentiate both sides with respect to $z$, carefully applying the chain and product rules:
$$
\frac{d}{dz}(e^{w}) - \frac{d}{dz}(wz) = 0
$$
$$
e^w \frac{dw}{dz} - \left( \frac{dw}{dz}z + w \cdot 1 \right) = 0
$$
Now, we can algebraically solve for $\frac{dw}{dz}$:
$$
(e^w - z)\frac{dw}{dz} = w \implies \frac{dw}{dz} = \frac{w}{e^w - z}
$$
Using the original relation $e^w = wz$, we can simplify the denominator to obtain a more compact expression:
$$
\frac{dw}{dz} = \frac{w}{wz - z} = \frac{w}{z(w-1)}
$$
This result is valid for $z \neq 0$ and $w(z) \neq 1$ [@problem_id:2264528]. This technique is not limited to a single function. If several [analytic functions](@entry_id:139584) are linked by an identity, [implicit differentiation](@entry_id:137929) can reveal hidden relationships between their derivatives. For instance, if three [analytic functions](@entry_id:139584) $f(z)$, $g(z)$, and $h(z)$ satisfy $f(z)^2 + g(z)^2 + h(z)^2 = C$ for some constant $C$, differentiating with respect to $z$ yields $2f(z)f'(z) + 2g(z)g'(z) + 2h(z)h'(z) = 0$. This implies that if we know the values of the functions and some of their derivatives at a point, we can determine the remaining derivative [@problem_id:2264514].

#### Derivatives of Composite Functions and Symmetries

The [chain rule](@entry_id:147422) is especially potent when combined with functional properties like symmetry. For example, if a function $f(w)$ is known to be **even**, meaning $f(w) = f(-w)$ for all $w$, its derivative must be **odd**. We can see this by differentiating the identity:
$$
\frac{d}{dw}f(w) = \frac{d}{dw}f(-w) \implies f'(w) = f'(-w) \cdot (-1) = -f'(-w)
$$
This tells us that $f'(w) = -f'(-w)$, the definition of an [odd function](@entry_id:175940). This simple fact can be leveraged in calculations. Suppose we construct a new function $g(z) = f(z^2)$ from an even function $f$. By the [chain rule](@entry_id:147422), its derivative is $g'(z) = f'(z^2) \cdot 2z$. Using the odd property of the derivative, $f'(z^2) = -f'(-z^2)$, we can express the result in a different form: $g'(z) = (-f'(-z^2)) \cdot 2z = -2z f'(-z^2)$ [@problem_id:2264515]. Such manipulations are common in the study of [power series](@entry_id:146836) and [special functions](@entry_id:143234).

A related application of the chain rule occurs when a complex function is composed with a differentiable path parameterized by a real variable. If $\gamma(t)$ is a [complex-valued function](@entry_id:196054) of a real variable $t$, and $f(z)$ is an analytic function, the derivative of the composition $F(t) = f(\gamma(t))$ with respect to $t$ is given by $F'(t) = f'(\gamma(t))\gamma'(t)$. For example, if $F(t) = \tan(\gamma(t))$ with $\gamma(t) = Pt + Qt^3$, its derivative is:
$$
\frac{dF}{dt} = \sec^2(\gamma(t)) \cdot \gamma'(t) = \sec^2(Pt+Qt^3) \cdot (P+3Qt^2)
$$
This type of derivative is fundamental to the theory of [contour integration](@entry_id:169446), where we integrate functions along paths in the complex plane [@problem_id:2264532].

### The Boundary of Analyticity: When the Rules Fail

The elegant machinery of [differentiation rules](@entry_id:145443) relies entirely on the analyticity of the functions involved. A common pitfall is to apply these rules to functions that are not analytic. Functions that depend on $\operatorname{Re}(z)$, $\operatorname{Im}(z)$, $\bar{z}$, or $|z|$ are typically not analytic, even if they are constructed from analytic components. For these functions, we must return to first principles—the Cauchy-Riemann equations—to investigate differentiability. The results are often surprising.

#### Case Study: $f(z) = z \operatorname{Re}(z)$

Consider the function $f(z) = z \operatorname{Re}(z)$. It is tempting to apply the [product rule](@entry_id:144424), but this is incorrect because $\operatorname{Re}(z)$ is not an analytic function. To determine where $f(z)$ is differentiable, we must check the Cauchy-Riemann equations. Let $z = x+iy$. Then $f(z) = (x+iy)x = x^2 + ixy$. The real and imaginary parts are $u(x,y) = x^2$ and $v(x,y) = xy$. Their [partial derivatives](@entry_id:146280) are:
$$
u_x = 2x, \quad u_y = 0, \quad v_x = y, \quad v_y = x
$$
The Cauchy-Riemann equations, $u_x = v_y$ and $u_y = -v_x$, require:
$$
2x = x \quad \text{and} \quad 0 = -y
$$
This system of equations has only one solution: $x=0$ and $y=0$. Therefore, the Cauchy-Riemann equations hold only at the point $z=0$. Since the [partial derivatives](@entry_id:146280) are continuous everywhere, this is sufficient to conclude that $f(z)$ is complex differentiable at $z=0$ and nowhere else [@problem_id:2264507]. Since differentiability requires an [open neighborhood](@entry_id:268496), this function is **analytic nowhere**.

#### Case Study: $f(z) = \sin(\bar{z})$

Here we have an [analytic function](@entry_id:143459), $\sin(w)$, composed with a non-analytic function, $w = \bar{z}$. Again, the [chain rule](@entry_id:147422) in its standard form does not apply. We analyze the function $f(z) = \sin(x-iy) = \sin(x)\cosh(y) - i\cos(x)\sinh(y)$. The real and imaginary parts are $u(x,y) = \sin(x)\cosh(y)$ and $v(x,y) = -\cos(x)\sinh(y)$. The Cauchy-Riemann equations yield:
$$
u_x = v_y \implies \cos(x)\cosh(y) = -\cos(x)\cosh(y) \implies 2\cos(x)\cosh(y) = 0
$$
$$
u_y = -v_x \implies \sin(x)\sinh(y) = -(\sin(x)\sinh(y)) \implies 2\sin(x)\sinh(y) = 0
$$
From the first equation, since $\cosh(y)$ is always positive, we must have $\cos(x)=0$. When $\cos(x)=0$, we know $\sin(x) = \pm 1 \neq 0$. Therefore, the second equation, $2\sin(x)\sinh(y)=0$, forces $\sinh(y)=0$, which implies $y=0$. Thus, the function is differentiable only at points where $y=0$ and $\cos(x)=0$. These are the points $z = \frac{\pi}{2} + n\pi$ for any integer $n$ [@problem_id:2264534]. Like the previous example, this function is differentiable on a set of isolated points but is analytic nowhere.

#### Case Study: $f(z) = \cos(|z|^2)$

Our final case study reveals an even more intricate structure. The function $f(z)=\cos(|z|^2)$ depends only on the distance from the origin. Let $z=x+iy$, so $f(z) = \cos(x^2+y^2)$. The real and imaginary parts are $u(x,y) = \cos(x^2+y^2)$ and $v(x,y)=0$. The Cauchy-Riemann equations become:
$$
u_x = -2x\sin(x^2+y^2) = v_y = 0
$$
$$
u_y = -2y\sin(x^2+y^2) = -v_x = 0
$$
These two conditions are satisfied if either $x=y=0$ (the origin) or if $\sin(x^2+y^2) = 0$. The condition $\sin(|z|^2)=0$ holds if $|z|^2 = k\pi$ for any non-negative integer $k$. This means the function is differentiable at the origin ($k=0$) and on an infinite number of concentric circles centered at the origin, with radii $\sqrt{k\pi}$ for $k=1, 2, 3, \dots$ [@problem_id:2264509]. This demonstrates that the set of points where a function is differentiable can be surprisingly complex, far beyond just isolated points.

### Deeper Connections and Advanced Formalisms

The rules of differentiation are not merely computational tools; they encode deep structural properties of [analytic functions](@entry_id:139584). Exploring these properties connects complex analysis to [operator theory](@entry_id:139990), [differential geometry](@entry_id:145818), and mathematical physics.

#### The Algebra of Differentiation Operators

We can formalize differentiation as an operator acting on a space of functions. Let $D = \frac{d}{dz}$ be the [differentiation operator](@entry_id:140145) and let $M_z$ be the "multiplication by $z$" operator, defined by $(M_z f)(z) = zf(z)$. What happens when we combine them? The order matters.
Applying $M_z$ then $D$:
$$
(D M_z f)(z) = D(z f(z)) = 1 \cdot f(z) + z \cdot f'(z) \quad \text{(by the product rule)}
$$
Applying $D$ then $M_z$:
$$
(M_z D f)(z) = z(D f(z)) = z f'(z)
$$
The difference between these two operations is known as the **commutator**, denoted $[D, M_z] = DM_z - M_zD$. For any [analytic function](@entry_id:143459) $f$, we find:
$$
([D, M_z]f)(z) = (f(z) + zf'(z)) - zf'(z) = f(z)
$$
This means the operator $[D, M_z]$ is simply the [identity operator](@entry_id:204623), $I$. The relation $[D, M_z] = I$ is a fundamental statement about the algebraic structure of differentiation [@problem_id:2264523]. This [non-commutativity](@entry_id:153545) is a cornerstone of quantum mechanics, where the operators for position and momentum satisfy a similar commutation relation, leading to the Heisenberg Uncertainty Principle.

#### The Laplacian and Wirtinger Calculus

A profound link exists between analyticity and harmonic functions—functions annihilated by the Laplacian operator $\Delta = \frac{\partial^2}{\partial x^2} + \frac{\partial^2}{\partial y^2}$. While the real and imaginary parts of an analytic function $f(z)$ are harmonic, the real-valued function $|f(z)|^2$ is generally not. However, its Laplacian has a remarkably elegant form.

To see this, we introduce the **Wirtinger derivatives**, a convenient formalism for handling [partial derivatives](@entry_id:146280) in the complex plane:
$$
\frac{\partial}{\partial z} = \frac{1}{2}\left(\frac{\partial}{\partial x} - i\frac{\partial}{\partial y}\right) \quad \text{and} \quad \frac{\partial}{\partial \bar{z}} = \frac{1}{2}\left(\frac{\partial}{\partial x} + i\frac{\partial}{\partial y}\right)
$$
In this calculus, the Cauchy-Riemann equations are equivalent to the single condition $\frac{\partial f}{\partial \bar{z}} = 0$, and the [complex derivative](@entry_id:168773) is $f'(z) = \frac{\partial f}{\partial z}$. The Laplacian can also be expressed concisely as $\Delta = 4 \frac{\partial^2}{\partial z \partial \bar{z}}$.

Let's compute the Laplacian of $|f(z)|^2 = f(z)\overline{f(z)}$ for an analytic function $f$:
$$
\Delta |f(z)|^2 = 4 \frac{\partial}{\partial z} \left( \frac{\partial}{\partial \bar{z}} (f \bar{f}) \right)
$$
First, applying the product rule to the inner derivative:
$$
\frac{\partial}{\partial \bar{z}}(f \bar{f}) = \left(\frac{\partial f}{\partial \bar{z}}\right)\bar{f} + f\left(\frac{\partial \bar{f}}{\partial \bar{z}}\right)
$$
Since $f$ is analytic, $\frac{\partial f}{\partial \bar{z}}=0$. Also, one can show that $\frac{\partial \bar{f}}{\partial \bar{z}} = \overline{\left(\frac{\partial f}{\partial z}\right)} = \overline{f'(z)}$. So, the expression simplifies to $f \overline{f'(z)}$.
Now we apply the second derivative:
$$
\frac{\partial}{\partial z} \left( f \overline{f'(z)} \right) = \left(\frac{\partial f}{\partial z}\right)\overline{f'(z)} + f\left(\frac{\partial \overline{f'(z)}}{\partial z}\right)
$$
The first term is $f'(z)\overline{f'(z)} = |f'(z)|^2$. The function $\overline{f'(z)}$ is "anti-analytic," meaning it depends only on $\bar{z}$. Thus, its derivative with respect to $z$ is zero. We are left with a beautiful and powerful identity:
$$
\Delta |f(z)|^2 = 4|f'(z)|^2
$$
This formula reveals a deep geometric connection: the "non-harmonicity" of the squared modulus at a point, as measured by the Laplacian, is directly proportional to the squared magnitude of the function's rate of change at that point [@problem_id:2264526]. For instance, given the function $f(z)=z^3-3z$, we find its derivative is $f'(z)=3z^2-3$. At the point $z_0=2i$, the derivative is $f'(2i) = 3(2i)^2 - 3 = -15$. According to our identity, the value of $\Delta|f(z)|^2$ at this point must be $4|-15|^2 = 4(225) = 900$. This result elegantly connects the derivative, a local property of an analytic function, to the curvature of its modulus surface.