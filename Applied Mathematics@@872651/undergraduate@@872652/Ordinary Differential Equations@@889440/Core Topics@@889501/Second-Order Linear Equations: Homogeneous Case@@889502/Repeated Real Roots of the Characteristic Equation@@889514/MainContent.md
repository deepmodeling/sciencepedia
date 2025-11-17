## Introduction
The study of second-order [linear homogeneous differential equations](@entry_id:165420) with constant coefficients is a cornerstone of applied mathematics, providing the language to describe countless physical phenomena from [mechanical vibrations](@entry_id:167420) to electrical circuits. The solution to any such equation, $ay'' + by' + cy = 0$, is entirely determined by the roots of its associated characteristic equation, $ar^2 + br + c = 0$. While the cases of distinct real roots and [complex conjugate roots](@entry_id:276596) lead to straightforward exponential and oscillatory solutions, a unique and pivotal scenario arises when the [characteristic equation](@entry_id:149057) has a single, repeated real root. This situation presents a challenge: how do we construct the required two [linearly independent solutions](@entry_id:185441) from only one root?

This article provides a comprehensive exploration of this critical case. Across the following sections, you will gain a deep understanding of both the mathematical machinery and the profound physical implications of repeated characteristic roots.
The **Principles and Mechanisms** section will unveil the form of the general solution, $y(t) = (C_1 + C_2 t)\exp(rt)$, and rigorously justify its validity through multiple methods, including [reduction of order](@entry_id:140559) and the operator approach. Following this, the **Applications and Interdisciplinary Connections** section will bridge theory and practice by exploring how this mathematical structure manifests as the crucial concept of [critical damping](@entry_id:155459) in fields like engineering, physics, and control theory. Finally, the **Hands-On Practices** section will provide an opportunity to solidify your knowledge by applying these techniques to solve a variety of practical problems.

## Principles and Mechanisms

In our study of second-order [linear homogeneous differential equations](@entry_id:165420) with constant coefficients, $a y'' + b y' + c y = 0$, the characteristic equation $a r^2 + b r + c = 0$ is the cornerstone of our solution method. The nature of its roots—whether they are distinct and real, or a [complex conjugate pair](@entry_id:150139)—dictates the form of the general solution. We now turn our attention to the third and final possibility: the case where the [discriminant](@entry_id:152620) of the quadratic is zero.

### The Degenerate Case: A Single Repeated Root

When the discriminant $\Delta = b^2 - 4ac$ is equal to zero, the characteristic equation yields not two distinct roots, but a single real root with a multiplicity of two. This root is given by $r = -\frac{b}{2a}$. This scenario presents an immediate challenge. A [second-order differential equation](@entry_id:176728) requires two [linearly independent solutions](@entry_id:185441), $y_1(t)$ and $y_2(t)$, to form a general solution $y(t) = C_1 y_1(t) + C_2 y_2(t)$. The single root provides only one of these, $y_1(t) = \exp(rt)$. How, then, do we find the second, missing solution?

This situation is not merely a mathematical curiosity; it corresponds to a fundamentally important physical behavior known as **[critical damping](@entry_id:155459)**. In mechanical or electrical systems, this is the precise condition that allows a system to return to its equilibrium state as rapidly as possible without any oscillation. For instance, consider a system governed by $y'' - 6y' + ky = 0$ [@problem_id:2204799]. For this system to be critically damped, the characteristic equation $r^2 - 6r + k = 0$ must have a single repeated root. This occurs when the discriminant is zero: $\Delta = (-6)^2 - 4(1)(k) = 0$, which yields $36 - 4k = 0$, or $k=9$. For this value of $k$, the [characteristic equation](@entry_id:149057) becomes $r^2 - 6r + 9 = (r-3)^2 = 0$, giving the single repeated root $r=3$.

It can be shown that when the characteristic equation has a single repeated root $r$, the two [linearly independent solutions](@entry_id:185441) are $y_1(t) = \exp(rt)$ and $y_2(t) = t\exp(rt)$. Consequently, the general solution is a [linear combination](@entry_id:155091) of these two functions.

**General Solution for a Repeated Root**
For a second-order homogeneous linear ODE with a repeated real characteristic root $r$, the general solution is of the form:
$$
y(t) = C_1 \exp(rt) + C_2 t \exp(rt) = (C_1 + C_2 t) \exp(rt)
$$
where $C_1$ and $C_2$ are arbitrary constants.

As an example, consider a physical system modeled by the equation $\frac{d^2y}{dt^2} - 14 \frac{dy}{dt} + 49y = 0$ [@problem_id:2196568]. The [characteristic equation](@entry_id:149057) is $r^2 - 14r + 49 = 0$, which factors into $(r-7)^2 = 0$. We have a repeated root $r=7$. Applying the general form, the solution is $y(t) = (c_1 + c_2 t)\exp(7t)$. This form is fundamental to describing systems tuned for rapid stabilization, such as quadcopter drones or other [feedback control systems](@entry_id:274717) [@problem_id:2138368]. If such a system has a characteristic root $\lambda = -3$ with [multiplicity](@entry_id:136466) two, its response is immediately known to be $\phi(t) = (C_1 + C_2 t)\exp(-3t)$.

Conversely, if we know the general solution for a [critically damped system](@entry_id:262921) is $y(t) = (c_1 + c_2 t)\exp(-5t)$, we can deduce the governing differential equation. This solution implies a repeated root at $r=-5$. The [characteristic equation](@entry_id:149057) must therefore be $(r - (-5))^2 = (r+5)^2 = r^2 + 10r + 25 = 0$. This corresponds to the differential equation $y'' + 10y' + 25y = 0$ [@problem_id:2196603].

### Justification of the Second Solution

The assertion that $y_2(t) = t\exp(rt)$ is the second solution requires rigorous proof. We can establish this fact through several methods, each offering a unique insight into the structure of the differential equation.

#### Method 1: Direct Verification

The most straightforward approach is to substitute $y(t) = t\exp(rt)$ into the general second-order ODE, $ay'' + by' + cy = 0$, and verify that it is indeed a solution under the condition of a repeated root. First, we compute the derivatives of $y(t) = t\exp(rt)$:
$$
y'(t) = \exp(rt) + rt\exp(rt) = (1+rt)\exp(rt)
$$
$$
y''(t) = r\exp(rt) + r(1+rt)\exp(rt) = (2r+r^2t)\exp(rt)
$$
Substituting these into the ODE gives:
$$
a(2r+r^2t)\exp(rt) + b(1+rt)\exp(rt) + c(t\exp(rt)) = 0
$$
Since $\exp(rt)$ is never zero, we can divide it out and group terms by powers of $t$:
$$
t(ar^2 + br + c) + (2ar + b) = 0
$$
For this equation to hold for all values of $t$, the coefficients of the polynomial in $t$ must both be zero. This yields a system of two conditions:
1.  $ar^2 + br + c = 0$
2.  $2ar + b = 0$

The first condition simply states that $r$ must be a root of the [characteristic equation](@entry_id:149057). The second condition, $2ar + b = 0$, gives $r = -\frac{b}{2a}$. This is precisely the formula for the vertex of the parabola $f(r) = ar^2 + br + c$, which is the location of the repeated root when the [discriminant](@entry_id:152620) $b^2 - 4ac$ is zero. Therefore, $y(t) = t\exp(rt)$ is a solution if and only if $r$ is a repeated root of the [characteristic equation](@entry_id:149057) [@problem_id:2196566].

#### Method 2: The Method of Reduction of Order

While direct verification is effective, it does not show how one might discover the second solution. A more constructive and powerful technique is the **[method of reduction of order](@entry_id:167826)**. This method allows us to find a second, [linearly independent solution](@entry_id:174476) $y_2(t)$ if we already know one non-[trivial solution](@entry_id:155162) $y_1(t)$.

We assume the second solution takes the form $y_2(t) = v(t)y_1(t)$ for some unknown function $v(t)$. For our case, $y_1(t) = \exp(rt)$, so we propose $y_2(t) = v(t)\exp(rt)$. We substitute this into the ODE $ay'' + by' + cy = 0$. The derivatives are:
$$
y_2'(t) = v'\exp(rt) + rv\exp(rt)
$$
$$
y_2''(t) = v''\exp(rt) + 2rv'\exp(rt) + r^2v\exp(rt)
$$
Substituting and grouping by derivatives of $v(t)$:
$$
a(v''\exp(rt) + 2rv'\exp(rt) + r^2v\exp(rt)) + b(v'\exp(rt) + rv\exp(rt)) + c(v\exp(rt)) = 0
$$
$$
\exp(rt) \left[ a v'' + (2ar+b)v' + (ar^2+br+c)v \right] = 0
$$
As before, the coefficient of $v$, which is $(ar^2+br+c)$, is zero because $r$ is a root of the characteristic equation. Furthermore, since $r$ is a repeated root, we also know that $2ar+b=0$. The equation miraculously simplifies:
$$
\exp(rt) [ a v'' ] = 0
$$
Since $a \neq 0$ and $\exp(rt) \neq 0$, we are left with the remarkably simple differential equation $v'' = 0$. Integrating this twice yields $v'(t) = C_2$ and $v(t) = C_2 t + C_1$. Substituting this back into our assumed form for $y_2(t)$:
$$
y_2(t) = (C_1 + C_2 t)\exp(rt) = C_1 \exp(rt) + C_2 t\exp(rt)
$$
This is precisely the general solution. The first term, $C_1 \exp(rt)$, is just our original solution $y_1(t)$. The new, linearly independent part is $t\exp(rt)$. By choosing $C_1=0$ and $C_2=1$, we identify the second fundamental solution as $y_2(t) = t\exp(rt)$ [@problem_id:2196585].

#### Method 3: An Alternative View: The Operator Method

A particularly elegant perspective arises from using differential operators. Let $D = \frac{d}{dt}$. The ODE $ay'' + by' + cy = 0$ can be written as $(aD^2 + bD + c)y = 0$. When the [characteristic polynomial](@entry_id:150909) has a repeated root $r$, the operator itself can be factored as $a(D-r)^2$. This means our differential equation can be written as:
$$
a(D-r)^2 y = 0
$$
We can solve this by treating it as a sequence of two first-order equations. Let's define an intermediate function $u(t) = (D-r)y$. The original equation then becomes $(D-r)u = 0$, or $u' - ru = 0$. This is a separable first-order equation whose solution is $u(t) = C_2 \exp(rt)$.

Now, we substitute this back into the definition of $u(t)$:
$$
(D-r)y = u(t) \quad \Rightarrow \quad y' - ry = C_2 \exp(rt)
$$
This is a first-order linear equation, which we can solve using an [integrating factor](@entry_id:273154) $\mu(t) = \exp(\int -r \, dt) = \exp(-rt)$. Multiplying the equation by $\mu(t)$ gives:
$$
\exp(-rt)y' - r\exp(-rt)y = C_2
$$
The left side is the derivative of a product: $\frac{d}{dt}(\exp(-rt)y) = C_2$. Integrating with respect to $t$ gives:
$$
\exp(-rt)y = C_2 t + C_1
$$
Finally, solving for $y(t)$ yields the familiar general solution:
$$
y(t) = (C_1 + C_2 t)\exp(rt)
$$
This method not only confirms the form of the solution but is also highly effective for solving [initial value problems](@entry_id:144620) [@problem_id:2196605].

### Linear Independence and the Wronskian

To confirm that $y_1(t) = \exp(rt)$ and $y_2(t) = t\exp(rt)$ form a valid [fundamental set of solutions](@entry_id:177810), we must verify that they are linearly independent. The standard tool for this is the **Wronskian**, defined for two functions $y_1$ and $y_2$ as the determinant:
$$
W(y_1, y_2)(t) = \begin{vmatrix} y_1(t) & y_2(t) \\ y_1'(t) & y_2'(t) \end{vmatrix} = y_1(t)y_2'(t) - y_2(t)y_1'(t)
$$
For our solutions, we have $y_1(t) = \exp(rt)$ and $y_2(t) = t\exp(rt)$. Their derivatives are $y_1'(t) = r\exp(rt)$ and $y_2'(t) = (1+rt)\exp(rt)$. Substituting these into the Wronskian determinant gives [@problem_id:2196570]:
$$
W(t) = \exp(rt) \cdot (1+rt)\exp(rt) - t\exp(rt) \cdot r\exp(rt)
$$
$$
W(t) = (1+rt)\exp(2rt) - rt\exp(2rt) = \exp(2rt) + rt\exp(2rt) - rt\exp(2rt)
$$
$$
W(t) = \exp(2rt)
$$
Since the exponential function is never zero for any finite $t$, the Wronskian is non-zero for all $t$. This formally proves that $\exp(rt)$ and $t\exp(rt)$ are [linearly independent](@entry_id:148207) and thus form a [fundamental set of solutions](@entry_id:177810) for the differential equation.

### Physical Interpretation: The Case of Critical Damping

As mentioned, the repeated root case corresponds to the physical phenomenon of critical damping. This is the boundary case separating oscillatory behavior ([underdamping](@entry_id:168002), [complex roots](@entry_id:172941)) from slow, non-oscillatory decay ([overdamping](@entry_id:167953), distinct real roots). For a stable system, the root $r$ must be negative ($r < 0$), ensuring that the solution $y(t) = (C_1 + C_2 t)\exp(rt)$ decays to zero as $t \to \infty$.

The behavior of a [critically damped system](@entry_id:262921) is unique. Although it is non-oscillatory by definition, it is possible for the system to "overshoot" the equilibrium position once. A solution $y(t)$ crosses the equilibrium when $y(t) = 0$. For a non-[trivial solution](@entry_id:155162), this occurs if $(C_1 + C_2 t) = 0$ at some time $t_{\text{cross}} > 0$, which requires $t_{\text{cross}} = -C_1/C_2$. This can happen at most once for $t>0$.

A particularly insightful property of these systems can be revealed by analyzing the motion after an equilibrium crossing [@problem_id:2196583]. Suppose a system crosses the equilibrium at $t_{\text{cross}}$ and reaches a point of maximum displacement (an extremum) at a later time $t_{\text{ext}}$. This extremum occurs when the velocity $y'(t)$ is zero. We found the velocity to be $y'(t) = (C_2 + r(C_1+C_2 t))\exp(rt)$. Setting this to zero gives:
$$
C_2 + rC_1 + rC_2 t_{\text{ext}} = 0
$$
Solving for $t_{\text{ext}}$ yields $t_{\text{ext}} = -\frac{C_1}{C_2} - \frac{1}{r}$.
The time interval between the equilibrium crossing and the subsequent peak is therefore:
$$
\Delta t = t_{\text{ext}} - t_{\text{cross}} = \left(-\frac{C_1}{C_2} - \frac{1}{r}\right) - \left(-\frac{C_1}{C_2}\right) = -\frac{1}{r}
$$
This remarkable result shows that for a stable, [critically damped system](@entry_id:262921) ($r < 0$), this time interval $\Delta t = -1/r$ is a positive constant that depends only on the intrinsic properties of the system (encapsulated by $r$) and not on the specific initial conditions that produced the overshoot. The quantity $\tau = -1/r$ represents a fundamental timescale for the system's response.

### Generalization to Higher-Order Equations

The pattern observed for second-order equations extends naturally to higher-order linear homogeneous ODEs. If the characteristic equation of an $n$-th order ODE has a real root $r$ with multiplicity $m$ (where $2 \le m \le n$), then there will be $m$ [linearly independent solutions](@entry_id:185441) associated with this root. These solutions are:
$$
\exp(rt), \quad t\exp(rt), \quad t^2\exp(rt), \quad \dots, \quad t^{m-1}\exp(rt)
$$
The part of the general solution corresponding to this root is a [linear combination](@entry_id:155091) of these $m$ functions:
$$
y_{\text{partial}}(t) = (C_1 + C_2 t + C_3 t^2 + \dots + C_m t^{m-1})\exp(rt)
$$

For example, if a fourth-order seismic isolation system has a characteristic equation with a single root $\lambda = -1$ of [multiplicity](@entry_id:136466) four, its governing ODE is effectively $(D+1)^4 y = 0$ [@problem_id:2196546]. The general solution is constructed from the four basis functions $\exp(-t)$, $t\exp(-t)$, $t^2\exp(-t)$, and $t^3\exp(-t)$. The complete general solution is:
$$
y(t) = (C_1 + C_2 t + C_3 t^2 + C_4 t^3)\exp(-t)
$$
This principle allows us to systematically construct solutions for complex, high-order systems, provided we can find the roots of their characteristic polynomials and their multiplicities.