## Introduction
Many problems in physics and engineering, from the vibrations of a drumhead to the temperature inside a cylindrical pipe, are most naturally described in [polar coordinates](@entry_id:159425). While partial differential equations (PDEs) govern these phenomena, solving them in Cartesian coordinates can be needlessly complex. This article addresses the challenge of adapting analytical techniques to these circular geometries by focusing on one of the most powerful tools available: the [method of separation of variables](@entry_id:197320). Across the following sections, you will gain a comprehensive understanding of this technique. The "Principles and Mechanisms" section will deconstruct the method, showing how to transform a PDE into simpler ordinary differential equations and apply boundary conditions. Next, the "Applications and Interdisciplinary Connections" section will demonstrate the method's far-reaching impact in fields like electrostatics, heat transfer, and quantum mechanics. Finally, the "Hands-On Practices" section will offer guided problems to test and reinforce your skills, bridging theory with practical application.

## Principles and Mechanisms

Many physical phenomena, from the [steady-state temperature](@entry_id:136775) in a metal plate to the [electrostatic potential](@entry_id:140313) in a charge-free region, are governed by partial differential equations (PDEs) whose solutions are most naturally sought in [coordinate systems](@entry_id:149266) that match the geometry of the boundaries. For problems involving circular, cylindrical, or annular domains, polar coordinates $(r, \theta)$ are indispensable. This chapter elucidates the principles and mechanisms of solving such PDEs using the [method of separation of variables](@entry_id:197320).

### The Laplacian and Governing Equations in Polar Coordinates

The cornerstone of our study is the Laplacian operator, $\nabla^2$. In two-dimensional [polar coordinates](@entry_id:159425), it takes the form:
$$ \nabla^2 u = \frac{\partial^2 u}{\partial r^2} + \frac{1}{r}\frac{\partial u}{\partial r} + \frac{1}{r^2}\frac{\partial^2 u}{\partial \theta^2} $$
This can also be written more compactly as:
$$ \nabla^2 u = \frac{1}{r}\frac{\partial}{\partial r}\left(r \frac{\partial u}{\partial r}\right) + \frac{1}{r^2}\frac{\partial^2 u}{\partial \theta^2} $$
We will apply the [method of separation of variables](@entry_id:197320) to several fundamental equations involving this operator. The most prominent is **Laplace's equation**, $\nabla^2 u = 0$, which describes [steady-state systems](@entry_id:174643) without sources, such as temperature distributions in thermal equilibrium or electrostatic potentials in charge-free regions.

We will also consider **Poisson's equation**, $\nabla^2 u = f(r, \theta)$, which extends this framework to systems with internal sources or sinks, such as a plate with internal heat generation [@problem_id:2132287]. Finally, we will investigate time-dependent problems like the **wave equation**, $\frac{\partial^2 u}{\partial t^2} = c^2 \nabla^2 u$, which governs the [vibrations of a circular membrane](@entry_id:169868) [@problem_id:2132260] [@problem_id:2132277].

### The Method of Separation of Variables

The power of this method lies in its ability to transform a PDE in multiple variables into a set of simpler [ordinary differential equations](@entry_id:147024) (ODEs), each in a single variable. For a function $u(r, \theta)$, we assume a solution that is a product of functions of each variable alone:
$$ u(r, \theta) = R(r) \Theta(\theta) $$
Substituting this [ansatz](@entry_id:184384) into Laplace's equation, $\nabla^2 u = 0$, gives:
$$ \frac{1}{r}\frac{d}{dr}\left(r \frac{dR}{dr}\right)\Theta(\theta) + \frac{1}{r^2} R(r) \frac{d^2\Theta}{d\theta^2} = 0 $$
To separate the variables, we multiply by $\frac{r^2}{R(r)\Theta(\theta)}$:
$$ \frac{r}{R(r)}\frac{d}{dr}\left(r \frac{dR}{dr}\right) + \frac{1}{\Theta(\theta)}\frac{d^2\Theta}{d\theta^2} = 0 $$
Rearranging, we find:
$$ \frac{r^2 R''(r) + r R'(r)}{R(r)} = -\frac{\Theta''(\theta)}{\Theta(\theta)} $$
The left side of this equation is a function of $r$ only, while the right side is a function of $\theta$ only. The only way this can be true for all $r$ and $\theta$ is if both sides are equal to a constant, which we call the **[separation constant](@entry_id:175270)**, $\lambda$. This yields two ODEs:
1.  **Angular Equation:** $\Theta''(\theta) + \lambda \Theta(\theta) = 0$
2.  **Radial Equation:** $r^2 R''(r) + r R'(r) - \lambda R(r) = 0$

The specific solutions to these ODEs, and thus the form of the overall solution, depend critically on the geometry of the domain and the associated boundary conditions.

### Solutions to Laplace's Equation on a Circular Disk

The interior of a circle ($0 \le r \le a$) is a [fundamental domain](@entry_id:201756) for exploring this method. The physical requirement that the solution be single-valued and continuous dictates that $\Theta(\theta)$ must be $2\pi$-periodic. For the angular equation $\Theta'' + \lambda \Theta = 0$, this periodicity condition restricts the [separation constant](@entry_id:175270) to be $\lambda = n^2$ for integers $n \ge 0$.
*   For $n=0$, $\lambda=0$, the solution is $\Theta(\theta) = C_0$, a constant.
*   For $n > 0$, $\lambda=n^2$, the general solution is $\Theta(\theta) = A_n \cos(n\theta) + B_n \sin(n\theta)$.

The [radial equation](@entry_id:138211) is a **Cauchy-Euler equation**. For each value of $\lambda=n^2$, we find the corresponding radial solutions:
*   For $n=0$, the equation $r(rR')' = 0$ integrates to $R(r) = C_1 \ln(r) + C_2$.
*   For $n > 0$, the equation $r^2 R'' + rR' - n^2 R = 0$ has solutions of the form $r^k$, leading to the general solution $R(r) = D_1 r^n + D_2 r^{-n}$.

A crucial physical constraint for interior problems is that the solution must remain finite everywhere, particularly at the center ($r=0$). This **finiteness condition** forces us to discard [singular solutions](@entry_id:172996). The terms $\ln(r)$ and $r^{-n}$ (for $n>0$) both diverge as $r \to 0$. Therefore, for any problem defined on a domain including the origin, their coefficients must be zero.

By combining the well-behaved angular and radial solutions, we can construct the general form of any solution to Laplace's equation that is regular inside a disk:
$$ u(r, \theta) = A_0 + \sum_{n=1}^{\infty} r^n (A_n \cos(n\theta) + B_n \sin(n\theta)) $$
The unknown coefficients $A_0, A_n, B_n$ are determined by the boundary conditions.

#### Dirichlet Boundary Conditions

The simplest boundary condition is the Dirichlet condition, where the value of the function is specified on the boundary. Consider finding the electrostatic potential inside a cylinder of radius $a$ where the potential on the boundary is given by $V(a, \theta) = V_0 \sin(3\theta)$ [@problem_id:2132268]. The general solution is:
$$ V(r, \theta) = A_0 + \sum_{n=1}^{\infty} r^n (A_n \cos(n\theta) + B_n \sin(n\theta)) $$
Applying the boundary condition at $r=a$:
$$ V(a, \theta) = A_0 + \sum_{n=1}^{\infty} a^n (A_n \cos(n\theta) + B_n \sin(n\theta)) = V_0 \sin(3\theta) $$
By the uniqueness of Fourier series expansions, we can match coefficients. All coefficients must be zero except for the one corresponding to the $\sin(3\theta)$ term. This gives $A_0=0$, $A_n=0$ for all $n$, and $B_n=0$ for $n \ne 3$. For $n=3$, we have $a^3 B_3 = V_0$, so $B_3 = V_0/a^3$. The solution is remarkably simple:
$$ V(r, \theta) = \frac{V_0}{a^3} r^3 \sin(3\theta) $$

More generally, the boundary condition may not be a single sinusoid but a more complex function $f(\theta)$. In this case, we must compute the full Fourier series of $f(\theta)$ to find all the coefficients. For instance, consider finding the [steady-state temperature](@entry_id:136775) in a disk of radius $R$ where the top half is held at temperature $+1$ and the bottom half at $-1$ [@problem_id:2132296]. The boundary function is an odd square wave. Its Fourier series contains only sine terms, with coefficients $b_n = \frac{4}{\pi n}$ for odd $n$ and $b_n=0$ for even $n$. Matching this to the general solution at $r=R$ gives:
$$ u(r, \theta) = \sum_{k=0}^{\infty} \frac{4}{\pi(2k+1)} \left(\frac{r}{R}\right)^{2k+1} \sin((2k+1)\theta) $$
This infinite series represents the complete solution inside the disk.

#### Neumann and Robin Boundary Conditions

The method extends elegantly to other boundary conditions that involve derivatives. A **Neumann condition** specifies the normal derivative on the boundary, which often represents a physical flux. For a circular disk, this is $\frac{\partial u}{\partial r}|_{r=a} = g(\theta)$. For a solution to exist, the net flux across the boundary must be zero, leading to the **[compatibility condition](@entry_id:171102)** $\int_0^{2\pi} g(\theta) d\theta = 0$.

Let's find the temperature in a disk of radius $a$ where the heat flux at the boundary is $\frac{\partial u}{\partial r}|_{r=a} = \alpha \cos(2\theta) + \beta \sin(3\theta)$, and the temperature at the center is fixed at $u(0, \theta) = T_0$ [@problem_id:2132288]. We start with the general [regular solution](@entry_id:156590) and compute its radial derivative:
$$ \frac{\partial u}{\partial r} = \sum_{n=1}^{\infty} n r^{n-1} (A_n \cos(n\theta) + B_n \sin(n\theta)) $$
At $r=a$, we match coefficients with the given flux function, yielding $2a A_2 = \alpha$ and $3a^2 B_3 = \beta$. All other $A_n$ and $B_n$ (for $n \ge 1$) are zero. The constant term $A_0$ is not determined by the derivative condition, but the condition at the center gives $u(0, \theta) = A_0 = T_0$. The full solution is:
$$ u(r, \theta) = T_0 + \frac{\alpha}{2a} r^2 \cos(2\theta) + \frac{\beta}{3a^2} r^3 \sin(3\theta) $$

A **Robin condition**, of the form $\frac{\partial u}{\partial r}|_{r=R} + \alpha u(R, \theta) = h(\theta)$, represents heat exchange with an external medium [@problem_id:2132241]. Each Fourier mode can be solved independently. Substituting the general series solution into the Robin condition at $r=R$ yields a linear algebraic equation for each coefficient, which is readily solved. For instance, for the term $V_2 \cos(2\theta)$ in the boundary data, we would find $(2 R a_2 + \alpha R^2 a_2) = V_2$, allowing us to solve for $a_2$.

### Extending the Domain: Exterior, Annular, and Wedge Regions

The same fundamental principles apply to more complex geometries, though the choice of which radial solutions to keep or discard changes.

#### Exterior Domains

For a problem defined on the region *outside* a circle, $r \ge a$, the domain extends to infinity. Physical solutions must remain bounded as $r \to \infty$. This new [boundedness](@entry_id:746948) condition requires us to discard the terms $r^n$ (for $n>0$) and $\ln(r)$ from our radial solutions, as they grow indefinitely. The general form of a bounded solution in an exterior domain is:
$$ u(r, \theta) = B_0 + \sum_{n=1}^{\infty} r^{-n} (A_n \cos(n\theta) + B_n \sin(n\theta)) $$
Consider finding the temperature outside a circular hole of radius $a$ where the boundary is held at $T(a, \theta) = V_0 \cos^2(\theta)$ [@problem_id:2132297]. Using the identity $\cos^2(\theta) = \frac{1}{2}(1 + \cos(2\theta))$, we match coefficients at $r=a$:
$$ B_0 + \sum_{n=1}^{\infty} a^{-n} (A_n \cos(n\theta) + B_n \sin(n\theta)) = \frac{V_0}{2} + \frac{V_0}{2} \cos(2\theta) $$
This immediately gives $B_0 = V_0/2$ and $a^{-2}A_2 = V_0/2$, or $A_2 = V_0 a^2/2$. All other coefficients are zero. The temperature distribution is:
$$ T(r, \theta) = \frac{V_0}{2} + \frac{V_0 a^2}{2r^2} \cos(2\theta) $$
Note that as $r \to \infty$, the temperature approaches a constant value $V_0/2$.

#### Annular Domains

In an annular region, $a \le r \le b$, neither the origin nor infinity is part of the domain. Therefore, there are no grounds to discard any of the radial solutions. The general solution to Laplace's equation in an annulus includes all terms:
$$ u(r, \theta) = (A_0 + B_0 \ln r) + \sum_{n=1}^{\infty} \left( (A_n r^n + B_n r^{-n}) \cos(n\theta) + (C_n r^n + D_n r^{-n}) \sin(n\theta) \right) $$
To solve for the coefficients, we need two boundary conditions, one at $r=a$ and one at $r=b$. For example, let's analyze an [annulus](@entry_id:163678) with an insulated inner boundary ($\frac{\partial T}{\partial r}|_{r=a} = 0$) and a fixed temperature at the outer boundary ($T(b, \theta) = T_0 \cos(\theta)$) [@problem_id:2132295]. Since the boundary conditions only involve the $\cos(\theta)$ mode, we only need to consider the $n=1$ cosine term:
$$ T(r, \theta) = (A_1 r + B_1 r^{-1}) \cos(\theta) $$
The [insulated boundary](@entry_id:162724) at $r=a$ implies $\frac{\partial T}{\partial r}|_{r=a} = (A_1 - B_1 a^{-2})\cos(\theta) = 0$, so $A_1 = B_1 a^{-2}$. The temperature condition at $r=b$ gives $(A_1 b + B_1 b^{-1}) = T_0$. Solving these two equations for $A_1$ and $B_1$ yields the complete solution for the temperature distribution.

#### Wedge-Shaped Domains

When the domain is a sector or wedge, defined by $0 \le r \le a$ and $0 \le \theta \le \alpha$, the angular periodicity is no longer $2\pi$. The boundary conditions on the straight edges $\theta=0$ and $\theta=\alpha$ determine the angular eigenfunctions. If, for instance, the edges are grounded ($V=0$), then the solutions to $\Theta'' + \lambda \Theta = 0$ must satisfy $\Theta(0)=0$ and $\Theta(\alpha)=0$. This leads to [eigenfunctions](@entry_id:154705) $\Theta_n(\theta) = \sin(\frac{n\pi}{\alpha} \theta)$ with eigenvalues $\lambda_n = (\frac{n\pi}{\alpha})^2$, for $n=1, 2, ...$.

The corresponding regular radial solutions are $R_n(r) = r^{\sqrt{\lambda_n}} = r^{n\pi/\alpha}$. Notice that the powers of $r$ are generally not integers. The general solution is a Fourier sine series in $\theta$ with these modified radial functions [@problem_id:2132249]:
$$ V(r, \theta) = \sum_{n=1}^{\infty} A_n r^{n\pi/\alpha} \sin\left(\frac{n\pi}{\alpha}\theta\right) $$
The coefficients $A_n$ are found by applying the boundary condition on the curved edge $r=a$.

### Beyond Laplace's Equation

The [method of separation of variables](@entry_id:197320) is a versatile tool that extends beyond steady-state, source-free problems.

#### Poisson's Equation and Internal Sources

When a system has a continuous internal source, its steady-state behavior is described by Poisson's equation, $\nabla^2 u = -f(r, \theta)$. A common approach is to find a particular solution $u_p$ that satisfies the inhomogeneous equation, and then the general solution is $u = u_p + u_h$, where $u_h$ is the general solution to the corresponding homogeneous (Laplace) equation.

In cases with high symmetry, the problem can simplify dramatically. For a circular plate with a uniform heat source $Q_0$ and a fixed boundary temperature $T_0$ at $r=a$, the governing equation is $\nabla^2 T = -Q_0/\kappa$ [@problem_id:2132287]. The [radial symmetry](@entry_id:141658) of the source and boundary implies the solution $T$ will depend only on $r$. The PDE reduces to an ODE:
$$ \frac{1}{r}\frac{d}{dr}\left(r\frac{dT}{dr}\right) = -\frac{Q_0}{\kappa} $$
This equation can be solved by direct integration. Integrating twice and applying the conditions of finiteness at $r=0$ and $T(a)=T_0$ uniquely determines the parabolic temperature profile:
$$ T(r) = T_0 + \frac{Q_0}{4\kappa}(a^2 - r^2) $$

#### The Wave Equation and Vibrating Membranes

For time-dependent problems such as the vibration of a circular membrane, we assume a solution of the form $u(r, \theta, t) = R(r)\Theta(\theta)T(t)$. For a radially symmetric vibration, $u$ depends only on $r$ and $t$, so we assume $u(r,t) = F(r)T(t)$. Substituting into the wave equation $u_{tt} = c^2 \nabla^2 u$ and separating variables yields:
$$ \frac{T''(t)}{c^2 T(t)} = \frac{F''(r) + \frac{1}{r}F'(r)}{F(r)} = -k^2 $$
The temporal equation $T'' + (ck)^2 T = 0$ gives sinusoidal oscillations in time. The [radial equation](@entry_id:138211), however, is different from what we saw with Laplace's equation:
$$ F''(r) + \frac{1}{r}F'(r) + k^2 F(r) = 0 $$
This is **Bessel's equation of order zero**. Its solutions are the Bessel functions $J_0(kr)$ and $Y_0(kr)$. As with the logarithm in the Laplacian case, the Bessel function of the second kind, $Y_0$, is singular at the origin and must be discarded for a membrane that includes $r=0$.

If the membrane is fixed at its edge ($u(R,t)=0$), then we must have $F(R) = J_0(kR) = 0$. This condition quantizes the possible values of $k$. They must be of the form $k_n = z_n/R$, where $z_n$ are the [positive roots](@entry_id:199264) of the Bessel function $J_0(z)$.

The resulting motion is a superposition of these **[normal modes](@entry_id:139640)**:
$$ u(r,t) = \sum_{n=1}^{\infty} J_0\left(\frac{z_n r}{R}\right) \left[ A_n \cos\left(\frac{c z_n t}{R}\right) + B_n \sin\left(\frac{c z_n t}{R}\right) \right] $$
The coefficients $A_n$ and $B_n$ are determined by the initial displacement $u(r,0)$ and initial velocity $\frac{\partial u}{\partial t}(r,0)$, respectively. This requires expanding the [initial conditions](@entry_id:152863) into a **Fourier-Bessel series**, using the [orthogonality property](@entry_id:268007) of Bessel functions. For an initial parabolic displacement $u(r,0) = P_0(1-r^2/R^2)$ and zero initial velocity, one can calculate the modal amplitudes $A_n$ through integration, finding that they are proportional to $1/(z_n^3 J_1(z_n))$ [@problem_id:2132277] [@problem_id:2132260]. Each term in the sum represents a [standing wave](@entry_id:261209) with a distinct radial shape and frequency, whose superposition describes the complex motion of the drumhead.