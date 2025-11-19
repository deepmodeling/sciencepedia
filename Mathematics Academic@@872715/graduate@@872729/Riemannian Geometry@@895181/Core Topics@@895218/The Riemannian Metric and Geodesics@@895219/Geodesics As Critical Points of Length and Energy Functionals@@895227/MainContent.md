## Introduction
In the landscape of curved spaces, what constitutes a "straight line"? In Riemannian geometry, this concept is embodied by the geodesic—the most direct path between two points. While geodesics can be defined through geometric axioms, a more profound and analytically powerful perspective arises from the calculus of variations. This approach reframes the search for a geodesic as an optimization problem: finding the path that minimizes a certain "cost," such as its total length or kinetic energy.

This article addresses the apparent redundancy and technical subtleties of having two primary measures—the length and energy functionals—to define the same object. It illuminates why the mathematically simpler energy functional is often preferred and how its critical points precisely correspond to the geodesics we seek. By exploring this variational framework, you will gain a deep understanding of the fundamental principles that govern the geometry of [curves on a manifold](@entry_id:196289).

Across the following chapters, we will first delve into the "Principles and Mechanisms," where we will define the length and energy functionals, derive the geodesic equation using the Euler-Lagrange formalism, and establish the equivalence between the two [variational problems](@entry_id:756445). Next, in "Applications and Interdisciplinary Connections," we will see this theory in action, calculating geodesics in canonical spaces and uncovering deep connections to Hamiltonian mechanics, general relativity, and [global analysis](@entry_id:188294). Finally, "Hands-On Practices" will provide you with opportunities to apply these concepts to solve concrete problems, solidifying your grasp of geodesics as the cornerstone of variational geometry.

## Principles and Mechanisms

In the study of Riemannian geometry, geodesics represent the most fundamental notion of "straightness" on a curved manifold. While they can be defined axiomatically through the concept of [parallel transport](@entry_id:160671), a more powerful and insightful perspective arises from the calculus of variations. This approach characterizes geodesics as critical points of functionals that measure the "cost" of a path, such as its length or energy. This chapter will explore the principles and mechanisms underlying this variational viewpoint, demonstrating how geodesics emerge as solutions to optimization problems and how this perspective facilitates a deep analysis of their local and global properties.

### Functionals for Measuring Paths: Length and Energy

To quantify the properties of a path on a Riemannian manifold $(M,g)$, we primarily use two functionals: the **[length functional](@entry_id:203503)** and the **energy functional**. Consider a piecewise smooth curve $\gamma: [a,b] \to M$. Its tangent vector at a point $\gamma(t)$ is $\dot{\gamma}(t)$, and its speed is given by the norm induced by the metric, $\|\dot{\gamma}(t)\|_g = \sqrt{g_{\gamma(t)}(\dot{\gamma}(t), \dot{\gamma}(t))}$.

The **[length functional](@entry_id:203503)**, denoted $L(\gamma)$, is defined as the integral of the speed along the curve:
$$
L(\gamma) = \int_{a}^{b} \|\dot{\gamma}(t)\|_g \, dt
$$
This definition corresponds to the intuitive notion of the total distance traversed along the geometric path traced by $\gamma$.

The **[energy functional](@entry_id:170311)**, denoted $E(\gamma)$, is defined as half the integral of the squared speed:
$$
E(\gamma) = \frac{1}{2} \int_{a}^{b} \|\dot{\gamma}(t)\|_g^2 \, dt = \frac{1}{2} \int_{a}^{b} g_{\gamma(t)}(\dot{\gamma}(t), \dot{\gamma}(t)) \, dt
$$
While less intuitive than length, the [energy functional](@entry_id:170311) can be thought of as a measure related to the kinetic energy of a particle traversing the path. As we will see, its mathematical properties make it a more convenient tool for variational analysis.

A crucial distinction between these two functionals lies in their behavior under **[reparametrization](@entry_id:176404)**. A [reparametrization](@entry_id:176404) of $\gamma$ is a new curve $\tilde{\gamma} = \gamma \circ \varphi$, where $\varphi: [\tilde{a}, \tilde{b}] \to [a,b]$ is a smooth, orientation-preserving diffeomorphism. The geometric image of $\tilde{\gamma}$ is identical to that of $\gamma$.

The [length functional](@entry_id:203503) is **[reparametrization](@entry_id:176404) invariant**. A direct calculation using the chain rule and a [change of variables](@entry_id:141386) shows that $L(\tilde{\gamma}) = L(\gamma)$ for any such [reparametrization](@entry_id:176404) $\varphi$ [@problem_id:2976641]. This is expected, as the geometric length of a path should not depend on how quickly it is traversed.

In contrast, the energy functional is **not [reparametrization](@entry_id:176404) invariant**. Its value explicitly depends on the speed profile of the curve. For instance, consider a simple affine [reparametrization](@entry_id:176404) $\varphi(t) = \alpha t + \beta$, where $\alpha > 0$. The reparametrized curve $\tilde{\gamma} = \gamma \circ \varphi$ has energy $E(\tilde{\gamma}) = \alpha E(\gamma)$. This dependency on [parametrization](@entry_id:272587) is not a flaw; rather, it is a key feature that we can exploit.

### Geodesics as Critical Points

The central idea of the variational approach is to define geodesics as curves that are "stationary" with respect to small perturbations, i.e., as critical points of the length or energy functionals for variations that keep the endpoints fixed. A critical point is a curve for which the [first variation](@entry_id:174697) of the functional vanishes.

#### The Challenge of the Length Functional

One might naturally assume that the [length functional](@entry_id:203503) is the primary object of study for finding shortest paths. However, its direct use in the standard Euler-Lagrange framework presents a significant technical challenge. The Lagrangian for length is $F_L(x,v) = \|v\|_g = \sqrt{g_{ij}(x) v^i v^j}$. This function is positively homogeneous of degree 1 in the velocity variable $v$. A direct consequence of this homogeneity is that the fiberwise Hessian matrix, with entries $\frac{\partial^2 F_L}{\partial v^i \partial v^j}$, is singular. The velocity vector $v$ itself is always in the kernel of this Hessian.

This degeneracy means that the resulting Euler-Lagrange equations do not form a regular system of [second-order differential equations](@entry_id:269365); one cannot uniquely solve for the acceleration components $\ddot{x}^i(t)$. This mathematical obstruction is a direct reflection of the physical [reparametrization invariance](@entry_id:197540) of the [length functional](@entry_id:203503)—the system has a "gauge freedom" corresponding to the choice of parametrization [@problem_id:2976660]. While it is possible to derive [equations of motion](@entry_id:170720), they are more complex. The resulting equation forces the [acceleration vector](@entry_id:175748) $\nabla_{\dot{\gamma}}\dot{\gamma}$ to be merely tangent to the velocity vector $\dot{\gamma}$, rather than being zero. This describes a geodesic path, but allows for any arbitrary (non-affine) [parametrization](@entry_id:272587) [@problem_id:2976660].

#### The Simplicity of the Energy Functional

The [energy functional](@entry_id:170311) provides an elegant way to circumvent this difficulty. Its Lagrangian, $F_E(x,v) = \frac{1}{2}\|v\|_g^2 = \frac{1}{2}g_{ij}(x) v^i v^j$, is a simple quadratic polynomial in the velocities. Its fiberwise Hessian is simply the metric tensor $g_{ij}(x)$, which is non-degenerate by definition. This regularity ensures that the Euler-Lagrange formalism can be applied straightforwardly to yield a well-posed system of equations for the acceleration.

Let us perform this fundamental calculation. For the Lagrangian $L(x, \dot{x}) = \frac{1}{2}g_{ij}(x) \dot{x}^i \dot{x}^j$, the Euler-Lagrange equations are:
$$
\frac{d}{dt}\left(\frac{\partial L}{\partial \dot{x}^k}\right) - \frac{\partial L}{\partial x^k} = 0
$$
Computing the [partial derivatives](@entry_id:146280) yields:
$$
\frac{\partial L}{\partial \dot{x}^k} = g_{ik} \dot{x}^i \quad \text{and} \quad \frac{\partial L}{\partial x^k} = \frac{1}{2}\frac{\partial g_{ij}}{\partial x^k} \dot{x}^i \dot{x}^j
$$
Substituting these into the Euler-Lagrange equation and carrying out the [total time derivative](@entry_id:172646) leads, after some manipulation with metric properties, to the **geodesic equation in [local coordinates](@entry_id:181200)** [@problem_id:2976676]:
$$
\ddot{x}^m + \Gamma^m_{ij} \dot{x}^i \dot{x}^j = 0
$$
Here, $\Gamma^m_{ij}$ are the Christoffel symbols of the second kind, which encode the geometry of the manifold as captured by the metric. This equation is the coordinate expression for the intrinsic condition that the **covariant acceleration** of the curve is zero:
$$
\nabla_{\dot{\gamma}}\dot{\gamma} = 0
$$
This is the modern definition of a geodesic. Thus, critical points of the [energy functional](@entry_id:170311) are precisely the geodesics of the manifold.

An immediate and vital consequence of the geodesic equation is that the speed of a geodesic is constant. We can see this by examining the derivative of the squared speed:
$$
\frac{d}{dt}\|\dot{\gamma}\|^2_g = \frac{d}{dt}g(\dot{\gamma}, \dot{\gamma}) = 2 g(\nabla_{\dot{\gamma}}\dot{\gamma}, \dot{\gamma})
$$
Since $\nabla_{\dot{\gamma}}\dot{\gamma} = 0$ for a geodesic, its speed must be constant [@problem_id:2976641].

### The Equivalence of the Variational Problems

We have established that critical points of the [energy functional](@entry_id:170311) are constant-speed geodesics. But what is the relationship to the original problem of minimizing length? The two problems are, in fact, deeply connected, and for many purposes, equivalent.

This connection is made precise by the **Cauchy-Schwarz inequality** applied to integrals. For any curve $\gamma$ on an interval $[a,b]$, we have:
$$
\left( \int_a^b \|\dot{\gamma}(t)\|_g \cdot 1 \, dt \right)^2 \le \left( \int_a^b \|\dot{\gamma}(t)\|_g^2 \, dt \right) \left( \int_a^b 1^2 \, dt \right)
$$
In terms of our functionals, this becomes:
$$
L(\gamma)^2 \le 2 E(\gamma) (b-a)
$$
This fundamental inequality relates the length and energy of any path. Equality holds if and only if the integrand $\|\dot{\gamma}(t)\|_g$ is proportional to the [constant function](@entry_id:152060) $1$, meaning $\|\dot{\gamma}(t)\|_g$ must be a constant [@problem_id:2976641].

This result has a profound implication: among all possible parametrizations of a given geometric path between two points within a fixed time interval $[a,b]$, the energy is uniquely minimized by the constant-speed parametrization [@problem_id:2976682]. Therefore, by fixing the time interval and seeking to minimize energy, we are implicitly selecting the "most efficient" [parametrization](@entry_id:272587) for any given path.

This allows us to formally establish the equivalence of the [variational problems](@entry_id:756445). A critical point of the [energy functional](@entry_id:170311) is a geodesic, which we have shown must have constant speed. A curve with constant speed is precisely one for which the Cauchy-Schwarz inequality becomes an equality. Therefore, a critical point of $E$ is also a critical point of $L$. Conversely, one can show that a critical point of $L$, when reparametrized to have constant speed (a [reparametrization](@entry_id:176404) which always exists for a [regular curve](@entry_id:267371)), becomes a critical point of $E$ [@problem_id:2976676].

An alternative and powerful argument shows that a "length-stationary" curve—a critical point of $L$ for fixed-endpoint variations—must satisfy the equation $\nabla_t T = 0$, where $T = \dot{\gamma}/\|\dot{\gamma}\|$ is the [unit tangent vector](@entry_id:262985) field. If such a curve is parametrized by arc-length (i.e., unit speed), then $T = \dot{\gamma}$, and the condition becomes $\nabla_t \dot{\gamma} = 0$, the geodesic equation. This confirms that length-stationary curves are precisely geodesics, up to [reparametrization](@entry_id:176404) [@problem_id:2976664].

In summary, the problem of finding geodesics can be tackled by finding critical points of either the length or [energy functional](@entry_id:170311). However, the energy functional's mathematical simplicity and the [well-posedness](@entry_id:148590) of its Euler-Lagrange equations make it the preferred tool for analysis.

### Beyond Stationarity: Minimality and Global Structure

Finding that geodesics are stationary points is only the first step. The calculus of variations also provides tools to determine whether a [stationary point](@entry_id:164360) is a true minimizer (local or global), a maximizer, or a saddle point. This inquiry leads us from local analysis to the global structure of the manifold.

#### The Global Setting: Completeness and the Hopf-Rinow Theorem

The global theory of geodesics is most elegantly formulated on **complete Riemannian manifolds**. A fundamental result, the **Hopf-Rinow Theorem**, states that for a connected Riemannian manifold, [metric completeness](@entry_id:186235) (the property that every Cauchy sequence of points converges) is equivalent to [geodesic completeness](@entry_id:160280) (the property that every geodesic can be extended to be defined for all time $t \in \mathbb{R}$).

This theorem has profound consequences. It guarantees that on a complete manifold, the [exponential map](@entry_id:137184) $\exp_p: T_pM \to M$, which maps a [tangent vector](@entry_id:264836) $v$ to the point reached by following the geodesic with [initial velocity](@entry_id:171759) $v$ for one unit of time, is defined on the entire tangent space $T_pM$. Furthermore, it guarantees that any two points $p, q \in M$ can be connected by at least one length-[minimizing geodesic](@entry_id:197967). This ensures that the problem of finding a "shortest path" always has a solution [@problem_id:2976663].

#### Second Variation, Jacobi Fields, and Conjugate Points

Stationarity does not imply minimality. On the surface of a sphere, for example, there are two geodesic arcs connecting any two non-[antipodal points](@entry_id:151589). Both are stationary points for length and energy, but only the shorter one is a global minimizer [@problem_id:2976662].

To distinguish between these cases, we must analyze the **second variation**. For a geodesic $\gamma$, the second variation of the energy functional for a variation with field $V$ (where $V(a)=V(b)=0$) is given by the **[index form](@entry_id:183467)**:
$$
I(V,V) = \frac{d^2}{ds^2}\bigg|_{s=0} E(\gamma_s) = \int_{a}^{b} \left( g(\nabla_t V, \nabla_t V) - g(R(V, \dot{\gamma})\dot{\gamma}, V) \right) dt
$$
where $R$ is the Riemann [curvature tensor](@entry_id:181383) [@problem_id:2976654]. For a geodesic to be a local minimizer of energy (and thus length), the [index form](@entry_id:183467) $I(V,V)$ must be non-negative for all admissible variation fields $V$.

The curvature term $g(R(V, \dot{\gamma})\dot{\gamma}, V)$ reveals how the manifold's curvature affects the stability of geodesics. Positive curvature tends to make the [index form](@entry_id:183467) negative, indicating instability, while negative curvature contributes to stability.

The Euler-Lagrange equation associated with this [index form](@entry_id:183467) functional is the **Jacobi equation**:
$$
\nabla_t^2 V + R(V, \dot{\gamma})\dot{\gamma} = 0
$$
Solutions to this equation are called **Jacobi fields**. They represent the infinitesimal behavior of nearby geodesics. A point $q = \gamma(t_0)$ is said to be **conjugate** to $p = \gamma(0)$ along $\gamma$ if there exists a non-trivial Jacobi field $J$ along $\gamma$ that vanishes at both $t=0$ and $t=t_0$. The existence of such a field indicates that a family of geodesics starting at $p$ is beginning to refocus at $q$.

The presence of conjugate points is directly tied to the failure of local minimality. The celebrated **Morse Index Theorem** states that a geodesic segment $\gamma|_{[0,b]}$ fails to be a local minimizer if and only if it contains a conjugate point to $p$ in its interior, $(0,b)$. The existence of such a point implies that there is a variation field $V$ for which the second variation is negative [@problem_id:2976662].

#### The Cut Locus and Global Minimality

While conjugate points signal the loss of *local* minimality, a geodesic may cease to be a *global* minimizer even before encountering a conjugate point. This leads to the concept of the **[cut locus](@entry_id:161337)**.

For a point $p \in M$, the **[cut point](@entry_id:149510)** along a unit-speed geodesic $\gamma_v$ starting from $p$ is the first point $\gamma_v(t)$ beyond which the segment $\gamma_v|_{[0,t]}$ is no longer the unique shortest path from $p$ to $\gamma_v(t)$. This failure can happen for two reasons:
1.  The point $\gamma_v(t)$ is the first conjugate point to $p$ along $\gamma_v$.
2.  There exists another [minimizing geodesic](@entry_id:197967) from $p$ to $\gamma_v(t)$ with the same length.

The set of all such cut points, taken over all initial directions $v$, forms the **cut locus** $C(p)$ of the point $p$. The cut time $c_p(v)$ along a direction $v$ is always less than or equal to the first conjugate time $t_{\text{conj}}(v)$ [@problem_id:2976644].

The domain $M \setminus C(p)$ is the region where every point is connected to $p$ by a unique [minimizing geodesic](@entry_id:197967). The distance from $p$ to its cut locus defines the **injectivity radius** $\mathrm{inj}(p)$, which is the radius of the largest ball in $T_pM$ on which the [exponential map](@entry_id:137184) is a diffeomorphism. Inside this "normal ball" of radius $\mathrm{inj}(p)$, the geometry is simple: geodesics from the center are unique minimizers [@problem_id:2976644]. The [cut locus](@entry_id:161337) thus marks the boundary of this simple picture and the onset of the manifold's more complex global topology and geometry.