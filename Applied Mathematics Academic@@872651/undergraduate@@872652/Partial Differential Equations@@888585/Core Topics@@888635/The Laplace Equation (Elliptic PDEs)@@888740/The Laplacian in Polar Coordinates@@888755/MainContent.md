## Introduction
The Laplacian operator, $\Delta$, is a cornerstone of [mathematical physics](@entry_id:265403), central to equations describing everything from heat flow to wave motion. While its Cartesian form is simple, many real-world systems, from vibrating drumheads to planetary orbits, exhibit circular symmetry, making Cartesian coordinates unwieldy and unnatural. This article addresses the fundamental need to adapt our mathematical tools to the geometry of the problem by transforming the Laplacian into [polar coordinates](@entry_id:159425). This transformation unlocks elegant and powerful solutions for a vast class of physical phenomena. In the following chapters, you will first learn the principles behind this [coordinate transformation](@entry_id:138577) and the primary method for solving PDEs in this new system: the separation of variables. You will then explore the broad applications of these techniques across diverse scientific fields, seeing how the same equation models heat transfer, electrostatics, and quantum mechanics. Finally, you will have the opportunity to solidify your understanding through a series of hands-on practice problems.

## Principles and Mechanisms

The Laplacian operator, denoted by $\Delta$ or $\nabla^2$, is a cornerstone of [mathematical physics](@entry_id:265403), appearing in fundamental partial differential equations (PDEs) that describe phenomena ranging from [heat diffusion](@entry_id:750209) and [wave propagation](@entry_id:144063) to electrostatics and fluid dynamics. While its expression in Cartesian coordinates, $\Delta u = u_{xx} + u_{yy}$, is compact, many physical problems possess symmetries that are more naturally described using other [coordinate systems](@entry_id:149266). For systems with circular or [cylindrical symmetry](@entry_id:269179), the [polar coordinate system](@entry_id:174894) $(r, \theta)$ is indispensable. This chapter elucidates the principles governing the transformation of the Laplacian into polar coordinates and explores the mechanisms for solving important PDEs in this new framework.

### From Cartesian to Polar Coordinates: The Transformation of the Laplacian

The transition from Cartesian coordinates $(x, y)$ to polar coordinates $(r, \theta)$ is defined by the relations $x = r \cos\theta$ and $y = r \sin\theta$. To express the Laplacian in terms of $r$ and $\theta$, we must transform the partial derivatives $\frac{\partial}{\partial x}$ and $\frac{\partial}{\partial y}$. This is accomplished using the [multivariable chain rule](@entry_id:146671). The inverse relations are $r = \sqrt{x^2 + y^2}$ and $\theta = \arctan(y/x)$.

The first-order [partial derivatives](@entry_id:146280) of the polar coordinates with respect to the Cartesian coordinates are:
$$
\frac{\partial r}{\partial x} = \frac{x}{\sqrt{x^2+y^2}} = \frac{r\cos\theta}{r} = \cos\theta
$$
$$
\frac{\partial r}{\partial y} = \frac{y}{\sqrt{x^2+y^2}} = \frac{r\sin\theta}{r} = \sin\theta
$$
$$
\frac{\partial \theta}{\partial x} = \frac{-y}{x^2+y^2} = \frac{-r\sin\theta}{r^2} = -\frac{\sin\theta}{r}
$$
$$
\frac{\partial \theta}{\partial y} = \frac{x}{x^2+y^2} = \frac{r\cos\theta}{r^2} = \frac{\cos\theta}{r}
$$

Using the [chain rule](@entry_id:147422), a partial derivative of a function $u$ with respect to $x$ can be written as:
$$
\frac{\partial u}{\partial x} = \frac{\partial u}{\partial r}\frac{\partial r}{\partial x} + \frac{\partial u}{\partial \theta}\frac{\partial \theta}{\partial x} = \cos\theta \frac{\partial u}{\partial r} - \frac{\sin\theta}{r} \frac{\partial u}{\partial \theta}
$$
Similarly, for the partial derivative with respect to $y$:
$$
\frac{\partial u}{\partial y} = \frac{\partial u}{\partial r}\frac{\partial r}{\partial y} + \frac{\partial u}{\partial \theta}\frac{\partial \theta}{\partial y} = \sin\theta \frac{\partial u}{\partial r} + \frac{\cos\theta}{r} \frac{\partial u}{\partial \theta}
$$

To find the second derivatives, $u_{xx}$ and $u_{yy}$, we must apply these operators again, carefully using the product rule as the coefficients $(\cos\theta, \sin\theta, 1/r)$ are functions of the coordinates. For example, to find $u_{xx} = \frac{\partial^2 u}{\partial x^2}$, we apply the operator $\left(\cos\theta \frac{\partial}{\partial r} - \frac{\sin\theta}{r} \frac{\partial}{\partial \theta}\right)$ to $u_x$. This calculation, while straightforward, is algebraically intensive. After carrying out the full differentiation and combining the results for $u_{xx}$ and $u_{yy}$, many terms cancel due to [trigonometric identities](@entry_id:165065) such as $\cos^2\theta + \sin^2\theta = 1$.

The final expression for the Laplacian in [polar coordinates](@entry_id:159425) is:
$$
\Delta u = \frac{\partial^2 u}{\partial r^2} + \frac{1}{r}\frac{\partial u}{\partial r} + \frac{1}{r^2}\frac{\partial^2 u}{\partial \theta^2}
$$
Or, using subscript notation for brevity:
$$
\Delta u = u_{rr} + \frac{1}{r}u_r + \frac{1}{r^2}u_{\theta\theta}
$$
The derivation confirms that the coefficient of the first-order radial derivative, $\frac{\partial u}{\partial r}$, is indeed $\frac{1}{r}$ [@problem_id:2145963]. This form of the operator is fundamental to analyzing PDEs on circular domains.

An alternative and often more useful form of the polar Laplacian is obtained by combining the first two terms:
$$
\Delta u = \frac{1}{r}\frac{\partial}{\partial r}\left(r \frac{\partial u}{\partial r}\right) + \frac{1}{r^2}\frac{\partial^2 u}{\partial \theta^2}
$$
This "compact" form is particularly advantageous when dealing with integration and questions of operator structure, as we will see later.

### Harmonic Functions in Polar Coordinates

A function $u$ is called **harmonic** in a domain if it satisfies **Laplace's equation**, $\Delta u = 0$. These functions are central to physics, describing [steady-state temperature](@entry_id:136775) distributions, electrostatic potentials in charge-free regions, and incompressible, irrotational fluid flows.

#### Radially Symmetric Harmonic Functions

The simplest case to analyze is that of a **radially symmetric** function, where $u$ depends only on the distance from the origin, $r$, and not on the angle $\theta$. We write this as $u = u(r)$. For such a function, all derivatives with respect to $\theta$ are zero: $u_\theta = 0$ and $u_{\theta\theta} = 0$. Consequently, the polar Laplacian simplifies significantly [@problem_id:2145997]:
$$
\Delta u = u_{rr} + \frac{1}{r}u_r = 0
$$
This is a second-order ordinary differential equation (ODE) for $u(r)$. We can solve it by letting $v(r) = u'(r)$, which gives the first-order separable ODE $v' = -v/r$. Solving for $v$ yields $v(r) = C_1/r$. Integrating a second time, we find the general solution for radially symmetric harmonic functions [@problem_id:2145983]:
$$
u(r) = C_1 \ln(r) + C_2
$$
where $C_1$ and $C_2$ are arbitrary constants.

This result reveals two fundamental building blocks for radially symmetric harmonic functions: a constant term and a logarithmic term. We can directly verify that $u(r) = \ln(r)$ is harmonic for $r>0$. Its derivatives are $u_r = 1/r$ and $u_{rr} = -1/r^2$. Substituting into the radial Laplacian gives $\Delta u = (-1/r^2) + (1/r)(1/r) = 0$ [@problem_id:2145993].

The logarithmic term, however, introduces a critical subtlety: it has a singularity at the origin, $r=0$, where $\ln(r) \to -\infty$. This has profound physical implications. For a problem defined on a **solid disk** which includes the origin, a physically meaningful solution (like temperature or potential) must remain finite everywhere. Therefore, the $\ln(r)$ term is physically inadmissible for such domains, forcing the constant $C_1$ to be zero [@problem_id:2145990]. However, for a domain that excludes the origin, such as an **annulus** ($a  r  b$) or the exterior of a disk ($r > a$), the $\ln(r)$ term is a valid and often essential part of the solution.

The singularity of the $\ln(r)$ potential is not just a mathematical artifact; it represents a physical reality. In two-dimensional electrostatics, the potential $u(r) = -K \ln(r/r_0)$ describes the [electrostatic field](@entry_id:268546) of an infinitely [long line](@entry_id:156079) of charge lying along the $z$-axis. While the Laplacian of this potential is zero everywhere for $r>0$, indicating no charge in that region, the singularity at $r=0$ corresponds to a concentration of charge precisely on the filament itself. By applying Gauss's law in two dimensions, one can show that the [linear charge density](@entry_id:267995) $\lambda$ is directly proportional to the coefficient of the logarithm, yielding $\lambda = 2\pi\epsilon_0 K$ [@problem_id:2145954].

### Separation of Variables for Laplace's Equation

To find general solutions to Laplace's equation that depend on both $r$ and $\theta$, we employ the powerful method of **separation of variables**. We assume a solution of the form $u(r, \theta) = R(r)\Theta(\theta)$, where $R$ is a function of $r$ only and $\Theta$ is a function of $\theta$ only. Substituting this into $\Delta u = 0$:
$$
R''(r)\Theta(\theta) + \frac{1}{r}R'(r)\Theta(\theta) + \frac{1}{r^2}R(r)\Theta''(\theta) = 0
$$
Multiplying by $r^2$ and dividing by $R(r)\Theta(\theta)$ allows us to separate the variables:
$$
r^2 \frac{R''(r)}{R(r)} + r \frac{R'(r)}{R(r)} = - \frac{\Theta''(\theta)}{\Theta(\theta)}
$$
Since the left side depends only on $r$ and the right side depends only on $\theta$, both sides must be equal to a constant, which we will call $\lambda$. This yields two separate ODEs:

1.  **The Angular Equation:** $\Theta''(\theta) + \lambda\Theta(\theta) = 0$
2.  **The Radial Equation:** $r^2 R''(r) + r R'(r) - \lambda R(r) = 0$

The key to determining the [separation constant](@entry_id:175270) $\lambda$ lies in the physical requirements on $\Theta(\theta)$. For problems on a full disk or [annulus](@entry_id:163678), the value of the function must be single-valued, meaning that returning to the same point after a full circle results in the same value. This imposes a **periodicity condition**: $\Theta(\theta) = \Theta(\theta + 2\pi)$.

Analyzing the angular equation, we find that periodic solutions only exist if $\lambda \ge 0$.
-   If $\lambda = 0$, the solution is $\Theta(\theta) = A_0 + B_0\theta$. Periodicity requires the linear term to vanish ($B_0=0$), leaving a constant solution.
-   If $\lambda > 0$, let $\lambda = k^2$ for $k>0$. The solution is $\Theta(\theta) = A \cos(k\theta) + B \sin(k\theta)$. The $2\pi$-[periodicity](@entry_id:152486) condition demands that $k$ must be a positive integer, i.e., $k = n = 1, 2, 3, \dots$.

Therefore, the [separation constant](@entry_id:175270) is quantized, $\lambda = n^2$ for $n = 0, 1, 2, \dots$. The general solution for the angular part is a superposition of these modes, which is a **Fourier series** [@problem_id:2145980]:
$$
\Theta(\theta) = A_0 + \sum_{n=1}^{\infty} (A_n \cos(n\theta) + B_n \sin(n\theta))
$$

For each integer $n$, the [radial equation](@entry_id:138211) becomes $r^2 R''(r) + r R'(r) - n^2 R(r) = 0$. This is a **Cauchy-Euler equation**.
-   For $n > 0$, the solutions are of the form $r^k$, leading to the general solution $R_n(r) = C_n r^n + D_n r^{-n}$.
-   For $n = 0$, we have already solved this: $R_0(r) = C_0 + D_0 \ln(r)$.

Combining these, the general solution to Laplace's equation in polar coordinates is a superposition of all possible separated solutions:
$$
u(r, \theta) = C_0 + D_0 \ln r + \sum_{n=1}^{\infty} \left[ (A_n r^n + B_n r^{-n})\cos(n\theta) + (C_n r^n + D_n r^{-n})\sin(n\theta) \right]
$$
When solving a specific [boundary value problem](@entry_id:138753), the geometry of the domain dictates which terms are kept. As noted before, for a solid disk, the terms $D_0 \ln r$ and $r^{-n}$ are discarded to ensure the solution is finite at the origin [@problem_id:2145990].

As a concrete example of applying the Laplacian to a function with both radial and angular dependence, consider the temperature profile $T(r, \theta) = C r^3 \sin(2\theta)$. Calculating the [partial derivatives](@entry_id:146280) and substituting them into the polar Laplacian formula yields $\Delta T = 5Cr\sin(2\theta)$ [@problem_id:2145973]. This result is non-zero, indicating that this temperature distribution is not harmonic. It is a solution to the **Poisson equation**, $\Delta T = S(r, \theta)$, where $S(r, \theta) = 5Cr\sin(2\theta)$ represents a spatially varying heat source or sink within the material.

### Integral Properties and Operator Theory

The structure of the polar Laplacian gives rise to important integral properties and allows for a more abstract operator-theoretic viewpoint.

#### The Mean Value Property

A remarkable consequence of the polar Laplacian's form is the **[mean value theorem](@entry_id:141085) for harmonic functions**. This theorem states that the value of a [harmonic function](@entry_id:143397) at the center of a disk is equal to the average of its values on the circumference. Let's define the circular average of a function $u$ at radius $r$ as:
$$
A(r) = \frac{1}{2\pi} \int_{0}^{2\pi} u(r, \theta) d\theta
$$
One can derive a powerful relationship between the rate of change of this average and the Laplacian of the function. By differentiating under the integral and using the compact form of the Laplacian, one can show:
$$
\frac{d}{dr}\left(r \frac{dA}{dr}\right) = \frac{r}{2\pi} \int_{0}^{2\pi} (\Delta u)(r, \theta) d\theta
$$
If $u$ is harmonic, then $\Delta u = 0$, which implies that $\frac{d}{dr}(r A'(r)) = 0$. This means $r A'(r)$ is a constant. For the derivative to be well-behaved at the origin, this constant must be zero, so $A'(r)=0$. Thus, the average value $A(r)$ is independent of the radius $r$. For a continuous function, this means $A(r) = u(0,0)$ for all $r$. If a function is not harmonic, its circular average will generally depend on the radius. For instance, for the non-[harmonic function](@entry_id:143397) $u(x,y) = k(x^2 - y^2)^2$, the circular average is $A(r) = \frac{k}{2}r^4$, and its rate of change is $\frac{dA}{dr} = 2kr^3$, which is clearly not zero [@problem_id:2145931].

#### Self-Adjointness of the Laplacian

In the study of linear operators, a crucial concept is that of **self-adjointness**, which is the operator equivalent of a real number. An operator $L$ is self-adjoint with respect to an inner product $\langle \cdot, \cdot \rangle$ if $\langle Lu, v \rangle = \langle u, Lv \rangle$ for all functions $u, v$ in its domain (satisfying appropriate boundary conditions).

For functions on a 2D domain, the natural inner product involves integrating over the area. In polar coordinates, the differential area element is $dA = r \, dr \, d\theta$. The factor of $r$ is the Jacobian of the [coordinate transformation](@entry_id:138577) and is essential. The inner product for complex-valued functions $f$ and $g$ on an [annular domain](@entry_id:167937) is thus defined as:
$$
\langle f, g \rangle = \int \int_A f(r,\theta) \overline{g(r,\theta)} \, r \, dr \, d\theta
$$
The compact form of the Laplacian, $\Delta u = \frac{1}{r}\frac{\partial}{\partial r}(r u_r) + \frac{1}{r^2}u_{\theta\theta}$, is particularly well-suited for this inner product. It can be shown through [integration by parts](@entry_id:136350) (Green's identities) that the Laplacian is self-adjoint with respect to this inner product, provided the functions satisfy certain boundary conditions (e.g., periodic in $\theta$, and vanishing or having vanishing derivatives on the radial boundaries). This property guarantees that the eigenvalues of the Laplacian are real and that its eigenfunctions form an [orthogonal basis](@entry_id:264024), which is the foundation for solving many PDEs via [eigenfunction expansions](@entry_id:177104). A direct calculation of an inner product involving the Laplacian, such as $\langle \nabla^2 u, v \rangle$ for specific functions $u$ and $v$, demonstrates the mechanics of working with this [weighted inner product](@entry_id:163877) space [@problem_id:2145960].