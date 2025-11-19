## Introduction
In the landscape of Riemannian geometry, a central challenge is defining and finding the "straightest possible" paths on curved manifolds. These paths, known as geodesics, generalize the notion of straight lines from Euclidean space to surfaces like spheres and beyond. While intuitively understood as locally distance-minimizing curves, a rigorous and powerful framework is needed to characterize them analytically. This article addresses this need by delving into the [calculus of variations](@entry_id:142234), demonstrating how geodesics elegantly emerge as the critical points of a functional that measures a curve's "energy."

This exploration is structured to build a comprehensive understanding, from foundational principles to practical applications. First, in **"Principles and Mechanisms,"** we will introduce the length and energy functionals, detail the variational framework, and perform the crucial [first variation of energy](@entry_id:635793) calculation to derive the celebrated geodesic equation. Next, **"Applications and Interdisciplinary Connections"** will showcase the utility of this variational approach, using it to compute geodesics in concrete spaces, uncover [conserved quantities](@entry_id:148503) through Noether's theorem, and reveal its profound impact on fields like general relativity and control theory. Finally, **"Hands-On Practices"** will provide targeted exercises to solidify these concepts through direct calculation. We begin by examining the core principles that link the energy of a curve to its geometric identity as a geodesic.

## Principles and Mechanisms

In the study of Riemannian geometry, one of the most fundamental inquiries is to identify and characterize the "straightest possible" paths between points on a manifold. In Euclidean space, these are straight lines. On a curved surface like a sphere, they are the great circles. These paths, known as **geodesics**, can be understood as curves that locally minimize distance. This intuitive notion is formalized through the [calculus of variations](@entry_id:142234), where geodesics emerge as the critical points of functionals that measure a curve's "size." This chapter elucidates the principles and mechanisms of this variational approach, focusing on how the concept of energy provides a powerful and elegant characterization of geodesics.

### The Length and Energy Functionals

To quantify the notion of a path's size on a Riemannian manifold $(M, g)$, two primary functionals are employed: the [length functional](@entry_id:203503) and the energy functional. For a piecewise smooth curve $\gamma: [a, b] \to M$, its velocity vector at time $t$ is denoted by $\dot{\gamma}(t) \in T_{\gamma(t)}M$. The speed of the curve is the norm of this vector, induced by the metric $g$ at the point $\gamma(t)$, given by $\|\dot{\gamma}(t)\| = \sqrt{g_{\gamma(t)}(\dot{\gamma}(t), \dot{\gamma}(t))}$.

The **[length functional](@entry_id:203503)**, $L(\gamma)$, is the most direct measure of a curve's metric size. It is defined as the integral of the curve's speed over its parameter interval:

$$
L(\gamma) = \int_a^b \|\dot{\gamma}(t)\| \, dt = \int_a^b \sqrt{g_{\gamma(t)}(\dot{\gamma}(t), \dot{\gamma}(t))} \, dt
$$

While geometrically intuitive, the square root within the integrand makes the [length functional](@entry_id:203503) somewhat cumbersome to handle in [variational calculus](@entry_id:197464). A mathematically more tractable alternative is the **[energy functional](@entry_id:170311)**, $E(\gamma)$. Inspired by the kinetic energy formula in classical mechanics ($\frac{1}{2}mv^2$), the [energy functional](@entry_id:170311) is defined as the integral of half the squared speed [@problem_id:3046480]:

$$
E(\gamma) = \frac{1}{2} \int_a^b \|\dot{\gamma}(t)\|^2 \, dt = \frac{1}{2} \int_a^b g_{\gamma(t)}(\dot{\gamma}(t), \dot{\gamma}(t)) \, dt
$$

The absence of the square root in the integrand of $E(\gamma)$ leads to simpler Euler-Lagrange equations. As we will see, minimizing energy is closely related to minimizing length, making the [energy functional](@entry_id:170311) a preferred tool for characterizing geodesics.

### The Variational Framework

The calculus of variations seeks to find curves that are [critical points](@entry_id:144653) (minima, maxima, or [saddle points](@entry_id:262327)) of a given functional. This is achieved by studying how the functional's value changes under small perturbations, or "variations," of the curve.

A **smooth variation** of a curve $\gamma: [a, b] \to M$ is a [smooth map](@entry_id:160364) $\Gamma: (-\epsilon, \epsilon) \times [a, b] \to M$ for some $\epsilon > 0$, such that $\Gamma(0, t) = \gamma(t)$ for all $t \in [a, b]$. This map represents a one-parameter family of curves, $\gamma_s(t) = \Gamma(s, t)$, with our original curve $\gamma$ being the member at $s=0$.

The "infinitesimal" change in the curve at $s=0$ is captured by the **variational vector field** along $\gamma$. This is a vector field $V$ along the curve $\gamma$ defined as the velocity of the transverse curves $s \mapsto \Gamma(s, t)$ at $s=0$:

$$
V(t) = \left.\frac{\partial \Gamma}{\partial s}(s, t)\right|_{s=0} \in T_{\gamma(t)}M
$$

A crucial aspect of the variational problem is the treatment of the curve's endpoints.
- A variation is said to have **fixed endpoints** if the start and end points of the curve do not change throughout the variation. That is, $\Gamma(s, a) = \gamma(a)$ and $\Gamma(s, b) = \gamma(b)$ for all $s \in (-\epsilon, \epsilon)$ [@problem_id:3046509]. This constraint directly implies that the variational vector field must vanish at the endpoints. Since the curve $s \mapsto \Gamma(s, a)$ is constant, its velocity vector must be zero. Thus, for fixed-endpoint variations, we have $V(a) = 0$ and $V(b) = 0$ [@problem_id:3046481] [@problem_id:3046515].

- A variation is said to have **free endpoints** if no such restrictions are placed on $\Gamma(s, a)$ and $\Gamma(s, b)$. In this case, the variational vector field $V(t)$ can be any arbitrary smooth vector field along $\gamma$, and $V(a)$ and $V(b)$ are unrestricted [tangent vectors](@entry_id:265494) at the endpoints [@problem_id:3046481].

### The First Variation of Energy and the Geodesic Equation

Our goal is to find the condition for a curve $\gamma$ to be a critical point of the [energy functional](@entry_id:170311) $E$. This means its [first variation](@entry_id:174697) must vanish for all admissible variations. We will focus on variations with fixed endpoints. The [first variation of energy](@entry_id:635793) is defined as:

$$
\delta E_\gamma(V) = \left.\frac{d}{ds} E(\gamma_s)\right|_{s=0} = \left.\frac{d}{ds}\right|_{s=0} \left( \frac{1}{2} \int_a^b g(\dot{\gamma}_s, \dot{\gamma}_s) \, dt \right)
$$

By differentiating under the integral and using the properties of the Levi-Civita connection $\nabla$, we arrive at the [first variation](@entry_id:174697) formula. The key steps of this fundamental derivation are as follows [@problem_id:3046485]:

1.  **Metric Compatibility**: The Levi-Civita connection is compatible with the metric, meaning $\nabla g = 0$. This allows us to express the derivative of the inner product as $\frac{\partial}{\partial s} g(\dot{\gamma}_s, \dot{\gamma}_s) = 2g(\nabla_{\partial/\partial s} \dot{\gamma}_s, \dot{\gamma}_s)$.
2.  **Torsion-Free Property**: The Levi-Civita connection is torsion-free, which implies that covariant derivatives commute on coordinate fields. This extends to the relation $\nabla_{\partial/\partial s} \dot{\gamma}_s = \nabla_{\partial/\partial t} V_s$, where $V_s(t) = \frac{\partial \Gamma}{\partial s}(s, t)$.
3.  **Integration by Parts**: We use the covariant derivative product rule, $\frac{d}{dt}g(V, \dot{\gamma}) = g(\nabla_{\dot{\gamma}}V, \dot{\gamma}) + g(V, \nabla_{\dot{\gamma}}\dot{\gamma})$, to move the [covariant derivative](@entry_id:152476) from the variational field $V$ to the curve's [velocity field](@entry_id:271461) $\dot{\gamma}$.

Combining these steps yields the general **[first variation](@entry_id:174697) formula for energy**:

$$
\delta E_\gamma(V) = \Big[ g(V(t), \dot{\gamma}(t)) \Big]_a^b - \int_a^b g(V(t), \nabla_{\dot{\gamma}}\dot{\gamma}(t)) \, dt
$$

For a variation with fixed endpoints, the boundary term vanishes because $V(a)=0$ and $V(b)=0$ [@problem_id:3046515]. The formula simplifies to:

$$
\delta E_\gamma(V) = - \int_a^b g(V(t), \nabla_{\dot{\gamma}}\dot{\gamma}(t)) \, dt
$$

For $\gamma$ to be a critical point of energy, we require $\delta E_\gamma(V) = 0$ for *all* smooth variational [vector fields](@entry_id:161384) $V$ that vanish at the endpoints. By the **fundamental lemma of the calculus of variations**, if the integral of a product of two functions is zero for all choices of one function (with appropriate boundary conditions), then the other function must be identically zero. This forces the covariant acceleration of the curve to vanish:

$$
\nabla_{\dot{\gamma}}\dot{\gamma} = 0
$$

This is the celebrated **[geodesic equation](@entry_id:136555)**. It provides an intrinsic, coordinate-free differential equation that characterizes the "straightest" paths on a manifold. It states that a curve is a geodesic if and only if its velocity vector is **parallel transported** along itself. This means that the velocity vector does not change in a covariant sense as one moves along the curve.

An immediate consequence of the geodesic equation is that geodesics have constant speed. We can see this by examining the derivative of the squared speed:
$$
\frac{d}{dt} \|\dot{\gamma}(t)\|^2 = \frac{d}{dt} g(\dot{\gamma}, \dot{\gamma}) = 2 g(\nabla_{\dot{\gamma}}\dot{\gamma}, \dot{\gamma})
$$
If $\gamma$ is a geodesic, then $\nabla_{\dot{\gamma}}\dot{\gamma} = 0$, which implies that $\frac{d}{dt} \|\dot{\gamma}(t)\|^2 = 0$. Therefore, the speed $\|\dot{\gamma}(t)\|$ is constant along any geodesic.

### Parametrization and the Geodesic Property

The way a curve is parametrized significantly affects the energy functional, but less so the [length functional](@entry_id:203503) and the geodesic property itself.

The [length functional](@entry_id:203503) $L(\gamma)$ is **invariant under [reparametrization](@entry_id:176404)**. If $\tilde{\gamma} = \gamma \circ \phi$ is an orientation-preserving [reparametrization](@entry_id:176404) of $\gamma$, then $L(\tilde{\gamma}) = L(\gamma)$. In contrast, the [energy functional](@entry_id:170311) $E(\gamma)$ is **not** invariant under general reparametrizations [@problem_id:3046511].

However, the [geodesic equation](@entry_id:136555) exhibits a special kind of invariance. If $\gamma(t)$ is a geodesic, and we consider an **affine [reparametrization](@entry_id:176404)** $t(s) = as+b$ (with $a \neq 0$), the new curve $\tilde{\gamma}(s) = \gamma(as+b)$ is also a geodesic. This can be seen by direct computation [@problem_id:3046496]:

$$
\nabla_{\frac{d\tilde{\gamma}}{ds}} \frac{d\tilde{\gamma}}{ds} = \nabla_{a\dot{\gamma}} (a\dot{\gamma}) = a^2 \nabla_{\dot{\gamma}}\dot{\gamma}
$$

Since $a \neq 0$, we have $\nabla_{\frac{d\tilde{\gamma}}{ds}} \frac{d\tilde{\gamma}}{ds} = 0$ if and only if $\nabla_{\dot{\gamma}}\dot{\gamma} = 0$. This shows that the property of being a geodesic is preserved under affine reparametrizations, which correspond to changes in speed and shifts in the starting parameter. This invariance is a property of any [affine connection](@entry_id:160152) and does not depend on the [metric compatibility](@entry_id:265910) or torsion-free properties of the Levi-Civita connection.

From a variational perspective, this invariance is explained by the fact that under an affine [reparametrization](@entry_id:176404) with $a>0$, the energy scales by a constant factor: $E(\tilde{\gamma}) = a E(\gamma)$ [@problem_id:3046496]. Since scaling a functional by a positive constant does not change its critical points, the underlying Euler-Lagrange equation—the geodesic equation—must be the same.

### The Interplay of Energy and Length

The choice to characterize geodesics via the energy functional rather than the more intuitive [length functional](@entry_id:203503) is motivated by mathematical convenience. The relationship between the two reveals why this choice is also geometrically sound.

For any curve $\gamma: [a, b] \to M$, the energy and length functionals are related by the **Cauchy-Schwarz inequality**:

$$
L(\gamma)^2 = \left( \int_a^b 1 \cdot \|\dot{\gamma}(t)\| \, dt \right)^2 \le \left( \int_a^b 1^2 \, dt \right) \left( \int_a^b \|\dot{\gamma}(t)\|^2 \, dt \right) = (b-a) \cdot 2E(\gamma)
$$

This gives the inequality $E(\gamma) \ge \frac{L(\gamma)^2}{2(b-a)}$. Equality holds if and only if $\|\dot{\gamma}(t)\|$ is proportional to $1$, meaning the curve has **constant speed** [@problem_id:3046511] [@problem_id:3046484].

This relationship has profound consequences:
1.  **Energy Minimizers Have Constant Speed:** For a fixed path between two points, the parametrization that minimizes energy is the one with constant speed. Any other [parametrization](@entry_id:272587) will have strictly greater energy.
2.  **Energy Minimizers are Length Minimizers:** A curve that minimizes energy between two points (over a fixed time interval) must be a [constant-speed geodesic](@entry_id:634525). This constant-speed property ensures it achieves the lower bound in the Cauchy-Schwarz inequality. It can be shown that this curve also minimizes length among all possible paths between the two points [@problem_id:3046484].
3.  **Critical Points of $E$ vs. $L$:** The variational characterizations differ subtly but importantly [@problem_id:3046514].
    *   A curve is a critical point of the **[energy functional](@entry_id:170311)** $E$ if and only if it is a geodesic ($\nabla_{\dot\gamma}\dot\gamma = 0$). No prior assumption about the curve's speed is needed.
    *   A curve is a critical point of the **[length functional](@entry_id:203503)** $L$ if and only if it is a geodesic that is parametrized with **constant speed**. For curves with non-constant speed, the Euler-Lagrange equation for $L$ is more complex and only implies that the [acceleration vector](@entry_id:175748) $\nabla_{\dot\gamma}\dot\gamma$ is parallel to the velocity vector $\dot\gamma$, not necessarily zero.

Because the [energy functional](@entry_id:170311) automatically selects for constant-speed parametrizations and its Euler-Lagrange equation is simpler, it provides a more robust and direct path to the [geodesic equation](@entry_id:136555).

### Example: A Local Coordinate Calculation

To see these principles in action, we can compute the [first variation of energy](@entry_id:635793) in a local [coordinate chart](@entry_id:263963) $(x^1, \dots, x^n)$. The energy functional is $E(\gamma) = \frac{1}{2}\int g_{ij}(\gamma(t)) \dot{\gamma}^i(t) \dot{\gamma}^j(t) \, dt$. The [first variation](@entry_id:174697) formula $\delta E_\gamma(V) = [ g(V, \dot{\gamma}) ]_a^b - \int g(V, \nabla_{\dot{\gamma}}\dot{\gamma}) dt$ can be expressed entirely in coordinates. The covariant acceleration term becomes $(\nabla_{\dot{\gamma}}\dot{\gamma})^k = \ddot{\gamma}^k + \Gamma^k_{ij} \dot{\gamma}^i \dot{\gamma}^j$, where $\Gamma^k_{ij}$ are the Christoffel symbols of the connection.

Consider the manifold $M=\mathbb{R}^2$ with coordinates $(x,y)$ and the metric given by components $g_{11}=1+x^2$, $g_{12}=xy$, $g_{22}=1+y^2$. Let's compute the [first variation](@entry_id:174697) for the curve $\gamma(t)=(t,0)$ for $t \in [0,1]$ with the variational field $V(t) = (t^2, t)$ [@problem_id:3046513].

First, we evaluate quantities along $\gamma(t)=(t,0)$:
-   Velocity: $\dot{\gamma}(t) = (1,0)$.
-   Metric components: $g_{11}=1+t^2$, $g_{12}=0$, $g_{22}=1$.
-   Christoffel symbols: A calculation yields the relevant symbols along $\gamma$ as $\Gamma^1_{11} = \frac{t}{1+t^2}$ and $\Gamma^2_{11} = 0$.
-   Covariant acceleration: $(\nabla_{\dot{\gamma}}\dot{\gamma})^k = \ddot{\gamma}^k + \Gamma^k_{ij}\dot{\gamma}^i\dot{\gamma}^j$. Since $\ddot{\gamma}=0$ and $\dot{\gamma}=(1,0)$, this simplifies to $(\nabla_{\dot{\gamma}}\dot{\gamma})^k = \Gamma^k_{11}$. Thus, $\nabla_{\dot{\gamma}}\dot{\gamma} = (\frac{t}{1+t^2}, 0)$.

Now, we compute the two parts of the [first variation](@entry_id:174697) formula, $\delta E_\gamma(V) = g(V(1), \dot{\gamma}(1)) - g(V(0), \dot{\gamma}(0)) - \int_0^1 g(V(t), \nabla_{\dot{\gamma}}\dot{\gamma}(t)) dt$:

1.  **Boundary Term**:
    -   At $t=1$: $\dot{\gamma}(1)=(1,0)$, $V(1)=(1,1)$, and the metric matrix is $\begin{pmatrix} 2  & 0 \\ 0 & 1 \end{pmatrix}$. So, $g(V(1), \dot{\gamma}(1)) = g_{ij}V^i\dot{\gamma}^j = g_{11}V^1\dot{\gamma}^1 = 2 \cdot 1 \cdot 1 = 2$.
    -   At $t=0$: $V(0)=(0,0)$, so $g(V(0), \dot{\gamma}(0)) = 0$.
    -   The total boundary contribution is $2-0=2$.

2.  **Integral Term**:
    -   The integrand is $g(V, \nabla_{\dot{\gamma}}\dot{\gamma}) = g_{ij}V^i(\nabla_{\dot{\gamma}}\dot{\gamma})^j = g_{11}V^1(\nabla_{\dot{\gamma}}\dot{\gamma})^1 = (1+t^2)(t^2)(\frac{t}{1+t^2}) = t^3$.
    -   The integral is $-\int_0^1 t^3 dt = -[\frac{t^4}{4}]_0^1 = -\frac{1}{4}$.

Combining these, the total [first variation](@entry_id:174697) is $\delta E_\gamma(V) = 2 - \frac{1}{4} = \frac{7}{4}$. This concrete example illustrates how the abstract coordinate-free formulation translates directly into tangible calculations involving the metric components and their derivatives.