## Introduction
Minimal [submanifolds](@entry_id:159439) are among the most fascinating and fundamental objects in [geometric analysis](@entry_id:157700), representing surfaces that are "economical" with respect to their area. From the shape of a [soap film](@entry_id:267628) spanning a wire frame to idealized models in physics, these surfaces appear as optimal solutions to [variational problems](@entry_id:756445). But how do we mathematically define and identify these shapes? The core challenge lies in finding a rigorous method to quantify the notion of "area minimization" for surfaces curving through space.

This article addresses this challenge by developing the theory of [minimal submanifolds](@entry_id:204492) through the powerful lens of the [calculus of variations](@entry_id:142234). You will learn to view surfaces not as static objects, but as candidates in a vast landscape of possibilities, with [minimal surfaces](@entry_id:157732) occupying the [critical points](@entry_id:144653).

The journey begins in the "Principles and Mechanisms" chapter, where we will construct the [area functional](@entry_id:635965) and compute its [first variation](@entry_id:174697), revealing the crucial role of the [mean curvature vector](@entry_id:199617). In "Applications and Interdisciplinary Connections," we will explore a gallery of classic examples, uncover deep ties to physics and [partial differential equations](@entry_id:143134), and touch upon modern advancements in the field. Finally, "Hands-On Practices" will allow you to apply these theoretical tools to concrete problems, solidifying your understanding of this elegant interplay between geometry and analysis.

## Principles and Mechanisms

Having established the foundational context of [submanifolds](@entry_id:159439), we now delve into the analytical principles that govern their geometry. The central theme of this chapter is the concept of area and how it changes under small deformations. This inquiry will lead us from the basic definition of an [area functional](@entry_id:635965) to the profound concept of [minimal submanifolds](@entry_id:204492), which represent the [critical points](@entry_id:144653) of this functional. We will find that this variational perspective unifies geometry and analysis, culminating in a powerful set of tools and a rich class of geometric objects.

### The Area Functional: Measuring Submanifolds

A primary task in [geometric analysis](@entry_id:157700) is to assign quantitative measures to geometric objects. For a [submanifold](@entry_id:262388), the most natural measure is its volume, or what is more commonly called its **area** for dimensions two and higher. To define area rigorously, we must first establish a way to measure lengths and angles on the [submanifold](@entry_id:262388) itself.

Let $i: M^m \to (N^n, g)$ be a smooth immersion of an $m$-dimensional manifold $M$ into an $n$-dimensional Riemannian manifold $(N, g)$. The ambient metric $g$ provides an inner product for tangent vectors in $T_p N$ for any point $p \in N$. We can use this structure to endow $M$ with its own metric. For any two [tangent vectors](@entry_id:265494) $X, Y \in T_p M$, their images under the differential map, $di_p(X)$ and $di_p(Y)$, are vectors in $T_{i(p)}N$. We can measure their inner product using the ambient metric $g$. This defines the **[induced metric](@entry_id:160616)** $g_M$ on $M$ as the pullback of $g$ by the immersion $i$:

$$
g_{M,p}(X, Y) := g_{i(p)}(di_p(X), di_p(Y))
$$

This is commonly written as $g_M = i^*g$. The fact that $i$ is an immersion ensures that $di_p$ is injective, which guarantees that $g_M$ is positive-definite and thus a valid Riemannian metric on $M$. [@problem_id:3048558]

With a metric $g_M$ on $M$, we can define its $m$-dimensional volume, or area. The standard **Riemannian volume form** (or area form), denoted $\mathrm{d}\mu_M$, is the unique $m$-form that evaluates to $1$ on any positively oriented, $g_M$-[orthonormal basis](@entry_id:147779) of any [tangent space](@entry_id:141028) $T_p M$. In [local coordinates](@entry_id:181200) $(x^1, \dots, x^m)$ on $M$, let $F$ be the local parametrization map. The components of the [induced metric](@entry_id:160616) form a matrix $G = (G_{ij})$ where

$$
G_{ij} = g_M\left(\frac{\partial}{\partial x^i}, \frac{\partial}{\partial x^j}\right) = g\left(F_*\left(\frac{\partial}{\partial x^i}\right), F_*\left(\frac{\partial}{\partial x^j}\right)\right)
$$

The function $\sqrt{\det G}$ represents the volume of the infinitesimal parallelepiped spanned by the [coordinate basis](@entry_id:270149) vectors. The volume form is then given locally by

$$
\mathrm{d}\mu_M = \sqrt{\det G} \, \mathrm{d}x^1 \wedge \dots \wedge \mathrm{d}x^m
$$

The total area of the [submanifold](@entry_id:262388) is obtained by integrating this [volume form](@entry_id:161784) over the entire manifold $M$. This defines the **[area functional](@entry_id:635965)**, which assigns a real number to an immersion $F: \Sigma^m \to (N^n, g)$ of a compact manifold $\Sigma$:

$$
A[F] = \int_{\Sigma} \mathrm{d}\mu_{F^*g}
$$

Here, $F^*g$ is the [induced metric](@entry_id:160616) on $\Sigma$ corresponding to the specific immersion $F$. Different ways of immersing $\Sigma$ into $N$ will generally result in different induced metrics and, consequently, different total areas. [@problem_id:3048542]

### The First Variation of Area

The [area functional](@entry_id:635965) provides a landscape on the infinite-dimensional space of immersions. The central question of the [calculus of variations](@entry_id:142234) is to find the "valleys" and "[saddle points](@entry_id:262327)" of this landscape—that is, the immersions that are [critical points](@entry_id:144653) for area. To do this, we must understand how the area changes under a small deformation.

Consider a **smooth one-parameter variation** of an immersion $F: \Sigma \to N$, given by a family of immersions $F_t: \Sigma \to N$ for $t \in (-\epsilon, \epsilon)$ with $F_0 = F$. The infinitesimal deformation at $t=0$ is captured by the **variational vector field** $V$ along $F(\Sigma)$, defined as:

$$
V(p) = \left.\frac{\partial F_t(p)}{\partial t}\right|_{t=0}
$$

This vector field $V$ lives in the tangent bundle of the ambient manifold $N$, restricted to the image of $\Sigma$, i.e., $V$ is a section of $F^*(TN)$. At each point $p \in F(\Sigma)$, the ambient tangent space $T_p N$ splits orthogonally into the [tangent space](@entry_id:141028) of the [submanifold](@entry_id:262388) and its [orthogonal complement](@entry_id:151540), the [normal space](@entry_id:154487):

$$
T_p N = T_p F(\Sigma) \oplus N_p F(\Sigma)
$$

This splitting is defined by the ambient metric $g$ and allows us to uniquely decompose the variational vector field $V$ into a tangential component $V^T$ and a normal component $V^\perp$. This decomposition $V = V^T + V^\perp$ is fundamental to understanding the effect of a variation. [@problem_id:3048559] The smoothness of the immersion guarantees that this decomposition varies smoothly, so if $V$ is a smooth field, then $V^T$ and $V^\perp$ are also smooth.

The **[first variation of area](@entry_id:195526)**, denoted $\delta A(V)$, is the rate of change of area at $t=0$, $\left.\frac{d}{dt}\right|_{t=0} A[F_t]$. A careful derivation, involving the differentiation of the metric determinant (Jacobi's formula) and the decomposition of covariant derivatives using the Gauss and Weingarten formulas, yields the celebrated [first variation](@entry_id:174697) formula:

$$
\delta A(V) = \int_{\Sigma} \left( \operatorname{div}_{\Sigma}(V^T) - \langle H, V^\perp \rangle \right) \mathrm{d}\mu
$$

Here, $\operatorname{div}_{\Sigma}$ is the [divergence operator](@entry_id:265975) on the [submanifold](@entry_id:262388) $(\Sigma, F^*g)$, and $H$ is the **[mean curvature vector](@entry_id:199617)**. This crucial geometric quantity emerges naturally from the calculation as the trace of the vector-valued **second fundamental form** $B$:

$$
H = \mathrm{tr}_{F^*g}(B)
$$

The second fundamental form $B(X, Y)$ measures the normal component of the ambient covariant derivative $\nabla_X Y$, essentially quantifying how the submanifold curves within the [ambient space](@entry_id:184743). [@problem_id:3048595]

### Minimal Submanifolds

The [first variation](@entry_id:174697) formula is the key to identifying critical points of the [area functional](@entry_id:635965). The analysis of this formula depends crucially on the topology of the [submanifold](@entry_id:262388) $\Sigma$, specifically whether it has a boundary.

#### Manifolds without Boundary

Let us first consider the case where $\Sigma$ is a compact manifold without a boundary (e.g., a sphere or a torus). By the [divergence theorem on manifolds](@entry_id:190198), the integral of the divergence of any vector field over a compact boundaryless manifold is zero. Thus, for the tangential component $V^T$:

$$
\int_{\Sigma} \operatorname{div}_{\Sigma}(V^T) \, \mathrm{d}\mu = 0
$$

This remarkable simplification means that the tangential part of the variation has no effect on the area to first order. A purely tangential variation corresponds to an infinitesimal [reparametrization](@entry_id:176404) of the submanifold, which intuitively should not change its [intrinsic geometry](@entry_id:158788) or total area. [@problem_id:3048595]

For a submanifold without a boundary, the [first variation](@entry_id:174697) formula reduces to:

$$
\delta A(V) = - \int_{\Sigma} \langle H, V^\perp \rangle \, \mathrm{d}\mu
$$

This tells us that the change in area is governed entirely by the interaction between the [mean curvature vector](@entry_id:199617) $H$ and the normal component of the variation $V^\perp$. [@problem_id:3048542]

A submanifold is defined to be **minimal** if it is a critical point of the [area functional](@entry_id:635965), meaning $\delta A(V)=0$ for all admissible variations $V$. From the simplified formula, this condition becomes:

$$
\int_{\Sigma} \langle H, V^\perp \rangle \, \mathrm{d}\mu = 0 \quad \text{for all } V
$$

Since we can construct variations with any desired smooth normal component $V^\perp$, the fundamental lemma of the [calculus of variations](@entry_id:142234) implies that the term multiplying $V^\perp$ in the integrand must be identically zero. This leads to the fundamental equivalence that characterizes [minimal submanifolds](@entry_id:204492) [@problem_id:3048543]:

A [submanifold](@entry_id:262388) $F(\Sigma)$ is **minimal** if and only if its **[mean curvature vector](@entry_id:199617) vanishes identically**, $H \equiv 0$.

This elegant result transforms a global variational problem (finding immersions that are critical for area) into a local condition described by a system of partial differential equations ($H=0$). This equation is intrinsic to the immersion and holds irrespective of the ambient manifold's curvature.

#### The Role of Boundary Conditions

If the manifold $\Sigma$ has a boundary $\partial\Sigma$, the divergence theorem produces a boundary term:

$$
\delta A(V) = \int_{\partial \Sigma} \langle V^T, \nu \rangle \, \mathrm{d}\sigma - \int_{\Sigma} \langle H, V^\perp \rangle \, \mathrm{d}\mu
$$

where $\nu$ is the outward-pointing conormal vector to the boundary. In this case, the tangential component $V^T$ can contribute to the change in area through its behavior at the boundary.

A common scenario in [variational problems](@entry_id:756445) is to fix the boundary of the submanifold. For a variation $F_t$ that is **boundary-fixed**, we have $F_t(p) = F(p)$ for all $p \in \partial\Sigma$. This implies that the variational vector field $V$ must be zero on the boundary, $V|_{\partial\Sigma}=0$. Consequently, its tangential component $V^T$ also vanishes on the boundary, and the boundary integral disappears. [@problem_id:3048582] In this case, the condition for a submanifold to be a critical point for area among all competitors with the same fixed boundary is again $H \equiv 0$ on the interior of the [submanifold](@entry_id:262388).

### Properties and Examples of Minimal Submanifolds

#### The Nature of Mean Curvature

The geometric nature of the [mean curvature vector](@entry_id:199617) $H$ depends on the [codimension](@entry_id:273141) of the submanifold.
*   For a **hypersurface** in $N^{m+1}$ ([codimension](@entry_id:273141) 1), the [normal space](@entry_id:154487) at each point is one-dimensional. We can choose a local unit [normal vector field](@entry_id:268853) $\nu$. The [mean curvature vector](@entry_id:199617) is then simply a multiple of this normal, $\vec{H} = H\nu$, where $H$ is the **scalar mean curvature**.
*   For a submanifold of higher [codimension](@entry_id:273141) ($m  n-1$), the [normal space](@entry_id:154487) has dimension greater than one. The mean curvature $H = \mathrm{tr}_{F^*g}(B)$ is a vector in this multi-dimensional [normal space](@entry_id:154487). There is no single preferred normal direction, and so the mean curvature is fundamentally a vector quantity. [@problem_id:3048545]

#### Gradient Flow and Mean Curvature Flow

The [first variation](@entry_id:174697) formula, $\delta A(V) = - \int_{\Sigma} \langle H, V^\perp \rangle \mathrm{d}\mu$, has a powerful physical interpretation. The inner product $\langle H, V^\perp \rangle$ is maximized when $V^\perp$ is in the direction of $H$. The negative sign implies that the area *decreases* most rapidly when the surface is deformed in the direction of its [mean curvature vector](@entry_id:199617).

If we consider a specific variation where the velocity is proportional to the [mean curvature vector](@entry_id:199617) itself, for instance $V = H$ (assuming a certain sign convention for $H$), the [first variation](@entry_id:174697) becomes:

$$
\delta A(H) = - \int_{\Sigma} \langle H, H \rangle \mathrm{d}\mu = - \int_{\Sigma} |H|^2 \mathrm{d}\mu \le 0
$$

Equality holds if and only if $H \equiv 0$. This shows that deforming a submanifold in the direction of its [mean curvature vector](@entry_id:199617) is a process that seeks to decrease area. This is the principle behind **[mean curvature flow](@entry_id:184231)**, a process that continuously deforms a surface to reduce its area, analogous to a gradient descent for the [area functional](@entry_id:635965). [@problem_id:3048593]

#### Example: Minimal Graphs

The theory of [minimal submanifolds](@entry_id:204492) connects beautifully with the theory of [partial differential equations](@entry_id:143134) (PDEs) when we consider [submanifolds](@entry_id:159439) that are graphs of functions. Let $\Omega \subset \mathbb{R}^n$ be a domain, and consider the [graph of a function](@entry_id:159270) $u: \Omega \to \mathbb{R}$ in $\mathbb{R}^{n+1}$. The area of this graph is given by the functional:

$$
\mathcal{A}[u] = \int_{\Omega} \sqrt{1 + |\nabla u|^2} \, dx
$$

The condition for this graph to be a [minimal surface](@entry_id:267317) is that its [mean curvature](@entry_id:162147) must be zero. The Euler-Lagrange equation corresponding to the [stationarity](@entry_id:143776) of this functional is the **[minimal surface equation](@entry_id:187309)**:

$$
\operatorname{div}\left(\frac{\nabla u}{\sqrt{1 + |\nabla u|^2}}\right) = 0
$$

This is a non-linear elliptic PDE for the function $u$. If we seek a solution that satisfies a **Dirichlet boundary condition**, $u|_{\partial\Omega}=g$, the admissible variations are functions $\varphi$ that vanish on the boundary, $\varphi|_{\partial\Omega}=0$. When computing the [first variation](@entry_id:174697), the [integration by parts](@entry_id:136350) generates a boundary term which is killed precisely by this condition on $\varphi$, leaving only the interior PDE. [@problem_id:3048548]

#### Local vs. Global Area Minimization

It is crucial to distinguish between being minimal and being a global area minimizer. The condition $H=0$ is a local, differential condition. It signifies that the [submanifold](@entry_id:262388) is a critical point of the [area functional](@entry_id:635965), meaning the area is stationary to first order. This is analogous to a point on a curve where the tangent is horizontal.

However, a critical point need not be a minimum; it could be a maximum or a saddle point. A minimal surface is only guaranteed to be stationary. To be a **local area minimizer**, a minimal surface must also be **stable**, meaning the [second variation of area](@entry_id:187529) is non-negative for all variations. An unstable [minimal surface](@entry_id:267317) is a saddle point for the [area functional](@entry_id:635965). [@problem_id:3048599]

A **global area minimizer** for a given boundary must have the least area among *all* possible surfaces spanning that boundary. While a global minimizer must be a [stable minimal surface](@entry_id:636062), the converse is not true. A classic example is the **catenoid**, the [surface of revolution](@entry_id:261378) formed by a [catenary curve](@entry_id:178436), which is a [minimal surface](@entry_id:267317) in $\mathbb{R}^3$. If one considers a [catenoid](@entry_id:271627) spanning two coaxial circular rings, it is a [minimal surface](@entry_id:267317) ($H=0$). However, if the rings are moved sufficiently far apart, the total area of two separate flat disks, one spanning each ring, becomes less than the area of the catenoid. In this case, the catenoid is a minimal surface but not the global area minimizer. [@problem_id:3048599] This highlights that minimality is fundamentally a local property, while area minimization is a global one.