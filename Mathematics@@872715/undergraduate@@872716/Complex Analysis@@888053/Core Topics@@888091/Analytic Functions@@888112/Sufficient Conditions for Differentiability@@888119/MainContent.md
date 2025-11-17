## Introduction
The derivative of a complex function, while defined similarly to a real derivative, is a far more powerful and restrictive concept. The requirement that the limit of the [difference quotient](@entry_id:136462) must be the same regardless of the path of approach in the two-dimensional complex plane imposes strict structural rules on a function. Verifying this limit definition directly, however, is often impractical. This raises a crucial question: how can we develop a more direct, algebraic test for differentiability?

This article provides a comprehensive answer by developing the essential tools for verifying [complex differentiability](@entry_id:140243). We will explore the [necessary and sufficient conditions](@entry_id:635428) that a function's real and imaginary parts must satisfy. The "Principles and Mechanisms" chapter will guide you through the derivation of the Cauchy-Riemann equations and establish the full theorem for sufficiency, which includes the critical role of continuity. In "Applications and Interdisciplinary Connections," you will discover the profound consequences of these conditions, uncovering the deep link between [analytic functions](@entry_id:139584), harmonic functions, and real-world problems in physics and vector calculus. Finally, the "Hands-On Practices" section will allow you to apply these theoretical tools to concrete examples, solidifying your ability to determine where a complex function is differentiable.

## Principles and Mechanisms

In the preceding chapter, we introduced the concept of the [complex derivative](@entry_id:168773). While its definition, $f'(z_0) = \lim_{z \to z_0} \frac{f(z) - f(z_0)}{z - z_0}$, is formally identical to that of a real derivative, its implications are far more profound. The requirement that this limit exists and is unique, regardless of the path along which $z$ approaches $z_0$ in the two-dimensional complex plane, imposes powerful constraints on the structure of a complex function. This chapter delves into these constraints, known as the Cauchy-Riemann equations, and establishes the precise conditions under which a complex function is differentiable.

### The Cauchy-Riemann Equations: A Necessary Condition

Let us consider a complex function $f(z)$ defined on a domain $D$. We can express this function in terms of its real and imaginary parts by writing $z = x + iy$ and $f(z) = u(x, y) + i v(x, y)$, where $u$ and $v$ are real-valued functions of two real variables, $x$ and $y$.

If $f$ is differentiable at a point $z_0 = x_0 + iy_0$, then the derivative $f'(z_0)$ must exist. This means the limit of the [difference quotient](@entry_id:136462) $\frac{\Delta f}{\Delta z}$ must be the same no matter how $\Delta z \to 0$. Let's explore two specific paths of approach.

First, consider approaching $z_0$ along a horizontal line. This corresponds to setting $\Delta z = \Delta x$ (so $\Delta y = 0$). The derivative becomes:
$$ f'(z_0) = \lim_{\Delta x \to 0} \frac{f(z_0 + \Delta x) - f(z_0)}{\Delta x} $$
$$ f'(z_0) = \lim_{\Delta x \to 0} \frac{[u(x_0+\Delta x, y_0) + i v(x_0+\Delta x, y_0)] - [u(x_0, y_0) + i v(x_0, y_0)]}{\Delta x} $$
$$ f'(z_0) = \lim_{\Delta x \to 0} \left[ \frac{u(x_0+\Delta x, y_0) - u(x_0, y_0)}{\Delta x} + i \frac{v(x_0+\Delta x, y_0) - v(x_0, y_0)}{\Delta x} \right] $$
Recognizing the definitions of [partial derivatives](@entry_id:146280), this simplifies to:
$$ f'(z_0) = \frac{\partial u}{\partial x}(x_0, y_0) + i \frac{\partial v}{\partial x}(x_0, y_0) $$
We denote these partial derivatives as $u_x(x_0, y_0)$ and $v_x(x_0, y_0)$.

Next, let's approach $z_0$ along a vertical line. This corresponds to setting $\Delta z = i \Delta y$ (so $\Delta x = 0$). The derivative is:
$$ f'(z_0) = \lim_{\Delta y \to 0} \frac{f(z_0 + i\Delta y) - f(z_0)}{i\Delta y} $$
$$ f'(z_0) = \lim_{\Delta y \to 0} \frac{[u(x_0, y_0+\Delta y) + i v(x_0, y_0+\Delta y)] - [u(x_0, y_0) + i v(x_0, y_0)]}{i\Delta y} $$
$$ f'(z_0) = \frac{1}{i} \lim_{\Delta y \to 0} \left[ \frac{u(x_0, y_0+\Delta y) - u(x_0, y_0)}{\Delta y} + i \frac{v(x_0, y_0+\Delta y) - v(x_0, y_0)}{\Delta y} \right] $$
This simplifies to:
$$ f'(z_0) = \frac{1}{i} \left( \frac{\partial u}{\partial y}(x_0, y_0) + i \frac{\partial v}{\partial y}(x_0, y_0) \right) = \frac{\partial v}{\partial y}(x_0, y_0) - i \frac{\partial u}{\partial y}(x_0, y_0) $$
We denote these partial derivatives as $v_y(x_0, y_0)$ and $u_y(x_0, y_0)$.

Since the derivative $f'(z_0)$ must be unique, these two expressions for it must be equal:
$$ u_x + i v_x = v_y - i u_y $$
Equating the real and imaginary parts of this equation gives us a pair of fundamental relations:
$$ \frac{\partial u}{\partial x} = \frac{\partial v}{\partial y} \quad \text{and} \quad \frac{\partial u}{\partial y} = - \frac{\partial v}{\partial x} $$
These are the **Cauchy-Riemann equations**. They are a necessary condition for the existence of the derivative of a complex function. If a function $f$ is differentiable at a point, its real and imaginary parts must satisfy these equations at that point.

### Sufficient Conditions for Differentiability

The Cauchy-Riemann equations are necessary for differentiability, but are they sufficient? It turns out that satisfying them at a single point is not enough to guarantee differentiability there. A crucial additional condition is required: the continuity of the partial derivatives.

**Theorem (Sufficient Conditions for Differentiability):**
Let $f(z) = u(x, y) + i v(x, y)$ be a complex function defined in a neighborhood of a point $z_0 = x_0 + iy_0$. If the four first-order [partial derivatives](@entry_id:146280) $u_x, u_y, v_x, v_y$
1.  exist in this neighborhood,
2.  are continuous at $(x_0, y_0)$, and
3.  satisfy the Cauchy-Riemann equations at $(x_0, y_0)$,
then the function $f$ is differentiable at $z_0$.

The continuity condition ensures that the first-order approximation of the function behaves correctly in all directions, not just along the axes. It guarantees that the function is "smooth" enough in the real, two-dimensional sense for the single complex limit to exist.

To see why this continuity is vital, consider the function defined as $f(z) = \frac{(\operatorname{Re}(z))(\operatorname{Im}(z))^2}{|z|^2}$ for $z \neq 0$ and $f(0) = 0$ [@problem_id:2267350]. In terms of $x$ and $y$, we have $u(x,y) = \frac{xy^2}{x^2+y^2}$ for $(x,y) \neq (0,0)$ and $u(0,0)=0$, while the imaginary part $v(x,y)$ is identically zero. At the origin, the [partial derivatives](@entry_id:146280) are found from the limit definition:
$u_x(0,0) = \lim_{h\to 0} \frac{u(h,0)-u(0,0)}{h} = \lim_{h\to 0} \frac{0-0}{h} = 0$.
$u_y(0,0) = \lim_{k\to 0} \frac{u(0,k)-u(0,0)}{k} = \lim_{k\to 0} \frac{0-0}{k} = 0$.
Since $v(x,y) = 0$, we also have $v_x(0,0) = 0$ and $v_y(0,0) = 0$. At the origin, the Cauchy-Riemann equations $u_x = v_y$ (since $0=0$) and $u_y = -v_x$ (since $0=0$) are satisfied. However, if we examine the limit of the [difference quotient](@entry_id:136462) $\frac{f(z)}{z}$ as $z \to 0$, we find that it is path-dependent. For instance, along the path $y=x$, the limit evaluates to $\frac{1}{2(1+i)}$, while along the real axis it is $0$. Therefore, $f(z)$ is not differentiable at the origin, despite satisfying the Cauchy-Riemann equations there. The failure arises because its partial derivatives are not continuous at the origin.

### Analyticity and its Verification

The most important functions in complex analysis are not just differentiable at isolated points but in an entire region. This leads to the central concept of **[analyticity](@entry_id:140716)**.

A function $f(z)$ is said to be **analytic** at a point $z_0$ if it is differentiable not only at $z_0$ but also at every point in some neighborhood of $z_0$. A function is analytic on a domain $D$ if it is analytic at every point in $D$. A function that is analytic on the entire complex plane $\mathbb{C}$ is called an **entire** function.

The distinction between [differentiability at a point](@entry_id:160837) and [analyticity](@entry_id:140716) is crucial. For example, consider the function $f(z) = (z-c)\bar{z}$ for some constant $c = 3+2i$ [@problem_id:2267353]. By expanding $f(z)$ into its real and imaginary parts, $u(x,y) = x^2 - 3x + y^2 - 2y$ and $v(x,y) = 3y - 2x$, and applying the Cauchy-Riemann equations, we find they are satisfied only at the single point $(x,y) = (3,2)$, or $z_0 = 3+2i$. Since the [partial derivatives](@entry_id:146280) are continuous everywhere, the function is differentiable at $z_0 = 3+2i$ and nowhere else. Because there is no [open neighborhood](@entry_id:268496) of $z_0$ throughout which $f$ is differentiable, this function is nowhere analytic.

Let's now use the [sufficient conditions](@entry_id:269617) to verify the [analyticity](@entry_id:140716) of several classes of functions.

**Linear Functions**: Consider a function of the form $f(z) = (ax+by) + i(cx+dy)$, where $a, b, c, d$ are real constants [@problem_id:2267367]. Here, $u(x,y) = ax+by$ and $v(x,y) = cx+dy$. The [partial derivatives](@entry_id:146280) are all constants: $u_x=a$, $u_y=b$, $v_x=c$, and $v_y=d$. These are continuous everywhere. For $f$ to be entire, the Cauchy-Riemann equations must hold for all $(x,y)$:
$u_x = v_y \implies a=d$
$u_y = -v_x \implies b=-c$
Thus, the function is entire if and only if $a=d$ and $b=-c$. In this case, $f(z)$ can be written as $(a+ic)z$, demonstrating that any complex-differentiable linear map from $\mathbb{R}^2$ to $\mathbb{R}^2$ corresponds to multiplication by a single complex number.

**Polynomial Functions**: Let's determine the conditions for the function $f(z) = (x^2 + ay^2) + i(bxy)$ to be entire [@problem_id:2267341]. We have $u = x^2+ay^2$ and $v = bxy$. The partial derivatives are $u_x=2x$, $u_y=2ay$, $v_x=by$, and $v_y=bx$. These are all polynomials and thus continuous everywhere. The Cauchy-Riemann equations must hold for all $x$ and $y$:
$u_x = v_y \implies 2x = bx \implies b=2$.
$u_y = -v_x \implies 2ay = -by \implies 2a = -b$.
Substituting $b=2$ into the second equation gives $2a = -2$, so $a=-1$. With these values, the function becomes $f(z) = x^2-y^2+i(2xy)$, which we recognize as $(x+iy)^2 = z^2$. As expected, $f(z)=z^2$ is an [entire function](@entry_id:178769).

**Transcendental and Rational Functions**: The same principles apply to more complex functions. For $f(z) = \sin(x)\cosh(y) + i\cos(x)\sinh(y)$, we can verify that the [partial derivatives](@entry_id:146280) are continuous and satisfy the Cauchy-Riemann equations for all $(x,y)$, confirming that this function is entire [@problem_id:2267346]. This function is, in fact, the standard definition of $\sin(z)$. The derivative can be computed as $f'(z) = u_x + iv_x = \cos(x)\cosh(y) - i\sin(x)\sinh(y)$, which simplifies to $\cos(z)$.

Similarly, the function $f(z) = \frac{x-1}{(x-1)^2+y^2} - i \frac{y}{(x-1)^2+y^2}$ can be shown to satisfy the Cauchy-Riemann equations for all $z \neq 1$ [@problem_id:2267357]. Its partial derivatives are rational functions and are continuous on its domain $\mathbb{C} \setminus \{1\}$. Thus, the function is analytic on its domain. Indeed, this function is simply $\frac{1}{z-1}$, which we know to be analytic everywhere except at its pole $z=1$.

### The Polar Form of the Cauchy-Riemann Equations

For functions naturally expressed in [polar coordinates](@entry_id:159425), where $z=re^{i\theta}$, it is convenient to have a corresponding form of the Cauchy-Riemann equations. By applying the chain rule to transform the Cartesian derivatives ($u_x, u_y, v_x, v_y$) into polar derivatives ($u_r, u_\theta, v_r, v_\theta$), one arrives at the **[polar form](@entry_id:168412) of the Cauchy-Riemann equations**:
$$ \frac{\partial u}{\partial r} = \frac{1}{r} \frac{\partial v}{\partial \theta} \quad \text{and} \quad \frac{\partial v}{\partial r} = -\frac{1}{r} \frac{\partial u}{\partial \theta} $$
These equations hold for $r > 0$. The derivative $f'(z)$ can then be expressed as $f'(z) = e^{-i\theta}(u_r + iv_r)$.

As an application, consider a function of the form $f(z) = u(r, \theta) + iv(r, \theta)$ where $u = A\ln(r) - B\theta$ and $v = C\theta + D\ln(r)$ [@problem_id:2267356]. We compute the [partial derivatives](@entry_id:146280): $u_r = A/r$, $u_\theta = -B$, $v_r = D/r$, and $v_\theta = C$. Applying the polar CR equations gives:
$u_r = \frac{1}{r}v_\theta \implies A/r = C/r \implies A=C$.
$v_r = -\frac{1}{r}u_\theta \implies D/r = -(-B)/r \implies D=B$.
Therefore, for this function to be analytic on a suitable domain, the constants must satisfy $A=C$ and $B=D$. For the specific case where $A=C=1$ and $B=D=0$, we get $f(z) = \ln(r) + i\theta$, which is the [principal branch](@entry_id:164844) of the [complex logarithm](@entry_id:174857), $\operatorname{Log}(z)$.

### Profound Consequences of Analyticity

The conditions for [analyticity](@entry_id:140716) are so restrictive that they impart a remarkable "rigidity" to complex functions. The real and imaginary parts become deeply intertwined, and the function's global behavior is often determined by its properties in a small region.

#### Harmonic Functions and Conjugates

If a function $f = u+iv$ is analytic, its real and imaginary parts are not independent. Assuming their second-order [partial derivatives](@entry_id:146280) are continuous (a fact we will prove later for all analytic functions), we can differentiate the Cauchy-Riemann equations:
$u_{xx} = (v_y)_x = v_{yx}$
$u_{yy} = (-v_x)_y = -v_{xy}$
Summing these gives $u_{xx} + u_{yy} = v_{yx} - v_{xy}$. Since the mixed partials are equal, we find:
$$ u_{xx} + u_{yy} = 0 $$
A real-valued function of two variables that satisfies this equation, known as **Laplace's equation**, is called a **[harmonic function](@entry_id:143397)**. A similar calculation shows that $v_{xx} + v_{yy} = 0$, so the imaginary part is also harmonic.

Given a [harmonic function](@entry_id:143397) $u(x,y)$, the Cauchy-Riemann equations can be used to find a corresponding harmonic function $v(x,y)$ such that $f=u+iv$ is analytic. This function $v$ is called a **[harmonic conjugate](@entry_id:165376)** of $u$. For instance, let's find the [harmonic conjugate](@entry_id:165376) for $u(x,y) = x^2 - y^2 + 2y$, given the condition $v(1,1)=4$ [@problem_id:2267352].
First, we compute the partials of $u$: $u_x = 2x$ and $u_y = -2y+2$.
From the CR equations, we must have:
1. $v_y = u_x = 2x$
2. $v_x = -u_y = -(-2y+2) = 2y-2$

Integrating the first equation with respect to $y$ gives:
$v(x,y) = \int 2x \, dy = 2xy + g(x)$, where $g(x)$ is an arbitrary function of $x$.
To find $g(x)$, we differentiate this expression with respect to $x$ and use the second equation:
$v_x = 2y + g'(x)$.
Setting this equal to $2y-2$, we get $2y+g'(x) = 2y-2$, which implies $g'(x) = -2$. Integrating yields $g(x) = -2x+C$ for some real constant $C$.
So, the family of [harmonic conjugates](@entry_id:174290) is $v(x,y) = 2xy - 2x + C$.
Using the condition $v(1,1)=4$, we find $2(1)(1) - 2(1) + C = 4$, which gives $C=4$. The unique [harmonic conjugate](@entry_id:165376) is $v(x,y) = 2xy - 2x + 4$. The resulting entire function is $f(z) = (x^2 - y^2 + 2y) + i(2xy - 2x + 4)$, which can be shown to simplify to $f(z) = z^2 - 2iz + 4i$.

#### The Rigidity of Analytic Functions

The structural link forged by the Cauchy-Riemann equations means that imposing even mild constraints on an analytic function can have drastic consequences.

Suppose both a function $f(z) = u+iv$ and its conjugate $\overline{f(z)} = u-iv$ are analytic on a domain $D$ [@problem_id:2267334]. For $f$ to be analytic, we have $u_x = v_y$ and $u_y = -v_x$. For $\overline{f}$ to be analytic, its real part $u$ and imaginary part $-v$ must also satisfy the CR equations: $u_x = (-v)_y = -v_y$ and $u_y = -(-v)_x = v_x$.
Comparing the two sets of equations:
$u_x = v_y$ and $u_x = -v_y \implies u_x = v_y = 0$.
$u_y = -v_x$ and $u_y = v_x \implies u_y = v_x = 0$.
Since all four [partial derivatives](@entry_id:146280) are zero throughout the domain, both $u$ and $v$ must be constant. Therefore, $f(z)$ must be a constant function, and its derivative is $f'(z) = u_x + iv_x = 0$.

This [principle of rigidity](@entry_id:161140) extends further. If an [entire function](@entry_id:178769) has its range constrained to a one-dimensional curve, it must be constant. For example, imagine an [entire function](@entry_id:178769) $f=u+iv$ whose values all lie on the line $u+2v=5$ [@problem_id:2267337]. Since this relation holds for all $(x,y)$, we can differentiate it with respect to $x$ and $y$:
$u_x + 2v_x = 0$
$u_y + 2v_y = 0$
Now, we can use the Cauchy-Riemann equations to substitute for $u_x$ and $u_y$:
$v_y + 2v_x = 0$
$(-v_x) + 2v_y = 0$
This is a system of two linear equations for $v_x$ and $v_y$. The only solution is $v_x=0$ and $v_y=0$. From the CR equations, this immediately implies that $u_x=0$ and $u_y=0$ as well. Since all [partial derivatives](@entry_id:146280) of $u$ and $v$ are zero everywhere, $f$ must be a [constant function](@entry_id:152060). If we know its value at a single point, say $f(1+i) = 1+2i$, then we know its value everywhere: $f(z) = 1+2i$ for all $z \in \mathbb{C}$. This is a striking result: an [entire function](@entry_id:178769) cannot be "flattened" onto a line without being trivialized into a single point. This stands in stark contrast to functions of a real variable, where many non-constant functions map the real line into a smaller interval.