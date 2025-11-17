## Introduction
In the study of [curved spaces](@entry_id:204335), the notion of a "straight line" is replaced by the concept of a geodesic—a path that is intrinsically the straightest possible. While intuitively understood as the shortest path between two points, a more fundamental definition arises from the idea of zero acceleration. However, defining acceleration in a coordinate-independent manner on a general manifold presents a significant challenge, as the naive differentiation of velocity components fails to produce a geometrically meaningful quantity. This article confronts this problem head-on, developing the necessary mathematical machinery to formulate the celebrated [geodesic equations](@entry_id:264349) in [local coordinates](@entry_id:181200).

This article is structured to guide the reader from fundamental principles to practical applications. We will begin by laying the theoretical groundwork, explaining why a new form of differentiation—the covariant derivative—is required, introducing the Christoffel symbols, and deriving the [geodesic equation](@entry_id:136555). We will then explore the equation's wide-ranging applications, from defining straight lines in curved spaces to its foundational role in General Relativity. Finally, a series of hands-on practices provides an opportunity to solidify this understanding by applying the theory to solve problems on canonical manifolds. Our investigation begins with the fundamental principles that govern motion and differentiation in the curved world of Riemannian manifolds.

## Principles and Mechanisms

In the study of Riemannian manifolds, the concept of a geodesic—the generalization of a "straight line" to [curved spaces](@entry_id:204335)—is of paramount importance. While intuitively understood as the shortest path between two points, a more fundamental definition arises from the notion of a path of zero acceleration. To formalize this, we must first develop a coordinate-invariant language for differentiation on manifolds. This chapter elucidates the principles and mechanisms underlying the description of geodesics in [local coordinates](@entry_id:181200), beginning with the challenge of defining acceleration and culminating in the celebrated [geodesic equations](@entry_id:264349).

### Velocity and Acceleration in Local Coordinates: The Need for a Connection

Let us begin by considering a smooth curve $\gamma: I \to M$ on a smooth $n$-dimensional manifold $M$, where $I \subseteq \mathbb{R}$ is an open interval. In a local [coordinate chart](@entry_id:263963) $(U, x)$ where $U$ is an open set containing the image of a portion of the curve, the curve is represented by a set of $n$ smooth functions of the parameter $t$, given by the composition $\xi(t) = x(\gamma(t)) = (x^1(t), \dots, x^n(t))$. This map $\xi$ is a curve in the Euclidean space $\mathbb{R}^n$, specifically within the open set $x(U)$.

The **velocity vector** of the curve at a point $p = \gamma(t_0)$ is an intrinsic geometric object, denoted $\dot{\gamma}(t_0)$, that resides in the [tangent space](@entry_id:141028) $T_pM$. It can be formally defined as a derivation acting on [smooth functions](@entry_id:138942) $f \in C^\infty(M)$, measuring the rate of change of $f$ along the curve:
$$
\dot{\gamma}(t_0)(f) = \frac{d}{dt}(f \circ \gamma)\bigg|_{t=t_0}
$$
In the [coordinate basis](@entry_id:270149) $\{\partial_i|_p = \frac{\partial}{\partial x^i}|_p\}$ for the tangent space $T_pM$, the components of this vector are found by applying it to the coordinate functions $x^i$ themselves. Denoting the components by $\dot{x}^i(t_0)$, we find:
$$
\dot{x}^i(t_0) = \dot{\gamma}(t_0)(x^i) = \frac{d}{dt}(x^i \circ \gamma)\bigg|_{t=t_0}
$$
This allows us to express the velocity vector in [local coordinates](@entry_id:181200) as a linear combination of the basis vectors:
$$
\dot{\gamma}(t_0) = \dot{x}^i(t_0) \partial_i\big|_p
$$
where we adopt the Einstein [summation convention](@entry_id:755635).

While the velocity vector $\dot{\gamma}(t_0)$ is an intrinsic object, its coordinate representation is not. If we change to a new coordinate system $(V, y)$, both the components and the basis vectors transform. The components $\dot{x}^i$ transform according to the Jacobian of the coordinate change, while the basis vectors $\partial_i$ transform by the inverse Jacobian. These two transformations precisely cancel, ensuring the vector itself remains invariant:
$$
\dot{\gamma} = \dot{x}^i \partial_i = \left( \frac{\partial y^a}{\partial x^i} \dot{x}^i \right) \left( \frac{\partial x^j}{\partial y^a} \partial_j \right) = \dot{y}^a \partial_a
$$
This confirms that the velocity vector is a well-defined geometric entity, independent of its description.

A natural next step is to define the acceleration of the curve. A naive approach would be to simply differentiate the [coordinate velocity](@entry_id:272549) components with respect to $t$, yielding the **[coordinate acceleration](@entry_id:264260)** $\ddot{x}^i(t) = \frac{d^2x^i}{dt^2}$. However, a fundamental problem arises: this quantity does not represent the components of an intrinsic geometric object. To see this, we can compute its transformation law under a coordinate change from $x$ to $y$. Differentiating the [velocity transformation](@entry_id:265594) law $\dot{y}^a = \frac{\partial y^a}{\partial x^i}\dot{x}^i$ with respect to $t$ using the product and chain rules yields:
$$
\ddot{y}^a = \frac{\partial y^a}{\partial x^i} \ddot{x}^i + \frac{\partial^2 y^a}{\partial x^i \partial x^j} \dot{x}^i \dot{x}^j
$$
For $\ddot{x}^i$ to be the components of a vector, the transformation law would need to be linear, i.e., $\ddot{y}^a = \frac{\partial y^a}{\partial x^i} \ddot{x}^i$. The presence of the second term, which is inhomogeneous (it does not depend on $\ddot{x}^i$) and involves second derivatives of the [coordinate map](@entry_id:154545), demonstrates that the [coordinate acceleration](@entry_id:264260) is not a vector. By itself, it has no coordinate-free geometric meaning. This failure motivates the introduction of a new structure—an [affine connection](@entry_id:160152)—to define a proper, geometrically meaningful notion of acceleration.

### The Covariant Derivative and the Christoffel Symbols

To differentiate [vector fields](@entry_id:161384) in a way that respects the geometry of the manifold, we introduce an **[affine connection](@entry_id:160152)**, denoted by $\nabla$. A connection provides a rule for taking the [directional derivative](@entry_id:143430) of a vector field, $\nabla_X Y$. In a local [coordinate chart](@entry_id:263963), the entire behavior of the connection is captured by its action on the basis [vector fields](@entry_id:161384). The coefficients of this action are the **Christoffel symbols** of the second kind, $\Gamma^k_{ij}$, defined by:
$$
\nabla_{\partial_i} \partial_j = \Gamma^k_{ij} \partial_k
$$
Geometrically, the Christoffel symbols measure how the [coordinate basis](@entry_id:270149) vectors change from point to point, as perceived by the connection $\nabla$. They are functions of position, $\Gamma^k_{ij}(x)$.

Crucially, the Christoffel symbols are not the components of a tensor. Their transformation law under a coordinate change from $x$ to $y$ can be derived from their definition and the rules of calculus. Let the symbols in the $y$-chart be $\tilde{\Gamma}^\alpha_{\beta\gamma}$. A careful derivation shows:
$$
\tilde{\Gamma}^{\alpha}_{\beta\gamma} = \frac{\partial y^{\alpha}}{\partial x^{k}} \frac{\partial x^{i}}{\partial y^{\beta}} \frac{\partial x^{j}}{\partial y^{\gamma}} \Gamma^{k}_{ij} + \frac{\partial y^{\alpha}}{\partial x^{k}} \frac{\partial^{2}x^{k}}{\partial y^{\beta} \partial y^{\gamma}}
$$
Just as with the [coordinate acceleration](@entry_id:264260), an inhomogeneous term involving second derivatives of the coordinate change appears. This confirms that the Christoffel symbols do not transform as a tensor. This seemingly problematic property is, in fact, exactly what is required. The non-tensorial nature of the Christoffel symbols is precisely tailored to cancel the non-tensorial behavior of the ordinary [coordinate acceleration](@entry_id:264260), allowing for the construction of a true geometric acceleration.

### The Geodesic Equation

The concept of a connection allows us to define the derivative of a vector field that is defined only along a curve. Let $V(t)$ be a [vector field along a curve](@entry_id:635143) $\gamma(t)$, with coordinate representation $V(t) = V^i(t)\partial_i|_{\gamma(t)}$. The **[covariant derivative](@entry_id:152476) of $V$ along $\gamma$**, denoted $\nabla_{\dot\gamma}V$, measures the rate of change of $V$ as it is transported along the curve. Using the properties of a connection, its components can be derived as:
$$
(\nabla_{\dot\gamma}V)^k = \frac{dV^k}{dt} + \Gamma^k_{ij} V^i \dot{x}^j
$$
The first term, $\frac{dV^k}{dt}$, is the ordinary rate of change of the vector's components. The second term, involving the Christoffel symbols, is a correction term that accounts for the change of the basis vectors themselves as we move along the curve.

We can now define a true geometric acceleration. The **covariant acceleration** of a curve $\gamma$ is the covariant derivative of its own [velocity field](@entry_id:271461) along the curve, $\nabla_{\dot\gamma}\dot{\gamma}$. To find its components, we simply substitute $V = \dot{\gamma}$ (so $V^i = \dot{x}^i$) into the formula above:
$$
(\nabla_{\dot\gamma}\dot{\gamma})^k = \frac{d}{dt}(\dot{x}^k) + \Gamma^k_{ij} \dot{x}^i \dot{x}^j = \frac{d^2x^k}{dt^2} + \Gamma^k_{ij}(x(t)) \frac{dx^i}{dt} \frac{dx^j}{dt}
$$
This quantity, formed by correcting the naive [coordinate acceleration](@entry_id:264260) $\ddot{x}^k$ with a term containing the Christoffel symbols, transforms as a genuine vector. The inhomogeneous terms in the transformation laws for $\ddot{x}^k$ and $\Gamma^k_{ij}$ cancel each other out perfectly, leaving a homogeneous transformation law:
$$
(\nabla_{\dot\gamma}\dot{\gamma})^a_{\text{in }y\text{-coords}} = \frac{\partial y^a}{\partial x^k} (\nabla_{\dot\gamma}\dot{\gamma})^k_{\text{in }x\text{-coords}}
$$
Because the covariant acceleration is a [true vector](@entry_id:190731), the condition that it is the zero vector is a coordinate-invariant geometric statement.

This leads to the definition of a geodesic. A **geodesic** is a curve of zero covariant acceleration; that is, a curve whose velocity vector remains parallel to itself as it is transported along the curve. The condition $\nabla_{\dot\gamma}\dot{\gamma}=0$ translates directly into a system of differential equations in [local coordinates](@entry_id:181200), known as the **[geodesic equations](@entry_id:264349)**:
$$
\frac{d^2 x^k}{dt^2} + \Gamma^k_{ij}(x(t)) \frac{dx^i}{dt} \frac{dx^j}{dt} = 0, \quad \text{for } k=1, \dots, n
$$
It is vital to distinguish between the geometric object and its coordinate description. The curve $\gamma(t)$ lives on the manifold $M$, while the [geodesic equations](@entry_id:264349) are a system of [ordinary differential equations](@entry_id:147024) (ODEs) for the coordinate functions $x^k(t)$ that describe a curve $\xi(t)$ in an open subset of $\mathbb{R}^n$. A solution $\xi(t)$ to this system, when mapped back to the manifold via the chart's inverse, $\gamma(t) = x^{-1}(\xi(t))$, yields a geodesic on $M$, as long as the solution remains within the chart's domain.

### The Levi-Civita Connection: Uniqueness and Origin from the Metric

We have defined the geodesic equation in terms of abstract Christoffel symbols. A critical question remains: which connection $\nabla$, and therefore which Christoffel symbols, should we use? On a Riemannian manifold $(M,g)$, there is a canonical choice given by the **Fundamental Theorem of Riemannian Geometry**. This theorem states that for any Riemannian metric $g$, there exists a unique [affine connection](@entry_id:160152) $\nabla$ that satisfies two natural geometric conditions:
1.  **Torsion-Free**: The connection is symmetric, meaning $\nabla_X Y - \nabla_Y X = [X,Y]$ for any vector fields $X,Y$. In [local coordinates](@entry_id:181200), this is equivalent to the symmetry of the Christoffel symbols in their lower indices: $\Gamma^k_{ij} = \Gamma^k_{ji}$.
2.  **Metric-Compatible**: The connection preserves the metric under parallel transport, meaning $\nabla g = 0$. This implies that the metric of two vector fields remains constant if they are parallel transported along a curve: $X(g(Y,Z)) = g(\nabla_X Y, Z) + g(Y, \nabla_X Z)$.

This unique connection is called the **Levi-Civita connection**. These two conditions are sufficient to derive an explicit formula for the Christoffel symbols purely in terms of the metric tensor components $g_{ij}$ and their [partial derivatives](@entry_id:146280):
$$
\Gamma^{k}_{ij} = \frac{1}{2} g^{k\ell} \left( \frac{\partial g_{j\ell}}{\partial x^i} + \frac{\partial g_{i\ell}}{\partial x^j} - \frac{\partial g_{ij}}{\partial x^\ell} \right)
$$
where $g^{k\ell}$ are the components of the [inverse metric tensor](@entry_id:275529). This remarkable result shows that the entire structure of geodesics—the "straight lines" of the space—is completely determined by the metric $g$, which defines lengths and angles.

### Geodesics as Paths of Extremal Length

An alternative and equally profound perspective on geodesics comes from the calculus of variations. Intuitively, geodesics should be the "shortest paths" between points. This can be formalized by seeking curves that are [critical points](@entry_id:144653) of the **[length functional](@entry_id:203503)**:
$$
L[\gamma] = \int_a^b \sqrt{g_{ij}(\gamma(t)) \dot{x}^i(t) \dot{x}^j(t)} \, dt
$$
The square root in the integrand makes the associated Euler-Lagrange equations complicated. A more convenient approach is to consider the **[energy functional](@entry_id:170311)**:
$$
E[\gamma] = \frac{1}{2} \int_a^b g_{ij}(\gamma(t)) \dot{x}^i(t) \dot{x}^j(t) \, dt = \frac{1}{2} \int_a^b ||\dot{\gamma}(t)||_g^2 \, dt
$$
The Euler-Lagrange equations for the [energy functional](@entry_id:170311), for curves with fixed endpoints, are precisely the [geodesic equations](@entry_id:264349) derived previously. A crucial consequence of this is that any solution to the [energy functional](@entry_id:170311)'s Euler-Lagrange equations must have **constant speed**, i.e., $||\dot{\gamma}(t)||_g = c$ for some constant $c$.

The length and energy functionals are intimately related. By the Cauchy-Schwarz inequality, one can show that for any curve $\gamma$ on $[a,b]$, $L[\gamma]^2 \le 2(b-a)E[\gamma]$, with equality holding if and only if the curve has constant speed. This implies that among all curves connecting two points, a curve that minimizes length can always be reparametrized to have constant speed, and in that [parametrization](@entry_id:272587), it will also minimize energy. Conversely, a curve that minimizes energy automatically has constant speed and therefore also minimizes length. Thus, geodesics can be understood both as paths of zero acceleration and as (locally) shortest paths.

### Existence, Uniqueness, and the Geodesic Flow

The [geodesic equation](@entry_id:136555) is a system of $n$ second-order, nonlinear, autonomous [ordinary differential equations](@entry_id:147024) for the coordinate functions $x^k(t)$. By introducing the velocities $v^k = \dot{x}^k$ as new variables, we can rewrite this as a system of $2n$ first-order ODEs on the coordinates $(x^k, v^k)$ of the [tangent bundle](@entry_id:161294) $TM$.
$$
\begin{cases}
\dot{x}^k  = v^k \\
\dot{v}^k  = -\Gamma^k_{ij}(x) v^i v^j
\end{cases}
$$
Standard ODE theory, specifically the **Picard–Lindelöf theorem**, can now be applied. This theorem guarantees the local existence and uniqueness of a solution to this system given a set of [initial conditions](@entry_id:152863). Geometrically, this means that for any point $p \in M$ and any tangent vector $v \in T_pM$, there exists a unique geodesic $\gamma(t)$ starting at $p$ with initial velocity $v$ (i.e., $\gamma(0) = p$ and $\dot{\gamma}(0)=v$).

For the theorem to apply, the right-hand side of the ODE system must be locally Lipschitz continuous. This condition is met if the Christoffel symbols $\Gamma^k_{ij}$ are continuously differentiable ($C^1$). Since the $\Gamma^k_{ij}$ are computed from first derivatives of the metric components $g_{ij}$, this requires the metric to be at least $C^2$. On a smooth ($C^\infty$) manifold, this condition is always satisfied, ensuring the existence and uniqueness of a local geodesic for any initial data. This powerful result provides the rigorous foundation for the intuitive idea of "shooting" a straight line in any direction from any point on the manifold, and the resulting evolution is described by the **[geodesic flow](@entry_id:270369)** on the [tangent bundle](@entry_id:161294).