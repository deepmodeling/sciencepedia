## Introduction
In the study of physics and engineering, while Cartesian coordinates are ubiquitous, many real-world systems exhibit circular or [cylindrical symmetry](@entry_id:269179)—from the ripples in a pond to the vibrations of a drumhead or the flow of heat through a pipe. For these scenarios, the familiar Fourier series based on sines and cosines is inadequate. The essential mathematical tool we need is the Fourier-Bessel series, which serves as the direct analogue to the Fourier series for functions defined on a circular domain. This article provides a comprehensive exploration of this powerful technique, addressing the challenge of how to represent functions and solve [partial differential equations](@entry_id:143134) in cylindrical [coordinate systems](@entry_id:149266).

This article is structured to build your understanding systematically. The first section, **Principles and Mechanisms**, lays the theoretical groundwork, showing how Bessel's equation arises from physical problems and how Sturm-Liouville theory provides the framework for constructing the series. The second section, **Applications and Interdisciplinary Connections**, demonstrates the versatility of Fourier-Bessel series by exploring their use in diverse fields such as [acoustics](@entry_id:265335), heat transfer, and quantum mechanics. Finally, the **Hands-On Practices** section allows you to solidify your knowledge by working through guided problems that apply the concepts you've learned.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms underpinning Fourier-Bessel series. We will explore their origin in the solution of partial differential equations, establish their theoretical foundation within the framework of Sturm-Liouville theory, and develop the practical methods for their application.

### The Genesis of Bessel's Equation in Physical Systems

Many fundamental physical phenomena occurring in circular or cylindrical domains, such as heat conduction, wave propagation, and electrostatic potentials, are described by [partial differential equations](@entry_id:143134) (PDEs). When these equations are expressed in polar or [cylindrical coordinates](@entry_id:271645), the [method of separation of variables](@entry_id:197320) often leads to a particular type of ordinary differential equation known as **Bessel's differential equation**.

Consider, for example, the vibration of a thin circular membrane of radius $R$, like a drumhead. Its displacement from equilibrium, $\psi(r, \theta, t)$, is governed by the two-dimensional wave equation, which in polar coordinates $(r, \theta)$ is:
$$ \frac{1}{r}\frac{\partial}{\partial r}\left(r\frac{\partial\psi}{\partial r}\right) + \frac{1}{r^2}\frac{\partial^2\psi}{\partial \theta^2} = \frac{1}{v^2} \frac{\partial^2 \psi}{\partial t^2} $$
Here, $v$ is the [wave propagation](@entry_id:144063) speed. We seek solutions by separating variables, assuming a solution of the form $\psi(r, \theta, t) = R(r)\Theta(\theta)T(t)$. Substituting this into the wave equation and rearranging isolates the temporal, angular, and radial dependencies. The angular dependence is typically harmonic, $\Theta(\theta) \sim e^{in\theta}$, which requires $\Theta''(\theta) = -n^2 \Theta(\theta)$ for integer $n$ to ensure periodicity. The temporal part becomes $T''(t) = -(kv)^2 T(t)$. This separation process ultimately yields an equation for the radial component $R(r)$:
$$ r^2 R''(r) + r R'(r) + (k^2 r^2 - n^2) R(r) = 0 $$
This is the celebrated **Bessel's differential equation** of order $n$. The constant $k$ is a [separation constant](@entry_id:175270) that will be determined by the boundary conditions of the physical problem. A similar process for the Helmholtz equation, $\nabla^2 u + k^2 u = 0$, also directly yields this [radial equation](@entry_id:138211) [@problem_id:2105064] [@problem_id:2105077]. This recurring emergence of Bessel's equation in problems with circular geometry motivates the development of a systematic method for representing functions using its solutions, analogous to how Fourier series use sines and cosines for rectangular geometries.

### Bessel's Equation and Singular Sturm-Liouville Theory

The theory of Fourier-Bessel series is most rigorously understood through the lens of **Sturm-Liouville theory**. A general Sturm-Liouville equation has the form:
$$ \frac{d}{dr}\left[p(r) \frac{dR}{dr}\right] + \left[-q(r) + \lambda w(r)\right]R(r) = 0 $$
where $\lambda$ is an eigenvalue. To cast Bessel's equation into this form, we can multiply it by $1/r$:
$$ R''(r) + \frac{1}{r}R'(r) + \left(k^2 - \frac{n^2}{r^2}\right)R(r) = 0 $$
Multiplying again by $r$ allows us to combine the first two terms:
$$ \frac{d}{dr}\left(r \frac{dR}{dr}\right) + \left(k^2 r - \frac{n^2}{r}\right)R(r) = 0 $$
Comparing this to the standard Sturm-Liouville form, we identify the eigenvalue as $\lambda = k^2$ and the constituent functions as:
- $p(r) = r$
- $q(r) = \frac{n^2}{r}$
- $w(r) = r$

The function $w(r)$ is known as the **weight function**, and its presence is crucial for defining the orthogonality of the solutions. A key feature of this particular problem on an interval $[0, R]$ is that the function $p(r) = r$ is equal to zero at the endpoint $r=0$. A regular Sturm-Liouville problem requires $p(r) > 0$ throughout the closed interval. Since this condition is violated, the Bessel-Sturm-Liouville problem is classified as a **singular Sturm-Liouville problem** [@problem_id:2105089]. This singularity at the origin imposes an important constraint on the set of physically acceptable solutions.

### Physical Regularity and the Choice of Bessel Functions

The general solution to Bessel's equation of order $n$ is a linear combination of two [linearly independent](@entry_id:148207) functions:
$$ R(r) = C_1 J_n(kr) + C_2 Y_n(kr) $$
Here, $J_n(x)$ is the **Bessel function of the first kind** of order $n$, and $Y_n(x)$ is the **Bessel function of the second kind** of order $n$ (also known as the Weber or Neumann function).

The distinction between these two functions becomes paramount when considering the physical domain. For any problem involving a solid disk or cylinder that includes the center point $r=0$, the physical quantity being modeled (e.g., temperature, displacement) must remain finite at the origin. An examination of the behavior of Bessel functions for small arguments reveals a critical difference:
- $J_n(x)$ is regular at $x=0$. For $n=0$, $J_0(0)=1$. For integer $n \ge 1$, $J_n(0)=0$. In all cases, $J_n(x)$ is bounded at the origin.
- $Y_n(x)$ is singular at $x=0$. As $x \to 0^+$, $|Y_n(x)| \to \infty$ for all orders $n$.

Therefore, for a solution to remain physically realistic (i.e., bounded) at $r=0$, the coefficient of the singular part must be zero. We must impose the condition $C_2 = 0$ [@problem_id:2105101]. This effectively discards the $Y_n$ family of solutions for problems on solid domains, leaving us with solutions of the form $R(r) = J_n(kr)$.

### Eigenvalues from Boundary Conditions

With the solution restricted to $R(r) = J_n(kr)$, we next apply the boundary condition at the outer radius of the domain, $r=a$. This condition determines the permissible values of the [separation constant](@entry_id:175270) $k$, leading to a discrete set of **characteristic wavenumbers** for $k$. The eigenfunctions corresponding to these wavenumbers will form the basis for our [series expansion](@entry_id:142878).

The two most common [homogeneous boundary conditions](@entry_id:750371) are:

1.  **Dirichlet Boundary Condition**: This corresponds to a fixed value at the boundary, often zero. For example, a drumhead fixed at its edge or a disk whose edge is held at a constant zero temperature. The condition is $R(a)=0$. Applying this to our solution gives:
    $$ J_n(ka) = 0 $$
    This is a **[transcendental equation](@entry_id:276279)** whose [positive roots](@entry_id:199264), let's call them $\alpha_{nm}$ for $m=1, 2, 3, \dots$, define the allowed values of the argument. The characteristic wavenumbers for the problem are then given by $\lambda_{nm} = \alpha_{nm}/a$. The corresponding eigenfunctions are $J_n(\lambda_{nm} r)$ [@problem_id:2105050] [@problem_id:2105047].

2.  **Neumann Boundary Condition**: This corresponds to a specified flux at the boundary, often zero. For example, an [insulated boundary](@entry_id:162724) on a disk where there is no heat flow. The condition is $R'(a)=0$. Differentiating our solution, $R'(r) = k J_n'(kr)$, and applying the condition yields:
    $$ k J_n'(ka) = 0 $$
    For a non-trivial solution ($k \neq 0$), this requires $J_n'(ka) = 0$. Again, this is a [transcendental equation](@entry_id:276279) whose [positive roots](@entry_id:199264) determine the characteristic wavenumbers for the problem [@problem_id:2105071].

In either case, the enforcement of a boundary condition at $r=a$ discretizes the possible values of $k$, yielding an infinite sequence of characteristic wavenumbers $\lambda_{n1}, \lambda_{n2}, \dots$ and a corresponding set of [eigenfunctions](@entry_id:154705) $\{J_n(\lambda_{nm} r)\}_{m=1}^{\infty}$.

### The Fourier-Bessel Series and Coefficient Calculation

The power of the Sturm-Liouville framework is that it guarantees that the set of [eigenfunctions](@entry_id:154705) $\{J_n(\lambda_{nm} r)\}_{m=1}^{\infty}$ obtained from a self-[adjoint problem](@entry_id:746299) is **orthogonal** over the interval $[0, a]$ with respect to the weight function $w(r)=r$. This means:
$$ \int_0^a r J_n(\lambda_{nm} r) J_n(\lambda_{nk} r) dr = 0 \quad \text{for } m \neq k $$
This [orthogonality property](@entry_id:268007) [@problem_id:2105112] allows us to expand an arbitrary, well-behaved function $f(r)$ defined on $[0, a]$ into a **Fourier-Bessel series**:
$$ f(r) = \sum_{m=1}^{\infty} c_m J_n(\lambda_{nm} r) $$

To find the coefficients $c_m$, we use a procedure analogous to that for standard Fourier series. We multiply both sides of the expansion by $r J_n(\lambda_{nk} r)$ (where $k$ is a specific integer index) and integrate from $0$ to $a$:
$$ \int_0^a r f(r) J_n(\lambda_{nk} r) dr = \int_0^a r \left( \sum_{m=1}^{\infty} c_m J_n(\lambda_{nm} r) \right) J_n(\lambda_{nk} r) dr $$
Assuming the series converges uniformly, we can interchange the summation and integration:
$$ \int_0^a r f(r) J_n(\lambda_{nk} r) dr = \sum_{m=1}^{\infty} c_m \int_0^a r J_n(\lambda_{nm} r) J_n(\lambda_{nk} r) dr $$
Due to orthogonality, every integral on the right-hand side is zero except for the single term where $m=k$. This isolates the coefficient $c_k$:
$$ \int_0^a r f(r) J_n(\lambda_{nk} r) dr = c_k \int_0^a r [J_n(\lambda_{nk} r)]^2 dr $$
Solving for $c_k$ yields the general formula for the Fourier-Bessel coefficients:
$$ c_k = \frac{\int_0^a r f(r) J_n(\lambda_{nk} r) dr}{\int_0^a r [J_n(\lambda_{nk} r)]^2 dr} $$
The integral in the denominator is the squared **norm** of the eigenfunction. Its value is a standard result that depends on the boundary condition used to define the characteristic wavenumbers. For the common Dirichlet case where $J_n(\lambda_{nk} a) = 0$, the normalization integral evaluates to:
$$ \int_0^a r [J_n(\lambda_{nk} r)]^2 dr = \frac{a^2}{2} [J_{n+1}(\lambda_{nk} a)]^2 = \frac{a^2}{2} [J_n'(\lambda_{nk} a)]^2 $$

#### Example: Expansion of a Constant Function
Let's find the order-zero Fourier-Bessel series for a constant function $f(r) = V_0$ on $[0, R]$, subject to the Dirichlet condition $J_0(\lambda_n R) = 0$. The coefficients are:
$$ c_n = \frac{\int_0^R r V_0 J_0(\lambda_n r) dr}{\int_0^R r [J_0(\lambda_n r)]^2 dr} $$
The numerator integral can be solved using the identity $\int x J_0(x) dx = x J_1(x)$:
$$ V_0 \int_0^R r J_0(\lambda_n r) dr = \frac{V_0}{\lambda_n^2} \int_0^{\lambda_n R} u J_0(u) du = \frac{V_0}{\lambda_n^2} [\lambda_n R J_1(\lambda_n R)] = \frac{V_0 R}{\lambda_n} J_1(\lambda_n R) $$
The denominator is given by the normalization formula for $n=0$: $\frac{R^2}{2}[J_1(\lambda_n R)]^2$. Combining these gives the coefficients [@problem_id:2105112] [@problem_id:2105047]:
$$ c_n = \frac{\frac{V_0 R}{\lambda_n} J_1(\lambda_n R)}{\frac{R^2}{2}[J_1(\lambda_n R)]^2} = \frac{2 V_0}{\lambda_n R J_1(\lambda_n R)} $$

#### Example: Expansion of a Parabolic Profile
For a more complex initial condition, such as a parabolic temperature profile $f(r) = A(R^2 - r^2)$, the calculation of the numerator integral, $\int_0^R r A(R^2-r^2) J_0(\lambda_k r) dr$, is more involved. It requires [integration by parts](@entry_id:136350) and the repeated use of Bessel function recurrence relations and integral identities. This process ultimately yields an analytic expression for the coefficients, demonstrating the broad applicability of the method [@problem_id:2105102].

These coefficients are the building blocks for solving complete PDE problems. For instance, in a [steady-state heat](@entry_id:163341) problem on a cylinder, a non-homogeneous boundary condition on one face is satisfied by expanding that boundary function into a Fourier-Bessel series. The resulting coefficients are then incorporated into the full solution, which includes terms that decay or grow along the cylinder's axis [@problem_id:2105050].

### Convergence of Fourier-Bessel Series

The convergence properties of Fourier-Bessel series are analogous to those of classical Fourier series, as described by Dirichlet's theorem. For a piecewise smooth function $f(r)$ on $[0, a]$, its Fourier-Bessel series converges:
- To $f(r)$ at every point of continuity in the open interval $(0, a)$.
- To the average of the left- and right-hand limits at any point $r_0$ of finite (jump) discontinuity. That is, the series converges to $\frac{1}{2} [f(r_0^-) + f(r_0^+)]$.

As a numerical example, consider a function on $[0, 5]$ defined as $f(r) = 17$ for $0 \le r  3$ and $f(r) = 8$ for $3  r \le 5$. At the point of discontinuity, $r=3$, the Fourier-Bessel [series expansion](@entry_id:142878) of this function will not converge to either 17 or 8. Instead, it will converge to the midpoint of the jump [@problem_id:2105090]:
$$ S = \frac{1}{2} (\lim_{r \to 3^-} f(r) + \lim_{r \to 3^+} f(r)) = \frac{1}{2}(17 + 8) = 12.5 $$
This predictable behavior is essential for correctly interpreting the mathematical solution in the context of the physical system it represents.