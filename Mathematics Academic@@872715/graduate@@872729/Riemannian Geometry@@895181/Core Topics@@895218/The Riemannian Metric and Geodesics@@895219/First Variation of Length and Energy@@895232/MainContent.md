## Introduction
In the landscape of Riemannian geometry, geodesics are the fundamental paths, the analogs of "straight lines" in curved spaces. While intuitively understood, their precise mathematical characterization requires a powerful analytic framework. The calculus of variations provides this framework by reframing the geometric search for the straightest path as an analytic problem: finding curves that are [critical points](@entry_id:144653) of functionals measuring length and energy. This approach not only yields a rigorous definition of geodesics but also uncovers deep connections to conservation laws and physical principles that span multiple scientific disciplines.

This article delves into the [first variation](@entry_id:174697) of the length and energy functionals to derive the [geodesic equation](@entry_id:136555). It addresses the subtle but crucial differences between these two functionals and explains why the energy functional often provides a more direct path to understanding. Through this exploration, you will gain a comprehensive understanding of how variational principles form the bedrock of modern [differential geometry](@entry_id:145818) and its applications.

The article is structured to build your knowledge systematically. The first chapter, **"Principles and Mechanisms,"** develops the core mathematical machinery, defining the functionals, introducing variations of curves, and deriving the [first variation](@entry_id:174697) formulas and their corresponding Euler-Lagrange equations. The second chapter, **"Applications and Interdisciplinary Connections,"** explores the far-reaching impact of these principles, from characterizing geodesics locally and globally to their role in physics, mechanics, and [data-driven modeling](@entry_id:184110). Finally, **"Hands-On Practices"** provides a set of targeted problems to solidify your computational skills and conceptual understanding of these foundational ideas.

## Principles and Mechanisms

In the study of Riemannian geometry, geodesics represent the straightest possible paths within a curved manifold. A powerful and general method for characterizing these fundamental curves is through the calculus of variations. This approach reframes the geometric problem of finding "straight lines" as an analytic problem of finding curves that are [critical points](@entry_id:144653) of certain functionals. The two most fundamental functionals in this context are **length** and **energy**. This chapter will develop the machinery necessary to compute the [first variation](@entry_id:174697) of these functionals, derive their respective Euler-Lagrange equations, and explore the profound relationship between them.

### Functionals on Spaces of Curves: Length and Energy

Let $(M,g)$ be a smooth $n$-dimensional Riemannian manifold. For a sufficiently [regular curve](@entry_id:267371) $c: [a,b] \to M$, we can define its length and energy. The velocity vector of the curve is denoted by $\dot{c}(t)$, and its speed is given by the norm induced by the metric: $\|\dot{c}(t)\| = \sqrt{g_{c(t)}(\dot{c}(t), \dot{c}(t))}$.

The **[length functional](@entry_id:203503)**, $L$, measures the total distance traversed by the curve:
$$
L(c) = \int_a^b \|\dot{c}(t)\| \,dt
$$

The **[energy functional](@entry_id:170311)**, $E$, is defined as:
$$
E(c) = \frac{1}{2} \int_a^b \|\dot{c}(t)\|^2 \,dt = \frac{1}{2} \int_a^b g(\dot{c}(t), \dot{c}(t)) \,dt
$$

For these integrals to be well-defined, the curve $c$ must possess a certain degree of regularity. While the theory is often first introduced for smooth ($C^\infty$) or continuously differentiable ($C^1$) curves, the natural domains for these functionals are broader. The [length functional](@entry_id:203503) is well-defined and finite for **absolutely continuous curves**. These are curves $c:[a,b] \to M$ which, in any local [coordinate chart](@entry_id:263963), are represented by absolutely continuous component functions. Such curves are [differentiable almost everywhere](@entry_id:160094), and their speed $\|\dot{c}\|$ is guaranteed to be a measurable function in the Lebesgue space $L^1([a,b])$. The energy functional, involving the square of the speed, requires a stronger condition: for the integral to be finite, the speed $\|\dot{c}\|$ must be in $L^2([a,b])$. This defines the first-order **Sobolev space of curves** on the manifold, denoted $H^1([a,b], M)$ [@problem_id:2975390]. As the interval $[a,b]$ is compact, we have the inclusion $L^2([a,b]) \subset L^1([a,b])$, which implies that any curve with finite energy also has finite length.

A crucial distinction between these two functionals lies in their behavior under [reparametrization](@entry_id:176404). The length of a curve is a geometric property of its image and should not depend on how fast we traverse it. Let $\varphi: [\alpha, \beta] \to [a,b]$ be a smooth, orientation-preserving [reparametrization](@entry_id:176404) (i.e., $\varphi'(\tau) > 0$). Let $\tilde{c}(\tau) = c(\varphi(\tau))$ be the reparametrized curve. By the chain rule, $\dot{\tilde{c}}(\tau) = \dot{c}(\varphi(\tau)) \varphi'(\tau)$. The speed transforms as $\|\dot{\tilde{c}}(\tau)\| = \|\dot{c}(\varphi(\tau))\| \varphi'(\tau)$. The length of $\tilde{c}$ is then:
$$
L(\tilde{c}) = \int_\alpha^\beta \|\dot{\tilde{c}}(\tau)\| \,d\tau = \int_\alpha^\beta \|\dot{c}(\varphi(\tau))\| \varphi'(\tau) \,d\tau
$$
A change of variables $t = \varphi(\tau)$, with $dt = \varphi'(\tau) d\tau$, transforms the integral back to the original:
$$
L(\tilde{c}) = \int_a^b \|\dot{c}(t)\| \,dt = L(c)
$$
Thus, the [length functional](@entry_id:203503) is **[reparametrization](@entry_id:176404)-invariant**.

The energy functional, however, is not. The integrand for the energy of the reparametrized curve is $\|\dot{\tilde{c}}(\tau)\|^2 = \|\dot{c}(\varphi(\tau))\|^2 (\varphi'(\tau))^2$. The energy of $\tilde{c}$ is:
$$
E(\tilde{c}) = \frac{1}{2} \int_\alpha^\beta \|\dot{c}(\varphi(\tau))\|^2 (\varphi'(\tau))^2 \,d\tau
$$
Performing the same [change of variables](@entry_id:141386) $t = \varphi(\tau)$ gives:
$$
E(\tilde{c}) = \frac{1}{2} \int_a^b \|\dot{c}(t)\|^2 \varphi'(\varphi^{-1}(t)) \,dt
$$
This is not equal to $E(c)$ unless $\varphi' \equiv 1$, which corresponds to a trivial [reparametrization](@entry_id:176404) (a shift in the starting point). This lack of invariance is not a defect; rather, it indicates that the [energy functional](@entry_id:170311) is sensitive to the parametrization of the curve, a property that proves to be exceptionally useful. The [critical points](@entry_id:144653) of the [energy functional](@entry_id:170311) are not just curves with a specific geometric trace, but curves with a specific [parametrization](@entry_id:272587) along that trace [@problem_id:2975419].

### The Calculus of Variations on Manifolds

To find the [critical points](@entry_id:144653) of $L$ and $E$, we must understand how they change under small perturbations, or variations, of a given curve.

#### Variations and Endpoint Conditions

A **smooth variation** of a curve $c: [a,b] \to M$ is a [smooth map](@entry_id:160364) $f: (-\epsilon, \epsilon) \times [a,b] \to M$, for some $\epsilon > 0$, such that $f(0, t) = c(t)$ for all $t \in [a,b]$. For each $s \in (-\epsilon, \epsilon)$, we have a curve $c_s(t) = f(s,t)$. The infinitesimal change of the variation at $s=0$ is captured by the **variational vector field** $V$ along $c$:
$$
V(t) = \left. \frac{\partial f(s,t)}{\partial s} \right|_{s=0}
$$
$V(t)$ is a vector in the [tangent space](@entry_id:141028) $T_{c(t)}M$ for each $t$.

The nature of a variational problem is heavily influenced by the constraints imposed on the endpoints of the variation.
- **Fixed Endpoints**: The variation is said to have fixed endpoints if $f(s,a) = c(a)$ and $f(s,b) = c(b)$ for all $s$. Differentiating these conditions with respect to $s$ at $s=0$ immediately shows that the variational field must vanish at the endpoints: $V(a)=0$ and $V(b)=0$ [@problem_id:2975392].
- **Free Endpoints**: If no constraints are placed on the endpoints, $f(s,a)$ and $f(s,b)$ are free to move. Any vector $v_a \in T_{c(a)}M$ and $v_b \in T_{c(b)}M$ can be realized as the endpoint values $V(a)$ and $V(b)$ of some variational field [@problem_id:2975392].
- **Endpoints on Submanifolds**: A common intermediate case is when the endpoints are constrained to lie on [submanifolds](@entry_id:159439). Suppose $f(s,a) \in N_a$ and $f(s,b) \in N_b$ for [submanifolds](@entry_id:159439) $N_a, N_b \subset M$. The curve $s \mapsto f(s,a)$ is a path that lies entirely within $N_a$. Its tangent vector at $s=0$, which is $V(a)$, must therefore belong to the [tangent space](@entry_id:141028) of the submanifold at that point: $V(a) \in T_{c(a)}N_a$. Similarly, $V(b) \in T_{c(b)}N_b$ [@problem_id:2975392] [@problem_id:2975401].

These endpoint conditions on $V$ are crucial, as they determine whether boundary terms in integration-by-parts arguments will vanish.

#### Covariant Derivatives and Their Commutation

To differentiate [vector fields](@entry_id:161384) along a varying curve, we need the concept of a **[covariant derivative along a curve](@entry_id:192566)**. Given a vector field $W$ along a curve $c(t)$, its [covariant derivative](@entry_id:152476) $\nabla_t W$ (also written $\frac{D}{dt}W$) measures the rate of change of $W$ along $c$. It is formally defined by extending $W$ to a local vector field $\widetilde{W}$ in a neighborhood of the curve and setting $\nabla_t W(t) := \nabla_{\dot{c}(t)} \widetilde{W}|_{c(t)}$. This definition is independent of the chosen extension [@problem_id:2975416]. In [local coordinates](@entry_id:181200) $\{x^i\}$ with Christoffel symbols $\Gamma^k_{ij}$, if $W(t) = W^k(t) \frac{\partial}{\partial x^k}$ and $\dot{c}(t) = \dot{x}^j(t) \frac{\partial}{\partial x^j}$, the components of the covariant derivative are given by:
$$
(\nabla_t W)^k(t) = \frac{d W^k}{dt} + \Gamma^k_{ij}(c(t)) \dot{x}^j(t) W^i(t)
$$
The [covariant derivative along a curve](@entry_id:192566) satisfies two fundamental properties inherited from the Levi-Civita connection $\nabla$:
1.  **Leibniz Rule for Functions**: For a smooth function $h: [a,b] \to \mathbb{R}$, $\nabla_t(hW) = \frac{dh}{dt} W + h \nabla_t W$.
2.  **Metric Compatibility**: For any two vector fields $W, Z$ along $c$, $\frac{d}{dt}g(W,Z) = g(\nabla_t W, Z) + g(W, \nabla_t Z)$.

A key technical result for variational formulas is the symmetry of second covariant derivatives for variations. Let $T = \frac{\partial f}{\partial t}$ and $V = \frac{\partial f}{\partial s}$ be the [coordinate vector](@entry_id:153319) fields of the variation $f(s,t)$. For the Levi-Civita connection, which is torsion-free, the covariant derivatives commute:
$$
\nabla_s T = \nabla_t V
$$
This can be verified by a direct calculation in [local coordinates](@entry_id:181200). The torsion-free property, $\Gamma^k_{ij} = \Gamma^k_{ji}$, cancels the terms involving Christoffel symbols, while the remaining terms cancel due to the equality of [mixed partial derivatives](@entry_id:139334) for the [smooth map](@entry_id:160364) $f(s,t)$ [@problem_id:2975377]. This identity allows us to switch the order of differentiation inside the variational integrals.

### The First Variation Formulas

We are now equipped to compute the [first variation of energy](@entry_id:635793) and length for a variation $f(s,t)$ with fixed endpoints. The goal is to find $\frac{d}{ds}E(c_s)|_{s=0}$ and $\frac{d}{ds}L(c_s)|_{s=0}$.

#### First Variation of Energy

We start with the energy functional $E(s) = \frac{1}{2} \int_a^b g(\partial_t f, \partial_t f) \,dt$. Differentiating under the integral sign and using [metric compatibility](@entry_id:265910):
$$
\frac{dE}{ds} = \frac{1}{2} \int_a^b \frac{\partial}{\partial s} g(\partial_t f, \partial_t f) \,dt = \int_a^b g(\nabla_s \partial_t f, \partial_t f) \,dt
$$
Using the commutation property $\nabla_s \partial_t f = \nabla_t \partial_s f$ and evaluating at $s=0$, where $\partial_t f = \dot{c}$ and $\partial_s f = V$:
$$
\left.\frac{dE}{ds}\right|_{s=0} = \int_a^b g(\nabla_t V, \dot{c}) \,dt
$$
Now, we integrate by parts using the [product rule](@entry_id:144424) for the metric: $g(\nabla_t V, \dot{c}) = \frac{d}{dt}g(V, \dot{c}) - g(V, \nabla_t \dot{c})$.
$$
\left.\frac{dE}{ds}\right|_{s=0} = \left[ g(V(t), \dot{c}(t)) \right]_a^b - \int_a^b g(V, \nabla_t \dot{c}) \,dt
$$
For a fixed-endpoint variation, $V(a)=V(b)=0$, so the boundary term vanishes. This leaves the **[first variation](@entry_id:174697) formula for energy**:
$$
\delta E = \left.\frac{dE}{ds}\right|_{s=0} = - \int_a^b g(V(t), \nabla_t \dot{c}(t)) \,dt
$$
A curve $c$ is a critical point of the energy functional if $\delta E = 0$ for all admissible variations $V$. By the fundamental lemma of the calculus of variations, this implies that the non-$V$ part of the integrand must be zero. Therefore, the **Euler-Lagrange equation for energy** is:
$$
\nabla_t \dot{c} = 0
$$
This is precisely the **geodesic equation**. It states that the acceleration vector of the curve must be zero. An important consequence is that the speed of an energy-critical curve must be constant: $\frac{d}{dt}\|\dot{c}\|^2 = \frac{d}{dt}g(\dot{c}, \dot{c}) = 2g(\nabla_t \dot{c}, \dot{c}) = 2g(0, \dot{c}) = 0$. Thus, the critical points of the [energy functional](@entry_id:170311) are precisely the **geodesics parametrized with constant speed** [@problem_id:2975395].

#### First Variation of Length

Now we consider the [length functional](@entry_id:203503) $L(s) = \int_a^b \|\partial_t f\| \,dt$. We assume the central curve $c$ is regular, so $\|\dot{c}(t)\| > 0$. Differentiating under the integral sign:
$$
\frac{dL}{ds} = \int_a^b \frac{\partial}{\partial s} \sqrt{g(\partial_t f, \partial_t f)} \,dt = \int_a^b \frac{g(\nabla_s \partial_t f, \partial_t f)}{\|\partial_t f\|} \,dt
$$
Let $T(t) = \dot{c}(t)/\|\dot{c}(t)\|$ be the [unit tangent vector](@entry_id:262985) to the curve $c$. Evaluating at $s=0$:
$$
\left.\frac{dL}{ds}\right|_{s=0} = \int_a^b \frac{g(\nabla_t V, \dot{c})}{\|\dot{c}\|} \,dt = \int_a^b g(\nabla_t V, T) \,dt
$$
Integrating by parts as before and using the fixed-endpoint conditions $V(a)=V(b)=0$, we arrive at the **[first variation](@entry_id:174697) formula for length**:
$$
\delta L = \left.\frac{dL}{ds}\right|_{s=0} = - \int_a^b g(V(t), \nabla_t T(t)) \,dt
$$
For $c$ to be a critical point of length, we must have $\delta L = 0$ for all admissible $V$. The resulting Euler-Lagrange equation is $\nabla_t T = 0$. This seems very similar to the energy equation, but the difference is crucial. Let's expand $\nabla_t T$ where $v(t) = \|\dot{c}(t)\|$ is the speed:
$$
\nabla_t T = \nabla_t \left(\frac{\dot{c}}{v}\right) = \frac{1}{v} \nabla_t \dot{c} + \dot{c} \frac{d}{dt}\left(\frac{1}{v}\right) = \frac{1}{v} \nabla_t \dot{c} - \frac{\dot{v}}{v^2} \dot{c} = \frac{1}{v} \left( \nabla_t \dot{c} - \frac{\dot{v}}{v} \dot{c} \right)
$$
The condition $\nabla_t T=0$ is therefore equivalent to $\nabla_t \dot{c} = \frac{\dot{v}}{v} \dot{c}$. This equation does not demand that the acceleration $\nabla_t \dot{c}$ be zero, only that it be parallel to the velocity vector $\dot{c}$. Such a curve is called a **pre-geodesic**. Its image on the manifold is a geodesic, but its [parametrization](@entry_id:272587) is not necessarily proportional to arc length [@problem_id:2975395].

This degeneracy is a direct consequence of the [reparametrization](@entry_id:176404)-invariance of the [length functional](@entry_id:203503). The functional is insensitive to variations that only change the [parametrization](@entry_id:272587), which correspond to tangential variational fields $V(t) = h(t) T(t)$. For such a variation, the [first variation](@entry_id:174697) $\delta L$ is always zero, because $g(T, \nabla_t T) = \frac{1}{2}\frac{d}{dt}g(T,T) = \frac{1}{2}\frac{d}{dt}(1) = 0$. Therefore, the [variational principle](@entry_id:145218) for length cannot "see" tangential components of the acceleration, and its Euler-Lagrange equation is correspondingly weaker [@problem_id:2975404].

### Unifying the Variational Principles

We have found that critical points of energy are constant-speed geodesics, while [critical points](@entry_id:144653) of length are geodesics with arbitrary (regular) parametrization. This suggests a deep connection, which we can make precise.

First, a length-critical curve fails to be energy-critical precisely when its speed is not constant [@problem_id:2975395]. If a curve has non-constant speed, its acceleration $\nabla_t\dot{c} = (\dot{v}/v)\dot{c}$ is non-zero, so it cannot be energy-critical. However, any such pre-geodesic can be reparametrized by arc length. The resulting curve will have constant speed, and since its image is a geodesic, it will satisfy the [geodesic equation](@entry_id:136555) $\nabla_t\dot{c} = 0$, making it energy-critical.

Second, consider the space of curves parametrized by unit speed, i.e., $\|\dot{c}(t)\| \equiv 1$. For such a curve, the [unit tangent vector](@entry_id:262985) $T$ is simply $\dot{c}$, and the speed $v$ is $1$.
The [first variation of energy](@entry_id:635793) is $\delta E = -\int_a^b g(V, \nabla_t \dot{c}) \,dt$.
The [first variation](@entry_id:174697) of length is $\delta L = -\int_a^b g(V, \nabla_t T) \,dt = -\int_a^b g(V, \nabla_t \dot{c}) \,dt$.
Under the unit-speed constraint, the [first variation](@entry_id:174697) formulas for length and energy become identical [@problem_id:2975403] [@problem_id:2975417]. They both yield the same Euler-Lagrange equation, $\nabla_t \dot{c} = 0$.

This observation provides a powerful practical and theoretical tool. While length is the more intuitive geometric quantity, its [reparametrization invariance](@entry_id:197540) introduces a degeneracy into its variational problem. The [energy functional](@entry_id:170311), by virtue of not being [reparametrization](@entry_id:176404)-invariant, automatically selects the "nicest" [parametrization](@entry_id:272587)—constant speed. Since the Cauchy-Schwarz inequality for integrals implies that for any curve $c$, $L(c)^2 \le (b-a) \cdot 2E(c)$, with equality if and only if $\|\dot{c}\|$ is constant, minimizing energy among all curves between two points is equivalent to finding the shortest path with its canonical constant-speed parametrization. Therefore, it is often more convenient to study geodesics as the critical points of the [energy functional](@entry_id:170311). This avoids the complexities of the "gauge freedom" of [parametrization](@entry_id:272587) and leads directly to a non-degenerate Euler-Lagrange equation whose solutions are the fundamental paths of Riemannian geometry [@problem_id:2975404].