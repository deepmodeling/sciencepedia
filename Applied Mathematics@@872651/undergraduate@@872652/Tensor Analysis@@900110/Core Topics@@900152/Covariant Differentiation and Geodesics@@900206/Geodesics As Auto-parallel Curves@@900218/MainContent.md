## Introduction
In the familiar flat expanse of Euclidean space, the notion of a "straight line" is unambiguous. It is both the shortest path between two points and a trajectory that never deviates from its course. But how does this concept translate to the curved surfaces and abstract manifolds studied in modern physics and mathematics? This article addresses this fundamental question by moving beyond the idea of a path of minimal length, which requires a metric, to a more general and powerful definition: the geodesic as an auto-parallel curve, a path of "zero turning". This approach, built on the machinery of the [affine connection](@entry_id:160152), provides a unified framework for understanding motion and geometry.

This exploration is structured into three chapters. In **Principles and Mechanisms**, we will rigorously define the auto-parallel curve and derive the celebrated geodesic equation from first principles. Next, in **Applications and Interdisciplinary Connections**, we will witness the profound impact of this concept, from describing the motion of planets in General Relativity to defining "straightness" in the abstract spaces of [information geometry](@entry_id:141183). Finally, **Hands-On Practices** will offer a series of guided problems to build practical skills in calculating and interpreting geodesics, solidifying the theoretical foundations.

## Principles and Mechanisms

In the study of curved spaces, one of the most fundamental questions we can ask is: what constitutes a "straight line"? In Euclidean space, a straight line is the shortest path between two points, and it is a path that does not "turn" or "curve". On a general manifold, these two notions—the path of [extremal length](@entry_id:187494) and the path of "zero turning"—coincide in the context of Riemannian geometry, but the concept of "zero turning" is more general, as it can be defined on a manifold equipped only with an [affine connection](@entry_id:160152), without need for a metric. This chapter will develop the concept of a geodesic from this latter perspective, defining it as an **auto-parallel curve**: a curve that parallel transports its own [tangent vector](@entry_id:264836).

### The Definition of an Auto-parallel Curve

Imagine walking on a curved surface, attempting to follow the straightest possible path. Intuitively, this means you should never turn left or right relative to the surface. At every step, your direction of travel should remain "parallel" to the direction you had an instant before. This concept is formalized using the machinery of the covariant derivative.

Let $x^\mu(\lambda)$ be a curve on a manifold, parameterized by a variable $\lambda$. The tangent vector to this curve is $u^\mu = \frac{dx^\mu}{d\lambda}$. The rate of change of this [tangent vector](@entry_id:264836) *along the curve itself* is given by the covariant derivative of $u^\mu$ in the direction of $u^\mu$, which we can write as $\frac{Du^\mu}{d\lambda} \equiv u^\nu \nabla_\nu u^\mu$.

An **auto-parallel curve** is defined as a curve whose [tangent vector](@entry_id:264836) is parallel-transported along itself. This means that the covariant derivative of the [tangent vector](@entry_id:264836) along the curve is zero:

$$
\frac{Du^\mu}{d\lambda} = u^\nu \nabla_\nu u^\mu = 0
$$

This equation is the mathematical statement of "zero turning". It asserts that from the perspective of the [intrinsic geometry](@entry_id:158788) of the manifold, the [tangent vector](@entry_id:264836) does not change as we move along the curve. The parameter $\lambda$ for which this simple form holds is not just any parameter; it is a special one known as an **affine parameter**. A geodesic, in this context, is defined as an auto-parallel curve parameterized by an affine parameter.

### The Geodesic Equation in Component Form

While the definition $u^\nu \nabla_\nu u^\mu = 0$ is elegant and geometrically meaningful, for practical calculations we need to express it in terms of [local coordinates](@entry_id:181200) and the coefficients of the [affine connection](@entry_id:160152), $\Gamma^\lambda_{\mu\nu}$. Recalling the component definition of the [covariant derivative](@entry_id:152476), $\nabla_\nu u^\mu = \partial_\nu u^\mu + \Gamma^\mu_{\nu\sigma} u^\sigma$, we can expand the auto-parallel condition.

Let's substitute the definition of the covariant derivative into the auto-parallel equation:
$$
u^\nu (\partial_\nu u^\mu + \Gamma^\mu_{\nu\sigma} u^\sigma) = 0
$$
The first term, $u^\nu \partial_\nu u^\mu$, can be expanded using the [chain rule](@entry_id:147422). Since $u^\mu$ is a function of the coordinates $x^\sigma$, which are themselves functions of $\lambda$, we have $u^\nu \partial_\nu u^\mu = \frac{dx^\nu}{d\lambda} \frac{\partial u^\mu}{\partial x^\nu} = \frac{du^\mu}{d\lambda}$.

Substituting this back, and relabeling the dummy indices in the connection term, we arrive at:
$$
\frac{du^\mu}{d\lambda} + \Gamma^\mu_{\sigma\nu} u^\sigma u^\nu = 0
$$
Finally, substituting $u^\mu = \frac{dx^\mu}{d\lambda}$ gives us the celebrated **geodesic equation**:

$$
\frac{d^2 x^\mu}{d\lambda^2} + \Gamma^\mu_{\nu\sigma} \frac{dx^\nu}{d\lambda} \frac{dx^\sigma}{d\lambda} = 0
$$

This is a system of $n$ second-order [ordinary differential equations](@entry_id:147024) (ODEs) for the coordinates $x^\mu(\lambda)$, where $n$ is the dimension of the manifold. The [connection coefficients](@entry_id:157618) $\Gamma^\mu_{\nu\sigma}$ act as terms analogous to a gravitational force field, deflecting the path from a simple straight line.

As a direct application, consider a two-dimensional space where the only non-zero [connection coefficients](@entry_id:157618) are $\Gamma^u_{vv} = -u$ and $\Gamma^v_{uv} = \frac{1}{u}$ (for a [symmetric connection](@entry_id:187741)) [@problem_id:1514200]. The [geodesic equations](@entry_id:264349) for the coordinates $(x^1, x^2) = (u, v)$ become:
For $\mu=u$: $\frac{d^2 u}{d\lambda^2} + \Gamma^u_{vv} (\frac{dv}{d\lambda})^2 = 0 \implies \frac{d^2 u}{d\lambda^2} = u (\frac{dv}{d\lambda})^2$.
For $\mu=v$: $\frac{d^2 v}{d\lambda^2} + 2\Gamma^v_{uv} \frac{du}{d\lambda}\frac{dv}{d\lambda} = 0 \implies \frac{d^2 v}{d\lambda^2} = -\frac{2}{u} \frac{du}{d\lambda}\frac{dv}{d\lambda}$.

Given [initial conditions](@entry_id:152863), such as a starting point $(u_0, 0)$ and an [initial velocity](@entry_id:171759) $(0, w_0)$, one can immediately calculate the initial "acceleration" components. In this case, at $\lambda=0$, we would find $\frac{d^2 u}{d\lambda^2} = u_0 w_0^2$ and $\frac{d^2 v}{d\lambda^2} = 0$. This demonstrates how the geometry of the space, encoded in the $\Gamma$ coefficients, determines the trajectory of [auto-parallel curves](@entry_id:189604).

A crucial consequence of the geodesic equation being a system of second-order ODEs is the **[existence and uniqueness theorem](@entry_id:147357) for geodesics**. This theorem states that for any point $p$ on the manifold and any [tangent vector](@entry_id:264836) $v$ in the [tangent space](@entry_id:141028) $T_p M$ at that point, there exists a unique geodesic $\gamma(\lambda)$ defined for some interval of $\lambda$ around zero, such that $\gamma(0) = p$ and $\dot{\gamma}(0) = v$. This means that specifying an initial position and an [initial velocity](@entry_id:171759) is sufficient to uniquely determine the path of a geodesic, at least locally [@problem_id:1641091].

### Physical Interpretation: Geodesics as Paths of Free Motion

The [geodesic equation](@entry_id:136555) finds its most profound application in physics, where it describes the motion of particles under the influence of gravity alone. The central idea of Einstein's General Relativity is that gravity is not a force, but a manifestation of spacetime curvature. A "free" particle—one subject to no non-gravitational forces—follows a geodesic through this [curved spacetime](@entry_id:184938).

We can build intuition for this in a simpler setting. Consider a particle constrained to move without friction on a curved surface embedded in three-dimensional Euclidean space, such as a sphere or a paraboloid [@problem_id:1641063]. According to Newtonian physics, the [net force](@entry_id:163825) on the particle is the sum of the [gravitational force](@entry_id:175476) and the [normal force](@entry_id:174233) from the surface. The [normal force](@entry_id:174233) acts to constrain the particle to the surface, and its magnitude is precisely what is needed to ensure the particle's acceleration vector, when combined with the external force vector, results in a trajectory that remains on the surface. If there are no external forces other than gravity (which is accounted for by the surface's shape in this analogy), the only force is the [normal force](@entry_id:174233) from the surface. This means the particle's acceleration vector must be entirely normal (perpendicular) to the surface at every point.

This physical condition—that the tangential component of acceleration is zero—is mathematically equivalent to the [geodesic equation](@entry_id:136555) $\nabla_{\dot{\gamma}}\dot{\gamma} = 0$. The [covariant derivative](@entry_id:152476) $\nabla_{\dot{\gamma}}\dot{\gamma}$ is precisely the projection of the ordinary [acceleration vector](@entry_id:175748) (from the ambient Euclidean space) onto the tangent plane of the surface. Thus, a particle moving "freely" on a surface follows a geodesic.

A beautiful illustration is the case of a **great circle** on a sphere [@problem_id:1641078]. A great circle is the intersection of the sphere with a plane passing through its center. If we parameterize a [great circle](@entry_id:268970) at unit speed, its [acceleration vector](@entry_id:175748) in the ambient $\mathbb{R}^3$ always points directly towards the center of the sphere. Since the vector from the center to any point on the sphere is normal to the surface at that point, the [acceleration vector](@entry_id:175748) is always normal to the sphere's surface. Its projection onto the [tangent plane](@entry_id:136914) is therefore the zero vector. This means the intrinsic acceleration is zero, and the great circle is a geodesic.

In the special case of a flat manifold, which can be described by a coordinate system where the metric tensor is constant and thus all Christoffel symbols vanish ($\Gamma^\mu_{\nu\sigma} = 0$), the [geodesic equation](@entry_id:136555) simplifies dramatically to [@problem_id:1514187]:
$$
\frac{d^2 x^\mu}{d\lambda^2} = 0
$$
The solution to this is $x^\mu(\lambda) = w^\mu \lambda + c^\mu$, which is the equation of a straight line. This confirms that our generalized definition of "straightness" correctly reproduces the familiar concept in [flat space](@entry_id:204618).

### The Affine Parameter and Conservation of Speed

We have emphasized that the simple form of the geodesic equation, $u^\nu \nabla_\nu u^\mu = 0$, holds for a special class of parameters called affine parameters. A key property of this parameterization emerges when the manifold is endowed with a metric $g_{\mu\nu}$ and the connection is **[metric-compatible](@entry_id:160255)**, meaning $\nabla_\alpha g_{\mu\nu} = 0$. This is the standard setting of Riemannian geometry, where the connection is the Levi-Civita connection derived from the metric.

Consider the squared magnitude (or "speed") of the [tangent vector](@entry_id:264836), $S(\lambda) = g_{\mu\nu} u^\mu u^\nu$. Let us examine how this quantity changes along an affinely parameterized geodesic. We calculate its derivative with respect to $\lambda$:
$$
\frac{dS}{d\lambda} = \frac{d}{d\lambda}(g_{\mu\nu} u^\mu u^\nu) = u^\alpha \nabla_\alpha (g_{\mu\nu} u^\mu u^\nu)
$$
Using the product rule for the covariant derivative, we get:
$$
\frac{dS}{d\lambda} = (\nabla_\alpha g_{\mu\nu}) u^\alpha u^\mu u^\nu + g_{\mu\nu} (u^\alpha \nabla_\alpha u^\mu) u^\nu + g_{\mu\nu} u^\mu (u^\alpha \nabla_\alpha u^\nu)
$$
In a [metric-compatible](@entry_id:160255) geometry, the first term vanishes because $\nabla_\alpha g_{\mu\nu} = 0$. The second and third terms contain the expression $u^\alpha \nabla_\alpha u^\mu$, which is zero by the geodesic equation. Therefore, we are left with:
$$
\frac{dS}{d\lambda} = 0
$$
This remarkable result [@problem_id:1514212] shows that **the squared magnitude of the [tangent vector](@entry_id:264836) is conserved along an affinely parameterized geodesic in a [metric-compatible](@entry_id:160255) space**. For a massive particle in spacetime, where $ds^2$ is the [proper time](@entry_id:192124) interval, this corresponds to the fact that [proper time](@entry_id:192124) elapses at a constant rate with respect to the affine parameter. For a curve parameterized by arc length $s$, this means $\frac{ds}{d\lambda}$ is constant, so the affine parameter is proportional to the arc length.

### Reparameterization of Auto-parallel Curves

The same geometric path—the set of points that form the geodesic—can be parameterized in infinitely many ways. Only affine parameters result in the simple [geodesic equation](@entry_id:136555) $u^\nu \nabla_\nu u^\mu = 0$. If we choose an arbitrary parameter, say $\tau$, the curve $x^\mu(\tau)$ will still be an auto-parallel curve, but its [tangent vector](@entry_id:264836) $v^\mu = \frac{dx^\mu}{d\tau}$ will satisfy a more general equation:
$$
v^\alpha \nabla_\alpha v^\beta = f(\tau) v^\beta
$$
where $f(\tau)$ is some scalar function of the parameter. The curve is still "straight" in the sense that its acceleration is parallel to its velocity, but the magnitude of this acceleration is non-zero.

Fortunately, it is always possible to reparameterize such a curve to find an affine parameter. Let's say we have a curve $x^\mu(\lambda)$ that satisfies $u^\alpha \nabla_\alpha u^\beta = \frac{k}{\lambda} u^\beta$, with $u^\beta = \frac{dx^\beta}{d\lambda}$ [@problem_id:1514183]. We seek a new parameter $s(\lambda)$ such that the new [tangent vector](@entry_id:264836) $v^\beta = \frac{dx^\beta}{ds}$ satisfies the affine geodesic equation $v^\alpha \nabla_\alpha v^\beta = 0$.

Using the [chain rule](@entry_id:147422), $v^\beta = \frac{d\lambda}{ds} u^\beta$. A detailed derivation shows that for $v^\alpha \nabla_\alpha v^\beta$ to be zero, the [reparameterization](@entry_id:270587) must satisfy the differential equation $\frac{d}{d\lambda}(\frac{ds}{d\lambda}) = f(\lambda) \frac{ds}{d\lambda}$. For the specific case $f(\lambda) = \frac{k}{\lambda}$, this equation is easily solved to give $\frac{ds}{d\lambda} = C \lambda^k$, and integrating gives $s(\lambda) = \frac{C}{k+1}\lambda^{k+1} + s_0$. By choosing integration constants appropriately, we can find a simple power-law relation like $s(\lambda) = \lambda^{k+1}$. This procedure allows us to move between different parameterizations and identify the physically significant affine one.

### Generalizations of the Geodesic Concept

The framework of [auto-parallel curves](@entry_id:189604) is powerful because it can be extended to more general geometries beyond the standard Riemannian case. Two important generalizations involve relaxing the conditions of [metric compatibility](@entry_id:265910) and symmetry of the connection.

#### Non-Metricity

What if the connection is not [metric-compatible](@entry_id:160255)? Such a situation is described by a non-zero **[non-metricity](@entry_id:180322) tensor**, $Q_{\alpha\mu\nu} = \nabla_\alpha g_{\mu\nu}$. Let's re-evaluate the change in the speed-squared $S = g_{\mu\nu} u^\mu u^\nu$ along an auto-parallel curve ($u^\alpha \nabla_\alpha u^\mu = 0$) in this context [@problem_id:1514209].
$$
\frac{dS}{d\lambda} = (\nabla_\alpha g_{\mu\nu}) u^\alpha u^\mu u^\nu + g_{\mu\nu} (u^\alpha \nabla_\alpha u^\mu) u^\nu + g_{\mu\nu} u^\mu (u^\alpha \nabla_\alpha u^\nu)
$$
The second and third terms still vanish due to the auto-parallel condition. However, the first term no longer vanishes. We are left with:
$$
\frac{dS}{d\lambda} = Q_{\alpha\mu\nu} u^\alpha u^\mu u^\nu
$$
This shows that in a geometry with [non-metricity](@entry_id:180322), the magnitude of the tangent vector is generally not conserved along an auto-parallel curve. The "length" of a vector changes as it is parallel-transported, and the speed of a particle on a geodesic can change.

#### Torsion

Another fundamental property of the Levi-Civita connection is that it is symmetric, $\Gamma^\lambda_{\mu\nu} = \Gamma^\lambda_{\nu\mu}$. In more general theories, such as Einstein-Cartan theory, the connection may have an anti-symmetric part, known as the **[torsion tensor](@entry_id:204137)**: $S^\lambda_{\mu\nu} = \frac{1}{2}(\Gamma^\lambda_{\mu\nu} - \Gamma^\lambda_{\nu\mu})$.

Let's consider a connection with torsion, $\Gamma^\lambda_{\mu\nu} = \{{}^\lambda_{\mu\nu}\} + S^\lambda_{\mu\nu}$, where $\{{}^\lambda_{\mu\nu}\}$ is the symmetric Levi-Civita part. Now, if a vector $V^\lambda$ is parallel-transported along a curve $x^\mu(\tau)$ using the full connection (i.e., $u^\mu \nabla_\mu V^\lambda = 0$), how does it appear to change from the perspective of the torsion-free Levi-Civita connection? Let $\mathring{D}/d\tau \equiv u^\mu \mathring{\nabla}_\mu$ be the [covariant derivative](@entry_id:152476) along the curve using only the Levi-Civita part. The relationship between the two covariant derivatives is $\nabla_\mu V^\lambda = \mathring{\nabla}_\mu V^\lambda + S^\lambda_{\mu\nu} V^\nu$.

Contracting with $u^\mu$ and using the parallel transport condition $u^\mu \nabla_\mu V^\lambda = 0$, we find [@problem_id:1514199]:
$$
0 = u^\mu \mathring{\nabla}_\mu V^\lambda + u^\mu S^\lambda_{\mu\nu} V^\nu
$$
$$
\frac{\mathring{D}V^\lambda}{d\tau} = -u^\mu S^\lambda_{\mu\nu} V^\nu
$$
This equation shows that a vector that is "straight" with respect to the full connection appears to be "deflected" from the perspective of standard Riemannian geometry, with the deflection governed by the [torsion tensor](@entry_id:204137). If we apply this to the tangent vector itself ($V^\lambda = u^\lambda$), an auto-parallel curve in a theory with torsion does not follow a geodesic of the underlying metric; it experiences an additional "force" proportional to torsion.

#### Projective Equivalence

Finally, a deep question arises: can two different connections, $\Gamma$ and $\tilde{\Gamma}$, produce the exact same set of unparameterized [auto-parallel curves](@entry_id:189604)? The answer is yes, if they are **projectively equivalent**. This occurs if the difference between the two connections, $S^\lambda_{\mu\nu} = \tilde{\Gamma}^\lambda_{\mu\nu} - \Gamma^\lambda_{\mu\nu}$, takes a specific form. The condition is that for any [tangent vector](@entry_id:264836) $V^\mu$, the "acceleration difference" $S^\lambda_{\mu\nu} V^\mu V^\nu$ must be proportional to the [tangent vector](@entry_id:264836) $V^\lambda$ itself. This ensures that the new acceleration still points along the path, merely changing its [parameterization](@entry_id:265163).

A rigorous derivation shows that the most general form for the difference tensor $S^\lambda_{\mu\nu}$ that satisfies this for all [vector fields](@entry_id:161384) is [@problem_id:1514191]:
$$
S^\lambda_{\mu\nu} = \delta^\lambda_\mu \psi_\nu + \delta^\lambda_\nu \psi_\mu
$$
for some arbitrary [covector field](@entry_id:186855) $\psi_\mu$. This means that adding a term of this form to a connection does not alter the geometric shape of its geodesics, only their affine parameterization. This reveals that the set of "straightest lines" on a manifold is not a property of a single connection, but of an entire equivalence class of connections related by such **projective transformations**. This underlines the richness and subtlety of the geometric structures that govern motion and geometry on a manifold.