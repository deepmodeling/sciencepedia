## Introduction
The complex function $w = z^2$ is a cornerstone of complex analysis, serving as a fundamental example of a non-linear analytic mapping. While algebraically simple, its geometric and topological consequences are profound, offering a gateway to understanding more advanced concepts like [conformal mappings](@entry_id:165890), critical points, and multi-valued functions. Many students new to the field struggle to visualize how such a simple formula can twist and stretch the complex plane in non-intuitive ways. This article bridges that gap by providing a comprehensive exploration of the mapping's properties and applications. Across the following chapters, you will gain a deep, multi-faceted understanding of this function. "Principles and Mechanisms" will break down the fundamental action of the mapping, exploring how it transforms points, curves, and angles. "Applications and Interdisciplinary Connections" will showcase its utility in solving real-world problems in geometry, physics, and engineering. Finally, "Hands-On Practices" will offer targeted exercises to solidify your comprehension and problem-solving skills.

## Principles and Mechanisms

The function $w = f(z) = z^2$ serves as a foundational example of a complex analytic mapping. While algebraically simple, its behavior reveals a wealth of geometric and [topological properties](@entry_id:154666) that are characteristic of complex functions, including conformality, critical points, and multi-valuedness. A thorough understanding of this mapping provides a crucial stepping stone to analyzing more intricate functions.

### The Fundamental Geometric Action: Squaring Moduli and Doubling Angles

The most direct way to understand the geometric effect of the mapping $w = z^2$ is to use the polar representation of a complex number. Let a point in the $z$-plane be given by $z = r e^{i\theta}$, where $r = |z|$ is its modulus (distance from the origin) and $\theta = \arg(z)$ is its argument (angle with the positive real axis). The mapping transforms this point to:

$w = z^2 = (r e^{i\theta})^2 = r^2 e^{i(2\theta)}$

Letting $w = R e^{i\phi}$, we can identify the [modulus and argument](@entry_id:165314) of the image point as $R = r^2$ and $\phi = 2\theta$. This simple relationship encapsulates the entire geometric action of the function:

1.  The **modulus is squared**: A point at a distance $r$ from the origin in the $z$-plane is mapped to a point at a distance $r^2$ from the origin in the $w$-plane.
2.  The **argument is doubled**: A point with an angle $\theta$ in the $z$-plane is mapped to a point with an angle $2\theta$ in the $w$-plane.

This twofold action has immediate consequences for the transformation of simple geometric shapes. For instance, a circle of radius $r_0$ in the $z$-plane, described by $|z| = r_0$, is mapped to a circle of radius $r_0^2$ in the $w$-plane, described by $|w| = r_0^2$. A ray emanating from the origin at a constant angle $\theta_0$, described by $\arg(z) = \theta_0$, is mapped to a new ray at an angle $2\theta_0$, described by $\arg(w) = 2\theta_0$.

This principle allows us to determine the image of more complex regions. For example, consider a sector in the $z$-plane defined by $x > 0$ and $0 \le y \le x$. These conditions correspond to points $z=re^{i\theta}$ where the argument $\theta$ lies in the interval $[0, \pi/4]$. Under the mapping $w=z^2$, the argument is doubled. Therefore, the image region will have arguments in the interval $[0, \pi/2]$. This corresponds to the first quadrant of the $w$-plane, where both the real part $u$ and the imaginary part $v$ are positive [@problem_id:2276433]. Similarly, an annular sector defined by $1 \le |z| \le 4$ and $\pi/4 \le \arg(z) \le \pi/2$ will be mapped to a new annular sector in the $w$-plane defined by $1^2 \le |w| \le 4^2$ and $2(\pi/4) \le \arg(w) \le 2(\pi/2)$, which is $1 \le |w| \le 16$ and $\pi/2 \le \arg(w) \le \pi$ [@problem_id:2276401].

### Cartesian Representation and Analytic Properties

While the polar representation is ideal for understanding the global geometry, the Cartesian representation is often more useful for algebraic manipulation and for verifying the analytic properties of the function. By substituting $z = x + iy$ into the function $w = u + iv = z^2$, we obtain:

$w = (x + iy)^2 = (x^2 - y^2) + i(2xy)$

By equating the real and imaginary parts, we find the explicit transformation equations:

$u(x, y) = x^2 - y^2$
$v(x, y) = 2xy$

These expressions allow us to investigate the function's properties as a mapping from $\mathbb{R}^2$ to $\mathbb{R}^2$. One of the central concepts in complex analysis is that of **analyticity**, which is linked to the **Cauchy-Riemann equations**. A function $f(z) = u(x,y) + iv(x,y)$ is analytic if its real and imaginary parts have continuous first partial derivatives that satisfy these equations:

$\frac{\partial u}{\partial x} = \frac{\partial v}{\partial y}$ and $\frac{\partial u}{\partial y} = -\frac{\partial v}{\partial x}$

For $f(z) = z^2$, we can compute these partial derivatives:

$\frac{\partial u}{\partial x} = 2x$,  $\frac{\partial v}{\partial y} = 2x$

$\frac{\partial u}{\partial y} = -2y$, $\frac{\partial v}{\partial x} = 2y$

We see that $\frac{\partial u}{\partial x} = \frac{\partial v}{\partial y}$ and $\frac{\partial u}{\partial y} = - \frac{\partial v}{\partial x}$ for all $(x,y)$. Since these partial derivatives are continuous everywhere, the function $f(z)=z^2$ is analytic on the entire complex plane, making it an **entire function** [@problem_id:2276415].

This Cartesian formulation is also essential for solving certain algebraic equations. For instance, to find points that are mapped to their own conjugate, we must solve $z^2 = \bar{z}$. Substituting $z = x+iy$ leads to the system of real equations $x^2 - y^2 = x$ and $2xy = -y$. Solving this system reveals the set of four "conjugate-fixed" points: $\{0, 1, -\frac{1}{2} + i\frac{\sqrt{3}}{2}, -\frac{1}{2} - i\frac{\sqrt{3}}{2}\}$ [@problem_id:2276426].

### Local Deformation: Conformality and Area Magnification

For an analytic function $f(z)$, its derivative $f'(z)$ carries profound geometric significance. For $f(z) = z^2$, the derivative is $f'(z) = 2z$.

At any point $z_0$ where $f'(z_0) \neq 0$, the mapping $w = f(z)$ is **conformal**. This means it acts as a local rotation and uniform scaling, preserving the angles between intersecting curves. For $w=z^2$, this property holds for all $z \neq 0$.

The magnitude of the derivative, $|f'(z_0)|$, represents the **local linear [magnification](@entry_id:140628) factor**. A tiny line segment of length $ds$ at $z_0$ is mapped to a line segment of approximate length $|f'(z_0)| ds$ at $w_0 = f(z_0)$.

Consequently, an infinitesimal area $dA_z$ around $z_0$ is mapped to an infinitesimal area $dA_w$ around $w_0$ that is scaled by the square of the linear magnification factor. This **local area [magnification](@entry_id:140628) factor**, $K$, is given by:

$K = |f'(z)|^2$

For the mapping $w = z^2$, the area magnification factor is $K = |2z|^2 = 4|z|^2 = 4(x^2+y^2)$. This shows that the mapping stretches areas more significantly for points farther from the origin. For example, at the point $z_0 = 2-i$, the derivative is $f'(2-i) = 2(2-i) = 4-2i$. The local area magnification is $K = |4-2i|^2 = 4^2 + (-2)^2 = 20$ [@problem_id:2276429]. This means a small region around $2-i$ is mapped to a region near $f(2-i) = 3-4i$ with an area approximately 20 times larger. This factor is precisely the Jacobian of the transformation from $(x,y)$ coordinates to $(u,v)$ coordinates, and it is used when calculating the area of a transformed region via integration [@problem_id:2276401].

### The Critical Point and Angle Distortion

The property of conformality breaks down at points where the derivative is zero. Such a point is called a **critical point**. For $w=z^2$, the only critical point is at $z=0$, since $f'(z) = 2z = 0$ only when $z=0$.

At a critical point, angles are not preserved. Instead, for a simple critical point like this one, they are multiplied by an integer factor related to the order of the zero of the derivative. For $w=z^2$, angles at the origin are doubled.

This effect can be visualized by considering two curves intersecting at $z=0$: the positive real axis ($C_1$, parametrized by $z(t)=t$ for $t \ge 0$) and the positive imaginary axis ($C_2$, parametrized by $z(s)=is$ for $s \ge 0$). These curves meet at a right angle, $\pi/2$. Their images under the mapping $w=z^2$ are:

-   Image of $C_1$: $w(t) = t^2$ for $t \ge 0$. This is the non-negative real axis in the $w$-plane.
-   Image of $C_2$: $w(s) = (is)^2 = -s^2$ for $s \ge 0$. This is the non-positive real axis in the $w$-plane.

In the $w$-plane, these two image curves form a single straight line, meeting at an angle of $\pi$ [radians](@entry_id:171693) at their intersection point $w=0$. The original angle of $\pi/2$ has been doubled to $\pi$, confirming the failure of conformality at the critical point [@problem_id:2276428].

### Global Properties: The Two-to-One Nature

While the mapping is locally one-to-one away from the critical point, it is not globally one-to-one. To see which points in the $z$-plane map to the same point in the $w$-plane, we solve the equation $z_1^2 = z_2^2$ for $z_1 \neq z_2$. This gives $z_1^2 - z_2^2 = 0$, or $(z_1 - z_2)(z_1 + z_2) = 0$. Since $z_1 \neq z_2$, we must have $z_1 = -z_2$.

This means that every non-zero point $w$ in the image plane is the image of exactly two points in the domain: $z$ and $-z$. These two points are antipodal, lying at the same distance from the origin but in opposite directions [@problem_id:2276397]. The only point in the $w$-plane that has a single preimage is $w=0$, which corresponds to the critical point $z=0$.

This "two-to-one" nature means the function effectively "folds" the $z$-plane. For example, the entire [upper half-plane](@entry_id:199119) ($\text{Im}(z)>0$) is mapped onto the entire $w$-plane, excluding the non-negative real axis. The lower half-plane ($\text{Im}(z)0$) is also mapped onto the exact same region.

### The Multi-Valued Inverse and the Branch Point at the Origin

The two-to-one nature of $w=z^2$ implies that its inverse, the square root function $z = \sqrt{w}$, is inherently **multi-valued**. For any non-zero $w_0$, there are two possible values for $\sqrt{w_0}$. This ambiguity prevents us from defining a standard, single-valued [inverse function](@entry_id:152416) on the entire complex plane.

The source of this multi-valuedness is the critical point's image, $w=0$, which is known as a **[branch point](@entry_id:169747)**. To understand its role, consider a continuous path in the $w$-plane that encircles the origin. Let's start at a point $w_0 = f(z_0)$. We then trace a single counter-clockwise circle in the $w$-plane, returning to $w_0$. In [polar coordinates](@entry_id:159425), this path can be described by letting the argument of $w$ increase by $2\pi$.

What is the corresponding path in the $z$-plane? Let $z(t)$ be the continuous path starting at $z_0$ such that $(z(t))^2 = w(t)$. We have $\arg(w(t)) = \arg(w_0) + 2\pi t$ for $t \in [0,1]$. Since $\arg(z) = \frac{1}{2}\arg(w)$, the argument of our path in the $z$-plane must change according to $\arg(z(t)) = \arg(z_0) + \pi t$. When the path in the $w$-plane completes its loop at $t=1$, the argument of $z$ has changed by $\pi$. The final point is therefore:

$z_f = |z_0| e^{i(\arg(z_0) + \pi)} = (|z_0| e^{i\arg(z_0)})e^{i\pi} = -z_0$

A closed loop around the branch point in the $w$-plane lifts to an open path in the $z$-plane that connects a point $z_0$ to its counterpart $-z_0$ [@problem_id:2276413]. This phenomenon demonstrates that it is impossible to define a continuous, single-valued square root function in any domain that contains a simple closed loop around the origin.

### Transforming Curvilinear Coordinates

One of the most powerful applications of [complex mappings](@entry_id:168731) is their ability to transform coordinate systems. The mapping $w=z^2$ provides a beautiful example of this, as it relates the simple Cartesian grid in the $w$-plane to a system of orthogonal hyperbolas in the $z$-plane.

From the relations $u=x^2-y^2$ and $v=2xy$, consider the preimages of the standard Cartesian grid lines $u=\text{constant}$ and $v=\text{constant}$.

-   The preimage of a vertical line $u=c_1$ in the $w$-plane is the set of points in the $z$-plane satisfying $x^2-y^2 = c_1$. This is the equation of a family of hyperbolas opening towards the real axis.
-   The [preimage](@entry_id:150899) of a horizontal line $v=c_2$ in the $w$-plane is the set of points satisfying $2xy = c_2$, or $xy = c_2/2$. This is a family of hyperbolas rotated by $\pi/4$ (asymptotic to the coordinate axes) [@problem_id:2276378].

The families of lines $u=c_1$ and $v=c_2$ are orthogonal in the $w$-plane. Because the mapping is conformal (for $z \neq 0$), their preimages, the families of hyperbolas $x^2-y^2=c_1$ and $2xy=c_2$, must also form an **[orthogonal system](@entry_id:264885) of curves** in the $z$-plane [@problem_id:2276438].

This property is of great utility in applied physics, particularly in two-dimensional electrostatics and fluid dynamics. For example, if the lines $u=c_1$ represent [equipotential lines](@entry_id:276883) and $v=c_2$ represent [electric field lines](@entry_id:277009) for a simple uniform field in the $w$-plane, then the corresponding hyperbolic curves in the $z$-plane represent the distorted equipotentials and field lines in a more complex physical setup, such as the field in a 90-degree corner. The mapping $w=z^2$ thus allows one to solve a difficult problem by transforming it into a much simpler one.